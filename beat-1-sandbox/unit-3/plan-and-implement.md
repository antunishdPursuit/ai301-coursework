# Unit 3: Plan and Build

Status: skill installed and evaluated; implementation plan and comment drafted. Live plan-check returned `accept` on all eight checks before posting and again after the as-built plan update. The initial comment check reported no voice-guide violations. The approved plan comment is posted. Implementation and controlled before/after validation are complete locally; branch push and portal submission remain pending.

## Posted upstream

**GitHub username**

antunishdPursuit

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5956700346

My [Week 2 report](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5904119559) established pass-through behavior with a mocked provider but no tone validation. The proposed classification step would run immediately after generation and before `parse_review_output` inside `generate_section`, covering both `generate_full_review` and direct callers.

A new `safety/tone_classifier.py` module would handle text extraction, the classification call, and result validation. For JSON responses, it would recursively collect nonempty string values including suggestions, and exclude bookkeeping fields like `section_name` and `confidence`. Plain text would be used directly. Constructive means specific, actionable, and respectful; honest criticism would pass. The classifier would return a decision and a reason; an unknown result would never count as approval.

On a negative or unknown result, `generate_section` would regenerate once with the original prompt plus a brief instruction to make feedback constructive while preserving format. A second failure would return a neutral unavailable `FeedbackSection` with confidence `0.0` and no suggestions; review generation would continue for remaining sections. Normal path: 10 provider calls for five sections with SDK transport retries disabled; at most 20 with all retries. Parser presentation behavior is a separate issue and outside this scope.

Does the `generate_section` placement work for you, or would a later hook fit the existing structure better?

<details>
<summary>Planned checks</summary>

Tests reuse `basic_profile.json` and prose from the seeded review as controlled inputs. Mock-controlled verdicts verify flow, not live classifier accuracy.

- Pass first time: one generation, one check; accepted raw response reaches the parser unchanged; full-review output preserves accepted content and suggestions, with citations added afterward.
- Fail then pass: first response never returned; second accepted response passes unchanged.
- Exhaustion: two failures return the neutral unavailable result for both `generate_section` and `generate_full_review`.
- Invalid result or timeout: treated as unknown; exhaustion path applies.

</details>

## Your branch

**Branch**

`fix/27-feedback-tone-check` (local; not pushed yet).

**Evidence**

Local implementation: `eedda67` and `8593fac`, based on `2f4e82f`. No branch push or PR yet.

Before, at `2f4e82f`, the [Week 2 script and recorded baseline](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5904119559) ran from the PathReview repository root:

```powershell
$env:PYTHONPATH = (Get-Location).Path
.\.venv\Scripts\python.exe -X utf8 -B "$env:TEMP\ai301-issue27-repro-eb27jham\reproduce_full.py"
```

Selected fields from the actual saved JSON output:

```json
{"case": "potentially_discouraging", "section_count": 5, "provider_call_count": 5, "content_preserved_with_citations": [true, true, true, true, true], "suggestions_preserved": [true, true, true, true, true]}
{"case": "encouraging_comparison", "section_count": 5, "provider_call_count": 5, "content_preserved_with_citations": [true, true, true, true, true], "suggestions_preserved": [true, true, true, true, true]}
```

After, on the implementation branch, the same two seed inputs ran through the real generator, extraction, classifier response validation, parser, and citation code. The provider remains mocked. The replay adds an explicit passing classifier response after each generation and changes the expected provider-call count to 10. These are controlled approvals, not measured tone labels.

```powershell
$env:PYTHONPATH = (Get-Location).Path
.\.venv\Scripts\python.exe -X utf8 -B '..\ai301-unit3-starter\eval\reproduce_full_after.py'
```

Selected fields from the actual output (exit 0):

```json
{"case": "potentially_discouraging", "section_count": 5, "provider_call_count": 10, "content_preserved_with_citations": [true, true, true, true, true], "suggestions_preserved": [true, true, true, true, true]}
{"case": "encouraging_comparison", "section_count": 5, "provider_call_count": 10, "content_preserved_with_citations": [true, true, true, true, true], "suggestions_preserved": [true, true, true, true, true]}
```

<details>
<summary>After-replay script for repeating the recorded command</summary>

Save the following as `reproduce_full_after.py` at the path in the command above, or replace that command's script path with its actual saved location. Run from the PathReview checkout root. It reads existing fixture and seed files without executing the database seeder.

```python
import ast
import json
import platform
import sys
from importlib.metadata import version
from pathlib import Path
from types import SimpleNamespace
from unittest.mock import MagicMock, patch
from rag.generator.review_generator import ReviewConfig, ReviewGenerator

repo = Path.cwd()
seed_path = repo / "scripts/seed_db.py"
tree = ast.parse(seed_path.read_text(encoding="utf-8"))
sections = []
for node in ast.walk(tree):
    if isinstance(node, ast.Dict):
        try:
            value = ast.literal_eval(node)
        except (ValueError, TypeError):
            continue
        if isinstance(value, dict) and {"section_name", "content", "suggestions"} <= value.keys():
            sections.append((node.lineno, value))
selected = [
    ("potentially_discouraging", next((line, item) for line, item in sections if "essentially invisible" in item["content"])),
    ("encouraging_comparison", next((line, item) for line, item in sections if item["content"].startswith("Significant improvement"))),
]
profile = json.loads((repo / "tests/fixtures/sample_profiles/basic_profile.json").read_text(encoding="utf-8"))
profile["projects"] = profile["repos"]
chunks = [{"text": item["readme_content"], "metadata": {"source_id": item["name"]}} for item in profile["repos"]]
print(json.dumps({"python": sys.version, "platform": platform.platform(), "openai": version("openai"), "structlog": version("structlog"), "mode": "existing seed replay with controlled classifier approval; no live model calls"}))
names = ["skills_feedback", "projects_feedback", "presentation_feedback", "gaps_feedback", "first_impression"]
sources = sorted({c["metadata"]["source_id"] for c in chunks[:5]})
citation = "\nSources: " + ", ".join(sources)
for label, (line, seed) in selected:
    client = MagicMock()
    client.with_options.return_value = client
    client.chat.completions.create.side_effect = [
        response
        for name in names
        for response in (
            SimpleNamespace(choices=[SimpleNamespace(message=SimpleNamespace(content=json.dumps({name: seed})))]),
            SimpleNamespace(choices=[SimpleNamespace(message=SimpleNamespace(content=json.dumps({"constructive": True, "reason": "Controlled pass-through comparison"})))]),
        )
    ]
    with patch("rag.generator.review_generator.openai.OpenAI", return_value=client):
        generator = ReviewGenerator(ReviewConfig(api_key="unused-mocked-client", base_url="http://127.0.0.1:1", model="mock-seed-replay"))
        result = generator.generate_full_review(profile, chunks)
    observed_names = [section.section_name for section in result]
    content_matches = [section.content == json.dumps(seed) + citation for section in result]
    suggestions_match = [section.suggestions == seed["suggestions"] for section in result]
    print(json.dumps({"case": label, "seed_line": line, "input_section": seed, "returned_sections": [{"section_name": s.section_name, "content": s.content, "suggestions": s.suggestions} for s in result], "section_names": observed_names, "section_count": len(result), "content_preserved_with_citations": content_matches, "suggestions_preserved": suggestions_match, "provider_call_count": client.chat.completions.create.call_count}, ensure_ascii=False))
    assert observed_names == names
    assert all(content_matches)
    assert all(suggestions_match)
    assert client.chat.completions.create.call_count == 10
```

</details>

The first eight new generator checks failed against the unmodified baseline. After implementation and three additional integration checks, all 43 new tests passed. They cover extraction, result validation, pass, regeneration, exhaustion, provider failures, accepted-output preservation, and continued full-review generation. None measures a live model's classification accuracy.

```powershell
.\.venv\Scripts\python.exe -m pytest tests/unit/test_tone_classifier.py tests/unit/test_review_generator.py -q
# 43 passed in 1.40s
.\.venv\Scripts\python.exe -m pytest tests/unit -q -m unit --tb=short
# 418 passed, 53 xfailed, 3 warnings in 24.72s
.\.venv\Scripts\python.exe -m ruff check .
# All checks passed!
.\.venv\Scripts\python.exe -m black --check .
# 113 files would be left unchanged.
.\.venv\Scripts\python.exe -m mypy api/ core/ ingestion/ rag/ agent/ safety/
# Success: no issues found in 77 source files
```

The full-suite warnings concern Pydantic configuration deprecation and unawaited AsyncMock coroutines outside the new tests. All existing expected-failure markers remain intact. Commit hooks (Ruff, Black, mypy) also passed. Live-provider/UI verification, remaining pre-push checks, branch publication, and portal submission are still pending.

## Eval iterations

**Run history**

One full official evaluation on October 2, 2026, using the harness's pinned Sonnet model: **19/20, PASS**. Category agreement: clear-accept 7/7, scope-creep 4/4, thread-convention 1/2, unbuildable 3/3, wrong-cause 4/4. Every category has at least one match. No rubric revisions or partial reruns followed this run. `eval-run.txt` is a byte-for-byte copy of the harness-written transcript, not an edited summary.

**Package analysis**

`pkg-20`: our rubric returned `accept`; the gold label is `reject`.

The package's repository policy says: "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance". The candidate comment does not disclose AI use, but the bundle does not establish that this candidate used AI. A reference to an AI-proposed solution in the maintainer's thread is not evidence of this candidate's tool use.

The gold-label note supplies the additional assumption: "every package here is treated as AI-assisted work". That note is not part of the bundle sent to the grader. Our result states: "package does not establish student AI use so disclosure is not triggered per evidence guide". I retained the disagreement rather than teaching the rubric to infer an unstated fact, consistent with the evidence boundary used in Unit 2. This explains the mismatch; it does not change the official gold label.

**Check rationale**

Exact current rubric row:

```text
| Thread and policy alignment | The draft comment compared with maintainer requests, thread highlights, and stated contribution rules. | The comment addresses applicable requests and conventions, including disclosure when the package establishes it is required. It neither contradicts maintainer direction nor relies on another student's plan as its own. Do not invent policies or assume undisclosed AI use. | required |
```

This check covers explicit maintainer direction and contribution rules, while requiring evidence before applying a conditional disclosure requirement. I kept the Unit 2 distinction between a policy's existence and evidence that the candidate used AI. I rejected a blanket assumption that every evaluated candidate used AI merely because this is an AI course.

**Trade-offs**

The evidence boundary costs one match on `pkg-20`. It can also miss undisclosed AI use when the package provides no evidence of that use. That is an explicit limit, not a claim that disclosure is optional when AI was used. The same unchanged rubric matched `pkg-04`, the other thread-convention case, so this choice did not erase the category. The full run met the category floor and passed; I made no subsequent rubric changes and therefore did not need a confirming rerun.
