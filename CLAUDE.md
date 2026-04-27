# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

"The Five Agents" — a multi-agent system built on the Claude API (Anthropic SDK).

## Architecture

Multi-agent orchestration system. The CEO Agent is the single entry point — it receives all tasks, decomposes them, routes to sub-agents, and returns a unified summary report. Always read `.claude/agents/CEO_AGENT.md` before working on any agent logic.

Memory persists between sessions in `memory/ceo_memory.md`.

## Development Commands

_To be added._

## Agents

### CEO Agent (orchestrator)
- Definition: [`.claude/agents/CEO_AGENT.md`](.claude/agents/CEO_AGENT.md)
- PRD: [`agents/CEO_AGENT_PRD.md`](agents/CEO_AGENT_PRD.md)
- Role: Receives all tasks, decomposes, routes to sub-agents, returns summary report
- Always load this agent first — it manages all others

### Yuval Agent (creative / image generation)
- Definition: [`.claude/agents/YUVAL_AGENT.md`](.claude/agents/YUVAL_AGENT.md)
- PRD: [`agents/YUVAL_AGENT_PRD.md`](agents/YUVAL_AGENT_PRD.md)
- Role: Analyzes `reference/` images, extracts visual style, crafts prompt, generates image via `/nano-banana-2`, saves to `outputs/`
- Depends on: `/nano-banana-2` skill (MCP)

### Sub-Agents (TBD)
To be defined. Update `.claude/agents/CEO_AGENT.md` Sub-Agent Roster when added.

## Skills

### nano-banana-2
- Definition: [`skills/nano-banana-2/SKILL.md`](skills/nano-banana-2/SKILL.md)
- Installed as: [`.claude/commands/nano-banana-2.md`](.claude/commands/nano-banana-2.md)
- Role: Generates images via Google Nano Banana 2 model through MCP
- MCP config: `.claude/settings.local.json` → `mcpServers.nano-banana-2`
- Requires env var: `NANO_BANANA_API_KEY`

### skill-creator
- Installed as: [`.claude/commands/skill-creator.md`](.claude/commands/skill-creator.md)
- Role: Create, test, and optimize new skills

### Superpowers
- Source: [`skills/superpowers/`](skills/superpowers/)
- Commands: `/brainstorm`, `/write-plan`, `/execute-plan`
- Agent: `.claude/agents/code-reviewer.md`
- Role: Full development methodology — brainstorm → plan → execute → test → review → merge
- 14 skills: brainstorming, writing-plans, executing-plans, test-driven-development, systematic-debugging, and more

## Directories

| Directory | Purpose |
|-----------|---------|
| `reference/` | Input images for style analysis by Yuval |
| `outputs/` | Generated images saved by Yuval |
| `memory/` | Persistent agent memory (`ceo_memory.md`) |
| `agents/` | PRD documents for each agent |
| `skills/` | Skill source files |
| `.claude/agents/` | Agent definitions (loaded by Claude Code) |
| `.claude/commands/` | Installed skills/commands |
