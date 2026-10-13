# Procedure: how this tool grades a PR package

## Read order

1. Determine live or eval mode. Enforce SKILL.md's live scope and voice seams; in eval use only bundle evidence.
2. Read the rubric and evidence guide. Refuse to grade if required components have no substantive content.
3. Read the issue, thread highlights, and repository requirements. Record the requested behavior and explicit standards.
4. Read the accepted plan, its scope pair, test plan, and deviation notes before the candidate description can frame the change.
5. Read the commit list and complete diff, then actual test evidence. Finally read the title and description to compare their claims with the artifacts.

## Evidence gathering

1. For plan fidelity, map each changed behavior to an in-scope plan item or deviation. Check the reverse direction for promised behavior absent from the diff. Compare description claims with both.
2. For test evidence, pair each delivered behavior and planned validation with the recorded inputs, expected result, and actual result. Record which checks are mocked, live, passed, failed, not run, or collected no tests. Identify required repository commands and their recorded outcomes.
3. For diff quality, inspect every changed file and hunk for relevance and leftovers. A small file count is not proof of a bounded diff.
4. For standards, map each explicit template, contribution, disclosure, branch, or maintainer requirement to the candidate's actual content. Use the evidence guide's exact locations.
5. Keep unavailable and conflicting evidence explicit. Do not repair a package with unstated facts, private instructions, gold labels, or unrelated files. If applicable sources conflict, quote both and any documented precedence or exception; absent a resolution, mark the affected check unclear.

## Check execution

1. Grade each rubric row in table order using its own pass condition and the evidence gathered for it. Re-read a specific source only to resolve a material ambiguity; do not restart the entire package.
2. Give each grade a deciding quote or fact with its source location. Distinguish a demonstrated omission or contradiction from genuinely unavailable evidence.
3. Evaluate honest deviations against the delivered outcome and disclosed limits. Do not equate incomplete scope with silent drift or a disclosed failing check with a fabricated pass.
4. Do not run tests, edit files, or publish to fill evidence gaps during grading.
5. In live mode, separately check the title and description against the voice guide; quote broken rules. Report procedure gaps without improvising around them.

## Verdict assembly

1. Apply the rubric rule: accept only when every required row passes; a required fail or unclear returns reject.
2. Lead the short summary with the first failing or unclear required check in rubric order, its deciding evidence, and the smallest missing action or evidence. Mention other blockers without duplicating the full artifact.
3. If all checks pass, summarize the supported outcome and any material disclosed limit. Report separate live voice notes or procedure gaps.
4. Emit every check in the final JSON exactly as SKILL.md requires. End immediately after that block.
