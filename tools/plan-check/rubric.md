# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| grounded-diagnosis | Candidate plan's cause and quoted repro evidence, compared with the issue trigger, observed result, and expected result. | The diagnosis explains the reproduced behavior without contradicting its artifacts or replacing the trigger. An unproven cause is identified as a hypothesis with a concrete verification step, not asserted as established fact. | required |
| bounded-root-fix | Candidate plan's change, in/out scope, and named files or areas, compared with the diagnosis and issue. | The proposed change addresses the cause at the responsible layer and stays within one issue-sized outcome; related implementation and regression tests are allowed, but unrelated rewrites, features, or symptom-only workarounds are not. Scope boundaries can be evident from concrete work rather than a separate heading. | required |
| executable-approach | Candidate plan's files or areas, operations, sequence, and dependencies. | A contributor can begin the next concrete operation and follow a plausible path to the fix without inventing the strategy. Exact line numbers and exhaustive pseudocode are unnecessary; unresolved design choices need a specific investigation and decision criterion before implementation. | required |
| decisive-tests | Candidate plan's test steps and expected observations, read against the repro evidence's inputs, commands, and artifacts. | Tests exercise the reproduced trigger through real affected code and name an observable outcome that distinguishes fixed from broken behavior. Include a relevant control or regression check when the change could alter neighboring behavior. Manual tests are valid; a bare promise to run tests or a stand-in that only copies the bug is insufficient. | required |
| honest-uncertainty | Candidate plan's claims, risks, unknowns, and any deviations, compared with issue and repro evidence. | Claims do not outrun the available evidence. Material uncertainties or risks exposed by the package are acknowledged with a check or mitigation; recorded deviations explain what changed and why. Do not require a risks or deviations section where no material uncertainty or build deviation is shown. | required |
| thread-and-conventions | Candidate plan comment and plan, compared with thread highlights and repo facts; live mode also reads contribution docs and the voice guide. | The comment independently communicates a diagnosis, bounded approach, and meaningful validation consistent with the plan, respects applicable maintainer requests and stated contribution policy, and includes required AI disclosure. A reference to quoted repro steps can supply test detail. Do not invent repo rules or treat a classmate's plan as ownership in Path Review. | required |

## Verdict rule

Return `accept` only when every required check is `pass`. Any required
`fail` or `unclear` produces `reject`; a `?` means `unclear`, not a partial
pass. Preferred checks, if added later, never change the verdict. Judge
substance, not length, headings, confidence, or the presence of a PR.
