# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Grounded diagnosis | The plan's stated cause compared with the issue and reproduction steps, results, and controls. | The proposed cause explains the observed behavior without contradicting the evidence. An unproven cause is identified as a hypothesis with a concrete check before dependent changes. For an enhancement, the plan identifies the supported behavior gap without claiming the missing feature was tested. | required |
| Bounded scope | The plan's included and excluded behavior, named files or areas, and approach compared with the issue's requested outcome. | The work is one bounded change directed at the supported cause or behavior gap. Each included change is necessary; unrelated rewrites or features are excluded. | required |
| Executable approach | The plan's work sequence, target files or functions, and decisions compared with repo facts and reproduction evidence. | Another contributor can start the work and determine what behavior to implement. Material dependencies and decision points are resolved or have a concrete verification step before dependent work; required changes are not left as vague intentions. | required |
| Observable validation | The plan's tests and expected results compared with the reproduction inputs, outputs, and failure conditions. | A repeatable test exercises the relevant behavior and states what distinguishes before from after. It tests the supported cause or requested enhancement, not only an incidental symptom, and includes relevant failure or boundary behavior. | required |
| Honest uncertainty | The plan's claims, risks, unknowns, and any deviations compared with issue facts and reproduction evidence. | Claims stay within the evidence. Material risks and unknowns have explicit handling; proposed tests are not described as completed, and deviations are explained when present. | required |
| Thread and policy alignment | The draft comment compared with maintainer requests, thread highlights, and stated contribution rules. | The comment addresses applicable requests and conventions, including disclosure when the package establishes it is required. It neither contradicts maintainer direction nor relies on another student's plan as its own. Do not invent policies or assume undisclosed AI use. | required |
| Useful plan comment | The candidate comment compared with the candidate plan and quoted reproduction evidence. | The comment conveys the issue-specific finding, bounded change, and observable validation, with enough evidence for a maintainer to assess the proposal. It agrees with the plan, distinguishes proposals from results, and makes no unsupported promise. Judge substance, not length or headings. | required |
| Related behavior | The plan's regression checks compared with affected callers and adjacent behavior described in the package. | The plan names a relevant existing behavior that must remain intact and how it will be checked. | preferred |

## Verdict rule

Return `accept` only when every required check is `pass`. Any required `fail` or `unclear` returns `reject`. Preferred checks never change the verdict. Use `fail` for a contradiction or a demonstrably missing required plan element; use `unclear` when the supplied evidence does not allow a decision.
