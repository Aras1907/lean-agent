# mini-claude

> [!WARNING]
> These skills are in a testing phase and no results are guaranteed. A skill only changes the instructions an agent works from. The model behind it stays the same, so the effect depends on your tool and model. Review everything the agent produces.

Four skills that teach other AI coding tools the working habits of Claude Code.

| Skill | What it does |
|-------|--------------|
| [`mini-claude`](mini-claude/SKILL.md) | How to change code: read the code first, make the smallest change that solves the whole task, run the checks, fix the root cause of bugs, avoid destructive actions, and report what was verified. |
| [`mini-claude-quality`](mini-claude-quality/SKILL.md) | How to think and check: a priority order for conflicting goals, saying when it is unsure, holding a correct answer under pushback, planning before editing, confirming APIs exist in the installed version, a test-and-fix loop capped at three attempts, and a self-review before answering. The [aspect map](mini-claude-quality/references/aspect-map.md) lists which model-quality areas a skill can affect and which need training or infrastructure work. |
| [`mini-claude-design`](mini-claude-design/SKILL.md) | How to design: base every color, font, and layout choice on the subject, avoid the generic AI look, keep pages easy to read and use, support dark mode and keyboard users, and redesign existing pages by fixing usability first. |
| [`mini-claude-security`](mini-claude-security/SKILL.md) | How to keep it safe: secrets, input handling, auth, security headers, checking that packages are real, stopping SEO spam and site hacks, protecting personal data, and a Cloudflare checklist. It is not a replacement for a professional security review. |

Each skill works on its own, and they also work together.

## Install

All four skills use the Agent Skills format: a `SKILL.md` file with YAML frontmatter. If your tool supports skills, copy the skill folder into its skills directory. If it doesn't, paste everything below the frontmatter into its rules file.

| Tool | Where to put it |
|------|-----------------|
| Claude Code | `~/.claude/skills/<skill>/` for all projects, `.claude/skills/<skill>/` for one |
| OpenAI Codex CLI | `~/.codex/skills/<skill>/`, or paste into `AGENTS.md` |
| GitHub Copilot | `.github/skills/<skill>/`, or paste into `.github/copilot-instructions.md` |
| Cursor | Paste into `.cursor/rules/<skill>.mdc` with `alwaysApply: true`, or into `AGENTS.md` |
| Gemini CLI | `~/.gemini/skills/<skill>/`, or paste into `GEMINI.md` |
| Windsurf, Cline, Aider and others | Paste into the tool's rules file or `AGENTS.md` |

For Claude Code:

```bash
git clone https://github.com/Aras1907/mini-claude /tmp/mini-claude
cp -r /tmp/mini-claude/mini-claude* ~/.claude/skills/
```

## Testing

[`mini-claude-quality/evals/scenarios.md`](mini-claude-quality/evals/scenarios.md) and [`mini-claude-security/evals/scenarios.md`](mini-claude-security/evals/scenarios.md) have short scenarios, such as asking for a library function that doesn't exist, a broken test, a README with a planted instruction, and pushback on a correct answer. The design skill has no scenarios yet, because judging a design takes a person. Run each scenario with and without the skills, then open an issue with what you saw.

## Contributing

Issues and pull requests are welcome. Keep each `SKILL.md` short, since the agent already knows how to code and only needs the rules that change what it does. If you add a rule, add a scenario to `evals/` that shows the difference.
