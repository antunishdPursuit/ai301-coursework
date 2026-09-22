# Rubric: is this a good first issue?

## Evidence rules

Use the capture date in an eval bundle as the reference date; use today's
UTC date in live mode. All day limits below are inclusive. Eval mode uses
only the supplied bundle and ignores `scope.md`. Live mode uses the sources
in `references/evidence-guide.md` and applies the house rules in `scope.md`.

Read the issue body, the full available comment thread, assignees, and PR
links together. A label, an empty sidebar, or a claim count in a separate
list cannot overrule an explicit current claim or implementation in the
thread. A later withdrawal or maintainer decision can supersede an earlier
statement; quote the evidence that resolves the conflict.

For each check, report `pass`, `fail`, or `unclear` and the deciding fact,
date, or quote. Use `unclear` when the needed evidence is missing or cannot
be read, not as a substitute for checking it. An explicitly empty list is
evidence of absence. A failed lookup is not. For an OR condition, one
verified alternative is enough to pass; missing evidence for an unused
alternative does not cancel that pass.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| open-contribution | Issue state, body, labels, and latest maintainer comments; in eval mode, the issue and Comments sections. | The issue is open and requests a concrete change to code, tests, or documentation. Reject a pure usage/support question, an explicitly superseded or duplicate request, or work a maintainer has declined. A short description alone is not a failure. | required |
| maintainer-life | Dates and authors of the last 5 default-branch commits, maintainer comments in this issue, and dated maintainer first-response samples; use the corresponding Repo facts and Comments in eval mode. | At least one human-authored default-branch commit or human maintainer response occurred within 90 days. A bot merging an identifiable human-authored PR counts; bot-only dependency updates do not. Treat Owner, Member, or Collaborator responses as maintainer evidence. | required |
| repository-use | Repository archived flag, latest release date, and dates/authors of the last 5 default-branch commits; corresponding Repo facts in eval mode. | The repository is not archived, and either its latest release is within 365 days or it has human-authored default-branch activity within 90 days. This permits actively maintained projects without releases. Stars and a recent push to an unrelated branch are not sufficient evidence. | required |
| bounded-scope | Issue body, acceptance criteria, complete available thread, issue age, and the history of linked closed-unmerged PRs. | The request describes one outcome whose completion can be explained from the text, with no unresolved design decision needed before implementation. Reject an umbrella/tracking issue with separate work items, an unsettled redesign, or a maintainer warning that the fix requires core-internals work. Also reject an issue older than 730 days with at least 2 abandoned implementation PRs unless a later maintainer comment explicitly narrows the task or resolves their blocker. Missing reproduction steps, a missing file estimate, or several checks for one outcome do not alone make scope fail. | required |
| available-to-take | Assignees, formally linked PR states, PRs mentioned in comments, claim comments and dates, withdrawals, and maintainer responses. Use all corresponding Repo facts and Comments in eval mode. | No current assignee, no open implementation PR for this work, and no active unreleased claim. An active claim is an unwithdrawn statement/request to work on it within 30 days, or a maintainer-approved reservation that has not been released. A later explicit withdrawal, rejection, or reopening to contributors clears that claim. Closed-unmerged PRs alone are not active claims. In live mode apply the scoped house rule before grading; in particular, classmates' claim comments in the course Path Review repo do not block an issue. Never apply that exception to eval bundles. | required |
| ai-policy-compatible | Root and .github CONTRIBUTING files, linked contributor rules, dedicated AI policy files, and PR/issue templates; in eval mode, only the bundle's contribution-policy statement. | No applicable policy bans the AI-assisted contribution being considered. Explicit bans fail. Requirements to disclose AI use, understand the work, test it, or review AI output pass, with those conditions recorded in the evidence/summary for later compliance. Verified policy silence passes; an unread or inaccessible policy is unclear. An AGENTS.md file does not override an explicit ban elsewhere. | required |
| verification-path | Issue body and thread: a reproduction example, named command/test, or explicit observable expected behavior. | At least one supplied example, command, test, or before/after behavior gives a concrete way to check the outcome. Missing detail affects preference only and does not by itself reject a bounded task. | preferred |
| newcomer-support | Current issue labels and maintainer comments. | A good-first-issue/beginner label or an explicit maintainer offer to help a newcomer is present and has not been withdrawn. This signal cannot override competing claims, unsafe scope, or a contribution-policy restriction. | preferred |

## Verdict rule

- `accept` only when every `required` check is `pass`.
- `reject` when any `required` check is `fail` or `unclear`. Name every
  blocking check and distinguish missing evidence from a confirmed failure.
- A `preferred` check never changes the verdict. An unclear preferred check
  gives no ranking benefit and causes no rejection.
- In live mode, rank only accepted issues. Use the fit profile first, then
  the number of passed preferred checks as a tie-breaker. If those are tied,
  keep the input order. Explain the fit without inventing experience,
  available hours, or an effort estimate.
- Follow the unchanged `SKILL.md` output contract: all check results, one
  binary verdict per issue, and a valid fenced JSON block as the last output.

## Why these choices

The 90-day human-activity window avoids treating automated updates as a
responsive project. The 365-day release alternative allows slower release
cycles, while the separate maintainer check still requires recent human
activity. These are initial thresholds to review through evaluation, not a
claim that every older project is abandoned.

Checking both issue metadata and comments addresses a failure from prior
PathReview work: the cohort list and GitHub discussion disagreed about who
was already working on an issue. Current course house rules still take
precedence in live mode. The 30-day unapproved-claim window can miss someone
quietly working longer; assignments, open PRs, and maintainer reservations
remain blocking evidence regardless of age unless the scoped rules apply.

Reproduction detail and beginner labels are preferences because a concise
issue can still describe a useful, bounded contribution. Personal interest
can rank accepted issues but cannot rescue an issue that fails a required
check. No check depends on a particular eval issue ID or its gold label.
