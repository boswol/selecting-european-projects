# Plan of Action

## Goal

Build a Claude Code-assisted workflow for selecting research funding calls, structured as a series of custom skills. Each phase is a learning milestone for how Claude Code skills work.

## Phases

### Phase 1 — Foundation
- [ ] Write research profile into `CLAUDE.md`
- [ ] Create `/find-calls` skill using web search to find open calls
- **Skill concepts learned:** reading `CLAUDE.md` context, basic tool use (WebSearch), writing output files

### Phase 2 — Evaluation
- [ ] Create `/evaluate-call <url>` skill to score a call against the profile
- [ ] Create `/shortlist` skill to maintain a ranked tracking list
- **Skill concepts learned:** accepting arguments, structured scoring, reading/writing persistent state

### Phase 3 — Proposal Kickoff
- [ ] Create `/draft-proposal-outline <call>` skill to produce a proposal structure
- **Skill concepts learned:** combining context (profile + call details) into a structured deliverable

### Phase 4 — Automation (optional)
- [ ] Use the `schedule` skill to run `/find-calls` on a weekly cron
- **Skill concepts learned:** scheduled remote agents, the `schedule` built-in skill

## How Skills Work in Claude Code

Skills are markdown files in `.claude/commands/<name>.md`. When you type `/<name>`, Claude Code loads the file as a prompt and executes it. Skills can:

- Read `CLAUDE.md` for project context automatically
- Use any tool Claude has access to (WebSearch, Read, Write, Bash, …)
- Accept `$ARGUMENTS` passed after the command name
- Chain multiple tool calls in a single workflow
