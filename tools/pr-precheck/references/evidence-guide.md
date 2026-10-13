# Evidence guide: where evidence lives in a PR package

Use the frozen bundle alone in eval mode. In live mode use the supplied drafts, committed branch artifacts, and relevant scoped repository sources. An assertion is not a substitute for its underlying evidence.

## Plan fidelity (harness category: silent-drift)

- **Eval:** Plan context's accepted scope, exclusions, files, test plan, and deviations; Candidate PR's Title, Description, Commits, and Diff.
- **Live:** plan.md and deviation notes, relevant posted plan and maintainer replies, git diff main...HEAD and git log main..HEAD, and pr_draft.md. Confirm the diff base and committed revision; an unstaged edit is not in that diff.
- **Good:** Every changed behavior maps to the bounded plan or an explained deviation. Missing planned behavior is explicitly disclosed. Title and description match the actual change. Honest reduced scope can pass; a claim of full delivery contradicted by the diff cannot.

## Test evidence (harness category: not-tested)

- **Eval:** Plan context's reproduction and Test plan, Candidate PR's Test evidence and testing claims, and Repo facts' stated checks.
- **Live:** test_evidence.md, plan.md's validation, the posted reproduction or assigned house pack, relevant source/tests in the diff, and the repository's documented commands.
- **Good:** Inputs, expected behavior, observed before/after results, and required check outcomes are visible and relevant. For an enhancement, the baseline may establish an absent behavior; after-change evidence must exercise the implemented behavior claimed. Controlled responses can prove branching or retry behavior without proving live classifier accuracy. Record failures, empty suites, and skipped checks accurately; do not convert them into passes.

## Diff quality (harness category: unreviewable)

- **Eval:** Candidate PR's full unified Diff and Commits, read against Plan context and the issue.
- **Live:** git diff main...HEAD and git log main..HEAD, including the changed file list and all hunks.
- **Good:** Each hunk serves the bounded change or necessary support. No debug leftovers, commented-out code, unrelated cleanup, generated debris, or local review drafts bury the fix. Reviewability depends on relevance, not a fixed file or commit count.

## Standards and comms (harness category: standards-wall)

- **Eval:** Repo facts' template asks, contribution instructions, stated AI policy, and Thread highlights; compare with the candidate title, description, branch information when supplied, and test evidence.
- **Live:** The scoped repository's actual PR template, docs/CONTRIBUTING.md or its documented equivalent, relevant maintainer direction, and applicable assignment requirements supplied with the live package. Compare with pr_draft.md and branch metadata. The voice guide supplies separate wording feedback.
- **Good:** Explicit asks have real answers, applicable disclosures appear, and no checkbox or claim invents a completed check. Eval packages do not inherit PathReview rules or assumed AI assistance because a course authored them. For this student's live AI301 PR, the verified Unit 4 assignment explicitly requires AI disclosure even without a dedicated template heading; put it in Notes for Reviewers. Keep grading rules distinct from repository review requirements. If those requirements conflict without a documented resolution, surface the conflict rather than silently choosing a convenient interpretation.
