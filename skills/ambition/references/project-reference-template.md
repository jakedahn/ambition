# Ambition in <project>

Copy this file to `references/<project>.md` and fill it in. The skill reads
it when a task is about this project, so the block it writes names real
things instead of generic ones. Point, don't restate: a fact about the code
belongs in the code's own guide, and this file links to it.

## The ceilings

Outcomes the product and its users imply. Three to six lines. Each one is a
sentence about the world, not about a feature: "a customer's engineer
depends on it most days", "anything their old tool exports opens here,
proven by round-trip". Edit when the aims move.

## Ladders that fit this project

Two to five ladders, one line each, from the literal task to the owning
rung to the redesign: "fix this import bug; every file a customer has sent
opens; the corpus is replayed nightly and the top failure class is fixed
each week; anything their tool exports opens".

## Raw material that exists here

Where the undigested data lives, with the pointer to reach it: product
events, the records of what users did, operations series and logs, test
corpora and benches, the ground truth the domain has (verification cases,
closed-form answers), CI history, the issue tracker and design records, the
voice of the customer. Name what is consent-gated or private, and the rule
for naming customers (usually: don't).

## Instruments the best in each field use

Per discipline the project touches: the named tools, checks and methods a
leading practitioner would insist on, and the make target or skill that
runs them. Say when an instrument does not fit the data (three customers is
not a regression).

## Outside judges already built

What, other than the model or the user, shows a result is right: the
running product driven end to end, the hermetic test lanes, ground-truth
cases, corpora with exact-match rates, benches with statistics, production
after deploy, a real customer's real input.

## What an agent here can reach

Locally, through connectors, and what it must not do without a person
(infrastructure applies, production writes, force-pushes). Those last go
in "what it needs" as decisions, never worked around.

## The crew

Methods, not voices. One line per role: what they check. Include a red team
(the power user trying to break it in ten minutes; the short seller reading
the numbers for the one that doesn't reconcile; the operator reading the
dashboards for the alert that would never fire).

## Where a next rung lives

Where an accepted next rung is recorded so it outlives the conversation: a
line in the area's plan file by PR, or an issue. Say which, and the default.

## Areas for `/ambition <area>`

The directories that count as areas, and which guide covers each.
