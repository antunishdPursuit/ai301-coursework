# Contribution: Retrieval evaluation for MoltNet #552

**Contribution Number:** [1]

**Student:** Dennis

**GitHub Username:** antunishdPursuit

**Issue:** [MoltNet #552](https://github.com/getlarge/themoltnet/issues/552)

**Pull Request:** [#2821](https://github.com/getlarge/themoltnet/pull/2821), still open as a draft. Latest verification and maintainer reply: November 2, 2026.

## Toolkit

**Unit 5: Refining my issue search — October 18, 2026**

I configured issue-scout for AI evaluation work. Its broad search returned unrelated results and candidates outside the course list, so I tightened the filters and checked course eligibility separately. The scout accepted #552, but a setup review estimated 10–16 hours for even a smaller baseline; I had not claimed it at this point.

**Unit 6: Checking my writing and saving context — October 18, 2026**

I installed the voice guard and saved the repository's search flow, rules and test commands in a local context file. The wiring check and claim-draft check passed after Windows path adjustments. The updated scope rubric matched 19 of 20 examples; I kept the remaining disagreement rather than changing the rubric to fit the expected label.

**Unit 7: Running the ship-gate — October 27, 2026**

I prepared a check manifest and ran the gate on the existing PR branch. Windows executable/UTF-8 adjustments and an external-manifest option let the tool run while keeping private documents outside the repository. The selected technical checks passed, but precheck passed five rows and blocked on missing course-required AI disclosure. I chose to leave the public disclosure unchanged unless the repository or maintainer asks; the course expectation and blocked result remain, and I did not change the rubric to obtain a pass.

**Unit 8: Reviewing the monitor's recommendation — October 27, 2026**

I prepared a response playbook and ran the free state check, then authorized a draft-only Claude/Sonnet run. The ten merged PRs sampled were all bot-authored, so their 4.72-hour median was not a useful deadline for my review. The monitor recommended WAIT, which I accepted. The initial playbook deferred an unsolicited follow-up until November 3. Later maintainer messages gave me concrete work to verify, so I responded to those updates after testing and reviewing each reply. Nothing sends automatically.

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

My original PR adds `libs/diary-service/evals/`, its tests and evaluation configuration, and search documentation. The maintainer adapted that baseline into `libs/retrieval-eval` in #2849, with dataset and Potato work in #2927 and #2848. My later work verifies those branches; I did not build their UI or change production retrieval.

**Toolkit**

- Tool: Codex-assisted source review and focused checks.
- What it produced: a fixture inventory and baseline scope.
- Difficulties: existing vector fixtures were not a ready-made semantic benchmark.
- What changed: I used existing prose with explicit relevance labels.

## Reproduction Process

**Environment Setup**

Verification used Windows, Node 24.22.1, pnpm 10.34.5 and Go 1.27.1 at `c138ccd906555b9ef8ad72909ee6deaafed2349e`. Prerequisites were locked dependencies, Docker, `pgvector/pgvector:pg16` and cached `Xenova/e5-small-v2` q8 files. The evaluation uses no paid inference API and forbids model downloads. Windows install and command adjustments left tracked configuration and the lockfile unchanged.

The November 2 follow-up used the maintainer's #2848 at `d1c87924`, Node 24.22.1 and pnpm 12.14.0. I ran `pnpm exec nx run @moltnet/retrieval-eval:eval:corpus` with an explicit local model cache and output workspace, then `pnpm exec nx run @moltnet/retrieval-eval:test --skipNxCache`. The corpus run generated fresh embeddings from cached model files and used a new disposable database.

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

**Original baseline failures (October 27; not rerun on November 2):**

- **Windows cache-path assertion:** embedding unit suite, 14 passed and 1 failed. A temporary portable-path diagnostic passed all 15, but that change is not in the PR.
- **Weather false positive:** real-embedding diary integration, 26 passed and 1 failed. The unrelated weather entry passes the existing vector-distance gate. Neither the failing test nor production search was changed.

At publication, my original branch was two commits ahead and 137 behind the inspected upstream snapshot. Later checks on the maintainer's branches do not establish that my original PR passes against newer main or full hosted CI.

**Follow-up verification, November 1–2:**

- **Real corpus at `d1c87924`:** all 56 searches completed across 276 approved entries, seven queries, four weight settings and two repeats at top ten. Every search returned ten distinct corpus entries, and all 28 repeat pairs matched. GPT-6.1 Sol independently checked the saved results and hashes. There are no relevance judgments yet, so quality metrics remain withheld; the run proves execution and repeatability only.
- **Full retrieval-evaluation unit suite at `d1c87924`:** 47 passed and 1 failed out of 48. The existing Windows permission assertion expects `0600`, while Node reports `0666`. Its failure prevents the later concurrent-update assertions in that test from running. I left the assertions unchanged.
- **Local metrics coverage on #2849's `8d83c6e`:** the original 25 tests passed. I added two tests for the open review findings and explicit checks that relative-time datasets omit binary metrics; all 27 then passed. These check existing behavior; they do not fix a demonstrated scoring bug. Commit `3354779d0` remains local and unpublished.
- **Checks for that local test change:** typechecking and formatting passed; lint had two existing warnings. The Nx secret-scan wrapper failed because of Windows quoting, but the equivalent direct full-project scan and normal commit hooks passed. That wrapper failure was not fixed or rerun during the corpus check.

The [November 2 PR reply](https://github.com/getlarge/themoltnet/pull/2821#issuecomment-6592906034) reports these results and limitations. Raw outputs remain local; generated package-manager metadata was restored, leaving the review checkouts clean.

**Toolkit**

- Tool: Vitest/Nx and independent GPT-6.1 Terra, GPT-6.1 Sol and GPT-6 Astra reviews.
- What it produced: runtime checks, recomputed metrics and a scope review.
- Difficulties: inherited failures and Windows differences complicated the results.
- What changed: I diagnosed and disclosed failures separately instead of counting their suites as passing.

## Implementation Notes

**October 18–19, 2026:** Claimed #552, inspected fixtures and added the corpus/metrics and runner in `27fa3813b` and `c138ccd90`. Reported results and asked about baseline scope and the larger dataset.

**October 23–26, 2026:** The issue discussion described 300 candidate entries and an existing review UI. The maintainer offered initial queries and labels; delivery of the final corpus remained unverified.

**October 27, 2026:** Recovered the checkout, restored dependencies and repeated checks. Opened draft PR #2821 and posted the approved linked reply. Later ran the Unit 7 gate and Unit 8 monitor, recording the blocked precheck and accepted WAIT recommendation.

**October 28–November 2, 2026:** Clarified that I had not accessed the earlier local UI. The maintainer shared the Potato workflow and later published the approved corpus through #2848. I tested the supplied corpus, reran the current unit suite and prepared the separate metrics-coverage tests. After reviewing the wording, I approved the November 2 reply on my existing PR; it was posted through GitHub CLI and verified against the draft.

**Toolkit**

- Tool: Codex, Git recovery and diagnostic runs.
- What it produced: a restored baseline and verified evidence for the PR.
- Difficulties: the original checkout was missing after cleanup, and descriptions of a local UI did not establish that I could access it.
- What changed: I verified the recovered commits and clarified tool access and ownership before planning further work.

## Pull Request

**PR Link:** [MoltNet #2821](https://github.com/getlarge/themoltnet/pull/2821).

**PR Description:** A reproducible fixture retrieval baseline with relevance labels, metric tests and an opt-in runner. It includes results and known failures and covers only the first increment of #552.

**Maintainer Feedback:** The maintainer adapted my baseline in [#2849](https://github.com/getlarge/themoltnet/pull/2849) and asked me to keep #2821 open. The [November 2 handoff](https://github.com/getlarge/themoltnet/pull/2821#issuecomment-6573726327), posted by the maintainer's LeGreffier bot, shared the corpus through #2848 and invited local retrieval testing while relevance review continues.

**Status:** As of November 2, #2821 remains an open draft. My [latest reply](https://github.com/getlarge/themoltnet/pull/2821#issuecomment-6592906034) reports the successful corpus run, the remaining Windows failure and the unpublished coverage tests. I asked whether the maintainer prefers a follow-up PR against #2849 or a patch. No approval or merge is claimed.

**Still Pending:**

- The maintainer's response and preferred delivery route for the local metrics tests. Keep #2821 open until its disposition is agreed.
- Compatible relevance labels, then rescoring the saved rankings. Adding queries, tuning retrieval or building more UI would need a separate scope agreement.
- Final review of this story, approval to commit and push the coursework update, and Assignment 5 submission. The Unit 7 disclosure-related block remains recorded; later test passes do not clear it.

**Toolkit**

- Tool: Codex/GitHub, ship-gate, the on-demand PR-monitor and a separate native Codex watcher.
- What it produced: the draft PR, reviewed issue and PR replies, gate report and private WAIT note.
- Difficulties: the PR-monitor omits issue/inline comments and does not include elapsed time in its unchanged-state check.
- What changed: I checked those discussions separately and require fresh reads and my approval before any later public response.

## Learnings and Reflections

**Technical Skills Gained**

I learned to separate a working evaluation from useful search results. The small fixture exposed unrelated results; the larger corpus ran repeatably but still lacks labels. Passing execution checks is not enough to claim better retrieval.

**Challenges Overcome**

Windows path and permission assertions needed different explanations from the weather false positive, so I kept those failures separate. I also learned to clarify access to a maintainer's local tool before assuming I could use or extend it. The two new metrics tests addressed specific review gaps without expanding the feature scope.

**What I'd Do Differently Next Time**

I would check the available data, labeling responsibilities and existing tools before planning the work. I would also keep better recovery notes and update this story as I go. For this contribution, measuring the current behavior was a useful first step; changing search settings would need more evidence and a separate scope agreement.

## Resources Used

- [MoltNet #552](https://github.com/getlarge/themoltnet/issues/552): scope, discussion and dataset ownership.
- [Search documentation at the tested commit](https://github.com/antunishdPursuit/themoltnet/blob/c138ccd906555b9ef8ad72909ee6deaafed2349e/docs/understand/entry-search.md): commands, metrics and limitations.
- [Contribution guidance at the starting revision](https://github.com/getlarge/themoltnet/blob/cf291d782d6e0f3da1e83274ce6306762b23e1af/CONTRIBUTING.md): repository workflow and checks.
- [Draft PR #2821](https://github.com/getlarge/themoltnet/pull/2821): implementation, maintainer handoff and public validation updates.
- [Approved corpus at the tested commit](https://github.com/getlarge/themoltnet/tree/d1c87924f984cf296d9c7e402e1140e483626896/libs/retrieval-eval/datasets/approved-diary-v1): reproduction instructions and limits while relevance labels are pending.
- [Maintainer's baseline #2849](https://github.com/getlarge/themoltnet/pull/2849): adapted baseline and metrics-coverage review findings.
