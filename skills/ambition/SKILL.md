---
name: ambition
description: Raise the ambition of a task before doing it, along the three axes from Felix Rieseberg's "How to be more ambitious" - Altitude (own the outcome beyond the task), Depth (do it the way the best person in the field would, on raw material, with their real instruments and an outside judge), and Range (bring in fields the task doesn't obviously need, and do what their practitioners do). Use whenever the user asks to be more ambitious, think bigger, go deeper, "make this prompt better", "what would an expert do here", "what should I be asking for instead", wants a plan, brief or roadmap pushed further, invokes /ambition, or hands over a routine recurring task (a deck, a report, a weekly summary, a review, a one-off bug fix, a tutorial) that hints at a larger goal. Also reach for it when a request reads as the user's best guess at a method rather than the outcome they want, even if they never say "ambitious".
---

# Ambition

Source: Felix Rieseberg, [How to be more ambitious: A tutorial for humans
with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/).
The premise: people underuse models because they ask for too little, and
"be more ambitious" is a slogan, not an instruction. This skill is the
instruction. It turns a task into the version of itself a more ambitious
person would have asked for, and says what that version needs.

## In a project you know

If `references/<project>.md` exists beside this file for the repository or
product the task is about, read it before step 1. The key is the task's
subject, not the working directory: a question about an unrelated docs site
gets no reference even when asked from inside the repo. A project reference
names what the method's slots resolve to there: the ceilings worth climbing
to, the raw material that exists, the instruments the best in each field
use, the judges already built, what an agent can reach, and the crew.
Without it, the block comes out generic; with it, every line names a real
thing. To write one for your own codebase, copy
`references/project-reference-template.md` to `references/<project>.md`
and fill it in; it points rather than restates, so the facts stay in the
code's own guides.

## Four kinds of ambition, three of which need help

| Axis | The question | Tell that it applies |
|---|---|---|
| Speed | Same work, less time | Needs no method. But when the user volunteers a time cost (a 25-minute suite, a two-day turnaround), carry it into the ask as a multiplier or a target; don't drop it. |
| Altitude | What does the user want to happen *next*? What's the goal beyond the goal? | The work serves an ultimate outcome. There will be meetings about it. The same task recurs. |
| Depth | How would the best person in this field do this, from the rawest material, with their real instruments, checked by something other than themselves? | The user wants this one thing done really well. |
| Range | Which other fields would change the result, and what do their practitioners actually do? | The task is a noun (a deck, a review, a doc) hiding verbs, or the obvious field has plateaued. |

Pick the axes the tells point at, and lead with one. When every tell fires,
which is common for recurring outcome work, lead with the axis that changes
the ask most and let the other two contribute a move each. Depth's moves
are the raw material and the judge, which never get cut, so Depth may need
two bullets; Range gets one. The failure
mode is applying all three in full: that makes the ask bigger, and bigger
is what this skill exists to avoid.

## The method

### 1. Find the goal beyond the goal

Before touching the task, write one sentence on what the user wants to be
true after the task is done. "Fix this crash" becomes "the app stays
crash-free." "Make QBR slides" becomes "leadership catches problems early and
moves money and people to the right places." The request and its context
usually hold the answer; ask only when two readings would send the work in
materially different directions.

That sentence is the ceiling. Everything between the literal ask and that
sentence is in scope to rewrite.

### 2. Altitude: climb the ladder

Each rung asks for more outcome and less method. The ladder for a quarterly
business review deck:

1. Fill the template with this quarter's numbers (the literal ask).
2. Explain. Give the model all the data you can get, not just the template's
   inputs: "Tell me what changed this quarter, why, and what we should do
   about it."
3. Decide. "Work out which three decisions are most urgent in the face of
   everything you've learned, and start working on potential directions with
   for/against arguments."
4. Redesign the process. "The review exists so leadership catches problems
   early and moves money and people to the right places. Design a better way
   to do that than a quarterly deck, show from our own history that it would
   have caught things sooner, and run it beside the current one for a
   quarter."

The same ladder for a support ticket: answer this ticket; answer every
ticket of this kind from the product's own logs; halve the tickets of this
kind by fixing what generates them; the product reports the class of
problem before anyone writes in.

Which rung to propose: the one at which the model owns the outcome rather
than the task (keeps the app crash-free; keeps CI trustworthy; knows each
customer's health week by week). That is usually the rung just below
redesigning the process around the outcome, and the redesign is the Next
rung. A plain task request with no "be ambitious" in it gets one rung up,
with the owning rung named as Next. Invoking this skill on a prompt, or
forwarding one to be made more ambitious, counts as "be ambitious". The ladder is for your reasoning; the
output shows the rung you propose and the one above it, nothing lower.

The owning rung is where durable workflows live: the model holds the
outcome instead of being re-prompted task by task. Reaching it usually means
changing the workflow first so the model can act alone. The post's own
example: going from "fix this crash" to "keep the app crash-free" meant
first letting Claude fetch crash reports, map app versions to git commits,
and reach real Windows, macOS and Linux machines to reproduce and verify
fixes. Whatever rung you propose, list the access it needs with the same
specificity.

Altitude fits outcome work and fits creative work poorly. For a poem, a brand
concept or a level design, the user's taste is the outcome; use depth and
range there instead.

### 3. Depth: use the real instruments

Vocabulary is not method. A model told to "act like a data scientist" will
switch words and keep using markdown tables. Depth means switching the actual
method, and the post's techniques are:

- **Insist on the instruments the best in the field use.** A database and a
  statistical model, not a table. A profiler, not a hunch. A convergence
  study, not one run. You don't have to know what the experts use; the model
  usually does, so ask it to name them and then hold it to them. When the
  user named only their stack, name the instruments that stack implies and
  mark them as assumptions to confirm. The instrument must fit the data:
  with three customers, the expert reads raw rows per account and baselines
  each against its own history; a regression over three points is costume.
- **Start from the rawest material.** Name what the expert would start from
  instead of what has already been digested for the user: the logs, not the
  dashboard; the transcript, not the summary; the repository, not the README.
- **Pick unreasonable goals and call them reasonable.** Need the page to load
  in 5 s instead of 10 s? Ask for 200 ms. Specific hard goals beat "do your
  best." When the model says it's impossible, say it's solvable and keep
  going. With no baseline to set a goal from, give a relative target (half,
  double) plus one absolute number the first run can be measured against
  ("it works inside 10 minutes"). Never leave a threshold as "N" or "a
  stated tolerance": pick the number and mark it as a starting value.
- **Challenge what's believed.** Most things a business believes are rough
  approximations. Hand over the raw data and have the belief checked
  adversarially: "We believe churn is an onboarding problem. Try to reproduce
  that from the raw data." If the user stated no belief, the original ask
  usually contains one: the method they asked for implies a diagnosis
  ("shorter" implies the problem is length). Name it and have it tested.
- **Produce new knowledge.** Once the model is inside the data, ask for the
  blind spots: "Build a simulation of our customers that reproduces the last
  year from our logs. Then find the earliest signal of churn we don't know
  about yet, and show it predicts on data it has not seen."
- **Use an outside judge.** Never let the model grade its own work. Name
  what, other than the model or the user, shows the result is right: a test
  that runs, held-out data, a benchmark, a second tool, a real user. Best is
  a tool the model can run for immediate feedback.

The post's own prompt for depth. Run it on yourself before writing the
block; it is a checklist, not text for the output:

> I want a deeper version of this task, not a bigger one. Before rewriting
> it: (1) say what a top professional in this field would do here that I'm
> not asking for; (2) name the rawest material they would start from instead
> of what has already been digested for me; (3) name the specific methods and
> tools they would use; (4) say what, other than you or me, would show the
> result is right. Then rewrite my prompt to ask for exactly that.

### 4. Range: nouns to verbs, then assemble the crew

- **Replace the nouns with verbs** (a trick from *The Art of Innovation*). A
  quarterly review isn't "a deck." It's "getting busy people to believe a
  story about cause and effect, and to decide under uncertainty, in 30
  minutes." The verbs point at fields the noun hid: persuasion, causal
  inference, decision science, time-boxed presentation. If the task is
  already a verb ("fix flaky tests"), skip this step and go to the crew.
- **Assemble the crew.** If this had to be extraordinary, who would you
  recruit? For a deck that must land: an analyst, a journalist, an editor,
  and if it's presented, a motion and audio designer. Add a red team, say a
  short seller and a forensic accountant. Then take from each what they *do*:
  the journalist's source-checking and lede, the short seller's hunt for the
  number that doesn't reconcile.
- **Do, don't role-play.** Asking the model to *write as* a short seller
  makes the transcript weirder without improving the outcome. Ask it to *do
  what a short seller does* to research a position. Each crew member
  contributes a method, a tool or a check, never a voice.

### 5. Write the ambitious version

Produce this block, inline, as text the user can paste. Budget: about 800
words for the whole response and never more than 900, with the rewritten
ask under 450. Over budget, cut in this order: merge "what changed" bullets, then
the ask's examples, then the lead-in down to one sentence. Never cut the target, the
judge or the access list. Depth is what survives the cut; breadth is what
goes.

**Goal beyond the goal:** one sentence about the world after the task is
done (the team, the product, the customer), not a description of the
artifact.

**The ask, rewritten:** the task restated so a capable agent with the right
access would deliver the outcome rather than the method. Keep the user's
words where they were right. Where their words name a method the evidence
might not support ("shorter", "clearer"), keep them as a predicted
consequence or a belief to test, not as the target. Make it something the
user could paste as a prompt or hand to a teammate.

**What changed and why:** two to five bullets, each tagged Altitude, Depth or
Range, each naming the specific move (the instrument, the raw source, the
target, the crew member's method). Several crew members can share one
Range bullet. A time cost the user volunteered belongs in the target line,
not in a bullet of its own. The judge is named once, here; "what it needs"
lists what the judge requires, not the judge again.

**What it needs:** what the rewritten ask requires to run: the data, tools,
access and outside judge, concretely. Which logs, which database, which
machine, which test, which held-out set. Include at least one thing the
user must grant or decide.

**Next rung:** the ask one level higher, and only what that level adds: the
resource, access or decision that would unlock it. Refer back to "what it
needs" ("the same two sources") rather than listing them again. When the
project reference says where an accepted rung is recorded, end with that
one line in every mode.

Worked example, from the post's crash case:

> **Goal beyond the goal:** the app stays crash-free without anyone filing
> fix requests.
>
> **The ask, rewritten:** Keep our desktop app crash-free. Pull crash reports
> as they arrive, map each to the app version and git commit, reproduce it on
> the affected OS, fix it, prove the fix on a real machine, and open the PR.
> Report weekly on crash-free sessions and on anything you couldn't
> reproduce. Starting target: 99.5% crash-free sessions within 60 days.
>
> **What changed and why:**
> - Altitude: the unit of work is the outcome (crash-free), not one crash.
> - Depth: reproduction on a real machine replaces reasoning from a stack
>   trace, and the judge is the reproduced crash no longer reproducing.
> - Depth: the target is a number (crash-free sessions), not "fewer crashes."
>
> **What it needs:** read access to the crash reporter, a version-to-commit
> map, Windows, macOS and Linux machines the agent can drive, and permission
> to open PRs.
>
> **Next rung:** prevent classes of crash before release by running the same
> reproduction harness against every release candidate. Unlocked by a
> release-candidate build the harness can target and a rule that it blocks
> the release.

A real ask at the owning rung runs longer than this example, two to four
paragraphs, because it carries the instruments and the numbers. It should
not run longer than that.

## How to respond

Match what the user asked for:

- **They asked for the rewrite** ("make this more ambitious", "what should I
  ask instead", "upgrade this prompt"): one or two sentences on why the
  original ask was a method rather than an outcome, then the block, then
  stop. The rewrite is the deliverable.
- **They asked for the work, ambitiously** ("be ambitious about this deck"):
  lead with the block in compact form, five or six lines, then do the
  ambitious version. If it needs access the user hasn't granted, do
  everything that doesn't depend on it and name the rest.
- **They asked for the work, plainly,** and it's a routine ask that hints at a
  larger goal: do what was asked, then close with one or two lines naming the
  next rung. Don't hijack the task.

## Invocation

- `/ambition` alone, mid-conversation: apply the method to the task in
  progress and reply in the mode above that matches how it was asked.
- `/ambition <ask or prompt>`: rewrite that ask.
- `/ambition <area>`, where the argument is a directory of the repo: read
  its README, its contributor guide (`CONTRIBUTING.md`, `AGENTS.md` or
  `CLAUDE.md`) and its plan (`PLAN.md`, `ROADMAP.md` or the like) where
  they exist (a subdirectory without its own is covered by its parent's),
  and the recent commits touching it. Treat the plan's next steps as the literal ask and propose
  the owning rung; if the plan already sits there, propose the redesign.
  Rewrite mode by default, and the budget stretches to 1,000 words because
  the access list and the recording line are not optional. End with where
  the accepted rung is recorded (the project reference says where;
  otherwise the area's plan or an issue).

## Anti-patterns

- **Bigger, not deeper.** More sections, more words, more deliverables.
  Ambition in depth removes the digested layer; it doesn't add a slide.
- **Costume.** "Approach this like a statistician" without a model, a
  dataset and a held-out check is a change of vocabulary.
- **Self-grading.** "I reviewed my work and it's correct" is not a judge.
- **Role-play.** Personas, dialogue, "as a CFO I'd say". Methods, not voices.
- **Altitude on taste.** Creative work keeps the user's taste as the outcome.
- **Every axis in full, every time.** Lead with one; the others get a move.
- **Placeholders.** "N days", "a stated tolerance", "an agreed threshold".
  Pick the number and label it a starting value.
- **Asking for access that doesn't exist.** All three axes assume the model
  has a computer and the relevant data. Say what's missing; don't pretend.

## Why this works

People trust themselves only in narrow lanes; Michelangelo turned down the
Sistine Chapel because he was a sculptor, not a painter. Psychology calls the
remedy self-efficacy, and it can be induced. Locke and Latham's review of 35
years of goal-setting research found that specific hard goals beat "try your
best." George Dantzig solved two open problems in statistics because he
thought they were homework. The four-minute mile stood for decades and then
fell to a second runner 46 days after Bannister. Set the harder goal, show
that it has been done, and allow the attempt to fail.
