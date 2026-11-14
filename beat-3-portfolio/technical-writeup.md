# Issue-scout: explain the challenge, keep the decision mine

## Overview

Issue-scout looks for open-source issues and uses written checks to help decide which ones fit the work I want to do. I wanted to use familiar technologies, including Python, JavaScript, HTML and CSS, while trying something more challenging. My contribution was directing the search preferences, approving a change to the scope rule, and reviewing the results. The searches and evaluations were AI-assisted. After the changes, the scout felt more aligned with my interests and future career path. It gave me a useful second opinion, but the final decision still had to be mine.

## What happened

I wanted to build on my earlier CodePath project and AI evaluation work. I did not want to be bogged down by easy beginner issues. I wanted something that would challenge my mind and give me experience with something new.

On October 18, the initial search-only test showed why the search needed adjustment. All five top results came from a general Python beginner query, and three came from one repository. After topic-first ranking, a limit on results per repository, and more specific title filters, the revised top five came from five repositories. These were search results, not five issues approved by the evaluator.

The scope rule also needed to match what I wanted. A difficult issue does not mean we cannot do it. I wanted the scout to explain the challenge and let us decide whether we could break it into something realistic, instead of rejecting it for us.

The saved October 18 change record describes the before and after:

> The old check rejected unsettled design and core-internals work, plus some old issues with abandoned attempts. The new check rejects only work without a single identifiable task; open design questions and unfamiliar subsystems inform difficulty instead of deciding the verdict.

The revised `scope-feasible` rule makes that distinction explicit:

> An unresolved design question or several affected files raises the difficulty rating instead of failing this check.

I approved that patch and a rerun on [MoltNet issue #552](https://github.com/getlarge/themoltnet/issues/552), which concerned evaluating search quality. I already wanted to do that issue. The scout was a second opinion to help me understand how difficult it would be and whether it was something we could realistically take on.

The subsequent October 18 direct-run output recorded:

> **Issue #552, `feat(evals): run evals on vector search with gold dataset / RAGAS approach`: accept.**
>
> **Difficulty note (Ambitious):** Several things are unresolved.

That was a result after the rule change, not a promise that the whole issue would fit our time budget. Breaking it into a smaller baseline made me more comfortable. It gave us something realistic to finish while still working on a more challenging issue.

A separate saved regression run checked the revised evaluator against 20 labeled examples:

```text
categories: claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 3/4
agreement: 19/20 scored items  (bar: 18/20: PASS)
```

One example still disagreed with its expected label. That result measures agreement on those examples, not whether every live recommendation is suitable.

## Limitations and what's next

The scout gave us a useful second opinion, but we still had to check the scope and rules ourselves before deciding what we could realistically finish. In the direct run, the evaluator marked the policy check as passing while also reporting unread contribution-related material. Review also challenged its preferred newcomer-support grade. The raw acceptance stayed in the record; it was not complete policy clearance or maintainer approval.

For the next issue, I still want the difficulty explained rather than used as an automatic rejection. Before deciding to take it on, I want to check the contribution rules myself and break the proposed work into a realistic baseline. The checks can help catch mistakes, but I still have to review the results and make the final decision.
