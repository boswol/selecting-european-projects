# Selecting European Research Projects

This project uses Claude Code to help identify interesting research funding calls and decide which ones are worth writing a proposal for.

## Project Purpose

Browse open funding calls (e.g., EU Horizon Europe, ERC, national grants), evaluate them against a research profile, and produce proposal outlines for the most promising ones.

## Research Profile

- **Research topics:** food safety, food security, agriculture, biological control, digital tool development
- **Keywords:** AI, artificial intelligence, generative AI, LLM, Agentic AI, decision support system, advisory tool
- **Institution type:** research institute
- **Preferred budget range:** €200k–€5M
- **Preferred consortium size:** small (3–5) or large (6+)
- **Target users:** farmers, food safety inspectors, food service professionals, policy makers
- **Delivery format:** web application, API/service
- **Constraints:** deadline no sooner than 3 months from today

## Skills

Skills are slash commands in `.claude/commands/`. Run them as `/skill-name [args]`.

| Skill | Command | Description | Status |
|---|---|---|---|
| Find calls | `/find-calls [filter]` | Web-searches for open funding calls matching the research profile; saves results to `calls/` | Built |
| Scan work programme | `/scan-workprogramme <filename>` | Reads a local PDF from `call_documents/` and extracts, scores, and saves all matching call topics | Built |
| Evaluate call | `/evaluate-call <url>` | Scores a single call URL against the profile (fit, feasibility, deadline, budget) | Built |
| Shortlist | `/shortlist` | Shows and updates the ranked list of calls being tracked | Planned |
| Draft outline | `/draft-proposal-outline <call>` | Produces a structured proposal outline for a selected call | Planned |

## Key Files and Directories

- `calls/` — one markdown file per discovered funding call
- `call_documents/` — downloaded work programme PDFs for local scanning with `/scan-workprogramme`
- `shortlist.md` — ranked tracking list of candidate calls (not yet created)
- `.claude/commands/` — skill definitions
- `.claude/commands/find-calls/REFERENCE.md` — curated list of funding portals by country and programme; used by `/find-calls` to know where to search
