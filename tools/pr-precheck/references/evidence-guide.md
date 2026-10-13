# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Eval: Issue and Thread highlights define the outcome; Plan context contains accepted scope, exclusions, files/areas, repro and test plan, including any deviation notes. Pair these with Candidate PR Diff, Title and Description. Structured bundles carry the same material in issue, thread_highlights, plan_context_markdown and pr fields.
- Live: issue body, relevant maintainer replies, posted plan and `plan.md` including deviations (or house plan and repro pack), complete three-dot branch diff against the verified default branch, draft PR title and description.
- Good: every material changed behavior and promised outcome fits the bounded plan or a specifically explained same-issue deviation. Supporting implementation and regression tests may be implied. Disclosed less-than-planned work can be ready when its meaningful outcome, omitted work and reason are clear; silent extra scope, missing functionality without a note, and contradicted claims are drift. A retained value visible in a diff proves that textual value was retained, not that rendering was tested.

## Test evidence (harness category: not-tested)

- Eval: Plan context's repro/test expectations and Repo facts' required checks, paired with Candidate PR Test evidence and diff. Locate actual commands or manual steps, inputs, environment, before/after observations, relevant controls, suite outcomes and disclosed omissions/failures. Do not require facts absent from captured policy.
- Live: `plan.md` test plan, posted repro or house repro pack, captured branch test output or concrete manual observation records, revision/environment information, and check commands stated in contribution docs or applicable repository check configuration. Inspect supplied evidence only; do not run tests or alter captures.
- Good: the original trigger reaches changed code and produces a discriminating observed result. A broad unrelated suite alone does not prove the fix. Captured output and specific manual observations establish results; “tests pass” or “renders unchanged” alone is a report, not proof of a passed test. Label reports, diff deductions and captured observations separately. Honestly disclosed failures or justified unrun secondary checks can coexist with readiness when meaningful proof remains and policy does not demand successful completion. Unexplained missing repo checks or no observable issue proof fails.
- Calibration reading discipline: calib-01 contains strict-parser before/after output and a concrete single retained config-value result. Its smoke rendering sentence is only a summary; do not claim a verified successful rendering run from it. The retained value in the diff independently supports a last-wins value argument, not runtime verification. Grade general conditions, never a package-specific exception or expected label.

## Diff quality (harness category: unreviewable)

- Eval: Candidate PR unified Diff and Commits, compared with Plan context and deviations. Read all supplied hunks; a commit subject does not prove its contents.
- Live: full branch diff from the verified default-branch comparison and full candidate commit list, paired with scoped plan/deviations. Note if supplied/tested working-tree changes are not in the branch comparison.
- Good: every hunk serves the same bounded change and exposes the fix for review. Debug leftovers, unused replacement code, large commented-out blocks, unrelated edits and gratuitous formatting/generated debris are failures when they bury or contaminate the change. Necessary generated artifacts or formatting are not automatically debris; identify their causal role. Commit count, prose length and template appearance do not determine reviewability.

## Standards and comms (harness category: standards-wall)

- Eval: Repo facts' PR-template asks, contribution and disclosure policy, plus actionable Thread highlights; pair each with Candidate PR Title/Description and any supplied submission metadata. If facts say no template or no AI policy, do not invent one. Personal voice and live scope are not evidence here.
- Live: the actual repository PR template in its stated location, `CONTRIBUTING.md` or other applicable contribution/policy documents, relevant maintainer requests, and scope house rules, paired with draft title/description and supplied fork/branch/base metadata. Read personal voice for separate summary notes only.
- Good: requested content is real and issue-specific, an issue reference is supplied when asked, actionable direction is addressed, and required AI assistance disclosure is present without inventing provider/model details. Equivalent substantive organization counts unless exact form is explicitly required. Empty placeholders are not content. Record each required ask and its matching text; distinguish an honest unsuccessful check result from ignoring a testing section or falsely claiming success.
