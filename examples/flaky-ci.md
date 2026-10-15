# Example: flaky CI tests, one at a time

The prompt:

> I keep asking Claude to fix flaky CI tests one at a time, whenever one bites us. Our CI runs on self-hosted GitHub Actions runners, the repo is a Go server plus a C++ kernel plus a Next.js frontend, and the test suite takes about 25 minutes. What should I be asking for instead? Be ambitious.

The response, with the skill loaded and nothing else (no repository access, no project reference):

---

Stop asking for the next repair and ask for the outcome: a CI signal you can trust. Here is the ask, rewritten.

**Goal beyond the goal:** A red check always means a real defect and a green check always means mergeable; nobody re-runs a job by hand, and the next flake is caught on its first flip rather than when it bites someone.

**The ask, rewritten:**

> Own the reliability of our CI, not the test that failed today. The repo is a Go server, a C++ kernel and a Next.js frontend; the suite takes about 25 minutes on self-hosted GitHub Actions runners.
>
> Start from the raw history, not the red job. Pull every workflow run, job and step from the last 90 days through the GitHub API, with per-test results (`go test -json`, CTest's JUnit output, the Playwright and Vitest JUnit reporters; add the reporters and upload them as artifacts where they are missing), and load it into one table: run, commit, job, runner host, test, outcome, duration, and the host's load, memory and disk at the time. Classify every failure: the same commit with different outcomes is a flake; anything else is a regression or an infrastructure failure. Give each flaky test a failure probability with a confidence interval and rank by cost: reruns multiplied by minutes multiplied by pull requests blocked.
>
> Fix causes, not tests. Group the flakes by root cause (leftover state on a shared runner: containers, ports, temp dirs, database names; sleep-based waits; order dependence; CPU and memory contention from sibling jobs on the same host; data races; floating-point tolerance and iteration-order assumptions in the kernel tests; calls to external services) and fix each class once. Before each fix, reproduce the flake under stress on a real runner with the neighbouring jobs running the way they do in CI: `go test -race -shuffle=on -count=200`, `ctest --repeat until-fail:200 --schedule-random` on a sanitizer build, `playwright test --repeat-each 50 --retries 0`. A fix is proven when the same stress run passes afterwards and the test does not flip again in the next two weeks of history. Open one PR per cause class with the reproduction command in the description.
>
> Leave the machinery behind. A job that runs after every workflow run, flags a test the first time it flips on one commit, quarantines it off the merge-blocking path while keeping it running, and files an issue with the reproduction command and the host state at failure. Split the suite into per-area jobs so a retry re-runs the failing job only (`gh run rerun --failed`), never the 25-minute whole. A weekly report with the numbers: main-branch pass rate, flake rate per test, time-to-green p50 and p95, manual reruns, and anything you could not reproduce.
>
> Targets: main-branch pass rate 99.5 % or better, zero manual reruns, no quarantined test older than two weeks, and a flake retry under five minutes.

**What changed and why:**

- Altitude: the unit of work is the signal (pass rate, reruns, time-to-green), not one test, and the detector catches the next flake on its first flip so nobody has to report it.
- Depth: the raw material is the complete run history with per-test results and runner state, not the one red job; "flake or regression" is decided by same-commit-different-outcome and a measured probability, not by reading the test.
- Depth: every fix is reproduced under stress on the real runner before and proven after, and the judge is that run plus the following two weeks of history, never "this should fix it".
- Depth: the goals are numbers (99.5 %, zero reruns, a five-minute retry) rather than "fewer flakes".
- Range: SRE practice treats CI as a service with an SLO and an error budget; reliability engineering's accelerated life testing (stress a part harder than production) is what the 200-count runs do, surfacing in ten minutes what CI would surface over a month.

**What it needs:**

- `gh` auth with Actions read on the repo (runs, jobs, logs, artifacts). Log retention defaults to 90 days, so the dataset starts when the pull starts.
- Per-test structured output uploaded as an artifact from every job: a small workflow change.
- A home for the table (SQLite in a bucket, or a schema in a Postgres you already run) plus a job that appends after each run.
- A self-hosted runner the agent can reach, by SSH or by a `workflow_dispatch` job it can trigger, to reproduce under real contention, and host metrics sampled by the job (`/proc/loadavg`, `free`, `df`, or node_exporter).
- Permission to open PRs and file issues, and authority over branch protection so a quarantined test can stop blocking merges.
- Outside judges: the stress run on the runner, and the pass-rate and flip-count numbers read back from the run history, not reported by the agent.

**Next rung:** The agent owns the SLO continuously and flakes never reach `main`. It runs on every `workflow_run` completion instead of when prompted, and any PR that adds or changes a test must pass that test 50 times under contention as a required check. What unlocks it: an always-on trigger with its own token (a scheduled or event-driven Claude Code run), runner capacity for the stress lane, and the branch-protection rule for the new required check.
