# Evidence guide: where proof lives in a reproduction package

In eval mode, use only the provided issue context, repo-facts block, claim, and report. Do not fetch live evidence to fill snapshot gaps. In live mode, inspect the issue and relevant thread, repository instructions, and the supplied drafts. The candidate report consists of what the drafts contain and quote, not unmentioned files elsewhere on the author's machine. Cite the decisive fact or excerpt for each grade; absent evidence is unclear, not an invitation to invent it.

## Environment

**Where it lives:** In an eval package, compare the report's environment record with the issue context and repo facts. Live, compare the draft's tested revision, runtime, dependencies, platform, and relevant settings with the issue and repository setup documentation.

**What good looks like:** Another person can identify the tested configuration and reproduce the material conditions. Version or platform differences are explicit, with their effect on the finding bounded. Require details relevant to the issue rather than an exhaustive machine inventory. For model-dependent behavior, identify the model and material generation settings; never include credentials.

Supports `environment-recorded`.

## Steps

**Where it lives:** Read the report's starting state, setup reference, supplied inputs or fixtures, exact commands or UI actions, and the action that triggers the observation. In eval mode these must be in the bundle. Live, follow references in the draft to determine whether the necessary inputs and instructions are available to the intended reader.

**What good looks like:** A reader can follow the same path from setup to observation without guessing a material value or hidden preparation step. A relevant documented setup procedure can be referenced rather than copied. If input is controlled or mocked, the report identifies where it enters the real code and supplies enough detail to repeat it. The number of steps is not a quality measure.

Supports `steps-rerunnable`.

## Behavior shown

**Where it lives:** Compare the issue's specific expected and reported behavior with the report's output excerpts, logs, screenshots, or test results. Read the inputs and procedure associated with each artifact, not the artifact in isolation.

**What good looks like:** The artifact shows the target behavior or a relevant attempt where it did not occur. For example, a dependency import error does not establish a feedback-tone defect. Static inspection can support a claim about missing code, but does not establish observed runtime output. A controlled provider response passed through actual application code can demonstrate how that code handles the response; it cannot prove a live model generated it or how frequently that happens. A mock that directly returns the desired conclusion, or a standalone script that merely restates the expected defect, is not evidence about the application path.

For nondeterministic behavior, record the attempts and actual outcomes and limit conclusions accordingly. Do not require an arbitrary number of runs or insist on reproducing a failure when the relevant evidence honestly shows otherwise.

Supports `issue-matched-evidence`.

## Honesty

**Where it lives:** Read the report's conclusion alongside its expected/observed comparison, environment, steps, artifacts, and limitations. Compare statements of completed work in the claim with the evidence supporting those statements.

**What good looks like:** The author distinguishes observation, interpretation, and open questions. An unsuccessful but relevant attempt is described as cannot-reproduce with the attempted conditions and results. Partial coverage remains partial. Claims of root cause, reliability, or a fix require corresponding evidence; confident wording cannot replace it. A prospective claim promises investigation, not work already completed.

Supports `honest-outcome` and the truthfulness of `issue-specific-claim`.

## Comms

**Where it lives:** In eval mode, use the issue context, repo-facts contribution-policy statements, claim comment, and repro report. Live, inspect the issue's relevant discussion, CONTRIBUTING instructions, applicable templates, and explicitly referenced AI-use rules; compare those with both draft comments. Read the installed scope and personal voice guide as instructed by SKILL.md.

**What good looks like:** The claim names this issue's behavior and a concrete investigation step. The report contributes the author's own evidence and states its result directly. Applicable disclosure and template requirements are met. Policy silence is distinct from inaccessible policy. In PathReview live mode, classmates' claims or reports do not block independent work, but copying their conclusions is not a substitute for personal evidence. These house exceptions never apply to frozen eval bundles.

The main finding and supporting evidence are easy to locate without enforcing a word count. The voice guide informs live feedback on wording, while the rubric controls the verdict. An accepted draft still requires Dennis's approval before posting.

Supports `issue-specific-claim`, `repo-conventions`, and `focused-report`.
