# Evidence guide: where evidence lives in a plan package

In eval mode, the bundle is the entire evidence source. In live mode, use the scoped issue, repository documents, the student's posted reproduction, and the supplied drafts. An unquoted local file cannot repair an incomplete plan package.

## Diagnosis and grounding

- Eval: issue context and repro-evidence block, compared with the candidate plan's diagnosis.
- Live: issue body and relevant maintainer comments, the student's posted reproduction comment, and the diagnosis and quoted evidence in the drafts. Use the house reproduction pack only when the course routes the student there.
- Good: the cause explains the actual observations and controls. For an enhancement, an established missing behavior supports a proposal; a mocked pass-through baseline does not validate the future feature. A hypothesis includes a concrete way to check it before relying on it.

## Scope

- Eval: candidate plan's scope, exclusions, named files or areas, and approach, compared with the issue and repro evidence.
- Live: the same parts of plan.md and the comment, checked against the issue's requested behavior and relevant source paths.
- Good: every change serves one supported outcome. File count alone does not determine scope. Necessary shared-code changes can be bounded; unrelated cleanup is not justified by proximity.

## Executability

- Eval: candidate plan's work sequence, affected code, decisions, and dependencies; cross-check the repo-facts and repro blocks.
- Live: plan.md and comment, with relevant source and CONTRIBUTING documentation checked for stated interfaces and workflow.
- Good: a contributor knows where to begin, what behavior to produce, and how blocking unknowns will be resolved before dependent work. Do not demand code already be written in a plan.

## Test plan

- Eval: candidate plan's validation steps and expected outcomes mapped to the repro-evidence inputs, controls, and observed failure.
- Live: proposed tests and quoted Week 2 evidence, including the original commands or inputs when relevant.
- Good: a repeatable check can distinguish the current behavior from the desired behavior and names the expected observation. Include relevant failure cases and preserve adjacent behavior. Merely running a test suite or checking output exists is insufficient when neither tests the proposed change.

## Honesty

- Eval: diagnosis, risks, unknowns, and deviations compared with all supplied source facts.
- Live: equivalent draft sections compared with the posted reproduction and issue evidence.
- Good: observations, hypotheses, proposed checks, and completed checks remain distinct. Unknowns have a handling step. Absence of a deviation section alone is not a failure when no deviation is established.

## Comms

- Eval: candidate plan comment against the plan, issue thread highlights, and repo-facts block's contribution rules and AI policy.
- Live: draft comment against plan.md, relevant issue comments, CONTRIBUTING, applicable templates, and explicit AI policy. Also read the voice guide for separate wording feedback.
- Good: the comment explains this plan's finding, bounded approach, and validation, follows applicable maintainer requests, and includes required disclosure when the evidence establishes that requirement applies. A classmate's plan does not block a student's own plan in the course repository. Do not assume hidden AI assistance from the fact that a course authored an eval package.
