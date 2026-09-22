# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27

**Verdict output**

## Issue #27 — Feedback tone check (live mode)

**Scope check:** `codepath/pathreview-ai301-fa26-s3` — within scope. Path Review house rule applies: classmates' claim comments do not block.
Reference date: 2026-09-22 (retrieved_at_utc).

---

### Check results

**open-contribution — pass**
Issue #27 is open, authored by a Collaborator (Aburke225), requests a concrete code change (add a post-generation tone classification step to `safety/content_filter.py` and `rag/generator/review_generator.py`), labeled "enhancement". Not a support question, not declined, not superseded.

**maintainer-life — pass**
Andrew Burke (Aburke225) committed human-authored code to `main` on 2026-09-16 — 6 days before retrieval, well within the 90-day window. All 5 default-branch commits are his; none are bot-only.

**repository-use — pass**
Repository is not archived. Human-authored default-branch activity on 2026-09-16 is within 90 days. No releases exist, but the rubric accepts active development in lieu of a release.

**bounded-scope — pass**
Single, fully-described outcome: add a prompt-based tone classification step after generation; classify each feedback section as constructive or negative; reject and regenerate sections that fail. Relevant files are named. Issue is 12 days old with zero closed PRs anywhere in the repo. No umbrella language, no unresolved design debate.

**available-to-take — pass**
Assignees: none. Open PRs: none (the repo has no PRs at all). Claim comments: none. Timeline shows only labeling events. Completely free under both the standard rule and the house rule.

**ai-policy-compatible — pass**
`docs/CONTRIBUTING.md` contains no AI ban or disclosure requirement — it covers commit conventions, CI, and code style only. All other retrieved policy files (PR template, issue templates, README) are silent on AI. Policy silence passes.

**verification-path (preferred) — pass**
Issue body states the observable before/after behavior: sections classified "negative (discouraging, vague, dismissive)" are rejected and regenerated; sections classified "constructive (actionable, specific, encouraging)" pass through. Sufficient to verify the outcome.

**newcomer-support (preferred) — fail**
Labels are `enhancement`, `devops`, `safety`, `tier-2`. No `good-first-issue` or `beginner` label. Comment thread is empty; no maintainer newcomer offer.

---

### Verdict: accept

All six required checks pass. One of two preferred checks passes (verification-path).

**Fit note:** This issue sits squarely in Dennis's stated interest — AI quality and safety in a Python codebase — and in the same safety subsystem worked on in the prior PathReview project. The scope is focused (one classification step, two named files) with a clear, verifiable outcome. The `tier-2` label signals moderate complexity; Dennis's profile says they are willing to take on a challenging issue when the outcome is clear, which it is here.

**Flag:** The author's 5–8 hour estimate is not Dennis's available time, and the weekly time budget has not been set. Confirm available hours before claiming in Unit 2.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27",
  "checks": [
    {
      "name": "open-contribution",
      "grade": "pass",
      "evidence": "Issue #27 is open, authored by a Collaborator, requests concrete code change to safety/content_filter.py and rag/generator/review_generator.py, labeled enhancement; not declined or superseded."
    },
    {
      "name": "maintainer-life",
      "grade": "pass",
      "evidence": "Andrew Burke (Aburke225) human-authored commit to main on 2026-09-16, 6 days before retrieval — within 90-day window."
    },
    {
      "name": "repository-use",
      "grade": "pass",
      "evidence": "Repository not archived; human-authored default-branch commit on 2026-09-16 within 90 days; no releases but active development satisfies the alternative condition."
    },
    {
      "name": "bounded-scope",
      "grade": "pass",
      "evidence": "Single outcome: add post-generation tone classification with reject/regenerate for failing sections; two files named; issue is 12 days old with zero closed PRs in the repo."
    },
    {
      "name": "available-to-take",
      "grade": "pass",
      "evidence": "No assignees, no open or closed PRs anywhere in the repo, no claim comments; timeline shows labeling events only."
    },
    {
      "name": "ai-policy-compatible",
      "grade": "pass",
      "evidence": "docs/CONTRIBUTING.md and all retrieved policy files contain no AI ban or disclosure requirement; policy silence passes."
    },
    {
      "name": "verification-path",
      "grade": "pass",
      "evidence": "Issue body describes observable before/after: sections classified negative are rejected and regenerated; constructive sections pass through."
    },
    {
      "name": "newcomer-support",
      "grade": "fail",
      "evidence": "Labels are enhancement/devops/safety/tier-2; no good-first-issue or beginner label; comment thread is empty with no maintainer newcomer offer."
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

These are the evaluator's agreement lines, in run order:

1. Initial attempt: `agreement: 0/0 scored items`. Authentication and Windows
   encoding errors prevented every case from being graded. This was an execution
   failure, not an accuracy score. An authentication diagnostic also produced no
   grade. I signed in again, and the retry used UTF-8.
2. Three-case practice run: `agreement: 3/3 scored items`.
3. After clarifying the abandoned-PR rule, the targeted `--only issue-03` rerun:
   `agreement: 1/1 scored items`.
4. Final full run: `agreement: 18/20 scored items  (bar: 18/20: PASS)`.

The final line matches `eval-run.txt`. The full run used Sonnet and met the
category floor: claimed 4/4, clear-accept 7/8, dead-repo 3/3, policy 1/1, and
scope 3/4. The rubric has not changed since that full run.

**Issue analysis**

For `issue-03`, the final full-run verdict was `reject`, and the instructor's
label was also `reject`. The deciding required check was `available-to-take`.
The evaluator recorded:

> PR #10985 is listed as open (an active implementation PR); DanielNoord (COLLABORATOR) on 2026-05-11: 'We are not looking for any other contributions other than @hamza-mobeen's PR.'

An open implementation PR and an explicit maintainer reservation independently
make this issue unavailable. In the first practice run, the skill also failed
`bounded-scope` because it treated closed, unmerged PRs as abandoned attempts.
Those states did not establish why the PRs closed. I approved a clarification
requiring discussion or maintainer evidence before counting an abandoned
implementation. In the final full run, `bounded-scope` passed, while the
availability evidence still correctly produced rejection. The course's shared
claim exception applies to live PathReview issues, not this evaluation snapshot.

**Check rationale**

The required `bounded-scope` check is quoted exactly from
`tools/issue-select/rubric.md`:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| bounded-scope | Issue body, acceptance criteria, complete available thread, issue age, and the history of linked closed-unmerged PRs. | The request describes one outcome whose completion can be explained from the text, with no unresolved design decision needed before implementation. Reject an umbrella/tracking issue with separate work items, an unsettled redesign, or a maintainer warning that the fix requires core-internals work. Also reject an issue older than 730 days with at least 2 abandoned implementation PRs unless a later maintainer comment explicitly narrows the task or resolves their blocker. A closed, unmerged PR alone does not prove abandonment. Check its discussion or the maintainer's explanation before counting it as an abandoned implementation. Missing reproduction steps, a missing file estimate, or several checks for one outcome do not alone make scope fail. | required |

I want a contribution with a clear outcome, rather than an umbrella project or
an unresolved redesign. The age-and-history condition is intended to catch work
that looks small but has repeatedly stalled. Its thresholds are draft choices,
not universal rules about old issues. I added the closed-PR clarification because
closing one proposed solution does not establish that the issue or implementation
was abandoned. Several steps toward one outcome also do not automatically make
an issue too broad.

**Trade-offs**

Requiring explicit abandonment evidence can miss a long-running, repeatedly
attempted issue when the snapshot does not explain why earlier PRs closed. In
the full run, `issue-15` was accepted although the instructor label was `reject`.
The evaluator's scope evidence was:

> Single bounded outcome (separate command/text fields); Slack payload example clarifies target format; no unresolved design decision; linked closed PRs #20840 and #23123 cannot be confirmed as abandoned implementations because their discussions are absent from the bundle.

I accept this limitation rather than treating every closed PR as proof of
abandonment. The snapshot contains only 40 of 97 comments, and evaluation mode
does not permit fetching the missing history. This full run shows the current
rule's outcome; I did not run `issue-15` with the earlier rubric, so I cannot
claim the clarification alone caused this disagreement.

There is also a conservative trade-off: the skill rejected `issue-19`, whose
instructor label was `accept`, because it treated two potential causes and
additional suggestions for one UI-freeze problem as unresolved scope. The
`issue-03` rerun was a targeted check of the clarification, not evidence that
all other decisions would stay unchanged. The confirming full run measured
these remaining limits and passed at 18/20.

---

## Selection rationale

**Selection rationale**

1. **Fit and time.** I chose issue #27 because I want to deepen my work on AI
   quality, safety, and constructive feedback. My previous PathReview work
   audited bias in stored reviews; this issue would let me build a check in the
   generation process itself. The author estimates 5–8 hours. I have not set a
   weekly time budget yet, so that estimate is not a commitment about my
   availability. I need to confirm that time before claiming the issue in Unit 2.
2. **What the rubric captures and what I weighed.** The verdict correctly
   identifies a focused outcome, recent human repository activity, and no
   current assignment or implementation PR. Beyond those checks, I weighed the
   chance to learn how to test constructive tone and handle failed classification
   or repeated regeneration. A limit on regeneration and behavior after that
   limit will need to be defined during implementation. An accepted issue does
   not mean those implementation details are already solved.
3. **Claiming difficulty.** At the live check, issue #27 had no assignees or
   comments, and the repository had no PRs. The course also allows classmates
   to work on the same issue, so another student's claim comment would not by
   itself block me. I expect little claim competition based on that evidence,
   but I will recheck the issue in Unit 2. I have not posted a claim or started
   implementation.

---

Related paths: `eval-run.txt` in this directory; the skill's files in
`tools/issue-select/`.
