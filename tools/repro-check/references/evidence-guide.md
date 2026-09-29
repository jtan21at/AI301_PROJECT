# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

**Where it lives:** In an eval bundle, compare the issue's version,
platform, configuration, and trigger conditions with the repo-facts asks
and the repro report's environment lines. In live mode, check the issue
body and maintainer replies, the repository's bug-report template and
setup docs, and the environment written in the draft repro comment.

**What good looks like:** The report names the tested project version or
revision plus every platform, runtime, install/build, backend, hardware,
or configuration fact that could affect this bug. It need not duplicate
irrelevant system inventory. A different version or platform is valid
evidence only when the difference is disclosed and the conclusion is
limited or supported by an appropriate control.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

**Where it lives:** In an eval bundle, read the issue's minimal example
and thread clarifications first, then locate the repro report's setup,
fixtures, configuration, commands, and ordered actions. In live mode,
also consult the repository's setup and contribution docs and verify that
everything a reader needs appears in, or is publicly linked from, the
draft comment.

**What good looks like:** Starting from a named state, a stranger can
create the input and execute every essential action through the trigger.
Commands retain issue-significant flags, syntax, ordering, and values.
Private repositories, hidden configs, unexplained credentials, or steps
such as "set up the project" without reproducible detail are gaps.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

**Where it lives:** Compare raw artifacts in the repro report, including
terminal output, exit status, logs, screenshots, measurements, and control
runs, with the issue body's exact observed and expected behavior and any
maintainer clarification. Expected/actual prose helps interpret an
artifact but is not a substitute for one.

**What good looks like:** The artifact makes the issue-specific symptom
observable and comes from the stated trigger. A similar error, a normal
version banner, an application merely running, or prose saying "confirmed"
does not prove the target. For cannot-reproduce, the artifact must show a
faithful attempt and the relevant non-occurrence; useful controls separate
the suspected condition from ordinary behavior.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

**Where it lives:** Cross-check reproduction claims, expected/actual
statements, frequency claims, root-cause language, and the claim comment
against the report's artifacts. Look for differences admitted in the
environment and steps and for scenarios the author explicitly did not
test.

**What good looks like:** The words say only what the evidence shows.
An honest cannot-reproduce records the real attempt, observable result,
important differences, and a bounded next hypothesis. A reproduced
result identifies the matching symptom without turning an exit code or
nearby error into proof. Unsupported certainty and unmarked causal guesses
fail even when confidently written.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

**Where it lives:** In an eval bundle, compare both candidate comments
with the issue details and the repo-facts bug-report and contribution
policies. In live mode, read the current issue thread, `.github` issue
templates, `CONTRIBUTING` or equivalent, and any AI policy before checking
the drafts. The voice guide adds personal rules in live mode but does not
replace repository policy.

**What good looks like:** A claim names the particular behavior or code
area and a realistic investigation/reporting step. It does not demand
ownership, post an interchangeable "+1", guarantee a fix, or invent a
deadline. The package supplies information the repository explicitly
requires. When the policy requires AI disclosure, the comment states the
tool and extent and reflects human review; do not invent a disclosure
requirement where the captured policy has none.
