# Contribution: Retrieval evaluation for MoltNet #552

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Dennis
**GitHub Username:** antunishdPursuit
**Issue:** https://github.com/getlarge/themoltnet/issues/552
**Pull Request:** Not opened yet.

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Refining my AI issue search (October 18, 2026)**

I configured issue-scout with my fit profile and an AI-focused search strategy, keeping my existing rubric and evidence guide. Early results included unrelated issues and status reports, so I tightened the filters and limited results to two per repository. The broad scan's accepted issues were not found on the course list, so I checked that list and used Claude Code to evaluate two candidates from it. The scout accepted themoltnet #552 and rejected agentic-operator-core #86, but a separate setup review estimated 10 to 16 hours for a reduced #552 baseline, so I have not chosen or claimed it.

**Unit 6: Checking my upstream writing and saving repository context (October 18, 2026)**

I consolidated my voice guide and installed the voice guard plus the external-repository scope updates. Both guard checks passed: the required wiring test stopped a command with no comment text, and the voice check accepted my actual claim draft. On Windows, I used the documented guide-pointer fallback and explicit executable paths, then saved a local repository memory file with the search flow, contribution rules, and verified test commands. The updated scope rubric passed the 20-example regression at 19/20; I kept the logo-toolbar disagreement instead of changing the rubric just to match the label.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched for AI quality, safety, and evaluation work, then checked the course list after the broad scan returned candidates outside it. I chose [themoltnet #552](https://github.com/getlarge/themoltnet/issues/552), which asks for a retrieval evaluation using labeled queries and expected results. In my previous peer review project, I built an offline bias audit over stored reviews and tested it without changing the detector. This issue lets me keep working in AI evaluation and learn how search settings affect relevant and unrelated results. I can spend about 10 hours a week for three weeks, starting with a focused baseline using existing fixtures.

After the scope update, my scout accepted #552 and rated it Ambitious. That verdict did not establish a one-week fit: a separate setup review estimated 10 to 16 hours for the smaller baseline. The scout also treated generic contributor guidance as newcomer support and graded the AI policy before reading all the linked material. I recorded those limits and checked the contribution workflow separately. I proposed the baseline as a first PR, with threshold and query-fanout experiments as follow-ups; that scope still needs maintainer feedback.

**Claim comment:** [My claim on #552](https://github.com/getlarge/themoltnet/issues/552#issuecomment-6256838651).

**Toolkit**

- Tool: issue-scout in Claude Code, using my AI-focused strategy, fit profile, and scope rubric.
- What it produced: saved candidate evaluations and an accept / Ambitious verdict for #552.
- Difficulties: the broad scan did not enforce course-list eligibility, and some supporting judgments needed further review.
- What changed: I checked course eligibility, applied the scope-feasible rubric patch, reran #552, and checked setup separately. The full rubric regression passed 19/20; I preserved the disagreement and the scout's original output.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
