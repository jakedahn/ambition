# ambition

A Claude Code plugin with one skill, `/ambition`. It turns a task into the
version a more ambitious person would have asked for, and says what that
version needs.

The method is entirely Felix Rieseberg's, from [How to be more ambitious: A
tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/).
The post is the instruction; this plugin is the post turned into a skill
the model follows every time. Beyond speed, ambition has three axes:

- **Altitude.** What do you want to happen next? Climb from the literal
  task to the rung where the agent owns the outcome ("keep CI trustworthy",
  not "fix this flaky test").
- **Depth.** Do it the way the best person in the field would: from the
  rawest material, with their real instruments, to a hard number, with an
  outside judge that is neither the model nor you.
- **Range.** Turn the task's nouns into verbs, assemble the crew, and take
  each member's method, never their voice.

What comes back is one block, about 800 words and never more than 900: the
goal beyond the goal, the rewritten ask (paste-able), what changed tagged by
axis, what it needs (data, access, the judge, and at least one decision you
must make), and the next rung with what unlocks it.

See [examples/flaky-ci.md](examples/flaky-ci.md) for a full response to
"I keep asking Claude to fix flaky CI tests one at a time. What should I be
asking for instead?"

## Install

```
/plugin marketplace add jakedahn/ambition
/plugin install ambition@jakedahn-ambition
```

The repository is private, so the machine adding the marketplace needs git
access to it (the `gh` CLI's credentials are enough).

To try it without installing, start Claude Code with the checkout loaded in
place:

```
claude --plugin-dir /path/to/ambition
```

## Use

- `/ambition` alone, mid-conversation: apply the method to the task in
  progress.
- `/ambition <prompt>`: rewrite that ask.
- `/ambition <area>`: read a directory's README, contributor guide and plan,
  and propose the rung above the plan.

The skill also triggers on its own when a request reads as a method rather
than an outcome, or when someone asks to think bigger, go deeper, or
"what should I be asking for instead".

## Make it know your project

The skill reads `skills/ambition/references/<project>.md` when a task is
about that project. Copy `references/project-reference-template.md`, name
it for your project, and fill in the ceilings, the raw material that exists,
the instruments, the judges already built, what an agent can reach, the
crew, and where an accepted next rung gets recorded. With it, every line of
the block names a real thing; without it, the block is generic.

## Tests

`skills/ambition/evals/evals.json` holds the prompts and assertions the
skill was built against with Anthropic's skill-creator loop. Across three
prompts it scored 11/11 on every case while the same model without the
skill scored 8/11, mostly on stating the goal, naming a next rung with its
unlock, listing the access it needs, and staying under 900 words.
