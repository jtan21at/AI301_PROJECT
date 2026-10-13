# Procedure: how this tool grades a PR package

## Read order

1. Identify mode. For live mode read scope first, verify target identity and stop for an unfilled or out-of-scope repo; then read voice. Eval mode reads neither. Read rubric and evidence guide, and verify authored checks and procedure steps exist before grading.
2. Read issue, thread and repository standards before candidate prose. Record the trigger, expected behavior, explicit maintainer direction, required template content, AI policy, applicable checks and any hard submission gates. Do not infer policies from silence.
3. Read original repro and accepted plan or house equivalents, then all deviation notes. Record intended outcome, scope and exclusions, changed areas, test steps and expected observations. This baseline must precede the diff so confident PR prose cannot redefine the plan.
4. Read the complete diff and commit list. Inventory every changed file and behavioral hunk, pairing each to planned work or a disclosed deviation. Read the draft title and description next; record claims and requested-content coverage.
5. Read test evidence last against the baseline, diff and claimed validation. Record commands/manual steps, actual inputs, environment, revision when available, before/after output, controls, suite outcomes, failures, omitted checks and explanations. Do not fill missing evidence from memory or execute new tests.

## Evidence gathering

1. For silent-drift, construct a pairing for each material planned outcome and every changed behavior: plan/issue fact, diff file and hunk, deviation note if needed, and matching description claim. Record both extra work and missing work. Supporting regression tests can fit implied scope; a new unrelated feature cannot. A specific disclosed narrower outcome is evaluated as revised work, not silently marked incomplete.
2. For not-tested, pair each repro/test-plan expectation with its actual candidate evidence. Separate raw captured results from summary assertions and code-based deductions. Record each repo-required check as observed pass, observed fail, reported only, or not run; attach reasons and residual risk for gaps or failures. Identify any explicit hard gate. A failure summary can establish that failure was disclosed, never that a test passed. A concrete manual observation with steps and actual observed behavior may be evidence without a console transcript.
3. For unreviewable, inspect every hunk for unrelated edits and debris. Name the file/hunk and why it obscures review; distinguish required generated changes or local formatting from unrelated churn. Use commits for context, not a numeric limit.
4. For standards-wall, list each actual policy/template/thread ask and pair it with substantive PR text or verified live submission metadata. Identify absent requirements and placeholders. Do not reject alternate headings, concise answers or equivalent organization absent an explicit formatting mandate. Apply only captured repo rules in eval mode. In live mode record voice violations separately, quoting rule and draft text; do not add them as verdict checks.

## Check execution

1. Execute silent-drift, not-tested, unreviewable, standards-wall in that order, even after failure. Reuse gathered evidence and reread the specific paired sources when necessary rather than silently adding evidence.
2. Assign pass only when the row's condition is supported; fail for a concrete contradiction, explicit violation, or essential evidence absent from a complete package. Use unclear when available evidence is ambiguous, truncated, or cannot establish a necessary fact. Missing nonessential headings are not missing evidence. For each grade give one decisive source/quote or describe exactly what is absent and where it should appear.
3. Evaluate disclosed departures and failed checks against the row's honest-outcome exception. Require specific limits/reasons, meaningful remaining issue validation and compliance with explicit hard gates. Do not turn a failed command into a passing command, or excuse a bare lack of testing by calling it honest.
4. Do not mark a command successful from “tests pass” or a rendering summary alone. Record those as reported/unverified. When a diff establishes a retained value, describe it as a diff-derived fact, not a successful runtime smoke test. A missing optional smoke capture is not by itself fatal if remaining observable proof satisfies the row and no rule makes that capture mandatory; unsupported runtime claims must not overstate what that proof establishes.
5. If a procedure gap prevents a check from being decided, report the gap, grade the affected check unclear, and use the normal verdict rule. Never invent checks, consult labels, or bend a condition toward an expected verdict.

## Verdict assembly

1. Accept only when all required checks pass; required fail or unclear holds the package. Include every check in rubric order. Preferred findings do not gate.
2. For rejection, use the first non-pass required check in rubric order as the deciding check in the readable summary, quote its decisive evidence or missing source, and give a concrete revision or evidence request. Mention other held checks without hiding them. For acceptance state what the evidence establishes and any disclosed limitations, not that all tests passed.
3. Report live voice findings separately with the rule quoted. Emit valid final fenced JSON with item, checks and verdict in the contract order; each check has name, grade and one-line evidence. Use supplied PR URL or stable candidate id, or bundle id. Validate allowed grades and binary verdict, and write nothing after the block. Refusals before grading do not invent a JSON verdict.
