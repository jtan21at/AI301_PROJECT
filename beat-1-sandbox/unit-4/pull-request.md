# Unit 4 — Test and Submit

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/190

Opened against `codepath/pathreview-ai301-fa26-s3:main` from the student's
fork. Public title and description were verified against the prepared
text; the description includes all PR-template sections, `Closes #72`,
actual before/after output, all four project-check results, generic AI
assistance disclosure, and limitations. CI was left unchecked at creation.

**Branch**

`fix/72-invalid-password-hash`

Head commit: `a8617308aff2fa7149a50fbd14f6c5c74e9fa80b`.
The committed diff contains only `core/security.py` and
`tests/unit/test_security.py`. Local `plan.md`, `comment.md`,
`pr_draft.md`, and `test_evidence.md` were not committed to the fix branch.

## Eval iterations

**Run history**

No official harness run occurred because the course model quota was
exhausted. One informal assistant review graded all 20 scored Markdown
packages using the installed skill, with gold labels withheld until all
80 per-check grades and 20 verdicts were frozen. It produced 6 accept
and 14 reject verdicts. The subsequent answer-key comparison found
19/20 agreement. categories: clear-accept 6/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3.
No paid or partial model runs, revised-score claims, or official PASS are
claimed. `eval-run.txt` contains the same unofficial 19/20 result
and all original check judgments, with provenance explicitly stated.
This alternative does not fulfill the requirement for a harness-written
full run; staff acceptance and any evaluation credit remain unconfirmed.

**Package analysis**

`pkg-03`: the frozen review verdict is `reject`; the gold verdict is
`reject`. The plan excludes a config-surface change, but the diff adds
`resolve_symlinks` and rewrites `truncate()` alongside the fallback fix.
The description claims “Implements the posted plan exactly” and
“No other behavior changes,” without reconciling those additions in the
plan's deviations. The silent-drift check therefore fails; the unrelated
hunks also make the diff less reviewable. A working main fix cannot
justify the false fidelity claim or the unannounced configuration change.

**Check rationale**

> | silent-drift | Plan context's intended behavior, in/out scope, named files or areas and deviation notes, paired with every diff hunk and the PR title/description's fidelity claims; issue and repro define the original outcome. | The diff delivers the plan's bounded outcome or a concretely disclosed, justified revision tied to the same issue. Necessary implementation and regression-test files need not have been individually enumerated. Material additions, omissions, and behavior changes are reconciled in plan/deviation context and accurately described; no silent scope expansion, unexplained incomplete implementation, or contradicted fidelity claim remains. An honest narrower outcome can pass when its limits and reason are explicit and it still meaningfully addresses the issue, not merely conceals the symptom. | required |

I wrote this around paired behavioral evidence rather than requiring that
every supporting file be listed in advance. Regression tests can fit an
issue-sized plan implicitly; new unrelated features cannot. I rejected a
blanket rule that any deviation is failure: a specifically explained,
meaningful narrower outcome can be ready, while a confident description
claiming exact fidelity over additional unplanned behavior must be held.
No official eval revision or rerun is claimed.

**Trade-offs**

This strict comparison can hold a genuinely honest shortfall when unseen
caller behavior or submission metadata remains uncertain. In `pkg-16`,
the review returned reject while gold accepts the narrowed image-load fix:
the startup behavior was explicitly deferred in both plan and description,
but the review was not convinced the shared helper preserved startup
behavior and treated required CLA status as unclear. I retained that
original judgment after seeing the key rather than inventing a revision
or rerun. The trade-off favors checkable fidelity over accepting plausible
but unseen behavior; future calibration should distinguish a recorded,
maintainer-aware deferral from hidden missing functionality.

## Actual change validation

The PR description includes the full captured commands and output:

- Original trigger: UnknownHashError; after: False.
- Targeted regression: normal pass, not xfail or strict XPASS.
- Security module: 25 passed.
- `make test-unit`: 376 passed, 52 xfailed; exit 0.
- `make lint`: All checks passed; exit 0.
- `make typecheck`: no issues in 76 source files; exit 0.
- `make test-integration`: 0 collected, pytest exit 5 / make exit 2.
  The assignment explicitly anticipates no integration tests; this is
  disclosed and its pass checkbox is not ticked.

Initial full-check attempts were blocked by missing local dependencies
and tools. After installing already-declared dependencies into the local
venv, the final captures above were obtained without source changes.
Existing Pydantic/cache-permission warnings and unrelated seeded xfails
are retained. CI was not claimed green at opening. The initial informal
PR precheck accepted readiness to OPEN; maintainer review remains gated
by the repository's green-CI policy.

## Remaining manual actions

Ask course staff whether the honestly labeled non-harness evaluation is
acceptable or whether additional course quota is available. Submit the
whole course repository URL in the course portal, enter actual hours
spent, and disclose the alternative evaluation. CI is now verified green; no workflow-approval action is pending.

## CI result verified after opening

The PR was opened with the CI checkbox unticked, as required. GitHub then
completed all five jobs successfully on the submitted head commit:
`lint`, `typecheck`, `test-unit`, `test-integration`, and `frontend`.

Run: https://github.com/codepath/pathreview-ai301-fa26-s3/actions/runs/38424729582

The captured API summary is in `ci-status.json`. The successful CI
integration job does not change the actual local 0-test result recorded
in the original PR evidence. No workflow approval is currently pending.
