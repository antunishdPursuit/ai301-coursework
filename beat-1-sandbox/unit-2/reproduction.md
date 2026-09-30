# Unit 2: Claim and Reproduce

## Your identity upstream

**GitHub username**

antunishdPursuit

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5808564140

Hi, I'm a student in AI301 and I'd like to investigate the feedback tone check described in this issue.

In `rag/generator/review_generator.py`, `generate_section` passes the LLM response to `parse_review_output` and returns the result directly. Nothing between generation and return checks whether the content is constructive. `safety/content_filter.py` handles a separate concern: `ContentFilter.filter` uses regex patterns to flag harmful phrases and is not designed for tone classification.

To investigate, I plan to supply a simulated discouraging provider response at the LLM boundary inside `generate_section` and observe whether it reaches the caller unchanged. I'll also check whether `generate_full_review` offers a natural insertion point for a classification step before sections are appended. The repository has existing sample data I can reuse where it fits: `tests/fixtures/sample_profiles/basic_profile.json` for profile input and seeded reviews in `scripts/seed_db.py` for context reference. I haven't confirmed whether those samples cover a tone scenario specifically, and the seeded reviews alone don't exercise the generation path. I'll report the observed results before proposing anything.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/27#issuecomment-5904119559

*Edited: clarified the baseline test's limits and added the insertion-point finding.*

At revision `2f4e82f`, neither `generate_section` nor `generate_full_review` checks tone. `ContentFilter` uses regex matching for harmful phrases.

A per-section check could go in `generate_full_review` immediately after `generate_section` returns, before citations are added and the section is appended.

The mocked test exercised the generator and parser, but only demonstrated pass-through behavior. It did not validate tone, and its response format differs from the current prompts.

Four prompts request structured JSON; `first_impression` requests prose. `_parse_json_output` appears to treat top-level keys as sections, while `generate_section` keeps the first parsed result. I have not traced this through live generation and the UI. Before adding a tone check, we need to confirm how the model's response becomes feedback text and whether all intended text reaches the check.

Feedback on placement welcome before I draft the proposal.

<details>
<summary>Baseline test details</summary>

**Environment:** revision `2f4e82f`, Python 3.11.9, Windows-10-10.0.26200-SP0, openai 3.19.2, structlog 26.1.0, controlled replay of existing seed sections with no live model calls.

**Steps** (run from repo root):

1. Activate the existing `.venv` and install dependencies:
   ```powershell
   .\.venv\Scripts\Activate.ps1
   pip install -e ".[dev]"
   ```
2. Save the script to a location outside the repository. Replace `ABSOLUTE_SCRIPT_PATH` with the full Windows path; quote it so spaces in the path are handled correctly.
3. Set `PYTHONPATH` and run:
   ```powershell
   $env:PYTHONPATH = (Get-Location).Path
   python -X utf8 -B "ABSOLUTE_SCRIPT_PATH"
   ```

**Observed baseline:** Each of the two existing seed inputs produced five returned sections and five provider calls. The seed content was preserved with source citations added, and suggestions were preserved. These checks measure pass-through behavior, not tone.

**Limitations:** The mock returned the same seed dict for all five calls within each run; identical content across all five sections is an artifact of the test setup. The profile used (`basic_profile.json`) contains `recipe-scaler` and `transit-delay-tracker`, and neither seed subject is derived from that profile. These runs confirm the generator passes content and citations through correctly but do not show how often a live model produces discouraging output with this profile, and they do not prove either seed would fail a classifier if one existed. No application fix was made.

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
print(json.dumps({"python": sys.version, "platform": platform.platform(), "openai": version("openai"), "structlog": version("structlog"), "mode": "controlled replay of existing seed sections; no live model calls"}))
names = ["skills_feedback", "projects_feedback", "presentation_feedback", "gaps_feedback", "first_impression"]
sources = sorted({c["metadata"]["source_id"] for c in chunks[:5]})
citation = "\nSources: " + ", ".join(sources)
for label, (line, seed) in selected:
    client = MagicMock()
    client.chat.completions.create.side_effect = [
        SimpleNamespace(choices=[SimpleNamespace(message=SimpleNamespace(content=json.dumps({name: seed})))])
        for name in names
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
    assert client.chat.completions.create.call_count == 5
```

</details>

## Eval iterations

**Run history**

One complete scored run was saved on September 24, 2026, using Sonnet on all 20 scored packages. The final agreement was 19/20. The harness reported:

```text
agreement: 19/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
```

This meets the numerical 18/20 threshold but fails the category floor: disclosure was 0/1. I am retaining that result, not reporting it as a passing course evaluation. The committed `eval-run.txt` is the original harness-written transcript, copied without edits. Its fingerprints match the uploaded `rubric.md`, `references/evidence-guide.md`, and `SKILL.md`. Later voice-guide changes and live-comment evaluations are separate from this scored run; they do not change its score.

**Package analysis**

I chose `pkg-20`, the Ghostty mode-2031 report. My skill returned `accept`; the gold label is `reject`. The saved evaluator's `repo-conventions` explanation says:

> Template fields (version, config, platform) present; no AI use evident in the drafts so mandatory AI disclosure is not triggered; communication style appropriate to the thread.

The package's repository-policy block explicitly requires disclosure:

> All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance

The gold-label note adds:

> course packages are treated as AI-assisted work

The supplied candidate comments do not disclose AI use, but they also do not state that AI was used. The evaluator applied the policy conditionally rather than assuming authorship from the existence of an evaluation package. The gold note supplies that assumption. This explains the disagreement; it does not change the gold label or the failed category result. I chose to keep the evidence-based rule rather than add a blanket assumption solely to match this package.

**Check rationale**

The exact current `repo-conventions` row in the uploaded rubric is:

```text
| repo-conventions | Claim and repro comments against the issue context, repo-facts policy statements, and applicable contribution instructions; Evidence guide: Comms. | The comments follow applicable communication and contribution rules, including required AI-assistance disclosure and templates where mandated. No required disclosure is omitted. Verified policy silence does not create a requirement; unread or unavailable policy evidence is unclear. Apply scoped house rules only in live mode. | required |
```

I kept this wording because a repository's actual policy should determine the communication requirements. I rejected treating every missing AI disclosure as a failure regardless of policy or evidence. Verified silence is different from an unread policy. In this case, the policy itself is explicit; the disagreement concerns whether the package establishes that AI assistance occurred. Required checks graded `unclear` still prevent acceptance under the rubric's verdict rule.

**Trade-offs**

The package demonstrates a limit I accept in this run: the evaluator can accept an undisclosed AI-assisted comment when the bundle supplies no evidence of that assistance. That happened for `pkg-20` under the gold convention. A stricter assumption could catch it, but could also reject human-written comments merely because a repository has an AI policy. In live work, I know when I used AI and must follow any applicable disclosure requirement.

I did not change the scored rubric or rerun the full evaluation to conceal this mismatch. The saved category line is:

```text
categories: clear-accept 8/8  disclosure 0/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
```

The uploaded scoring-file fingerprints still match the recorded run, so the 19/20 result remains tied to the submitted rubric. The live PathReview report was expanded from a section-only test to `generate_full_review`, then evaluated again before posting. That improved the investigation's coverage, but it is not another scored 20-package run and does not satisfy the unmet disclosure category.
