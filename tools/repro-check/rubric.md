# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-specific-and-honest | The candidate claim comment, read against the issue title/body and thread highlights. | The comment identifies the particular behavior or code area being investigated, states a concrete next investigation or reporting step, and makes no unsupported claim of reproduction, entitlement to assignment, guaranteed fix, or deadline. A claim made before reproduction may promise an investigation and report, but not its result. | required |
| environment-recorded | The repro report's environment record, read against environment details in the issue and the repo-facts bug-report asks. | The record identifies the tested project version or revision and the platform, runtime, build/install source, configuration, hardware, or backend details that could materially change this issue's trigger. Differences from the issue's target are named and either controlled for or treated as limits on the conclusion. | required |
| steps-rerunnable | The repro report's starting state, fixtures, configuration, and ordered commands/actions, read against the issue's stated trigger. | A stranger can recreate the needed inputs using public or fully included material and follow the attempt from a stated starting state through the trigger. No essential command, option, credential, private repository, configuration, or issue-specific action is omitted. | required |
| behavior-matches-target | The repro report's raw artifacts (output, logs, measurements, screenshots, or control results), compared with the issue's described trigger, observed behavior, and expected behavior. | The artifacts visibly test the same trigger and distinguish the reported behavior from an adjacent error or normal operation. A reproduction shows the issue-specific symptom; a cannot-reproduce shows the attempted trigger and observable non-occurrence. Version or input deviations are not silently substituted for the target. | required |
| conclusion-supported | The claim comment and the repro report's result, expected/actual statements, and causal language, checked against the artifacts and disclosed limits. | Every conclusion stays within what the shown evidence establishes. Reproduced and cannot-reproduce outcomes are stated plainly; inconsistencies, changed versions, failed controls, or untested scenarios are disclosed. Root-cause claims are either directly evidenced or clearly labeled as hypotheses. | required |
| repo-conventions | The repo-facts bug-report asks and contribution/AI policy, compared with both candidate comments and the repro report. | The package supplies the convention-required information relevant to an issue comment and follows any stated communication or AI-disclosure rule. If disclosure is required, it names the tool and extent of assistance; if the captured policy does not require issue-comment disclosure, absence of one passes. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only when every required check passes. Reject when any required
check fails or is unclear, because missing evidence cannot establish that
the package is ready to post. Preferred checks, if added later, may improve
the report but never change the verdict.
