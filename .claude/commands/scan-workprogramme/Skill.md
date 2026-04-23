---
name: Scan Work Programme
description: Read a local work programme PDF from the call_documents/ directory and extract, score, and save all call topics relevant to the research profile. Use when you have downloaded a funding work programme PDF and want to systematically scan it for matching calls.
---

Scan the work programme PDF given in $ARGUMENTS for funding call topics matching the research profile defined in the **Research Profile** section of `CLAUDE.md`. Use all fields from that section (topics, keywords, institution type, budget range, consortium size, deadline constraint) when filtering and scoring topics.

If $ARGUMENTS is a filename (e.g. `wp-9-food.pdf`), look for it in `call_documents/`. If it is a full path, use it directly. If $ARGUMENTS is empty, list all PDFs in `call_documents/` and ask which one to scan.

## Steps

### 1 — Extract text from the PDF

Run this Python script via Bash to extract the full text:

```python
import fitz  # pymupdf — install with: pip install pymupdf
doc = fitz.open("<path_to_pdf>")
full_text = "".join(page.get_text() for page in doc)
print(f"Pages: {len(doc)}, Characters: {len(full_text)}")
```

If pymupdf is not installed, run `pip install pymupdf` first.

### 2 — Extract all call overview tables

Call overviews follow this pattern in EU work programmes:
```
Call - <Call Name> (<Year>)
HORIZON-<PROGRAMME>-<YEAR>-<CALL-ID>
Opening: <date>
Deadline(s): <date(s)>
Topics | Type of Action | Budget | EU contribution per project | Projects
<TOPIC-ID>: <Title>  <type>  <budget>  <per-project>  <count>
```

Extract all call overview tables by searching for `Opening:` and `Deadline` markers. For each call block, record:
- Call identifier (e.g. HORIZON-CL6-2026-03)
- Opening date
- Deadline(s) — note if multi-stage (first stage / second stage)
- All topic IDs and titles listed in that call block

### 3 — Extract topic body text

For each topic ID found in the overview tables, find its **body section** in the document (the second occurrence of the topic ID — the first is usually in the table of contents). Extract:
- Expected outcomes
- Scope description
- Eligibility / consortium conditions
- TRL requirements
- Any AI, digital, data, or sectoral keywords in the text

### 4 — Filter and score

Filter topics to those where the deadline is ≥3 months from today. For each remaining topic, score:

| Dimension | 1–5 | Criteria |
|---|---|---|
| Topic fit | 1–5 | Match to food safety / food security / agriculture / biological control |
| Keyword fit | 1–5 | Explicit mention of AI, generative AI, LLM, digital solutions, data |
| Budget fit | 1–5 | 5 = within €200k–€5M; deduct 1 per doubling outside range |
| Deadline fit | 5 or 1 | 5 if ≥3 months from today; 1 if already passed or <3 months |
| Feasibility | 1–5 | Can a research institute lead/co-lead? Industry requirement, TRL expectations |

Compute overall score = average of five dimensions.

### 5 — Save qualifying topics

For each topic with overall score ≥ 3.5 that does **not** already have a file in `calls/`, save a new file `calls/<slug>.md` using this format:

```markdown
# <Call Title>

- **Programme:** <programme>
- **Call ID:** <topic ID>
- **URL:** https://ec.europa.eu/info/funding-tenders/opportunities/portal/screen/opportunities/topic-details/<topic-id-lowercase>
- **Deadline:** <date> (<N days from today>)
- **Budget per project:** <range>
- **Action type:** <RIA / IA / CSA>
- **Fit score:** <overall>/5 — <one sentence justification>

## Description
<2–3 sentence summary from scope/outcomes text>

## Relevance to Profile
<Why this matches: which topics/keywords align, consortium fit, budget notes>

## Source
Extracted from: `call_documents/<filename>`
```

For topics with score 1–2.9, list them in the summary table but do not create files.

### 6 — Print summary

Print a ranked summary table of all topics evaluated, sorted by overall score descending:

```
| Score | Call ID | Title | Deadline | Budget/project | Status |
|---|---|---|---|---|---|
| 4.8/5 | HORIZON-... | ... | dd Mon yyyy | €X–YM | Saved to calls/ |
| 3.2/5 | HORIZON-... | ... | dd Mon yyyy | €X–YM | Saved to calls/ |
| 2.1/5 | HORIZON-... | ... | dd Mon yyyy | €X–YM | Below threshold |
| 1.0/5 | HORIZON-... | ... | PASSED | — | Deadline passed |
```

Also print a brief note about any calls whose first-stage deadline has passed but second-stage is still open — flag as "invited applicants only".
