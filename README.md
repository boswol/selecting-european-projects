# Selecting European Research Projects

A Claude Code-assisted workflow for discovering, evaluating, and shortlisting research funding calls — and generating proposal outlines for the best matches.

---

## What this project does

1. **Finds** open funding calls (EU Horizon Europe, ERC, EIC, national funders like NWO) that match a research profile
2. **Evaluates** each call against the profile for fit, feasibility, deadline, and budget
3. **Shortlists** the most promising calls in a ranked tracking list
4. **Drafts** structured proposal outlines for selected calls

---

## Research profile

Defined in [CLAUDE.md](CLAUDE.md). Claude reads this automatically in every session.

| Field | Value |
|---|---|
| Topics | Food safety, food, agriculture, biological control, climate |
| Keywords | AI, artificial intelligence, generative AI, LLM, Agentic AI |
| Institution type | Research institute |
| Budget range | €200k–€5M per project |
| Consortium size | Small (3–5) or large (6+) |
| Deadline constraint | No sooner than 3 months from today |

To change the profile, edit the **Research Profile** section in `CLAUDE.md`. All skills pick up the change automatically on their next run.

---

## Skills

Skills are slash commands stored in `.claude/commands/<skill-name>/`. Each skill has a `Skill.md` (instructions + YAML metadata) and optionally a `REFERENCE.md` (supplemental data Claude loads on demand).

Run a skill by typing `/<skill-name>` in Claude Code. Arguments can be appended: `/find-calls Horizon Europe`.

| Command | Description | Status |
|---|---|---|
| `/find-calls [filter]` | Web-searches open funding calls matching the profile and saves results to `calls/` | Built |
| `/evaluate-call <url>` | Scores a single call against the profile (fit, feasibility, deadline, budget) | Planned |
| `/shortlist` | Shows and updates the ranked list of tracked calls | Planned |
| `/draft-proposal-outline <call>` | Produces a structured proposal outline for a selected call | Planned |

### How skills work in Claude Code

- Skills live in `.claude/commands/<name>/Skill.md`
- The YAML frontmatter (`name`, `description`) tells Claude when to invoke the skill
- `CLAUDE.md` is automatically in context for every skill run — no copy-pasting the profile
- `$ARGUMENTS` in the skill body is replaced with whatever you type after the command name
- A `REFERENCE.md` alongside `Skill.md` can hold supplemental data (e.g., portal lists, scoring rubrics); Claude loads it on demand

---

## File structure

```
.
├── CLAUDE.md                          # Research profile + skill index (loaded every session)
├── PLAN.md                            # Phased build roadmap
├── README.md                          # This file
├── calls/                             # One file per discovered funding call
│   ├── cl6-2026-03-governance-08-ai-food.md
│   └── cl6-2026-03-governance-10-agriculture-peer-learning.md
└── .claude/
    └── commands/
        └── find-calls/
            ├── Skill.md               # Skill instructions + YAML metadata
            └── REFERENCE.md           # Funding portals by country
```

---

## Calls found so far

| Fit | Call | Deadline | Budget/project | Status |
|---|---|---|---|---|
| 5/5 | [HORIZON-CL6-2026-03-GOVERNANCE-08 — AI Solutions in Food](calls/cl6-2026-03-governance-08-ai-food.md) | 23 Sep 2026 | ~€7.5M | Open — verify deadline |
| 2/5 | [HORIZON-CL6-2026-03-GOVERNANCE-10 — On-Farm Peer Learning](calls/cl6-2026-03-governance-10-agriculture-peer-learning.md) | 23 Sep 2026 | ~€4–5M | Open |

> Additional calls (NWO KIC AI for Agriculture, LIFE 2026, EIC Pathfinder Challenges) are being investigated. Run `/find-calls` to update.

---

## Quickstart

1. Review and update the research profile in [CLAUDE.md](CLAUDE.md)
2. Run `/find-calls` to search for open calls — results are saved to `calls/`
3. Run `/evaluate-call <url>` on a specific call for a detailed score (skill coming soon)
4. Run `/shortlist` to see the ranked list (skill coming soon)
5. Run `/draft-proposal-outline <call-file>` to generate a proposal outline (skill coming soon)
