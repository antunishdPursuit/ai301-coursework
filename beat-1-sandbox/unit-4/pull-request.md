# Unit 4: Test and Submit

Status: local preparation only. The PR has not been opened, and these Unit 4 files have not been published or submitted to the course portal.

## Your pull request

**Pull request**

Pending Dennis's review and approval. No PR URL exists yet. Target: codepath/pathreview-ai301-fa26-s3, issue #27.

**Branch**

`fix/27-feedback-tone-check`

The existing fork branch is published at `8593facae77e546e180c14a4c64616febe83becf`. This branch link is context, not a substitute for the PR URL:
https://github.com/antunishdPursuit/pathreview-ai301-fa26-s3/tree/fix/27-feedback-tone-check

## Eval iterations

**Run history**

One full official Sonnet run on October 10, 2026. No targeted reruns or skill revisions followed it.

> agreement: 18/20 scored items  (bar: 18/20: PASS)

Category matches: clear-accept 5/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3. All 20 packages completed without errors. The unchanged harness wrote the accompanying `eval-run.txt`; its four fingerprints match the skill copied into `tools/pr-precheck/`.

**Package analysis**

`pkg-08`: our skill returned `reject`; the gold label is `accept`. The deciding check was Accurate PR claims, graded `unclear`:

> Description says 'plan posted on the thread', but thread highlights list '2 comments total' and neither is a plan, while Plan context says 'the posted plan'; the sources conflict.

The bundle's Plan context explicitly says:

> The accepted plan this PR claims to implement, excerpted from the posted plan (with the repro evidence it built on):

The evaluator treated absence from the thread highlights as conflicting evidence even though the bundle explicitly supplies the posted plan. That is an overly strict reading of this example. The code, observable tests, and checklist passed the other five checks.

**Check rationale**

Exact row from the submitted rubric:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Accurate PR claims | Candidate title and description compared with the diff, plan, and test evidence. | Claims describe what this change actually delivers and what was verified. No claimed feature, fidelity, test result, or certainty contradicts the artifacts. | required |

I kept this required because a polished description can overstate what the diff or test evidence supports. I rejected using presentation quality or length as evidence of readiness. No wording was changed after the first run; the two disagreements remain visible rather than weakening the check just to raise the score.

**Trade-offs**

Strict claim checking can reject a package that is otherwise useful and accepted by the course. In `pkg-08`, it treated thread highlights as a complete record. In `pkg-16`, it questioned whether the reported error message matched the displayed diff; the gold label accepts the bounded, disclosed work. That second discrepancy deserves review, not an automatic assumption that either label proves the full execution path.

I retained both disagreements and the passing 18/20 run. There was no loosened rule, no canary run, and no revised skill presented as evaluated. This result measures agreement on the course's frozen examples, not the quality of every future live PR.

---

Related paths: `eval-run.txt` in this directory; the complete installed skill copy under `tools/pr-precheck/`.
