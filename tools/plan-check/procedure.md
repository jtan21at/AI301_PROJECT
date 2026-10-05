# Procedure: how this skill grades a plan package

## Read order

1. Identify eval versus live mode. In eval mode use only the frozen bundle and ignore scope and voice. In live mode first read scope.md and stop without grading if the repo is unfilled or the issue is outside it; then read voice-guide.md.
2. Read rubric.md and references/evidence-guide.md. Record each check and weight. Stop if either rubric checks or procedure steps are empty.
3. Read the issue, thread highlights or live thread, and repo facts or applicable contribution docs before the drafts. Record the trigger, expected behavior, maintainer constraints, and explicit policies, without assuming unstated rules.
4. Read repro evidence next. Record actual inputs, environment, observations, controls, and what the evidence does and does not establish.
5. Read the candidate plan, then its comment. Record the stated cause, changes, exclusions, files or areas, operations, tests with expected results, uncertainty, and deviations. This order prevents the plan's confident wording from redefining the evidence.

## Evidence gathering

1. For grounded-diagnosis, pair the plan's causal claim with the exact repro observation it explains. In live mode compare with the student's posted repro, but only evidence quoted or contained in the drafts supports their package; external files cannot silently repair a missing quote.
2. For bounded-root-fix, map each proposed change to the diagnosis and identify exclusions or clearly implied boundaries. Note unrelated work and symptom masking.
3. For executable-approach, record the named implementation location, first action, following operations, and dependency or investigation gates. Use areas when the package does not provide exact paths.
4. For decisive-tests, pair each planned input or repro step with the expected post-fix observation and relevant control. Record whether the check reaches real affected code; do not demand automated tests where a decisive manual check is appropriate.
5. For honest-uncertainty, compare certainty claims to repro limits and note each material risk with its mitigation. Read deviations if present, but do not invent missing risks.
6. For thread-and-conventions, compare the comment's actual text with the plan, maintainer requests, and explicit repo rules, including AI-use policy. In live mode also record voice-rule violations with the rule quoted. In eval mode never apply personal voice rules.

## Check execution

1. Execute all checks in table order, even if an earlier check fails. Use the evidence gathered for that check, rereading the relevant pair of sections only when needed.
2. Assign pass only if the stated pass condition is supported. Assign fail for a contradiction, an absent essential plan component, or an explicit rule violation. Assign unclear when evidence is present but cannot decide the condition. Never infer a favorable missing fact.
3. For each grade, quote or identify the decisive fact in one line; for absence, name the missing evidence and its expected location. Do not grade the formatting or insist on headings, line numbers, or a fixed number of tests.
4. A tentative diagnosis can pass if it fits the repro and has a concrete discriminating investigation before choosing the fix. A vague promise to investigate cannot replace an approach. A failed comms policy check is not rescued by otherwise strong tests.
5. If the procedure leaves an actual gap, report it in the summary rather than making up a step. Do not use gold labels as evidence or tune a grade to an expected score.

## Verdict assembly

1. Apply the rubric's verdict rule to all checks: accept only if every required check passes; reject if any required check fails or is unclear. Preferred checks never gate.
2. Before the JSON, summarize the deciding evidence and any live voice-rule violation. State a concrete revision for a held check without rewriting or posting the plan yourself.
3. Emit a final fenced JSON object with item (bundle id or issue URL), checks (name, grade as pass/fail/unclear, evidence), and verdict (accept/reject). Include every check, validate JSON syntax, and write nothing after the block.
