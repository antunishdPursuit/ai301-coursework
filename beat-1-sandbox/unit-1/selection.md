# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

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

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
