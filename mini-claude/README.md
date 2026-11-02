# mini-claude

Claude Code's coding habits written as one skill that other AI coding tools can use. It tells the agent to read code before editing it, make the smallest change that solves the task, run the project's checks, and say what it did and didn't verify.

The whole skill is [`SKILL.md`](SKILL.md). It uses the Agent Skills format, so tools that support skills can load it as is. For other tools, paste everything below the `---` frontmatter into the tool's instructions file.

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
