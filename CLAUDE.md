# Selecting European Research Projects

This project uses Claude Code to help identify interesting research funding calls and decide which ones are worth writing a proposal for.

## Project Purpose

Browse open funding calls (e.g., EU Horizon Europe, ERC, national grants), evaluate them against a research profile, and produce proposal outlines for the most promising ones.

## Research Profile

> Fill this in before using the skills below.

- **Research topics:** (food safety, food, agriculture, biological control, climate)
- **Keywords:** (AI, artificial intelligence, generative AI, LLM, Agentic AI)
- **Institution type:** (research institute)
- **Preferred budget range:** (€200k–€5M)
- **Preferred consortium size:** (small 3–5, large 6+)
- **Constraints:** (deadline no sooner than 3 months out)

## Skills

Skills are slash commands in `.claude/commands/`. Run them as `/skill-name [args]`.

| Skill | Command | Description |
|---|---|---|
| Find calls | `/find-calls` | Web-searches for open funding calls matching the research profile |
| Evaluate call | `/evaluate-call <url>` | Scores a single call against the profile (fit, feasibility, deadline, budget) |
| Shortlist | `/shortlist` | Shows and updates the ranked list of calls being tracked |
| Draft outline | `/draft-proposal-outline <call>` | Produces a structured proposal outline for a selected call |

## Key Files

- `calls/` — fetched call summaries (one file per call)
- `shortlist.md` — ranked tracking list of candidate calls
- `.claude/commands/` — skill definitions
