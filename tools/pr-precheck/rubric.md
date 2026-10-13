# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan fidelity | Plan context or plan.md: scope, exclusions, approach, and deviations; compared with every behavior in the diff. | Changes and omissions match the accepted plan or are explicitly explained in its deviation notes and the PR. A disclosed bounded shortfall can pass; silent additions or omissions cannot. | required |
| Accurate PR claims | Candidate title and description compared with the diff, plan, and test evidence. | Claims describe what this change actually delivers and what was verified. No claimed feature, fidelity, test result, or certainty contradicts the artifacts. | required |
| Observable validation | Test evidence compared with the plan's test plan and original reproduction or enhancement requirements. | Concrete inputs, expected behavior, and observed results support the delivered behavior. Missing coverage is disclosed and does not replace all evidence for the change. A mocked flow test is not claimed as live model or UI validation. | required |
| Repository checks | Test-evidence commands and outcomes compared with checks specified in repo facts or contribution instructions. | Required checks have visible execution results, including failures or documented empty suites. Not-run checks have an applicable documented exception, not just a promise to run later. A failed result is not automatically a failure of this row when honestly reported; explicit repository readiness requirements are assessed below. | required |
| Reviewable diff | Unified diff and commits compared with the issue and bounded plan. | The relevant change is inspectable without unrelated cleanup, formatting churn, debug leftovers, dead code, generated debris, or unrelated local drafts. Necessary supporting changes are explained. Disclosure alone does not make unrelated cleanup relevant. | required |
| Stated standards | Repo facts or live template and contribution policy, applicable issue-thread requests, branch and candidate PR text. | The PR meets explicit applicable template, contribution, branch, issue-reference, and disclosure requirements, including documented exceptions. Required sections contain useful content or an explained not-applicable result. Do not invent a policy or infer AI use absent evidence. | required |

## Verdict rule

Return `accept` only if all required checks pass. A required `fail` or `unclear` means `reject`. Use `fail` for a demonstrated contradiction or missing required artifact; use `unclear` when available evidence cannot establish the result. A disclosed shortfall can pass the relevant rows when the delivered change remains bounded, evidenced, and honestly described; disclosure does not excuse fabricated results or an explicit unmet readiness rule.
