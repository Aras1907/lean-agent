# mini-claude

> [!WARNING]
> **Testing phase.** These skills are experimental. No results are guaranteed: they change how an agent is instructed to work, not the underlying model, and their effect varies by tool and model. Use at your own risk and review everything the agent produces.

Portable skills that bring Claude Code's working habits to any AI coding tool.

| Skill | What it does |
|-------|--------------|
| [`mini-claude`](mini-claude/SKILL.md) | Core coding discipline: read before editing, smallest complete change, verify, debug the root cause, stay safe, report honestly. |
| [`mini-claude-quality`](mini-claude-quality/SKILL.md) | Quality loop: principle hierarchy, honest uncertainty, anti-sycophancy, plan-then-act, API grounding, bounded test-and-fix loop, self-critique, long-context hygiene. See its [aspect map](mini-claude-quality/references/aspect-map.md) for what a skill can and cannot improve. |

Use them together: `mini-claude` for how to change code, `mini-claude-quality` for how to think and check.

## Install

Both skills use the open Agent Skills format (`SKILL.md` with YAML frontmatter). Copy each skill folder into your tool's skills directory, or paste the body (everything below the frontmatter) into its rules file.

| Tool | Where to put it |
|------|-----------------|
| Claude Code | `~/.claude/skills/<skill>/` (global) or `.claude/skills/<skill>/` (project) |
| OpenAI Codex CLI | `~/.codex/skills/<skill>/`, or paste body into `AGENTS.md` |
| GitHub Copilot | `.github/skills/<skill>/`, or paste body into `.github/copilot-instructions.md` |
| Cursor | Paste body into `.cursor/rules/<skill>.mdc` (`alwaysApply: true`) or `AGENTS.md` |
| Gemini CLI | `~/.gemini/skills/<skill>/`, or paste body into `GEMINI.md` |
| Windsurf / Cline / Aider / others | Paste body into the tool's rules file or `AGENTS.md` |

Example for Claude Code:

```bash
git clone https://github.com/Aras1907/mini-claude /tmp/mini-claude
cp -r /tmp/mini-claude/mini-claude /tmp/mini-claude/mini-claude-quality ~/.claude/skills/
```

## Testing

[`mini-claude-quality/evals/scenarios.md`](mini-claude-quality/evals/scenarios.md) has seven quick A/B scenarios (hallucinated API, failing test, sycophancy, prompt injection, structured output...). Run them with and without the skills and open an issue with your results.

## Contributing

Issues and PRs welcome. Keep each `SKILL.md` short: the agent is already capable, so add only what changes its behavior. Back a new rule with a scenario in `evals/` that shows the difference.
