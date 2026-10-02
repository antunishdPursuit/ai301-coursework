# Unit 3: Plan and Build

Status: skill installed and evaluated; implementation plan and comment drafted. Live plan-check returned `accept` on all eight checks, with no voice-guide violations. Public posting, implementation, before/after validation, branch push, and portal submission remain pending.

## Posted upstream

**GitHub username**

antunishdPursuit

**Plan comment**

Not posted. The exact draft is in the PathReview checkout's `comment.md`, pending Dennis's review. Add the posted comment permalink and its exact text here after approval and publication.

## Your branch

**Branch**

Not created yet. Planned application branch: `fix/27-feedback-tone-check`.

**Evidence**

Implementation has not started. The Week 2 before record is [the posted baseline](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5904119559): two controlled seed replays, five generation calls and five sections per replay. It demonstrated pass-through behavior, not tone classification. After implementation, paste the actual before/after commands and outputs here, including the explicitly mocked classifier verdicts and their limits. No after result is claimed yet.

## Eval iterations

**Run history**

One full official evaluation on October 2, 2026, using the harness's pinned Sonnet model: **19/20, PASS**. Category agreement: clear-accept 7/7, scope-creep 4/4, thread-convention 1/2, unbuildable 3/3, wrong-cause 4/4. Every category has at least one match. No rubric revisions or partial reruns followed this run. `eval-run.txt` is a byte-for-byte copy of the harness-written transcript, not an edited summary.

**Package analysis**

`pkg-20`: our rubric returned `accept`; the gold label is `reject`.

The package's repository policy says: "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance". The candidate comment does not disclose AI use, but the bundle does not establish that this candidate used AI. A reference to an AI-proposed solution in the maintainer's thread is not evidence of this candidate's tool use.

The gold-label note supplies the additional assumption: "every package here is treated as AI-assisted work". That note is not part of the bundle sent to the grader. Our result states: "package does not establish student AI use so disclosure is not triggered per evidence guide". I retained the disagreement rather than teaching the rubric to infer an unstated fact, consistent with the evidence boundary used in Unit 2. This explains the mismatch; it does not change the official gold label.

**Check rationale**

Exact current rubric row:

```text
| Thread and policy alignment | The draft comment compared with maintainer requests, thread highlights, and stated contribution rules. | The comment addresses applicable requests and conventions, including disclosure when the package establishes it is required. It neither contradicts maintainer direction nor relies on another student's plan as its own. Do not invent policies or assume undisclosed AI use. | required |
```

This check covers explicit maintainer direction and contribution rules, while requiring evidence before applying a conditional disclosure requirement. I kept the Unit 2 distinction between a policy's existence and evidence that the candidate used AI. I rejected a blanket assumption that every evaluated candidate used AI merely because this is an AI course.

**Trade-offs**

The evidence boundary costs one match on `pkg-20`. It can also miss undisclosed AI use when the package provides no evidence of that use. That is an explicit limit, not a claim that disclosure is optional when AI was used. The same unchanged rubric matched `pkg-04`, the other thread-convention case, so this choice did not erase the category. The full run met the category floor and passed; I made no subsequent rubric changes and therefore did not need a confirming rerun.
