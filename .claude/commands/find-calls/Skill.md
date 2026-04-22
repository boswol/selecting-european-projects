---
name: Find Calls
description: Search for open research funding calls (EU Horizon Europe, ERC, national grants) matching the research profile in CLAUDE.md. Use when looking for new grant opportunities to evaluate.
---

Search for open research funding calls that match the research profile in CLAUDE.md.

The research profile is:
- Topics: food safety, food, agriculture, biological control, climate
- Keywords: AI, artificial intelligence, generative AI, LLM, Agentic AI
- Institution type: research institute
- Budget range: €200k–€5M
- Consortium size: small (3–5) or large (6+)
- Constraint: deadline no sooner than 3 months from today

Steps:
1. Use WebSearch to find currently open EU funding calls relevant to the profile. Search across these sources:
   - EU Funding & Tenders Portal (ec.europa.eu/info/funding-tenders)
   - Horizon Europe work programmes
   - Any other relevant national or international research funding bodies
   Use search queries like "open Horizon Europe call food AI 2026", "EU funding call agriculture artificial intelligence", "Horizon Europe biological control call 2026", and similar variations.

2. For each promising call found (aim for 5–10 results), collect:
   - Call title
   - Funding body / programme
   - URL
   - Brief description (1–2 sentences)
   - Budget per project (if available)
   - Deadline
   - Fit score (1–5) based on how well it matches the research profile

3. Save each call as a separate markdown file in `calls/<slug>.md` using this format:
```
# <Call Title>

- **Programme:** <funding programme>
- **Call ID:** <identifier>
- **URL:** <url>
- **Deadline:** <date>
- **Budget per project:** <range or TBD>
- **Action type:** <RIA / IA / CSA>
- **Fit score:** <1–5> — <one sentence justification>

## Description
<2–3 sentence summary of the call>

## Relevance to Profile
<Why this call matches: which topics/keywords align, consortium fit, etc.>
```

4. After saving all files, print a summary table of all calls found, sorted by fit score descending.

If $ARGUMENTS is provided, treat it as an additional search constraint (e.g., a specific programme, country, or topic) and narrow the search accordingly.

## Resources

See `REFERENCE.md` for a curated list of funding portals organised by country and programme. Consult it to select the most relevant portals to search for a given query.
