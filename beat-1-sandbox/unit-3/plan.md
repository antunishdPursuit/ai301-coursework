# Plan: constructive feedback tone checks for #27

Status: approved, posted, and implemented locally on October 2, 2026. Controlled tests passed; live tone-classification accuracy and UI behavior remain unverified.

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27
Baseline revision: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.
Implementation branch: `fix/27-feedback-tone-check`, following the course skill's house rule.

## Evidence and diagnosis

The issue requests: "After generation, add a tone classification step that uses a prompt to classify whether each feedback section is constructive (actionable, specific, encouraging) or negative (discouraging, vague, dismissive). Reject and regenerate sections that fail."

My [Week 2 report](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5904119559) states: "The mocked test exercised the generator and parser, but only demonstrated pass-through behavior. It did not validate tone, and its response format differs from the current prompts."

Static inspection confirms that `generate_section` calls the model, parses its response, and returns the first parsed result. `generate_full_review` calls it for five sections, then adds citations. `ContentFilter` uses regex patterns for harmful phrases, a separate concern from constructive tone. This is a missing enhancement, not a reproduced classifier defect.

Four prompts request structured JSON; `first_impression` requests prose. The parser turns top-level keys into sections and the generator keeps the first. This can leave generated text outside a check placed after parsing. I have not verified the effect through live generation and the UI. The proposal avoids depending on a parser fix by checking all textual values in the raw response before that selection. It does not repair or claim to repair the parser's presentation or field-selection behavior.

## Scope and approach

Change only these application files:

- New `safety/tone_classifier.py`: extract text for tone checking, make the classification request, and validate its result.
- `rag/generator/review_generator.py`: invoke the check in `generate_section` immediately after each generation and before `parse_review_output`; bound regeneration and handle exhaustion.
- New `tests/unit/test_tone_classifier.py` and `tests/unit/test_review_generator.py`: test the new behavior and preservation of accepted output.

Leave `ContentFilter`, generation templates, output parser, frontend, Docker, database contents, and existing fixtures unchanged. No new sample-data files. The local plan and comment stay out of application commits.

1. In the classifier, accept the generated response and requested section name. For valid JSON, including fenced JSON, recursively collect nonempty string values, including suggestions, with their field paths. Exclude bookkeeping fields named `section_name` and `confidence`; do not send JSON syntax or numeric scores as feedback prose. For plain text, use the text itself. Invalid JSON-looking responses or responses without text produce an unknown result, not a pass. This extraction serves classification only; it must not rewrite the response returned to the existing parser.
2. Use a separate classifier prompt with the same configured provider/model. Supply the section name and extracted text as data. The instruction asks whether the entire section is respectful, specific, and useful, with actionable next steps where appropriate. Honest criticism can pass; praise is not required. Discouraging personal judgments, dismissive wording, and vague criticism fail. A concise first-impression summary need not contain a detailed action list. Tone is not a factual-accuracy check.
3. Require one JSON object: `{"constructive": true, "reason": "brief explanation"}`. The constructive value may be `true`, `false`, or `null` for unknown; the reason must be a nonempty string. Missing fields, wrong types, invalid JSON, an empty response, or a provider error are unknown and never count as approval. Treat supplied text as material to assess, never instructions to follow.
4. In `generate_section`, accept only `constructive: true`, then run the existing parser unchanged. On a negative or unknown result, regenerate once using the original generation prompt plus a brief instruction to make feedback constructive while preserving its requested format. Do not reuse failed text as accepted output or retry indefinitely.
5. If the second attempt also fails, return a neutral unavailable `FeedbackSection` with the requested name, confidence `0.0`, and no suggestions. Do not expose rejected text or provider error details. Full-review generation continues with the remaining sections; direct callers receive the same fallback. Exceptions during generation also use this bounded failure path.
6. Bound generation and classification calls with a 30-second timeout and disabled SDK transport retries on these calls. Two attempts per section mean at most four calls per section, or 20 for a five-section review; the normal path uses 10. This is a call-count limit, not a guaranteed total runtime. Record only section, outcome, and attempt in new logs, not portfolio text.

## Validation and expected observations

Reuse `tests/fixtures/sample_profiles/basic_profile.json` and read review content/suggestions from `scripts/seed_db.py` as literals, without running the seeder or changing Docker data. Mock provider responses in the tests. Control verdicts explicitly; neither seed has a validated tone label.

- Extraction: plain prose, nested JSON, fenced JSON, and suggestions reach the classifier. Reuse existing seed prose under the field names requested by current templates to check that later fields are included. Numeric-only or malformed structured output remains unknown. This checks extraction, not model quality.
- Classification result handling: valid pass/fail/unknown, wrong types, missing reason, malformed JSON, empty output, and timeout produce the stated results. A quoted instruction inside feedback remains data in the request.
- Pass first time: one generation and one check; accepted raw response reaches the existing parser unchanged.
- Fail then pass: two generations and two checks; the first response is never returned. Reuse the two existing seed texts as controlled responses, without asserting their real tone labels.
- Repeated failure or unknown: stop after two attempts and return the neutral unavailable result. Cover both direct `generate_section` and `generate_full_review`.
- Full review: each generated response is checked before citations. For the existing section-envelope baseline format, retain five section names, accepted content, suggestions, and citations. First-pass acceptance uses 10 provider calls; two attempts for all five sections never exceeds 20.

Capture the original Week 2 script and output as the before record. Adapt its provider stub to supply explicit classifier responses for the after record; do not present those verdicts as live classification. Run new tests against the baseline first to show the missing contract, then against the implementation. Report the commands and actual output.

From the repository root, using the existing virtual environment:

```powershell
.\.venv\Scripts\python.exe -m pytest tests/unit/test_tone_classifier.py tests/unit/test_review_generator.py -q
.\.venv\Scripts\python.exe -m ruff check .
.\.venv\Scripts\python.exe -m black --check .
.\.venv\Scripts\python.exe -m mypy api/ core/ ingestion/ rag/ agent/ safety/
.\.venv\Scripts\python.exe -m pytest tests/unit -v -m unit
```

Before pushing, follow the repository's remaining applicable checks and report any environment blocker. No fixture additions, Docker repair, or unrelated fixes are included to force checks green.

## Risks and limits

- The extra model calls increase latency and cost; the one-regeneration cap bounds calls and can leave a section unavailable.
- Prompt judgments can misclassify respectful criticism. Mocked tests verify integration, retry limits, and result handling; they do not measure live classifier accuracy. Review the prompt with the maintainer and keep any future labeled evaluation separate from these results.
- Text extraction must cover all fields before the parser drops any. That is the first implementation check; if doing so requires changing the output contract, stop and revise the plan before broadening scope.
- Existing parser/UI behavior and the known local Chroma startup failure remain separate. No claim of end-to-end UI validation is made.
- The plan comment is a proposal. Dennis reviews its exact wording before publication; the branch is built after that step. Use coherent Conventional Commits for classifier behavior and generator integration, each with its relevant tests.

## Deviations

The implementation followed the approved Week 3 plan; there were no changes to its behavior or file scope. The four approved files were the only application files committed. The placement is earlier than the tentative Week 2 suggestion, as already stated in the approved plan: before parsing inside `generate_section`.

Local commits: `eedda67` adds the classifier and its tests; `8593fac` integrates checks and bounded regeneration. Validation: 43 focused tests passed; the full unit suite had 418 passed, 53 expected failures, and 3 warnings. Repository-wide Ruff, Black check, and mypy passed, as did the commit hooks. Both original seed replays preserved content, suggestions, and citations under controlled classifier approval, with 10 calls each. No new sample-data files, database changes, live model quality test, Docker repair, or UI verification were performed. The [implementation branch](https://github.com/antunishdPursuit/pathreview-ai301-fa26-s3/tree/fix/27-feedback-tone-check) is published at `8593facae77e546e180c14a4c64616febe83becf`. Portal submission remains pending.

## Publication checks

The frontend source tree is identical to the baseline. `npm test -- --run` produced 17 passed and one timeout twice: `ProfileForm > validates portfolio URL character limit` exceeds the default 5-second limit locally. A diagnostic run, `npm test -- --run --testTimeout=15000`, passed all 18 tests. No frontend files or timeout settings were changed. The default-command timeout remains a limitation; no green remote CI or live UI result is claimed.

`pytest tests/integration -q --tb=short` collected no tests (exit 5). The repository's CI explicitly allows this for its empty integration directory; it is not evidence of runtime integration coverage.
