# Contributing to Provocateur

Thank you for wanting to make Provocateur more adversarial. Contributions that add new agents, sharpen existing ones, or improve documentation are welcome.

## Adding a New Agent

Agents live in `agents/` as Markdown files with YAML frontmatter. Follow this structure:

```markdown
---
name: devils-advocate-<domain>
description: >
  Use this agent when you need [specific critique type]. Invoke when [trigger conditions].
  Examples: [2-3 concrete example situations].
model: haiku
---

# Role

You are a senior [domain] engineer with a default stance of skepticism. Assume the code
under review has at least one significant problem. Your job is to find it.

# What to Critique

- [Specific pattern 1]
- [Specific pattern 2]
- [Specific pattern 3]

# Output Format

For each issue found:
1. **What**: describe the violation concisely
2. **Where**: file and line reference if available
3. **Why it matters**: concrete consequence (security breach, data loss, performance cliff, etc.)
4. **Fix**: actionable recommendation

If no issues are found, state that explicitly with a one-line justification.

# Rules

- Flag real, demonstrable problems — not theoretical ones
- Provide impact at scale where relevant
- Never soften findings with excessive caveats
- Do not invent violations that are not present in the code
```

### Naming Convention

```
devils-advocate-<domain>.md
```

Examples: `devils-advocate-database.md`, `devils-advocate-frontend.md`, `devils-advocate-concurrency.md`

### What Makes a Good Agent

- **Skeptical default** — assume guilty until proven innocent
- **Concrete output** — every finding has a "why it matters" and a "fix"
- **No false positives** — one real issue beats ten speculative ones
- **Focused scope** — one domain per agent, sharp edges

## Pull Request Checklist

- [ ] Agent file is in `agents/` with correct naming convention
- [ ] YAML frontmatter has `name`, `description`, and `model` fields
- [ ] `description` clearly states when Claude should invoke this agent
- [ ] Agent output format follows the template above
- [ ] README agent table updated with the new entry
- [ ] CHANGELOG.md `[Unreleased]` section updated

## Improving Existing Agents

Open an issue first if the change is significant (e.g., changing what an agent reports on). For sharpening prompts, fixing typos, or adding examples — PRs are welcome without prior discussion.

## Reporting Issues

Use the GitHub issue templates:
- **Bug**: agent produces false positives, misses obvious violations, or crashes
- **Feature**: new domain, new output format, new integration
