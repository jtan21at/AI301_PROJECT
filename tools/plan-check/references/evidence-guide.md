# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Eval: read Issue and Repro evidence before Candidate plan's cause. For example, calib-01 records a successful remote update and stale color until re-entry; the cause must explain that distinction, not claim the push failed.
- Live: read issue body and the student's posted Unit 2 repro comment, then diagnosis and repro quotations in plan.md and comment.md. Only the drafts' contained or quoted evidence supports the package; files elsewhere are not implicit evidence.
- Good: a cause accounts for the same trigger and actual observation; a hypothesis is labeled and paired with a discriminating check. A traceback identifies an observed failure site, not automatically the entire cause.

## Scope

- Eval: Candidate plan's Change, In, Out, files, and areas; compare with Issue and repro-supported cause.
- Live: draft scope, exclusions, files-to-touch, approach, and any recorded deviations.
- Good: every changed behavior serves one issue-sized outcome at the causal layer. Implementation plus regression tests is bounded; unrelated architecture work or masking the visible symptom is not. Explicit headings are not required if boundaries are clear.

## Executability

- Eval: Candidate plan's approach, named locations, ordered operations, and investigation gates. In calib-01, the sync controller push callback and commits-context refresh identify a concrete next edit.
- Live: plan.md's files and approach, checked against the draft comment's promised strategy. Repository inspection may verify plausibility but cannot supply an absent strategy on the author's behalf.
- Good: another contributor can start a named operation, resolve dependencies in a stated order, and choose among unknown options using a supplied criterion. Exact line numbers are optional; 'fix the bug' is not an operation.

## Test plan

- Eval: Candidate plan's tests and expected outcomes compared with Repro evidence's steps, inputs, controls, and artifacts. In calib-01, the color must change at step 3 without leaving the view; a remote ref update alone would not prove the UI fix.
- Live: draft test commands or manual steps, expected post-fix results, quoted Unit 2 trigger and baseline, and relevant regression checks.
- Good: an observation separates the original failure from the intended behavior through real affected code. Valid-password controls matter for an invalid-hash fix; broad test-suite promises alone are insufficient. Manual checks can be decisive.

## Honesty

- Eval: Candidate plan's certainty, risks, unknowns, and deviation notes compared with the limits of Repro evidence and the issue discussion.
- Live: draft risks and unknowns and plan.md's Deviations, compared with quoted baseline evidence and posted plan.
- Good: material unresolved causes or behavior changes are named with a way to verify or mitigate them. A build change is explained rather than hidden. Do not require speculative risks or a deviation note in an unbuilt practice plan.

## Comms

- Eval: Candidate plan comment versus Candidate plan, Thread highlights, and Repo facts, including contribution policy and explicit AI-use requirements. In calib-01 selective PR review is a review-bandwidth constraint, not a blanket ban on issue comments.
- Live: issue body and relevant maintainer replies, CONTRIBUTING or other applicable repo policy, scope.md house rules, draft comment, and voice-guide.md.
- Good: the comment contains its own grounded, bounded proposal and observable validation consistent with the plan, responds to actionable maintainer requests, and follows stated disclosure rules. Referencing quoted repro steps is valid shorthand; 'same approach as above' is not an independent plan. Path Review classmates do not block each other's plans. Eval mode does not read personal voice or live GitHub.
