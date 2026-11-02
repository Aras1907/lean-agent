# mini-claude

The coding habits that make Claude Code reliable, packaged as one portable skill for any AI coding tool: read before editing, smallest complete change, verify with real checks, debug the root cause, stay safe, report honestly.

The whole skill is [`SKILL.md`](SKILL.md). It uses the open Agent Skills format (YAML frontmatter + markdown), so tools that support skills load it directly; for the rest, paste the body (everything below the `---` frontmatter) into the tool's instructions file.

## Install

| Tool | Where to put it |
|------|-----------------|
| Claude Code | `~/.claude/skills/mini-claude/SKILL.md` (global) or `.claude/skills/mini-claude/SKILL.md` (project) |
| OpenAI Codex CLI | `~/.codex/skills/mini-claude/SKILL.md`, or paste body into `AGENTS.md` |
| GitHub Copilot | `.github/skills/mini-claude/SKILL.md`, or paste body into `.github/copilot-instructions.md` |
| Cursor | Paste body into `.cursor/rules/mini-claude.mdc` (set `alwaysApply: true`) or `AGENTS.md` |
| Gemini CLI | Paste body into `GEMINI.md` |
| Windsurf / Cline / Aider / others | Paste body into the tool's rules file, or `AGENTS.md` |

See the [repo README](../README.md) for install steps and the testing-phase notice.
