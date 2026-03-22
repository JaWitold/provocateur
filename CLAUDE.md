# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

Provocateur is a Claude Code plugin — a collection of 7 specialized devil's advocate agents distributed as Markdown files. There is no build system, no runtime, and no tests. The "code" is the agent prompts themselves.

## Repository Structure

```
agents/          — One Markdown file per agent (the plugin's entire content)
.claude-plugin/
  plugin.json    — Plugin manifest (name, version, description, keywords)
```

## Agent File Format

Every agent in `agents/` is a Markdown file with YAML frontmatter:

```markdown
---
name: devils-advocate-<domain>
description: |
  Use this agent when [trigger condition]. Examples: <example>...</example>
model: haiku
---

[Agent system prompt]
```

Required frontmatter fields: `name`, `description`, `model`. The `description` field drives when Claude auto-selects the agent — it must clearly state trigger conditions and include 2–3 `<example>` blocks.

## Agent Naming Convention

```
agents/devils-advocate-<domain>.md
```

## Adding a New Agent

1. Create `agents/devils-advocate-<domain>.md` following the format above
2. Agent body must include: Role, What to Critique, Output Format, Rules sections
3. Output format must produce: What / Where / Why it matters / Fix for each finding
4. Update the agent table in `README.md`
5. Add an entry under `[Unreleased]` in `CHANGELOG.md`

## Current Agents and Their Scope

| Agent | Domain |
|-------|--------|
| `devils-advocate-code` | SOLID, Clean Architecture, DRY/KISS/YAGNI |
| `devils-advocate-security` | OWASP Top 10, CVEs, crypto, injection |
| `devils-advocate-api-design` | HTTP semantics, REST conventions, response contracts |
| `devils-advocate-performance` | N+1 queries, unbounded fetches, missing indexes |
| `devils-advocate-unit-tests` | PHPUnit compliance, coverage gaps, mock discipline |
| `devils-advocate-feature-tests` | Integration patterns, Foundry, SchemaTool |
| `devils-advocate-static-analysis` | PHPStan level 9, PHP-CS-Fixer, type safety |

## Plugin Installation (for reference)

```bash
git clone https://github.com/JaWitold/provocateur ~/.claude/plugins/provocateur
```

Register in `~/.claude/settings.json`:
```json
{ "plugins": ["~/.claude/plugins/provocateur"] }
```
