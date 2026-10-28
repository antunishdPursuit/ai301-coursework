# Contribution: Retrieval evaluation for MoltNet #552

**Contribution Number:** [1]

**Student:** Dennis

**GitHub Username:** antunishdPursuit

**Issue:** [MoltNet #552](https://github.com/getlarge/themoltnet/issues/552)

**Pull Request:** [#2821](https://github.com/getlarge/themoltnet/pull/2821) — draft, awaiting review.

## Toolkit

**Unit 5: Refining my issue search — October 18, 2026**

I configured issue-scout for AI evaluation work. Its broad search returned unrelated results and candidates outside the course list, so I tightened the filters and checked course eligibility separately. The scout accepted #552, but a setup review estimated 10–16 hours for even a smaller baseline; I had not claimed it at this point.

**Unit 6: Checking my writing and saving context — October 18, 2026**

I installed the voice guard and saved the repository's search flow, rules and test commands in a local context file. The wiring check and claim-draft check passed after Windows path adjustments. The updated scope rubric matched 19 of 20 examples; I kept the remaining disagreement rather than changing the rubric to fit the expected label.

**Unit 7: Running the ship-gate — October 27, 2026**

I prepared a check manifest and ran the gate on the existing PR branch. Windows executable/UTF-8 adjustments and an external-manifest option let the tool run while keeping private documents outside the repository. The selected technical checks passed, but precheck passed five rows and blocked on missing course-required AI disclosure. I chose to leave the public disclosure unchanged unless the repository or maintainer asks; the course expectation and blocked result remain, and I did not change the rubric to obtain a pass.

**Unit 8: Reviewing the monitor's recommendation — October 27, 2026**

I prepared a response playbook and ran the free state check, then authorized a draft-only Claude/Sonnet run. The ten merged PRs sampled were all bot-authored, so their 4.72-hour median was not a useful deadline for my review. The monitor recommended WAIT, which I accepted. My playbook allows consideration of one follow-up no earlier than November 3, after checking for new discussion and any promised timeframe; nothing sends automatically.

## Why I Chose This Issue

I wanted to continue the AI evaluation work I had started with an offline bias audit of stored peer reviews. MoltNet #552 offered a chance to learn how search settings affect relevant and unrelated results. With about ten hours a week for three weeks, I proposed a small fixture baseline first, which the maintainer later confirmed would be useful.

The scout rated the issue Ambitious. It helped find a candidate, but its assumptions about newcomer support and AI policy needed separate checking. That made the smaller scope important.

**Claim comment:** [My claim on #552](https://github.com/getlarge/themoltnet/issues/552#issuecomment-6256838651).

**Toolkit**

- Tool: Claude Code issue-scout with my fit profile and scope rubric.
- What it produced: candidate evaluations and an accept / Ambitious verdict.
- Difficulties: course eligibility and supporting claims needed verification.
- What changed: I checked the course list, contribution rules and setup effort before committing to the baseline.

## Understanding the Issue

**Problem Description**

MoltNet had individual search tests but needed a labeled evaluation to compare retrieval quality. This PR adds the first fixture baseline; it does not complete all of #552.

**Expected Behavior**

Run fixed queries against labeled entries, report relevant and unwanted results, and save enough information to repeat the measurement. Missing models or invalid results must cause failure rather than a silent keyword-only fallback.

**Current Behavior**

On the 12-entry corpus, relevance-only weights retrieve all labeled relevant entries within the top three results for five answerable queries. Unrelated entries also appear. The no-match query returns 1, 3 or 5 unwanted results at k=1/3/5 under every tested setting. This small reused corpus is not a held-out benchmark.

**Affected Components**

The additions are in `libs/diary-service/evals/`, its tests and evaluation configuration, and `docs/understand/entry-search.md`. The runner reuses the existing database search and embedding services without changing production retrieval.

**Toolkit**

- Tool: Codex-assisted source review and focused checks.
- What it produced: a fixture inventory and baseline scope.
- Difficulties: existing vector fixtures were not a ready-made semantic benchmark.
- What changed: I used existing prose with explicit relevance labels.

## Reproduction Process

**Environment Setup**

Verification used Windows, Node 24.22.1, pnpm 10.34.5 and Go 1.27.1 at `c138ccd906555b9ef8ad72909ee6deaafed2349e`. Prerequisites were locked dependencies, Docker, `pgvector/pgvector:pg16` and cached `Xenova/e5-small-v2` q8 files. The evaluation uses no paid inference API and forbids model downloads. Windows install and command adjustments left tracked configuration and the lockfile unchanged.

**Steps to Reproduce**

1. Check out the tested commit and prepare the documented dependencies, Docker and model cache.
2. In PowerShell, set `$env:NX_LOAD_DOT_ENV_FILES = 'false'`.
3. Run `pnpm exec nx run @moltnet/diary-service:retrieval-eval-typecheck` and `pnpm exec nx run @moltnet/diary-service:test --args=retrieval-metrics.test.ts`.
4. Run `pnpm exec nx run @moltnet/diary-service:retrieval-eval` and inspect the JSON under `.cache/retrieval-eval/`, including repeat differences and no-match results.

**Reproduction Evidence**

The [runner commit](https://github.com/antunishdPursuit/themoltnet/commit/c138ccd906555b9ef8ad72909ee6deaafed2349e) contains the executable check. The October 27 saved result, `baseline-1793080205829.json`, records the commit, configuration, hashes and ordered results. All 144 trial metrics and 12 summary rows were independently recomputed and matched. Raw logs and screenshots remain private; the [PR test plan](https://github.com/getlarge/themoltnet/pull/2821) provides the public summary.

**Toolkit**

- Tool: Nx, local E5 embeddings and Testcontainers PostgreSQL/pgvector.
- What it produced: repeatable results with recorded configuration.
- Difficulties: time, access metadata and model caches could affect comparisons.
- What changed: the runner freezes database time and resets access metadata; a separate diagnostic disabled secondary caches to check missing-model failure.

## Solution Approach

**Analysis**

In `libs/database/src/repositories/diary-entry.repository.ts`, `createDiaryEntryRepository().search()` calls `diary_search()`. The new runner measures that existing path. The weather false positive illustrates the gap: its cosine distance of about 0.294 passes the existing 0.6 gate despite no full-text match. That finding alone does not establish a better cutoff.

**Proposed Solution**

Use 12 entries and six queries with fixed relevance labels. Compare four weight configurations at k=1/3/5, twice each, reporting precision, recall and false positives. Larger datasets, graded labels, threshold tuning, fanout and UI additions remain separate follow-ups.

**Implementation Plan**

1. Add `retrievalEntries` and `retrievalQueries` in `libs/diary-service/evals/fixtures/retrieval-corpus.ts`, and `calculateRetrievalMetrics()` in `libs/diary-service/evals/retrieval-metrics.ts`. Test both in `libs/diary-service/__tests__/retrieval-metrics.test.ts`.
2. Add `libs/diary-service/evals/retrieval.eval.ts`, calling `repo.search()` with real embeddings and a disposable database.
3. Add evaluation targets in `libs/diary-service/package.json`, dedicated Vitest/TypeScript configuration, and instructions in `docs/understand/entry-search.md`.

**Toolkit**

- Tool: Codex-assisted implementation, Vitest/Nx and Git.
- What it produced: two commits covering eight files.
- Difficulties: a successful evaluation run could be mistaken for good search quality.
- What changed: I reported the no-match results separately and documented the corpus limits without tuning production search.

## Testing Strategy

Two observable checks show the contribution's result:

1. **Added measurement:** the previously missing evaluation target now produces results for 144 searches and 12 summary rows, with zero differences between repeats. This proves repeatable measurement, not improved ranking.
2. **Repository checks:** the October 27 checks at `c138ccd90` passed 142 diary-service unit tests (104 existing, 38 new), 36 diary-repository integration tests and 27 diary-service integration tests without real embeddings. Typechecks, secret scanning and Nx synchronization passed; lint had two existing warnings and no errors.

The evaluation ran again with cached model files and a newly created database. A separate missing-model diagnostic failed as expected. Formatting passed on committed LF content; the Windows CRLF checkout produced line-ending warnings.

**Two existing failures remain:**

- **Windows cache-path assertion:** embedding unit suite, 14 passed and 1 failed. A temporary portable-path diagnostic passed all 15, but that change is not in the PR.
- **Weather false positive:** real-embedding diary integration, 26 passed and 1 failed. The unrelated weather entry passes the existing vector-distance gate. Neither the failing test nor production search was changed.

At publication the branch was two commits ahead and 137 behind the inspected upstream snapshot. Runtime compatibility with newer main and full hosted CI remain unverified. The one successful Semgrep scan observed later is not a full CI pass.

**Toolkit**

- Tool: Vitest/Nx and independent GPT-6.1 Terra, GPT-6.1 Sol and GPT-6 Astra reviews.
- What it produced: runtime checks, recomputed metrics and a scope review.
- Difficulties: inherited failures and Windows differences complicated the results.
- What changed: I diagnosed and disclosed failures separately instead of counting their suites as passing.

## Implementation Notes

**October 18–19, 2026:** Claimed #552, inspected fixtures and added the corpus/metrics and runner in `27fa3813b` and `c138ccd90`. Reported results and asked about baseline scope and the larger dataset.

**October 23–26, 2026:** The issue discussion described 300 candidate entries and an existing review UI. The maintainer offered initial queries and labels; delivery of the final corpus remained unverified.

**October 27, 2026:** Recovered the checkout, restored dependencies and repeated checks. Corrected wording about the existing UI, opened draft PR #2821 and posted the approved linked reply. Later ran the Unit 7 gate and Unit 8 monitor, recording the blocked precheck and accepted WAIT recommendation.

**Toolkit**

- Tool: Codex, Git recovery and diagnostic runs.
- What it produced: a restored baseline and verified evidence for the PR.
- Difficulties: the original checkout was missing after cleanup, and earlier wording overlooked the existing UI.
- What changed: I verified the recovered commits and corrected the UI wording before publication.

## Pull Request

**PR Link:** [MoltNet #2821](https://github.com/getlarge/themoltnet/pull/2821).

**PR Description:** A reproducible fixture retrieval baseline with relevance labels, metric tests and an opt-in runner. It includes results and known failures and covers only the first increment of #552.

**Maintainer Feedback:** The maintainer supported a baseline-first PR and offered initial queries and labels. My [October 27 reply](https://github.com/getlarge/themoltnet/issues/552#issuecomment-6435002639) links the PR and asks what capability is missing from the existing UI and whether additions should be separate work.

**Status:** Open as a draft. As of October 27 at 4:27 p.m. EDT, there were no PR comments, submitted reviews or inline comments, and no new issue reply. I accepted WAIT; no approval or merge is claimed. The Unit 7 block remains recorded above.

**Toolkit**

- Tool: Codex/GitHub, ship-gate, the on-demand PR-monitor and a separate native Codex watcher.
- What it produced: the draft PR, approved issue reply, gate report and private WAIT note.
- Difficulties: the PR-monitor omits issue/inline comments and does not include elapsed time in its unchanged-state check.
- What changed: I checked those discussions separately and require fresh reads and my approval before any later public response.

## Learnings and Reflections

**Technical Skills Gained**

I learned to separate two questions: does the evaluation run correctly, and are the search results useful? Our run was repeatable, but it still returned unrelated entries. Working through precision, recall and the no-match query made that difference clearer.

**Challenges Overcome**

The two failing tests needed different explanations: one was a Windows path assertion, while the other exposed a search-quality problem. I kept both visible. The review also caught my assumption that a labeling UI needed to be built when one already existed.

**What I'd Do Differently Next Time**

I would check the available data, labeling responsibilities and existing tools before planning the work. I would also keep better recovery notes and update this story as I go. For this contribution, measuring the current behavior was a useful first step; changing search settings would need more evidence and a separate scope agreement.

## Resources Used

- [MoltNet #552](https://github.com/getlarge/themoltnet/issues/552): scope, discussion and dataset ownership.
- [Search documentation at the tested commit](https://github.com/antunishdPursuit/themoltnet/blob/c138ccd906555b9ef8ad72909ee6deaafed2349e/docs/understand/entry-search.md): commands, metrics and limitations.
- [Contribution guidance at the starting revision](https://github.com/getlarge/themoltnet/blob/cf291d782d6e0f3da1e83274ce6306762b23e1af/CONTRIBUTING.md): repository workflow and checks.
- [Draft PR #2821](https://github.com/getlarge/themoltnet/pull/2821): implementation and public validation summary.
