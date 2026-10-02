# Procedure: how this skill grades a plan package

## Read order

1. Determine live or eval mode. In live mode, read scope and voice guide first and enforce the repository boundary. In eval mode, ignore both and use only the supplied bundle.
2. Read this procedure, the rubric, and the evidence guide. If a required component is empty, stop as SKILL.md directs.
3. Read the issue, maintainer signals, and repository rules. Record the requested outcome and explicit constraints.
4. Read the reproduction evidence before the proposed plan. Record inputs, observed results, controls, and limits, so a confident diagnosis cannot replace the evidence.
5. Read the candidate plan and comment. Identify the stated cause or behavior gap, scope, implementation sequence, validation, risks, and deviations.

## Evidence gathering

1. Use each matching family in the evidence guide to gather the exact deciding quote or fact and its source section or live URL.
2. For diagnosis, compare the cause with each relevant observation and control. For scope, map included changes to that cause or requested enhancement.
3. For executability, identify the first action, affected code, behavior decisions, and unresolved dependencies. For validation, map test inputs and expected outputs to the reproduction or requested enhancement.
4. For honesty, compare claimed certainty and completion with the evidence and note risks or deviations. For communication, compare the comment with the plan, maintainer requests, and explicit policies.
5. Record missing or conflicting evidence explicitly. Never fill gaps from model knowledge, gold labels, hidden assumptions, or unrelated local files. In live mode, fetch only relevant public issue and repository evidence; inaccessible material stays unknown.

## Check execution

1. Grade every check in table order, including preferred checks. Apply its stated pass condition, not an unstated quality preference.
2. Cite the deciding quote or fact for each grade. A contradiction or absent required plan element is `fail`; genuinely insufficient source evidence is `unclear`. Do not treat an unstated repository policy as a violation.
3. Re-read only the specific conflicting source when needed. Do not execute the proposed implementation or tests to compensate for a plan that omits them.
4. In live mode, separately check the comment against the voice guide and quote any broken rule in the summary. Voice alone does not change the rubric verdict.
5. Report any procedure gap instead of silently inventing a grading step.

## Verdict assembly

1. Apply the rubric's verdict rule mechanically: all required checks pass means `accept`; otherwise `reject`. Preferred grades do not gate acceptance.
2. Give a short summary of decisive findings and any live voice notes. Include the evidence needed to understand failed or unclear checks.
3. Emit the final fenced JSON in SKILL.md's exact format, with every check and an evidence line, and nothing after it. Do not post, edit, or implement anything as part of grading.
