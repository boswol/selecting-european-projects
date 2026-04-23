# Selecting European Research Projects

A Claude Code-assisted workflow for discovering, evaluating, and shortlisting research funding calls — and generating proposal outlines for the best matches.

---

## What this project does

1. **Finds** open funding calls (EU Horizon Europe, ERC, EIC, VLAIO, national funders) matching a research profile
2. **Scans** downloaded work programme PDFs to extract and score all relevant call topics
3. **Evaluates** individual calls against the profile for fit, feasibility, deadline, and budget
4. **Shortlists** the most promising calls in a ranked tracking list *(planned)*
5. **Drafts** structured proposal outlines for selected calls *(planned)*

---

## Research profile

Defined in [CLAUDE.md](CLAUDE.md). Claude reads this automatically in every session.

| Field | Value |
|---|---|
| Topics | Food safety, food security, agriculture, biological control |
| Keywords | AI, artificial intelligence, generative AI, LLM, Agentic AI |
| Institution type | Research institute |
| Budget range | €200k–€5M per project |
| Consortium size | Small (3–5) or large (6+) |
| Deadline constraint | No sooner than 3 months from today |

To change the profile, edit the **Research Profile** section in `CLAUDE.md`. All skills pick up the change automatically.

---

## Skills

Skills are slash commands stored in `.claude/commands/<skill-name>/Skill.md`.

Run a skill by typing `/<skill-name>` in Claude Code. Arguments follow the command name: `/find-calls Horizon Europe`.

| Command | Description | Status |
|---|---|---|
| `/find-calls [filter]` | Web-searches open funding calls matching the profile; saves results to `calls/`; optional filter narrows to a programme, country, or topic | **Built** |
| `/scan-workprogramme <filename>` | Reads a local PDF from `call_documents/`, extracts all call topics, scores each against the profile, and saves qualifying calls (score ≥3) to `calls/` | **Built** |
| `/evaluate-call <url>` | Fetches a call URL, scores it on 5 dimensions (topic fit, keyword fit, budget fit, deadline fit, feasibility), and writes a go/no-go recommendation | **Built** |
| `/shortlist` | Shows and updates the ranked list of tracked calls | *Planned* |
| `/draft-proposal-outline <call>` | Produces a structured proposal outline for a selected call | *Planned* |

### How skills work

- Skills live in `.claude/commands/<name>/Skill.md`
- YAML frontmatter (`name`, `description`) tells Claude when to trigger the skill automatically
- `CLAUDE.md` is in context for every skill run — no need to repeat the profile
- `$ARGUMENTS` is replaced with whatever you type after the command name
- `REFERENCE.md` alongside a `Skill.md` holds supplemental data Claude loads on demand

---

## File structure

```
.
├── CLAUDE.md                            # Research profile + skill index (auto-loaded every session)
├── PLAN.md                              # Phased build roadmap
├── README.md                            # This file
├── calls/                               # One file per discovered or evaluated funding call
│   ├── cl6-2026-03-governance-08-ai-food.md          # CLOSED Apr 2026 — watch 2027 equivalent
│   ├── eupahw-call2-animal-health-welfare.md          # Pre-proposal closed; monitor Call 3
│   ├── futurefoods-call2-sustainable-food-systems.md  # Pre-proposal closed; monitor Call 3
│   ├── life-2026-nature-biodiversity-sap.md           # Open — deadline Sep 22 2026
│   ├── eic-pathfinder-challenges-2026.md              # Open — deadline Oct 28 2026
│   ├── msca-raise-doctoral-networks-2026-ai-agriculture.md  # Opens May 28 — deadline Nov 24 2026
│   ├── vlaio-onderzoeksproject-rolling.md             # Rolling — company must lead
│   └── vlaio-autumn-2026-calls-watch.md               # Pipeline — opens Sep–Nov 2026
├── call_documents/                      # Downloaded work programme PDFs for /scan-workprogramme
│   └── wp-9-food-bioeconomy-natural-resources-agriculture-and-environment_horizon-2026-2027_en.pdf
└── .claude/
    └── commands/
        ├── find-calls/
        │   ├── Skill.md                 # /find-calls skill
        │   └── REFERENCE.md            # Funding portals by country/programme
        ├── scan-workprogramme/
        │   └── Skill.md                # /scan-workprogramme skill
        └── evaluate-call/
            └── Skill.md                # /evaluate-call skill
```

---

## Calls tracked

| Fit | Call | Deadline | Budget/project | Status |
|---|---|---|---|---|
| 5/5 | [CL6-GOVERNANCE-08 — AI Solutions in Food](calls/cl6-2026-03-governance-08-ai-food.md) | ~~Apr 15 2026~~ | ~€7.5M | **CLOSED** — watch 2027 equivalent |
| 3/5 | [MSCA-RAISE — AI in Agriculture Doctoral Networks](calls/msca-raise-doctoral-networks-2026-ai-agriculture.md) | 24 Nov 2026 | ~€3–5M per network | Opens 28 May — prepare now |
| 3/5 | [EUPAHW Call 2 — Animal Health & Welfare](calls/eupahw-call2-animal-health-welfare.md) | 16 Sep 2026 | ~€500k–€2M | Pre-proposal closed |
| 3/5 | [FutureFoodS Call 2 — Sustainable Food Systems](calls/futurefoods-call2-sustainable-food-systems.md) | 27 Jul 2026 | ~€500k–€2M | Pre-proposal closed |
| 2/5 | [LIFE 2026 — Nature & Biodiversity SAPs](calls/life-2026-nature-biodiversity-sap.md) | 22 Sep 2026 | €1M–€5M | **Open** |
| 2/5 | [EIC Pathfinder Challenges 2026](calls/eic-pathfinder-challenges-2026.md) | 28 Oct 2026 | up to €4M | **Open** — challenges don't match profile directly |
| 3/5 | [VLAIO Autumn 2026 — TETRA/COOCK+/LA-trajecten](calls/vlaio-autumn-2026-calls-watch.md) | Sep–Nov 2026 | €150k–€1M | Not yet open — monitor from Aug 2026 |
| 2/5 | [VLAIO Onderzoeksproject — Rolling R&D Subsidy](calls/vlaio-onderzoeksproject-rolling.md) | Rolling | €100k–€3M | Always open — company must lead |

---

## Quickstart

1. Review and update the research profile in [CLAUDE.md](CLAUDE.md)
2. Run `/find-calls` to search the web for open calls — results saved to `calls/`
3. Drop a work programme PDF into `call_documents/` and run `/scan-workprogramme <filename>` to extract and score all topics
4. Run `/evaluate-call <url>` on any specific call page for a detailed 5-dimension score and go/no-go recommendation
5. Run `/shortlist` to see the ranked list *(skill coming soon)*
6. Run `/draft-proposal-outline <call-file>` to generate a proposal outline *(skill coming soon)*
