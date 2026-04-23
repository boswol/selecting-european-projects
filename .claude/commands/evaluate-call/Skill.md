---
name: Evaluate Call
description: Score a single funding call against the research profile in CLAUDE.md on fit, feasibility, deadline, and budget. Use when you have a specific call URL and want a detailed evaluation before deciding whether to pursue it.
---

Evaluate the funding call at the URL provided in $ARGUMENTS against the research profile defined in the **Research Profile** section of `CLAUDE.md`. Use all fields from that section (topics, keywords, institution type, budget range, consortium size, deadline constraint) when scoring and making the recommendation.

## Steps

1. **Fetch the call page.** Use WebFetch on $ARGUMENTS to retrieve the full call text. If the page is behind a login or unavailable, use WebSearch to find the call details by its ID or title.

2. **Extract the key facts:**
   - Call title and ID
   - Funding programme
   - Deadline
   - Budget per project (total and per beneficiary if available)
   - Action type (RIA / IA / CSA / other)
   - Consortium requirements (min partners, eligibility)
   - Core topic / scope description
   - Any explicit AI, data, or digital requirements

3. **Score the call on five dimensions** (each 1–5, where 5 = perfect match):

   | Dimension | What to assess |
   |---|---|
   | **Topic fit** | How well does the call's scientific scope match food safety, food security, agriculture, or biological control? |
   | **Keyword fit** | Does the call explicitly require, encourage, or reward AI / ML / generative AI / LLM / agentic AI approaches? |
   | **Budget fit** | Is the budget per project within €200k–€5M? Score 5 if central, lower if far outside range. |
   | **Deadline fit** | Is the deadline ≥3 months from today (pass = 5, fail = 1)? Note exact days remaining. |
   | **Feasibility** | Can a research institute realistically lead or be a core partner? Consider eligibility rules, consortium structure, required industry involvement, TRL expectations. |

   Compute an **overall score** = average of the five dimensions (rounded to 1 decimal).

4. **Write a recommendation** (3–5 sentences): Should the team pursue this call? What is the strongest argument for and against? What would need to be true (e.g., finding an industry partner, assembling a consortium) for this to be viable?

5. **Print the full evaluation** in this format:

```
# Evaluation: <Call Title>

- **Call ID:** <id>
- **URL:** <url>
- **Deadline:** <date> (<N days from today>)
- **Budget per project:** <range>
- **Action type:** <type>
- **Consortium:** <requirements>

## Scores

| Dimension | Score | Rationale |
|---|---|---|
| Topic fit | X/5 | … |
| Keyword fit | X/5 | … |
| Budget fit | X/5 | … |
| Deadline fit | X/5 | … |
| Feasibility | X/5 | … |
| **Overall** | **X.X/5** | |

## Recommendation
<3–5 sentence go/no-go recommendation with key conditions>

## Key Facts
<bullet list of the most important facts from the call text — scope, eligibility, consortium rules, indicative topics, expected outcomes>
```

6. **Optionally update the calls file.** If a file for this call already exists in `calls/`, append the evaluation scores and recommendation to it under a new `## Evaluation` section. If no file exists and the overall score is ≥3, create one using the standard `find-calls` format (extended with the Evaluation section).
