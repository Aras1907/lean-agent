# lean-agent

> [!WARNING]
> This project is in a testing phase and no results are guaranteed. These files only change the instructions an agent works from. The model stays the same, so results depend on your model. Review everything the agent produces.

Short, strict rules that help small models in [OpenCode](https://opencode.ai) write code more carefully, design better pages, and avoid common security mistakes.

## What's inside

| File | Loaded | What it does |
|------|--------|--------------|
| [`AGENTS.md`](AGENTS.md) | Always | The core rules in about 300 words: read before editing, keep changes small, check APIs exist, run the tests, be honest, ask before risky actions. It also tells the model which skill to load. |
| [`lean-agent`](lean-agent/SKILL.md) | When needed | An 8-step workflow for coding tasks: understand, read, plan, check APIs, edit, test-and-fix loop with a 3-try limit, self-review, report. |
| [`lean-agent-design`](lean-agent-design/SKILL.md) | When needed | Design rules for pages and apps that look made for their subject, read easily, work in dark mode, and work with a keyboard. Comes with a [starter CSS file](lean-agent-design/references/starter.css). |
| [`lean-agent-security`](lean-agent-security/SKILL.md) | When needed | Security and privacy rules: secrets, input, login, headers, fake packages, uploads, logs, search spam. Extra files for [Cloudflare](lean-agent-security/references/cloudflare.md), [SEO spam](lean-agent-security/references/seo-spam.md), and [privacy](lean-agent-security/references/privacy.md) load only when the task needs them. |

## Why it's built this way

Small models have less room for instructions and follow long text less reliably. So:

- The rules that matter on every task live in `AGENTS.md`, because OpenCode always loads it. A small model doesn't have to remember to load a skill to get them.
- Everything else is a skill. OpenCode only shows the model each skill's name and description, and loads the full text when the model asks for it.
- Each skill is about 700 words of short, numbered steps. One rule per line, written as a direct instruction.
- Long reference material sits in separate files that the skill tells the model to read only for matching tasks.

## Install in OpenCode

Use it for all projects:

```bash
git clone https://github.com/Aras1907/lean-agent ~/lean-agent
mkdir -p ~/.config/opencode/skills
cp -r ~/lean-agent/lean-agent ~/lean-agent/lean-agent-design ~/lean-agent/lean-agent-security ~/.config/opencode/skills/
cat ~/lean-agent/AGENTS.md >> ~/.config/opencode/AGENTS.md
```

The last line adds the rules to the end of your global `AGENTS.md` and keeps anything already in it.

Or use it for one project, run from the project folder:

```bash
git clone https://github.com/Aras1907/lean-agent /tmp/lean-agent
mkdir -p .opencode/skills
cp -r /tmp/lean-agent/lean-agent /tmp/lean-agent/lean-agent-design /tmp/lean-agent/lean-agent-security .opencode/skills/
cat /tmp/lean-agent/AGENTS.md >> AGENTS.md
```

To always get the latest rules without copying `AGENTS.md`, point OpenCode at it in `opencode.json` instead:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["https://raw.githubusercontent.com/Aras1907/lean-agent/main/AGENTS.md"]
}
```

OpenCode fetches the file at the start of each session. You still need to copy the skill folders.

Restart OpenCode after installing. To check the skills loaded, ask the agent which skills it has.

## Other agents

Any agent that reads `AGENTS.md` and Agent Skills folders can use the same files. The folders `~/.agents/skills/` (global) and `.agents/skills/` (project) are read by OpenCode and several other agents.

## Testing

[`lean-agent/evals/scenarios.md`](lean-agent/evals/scenarios.md) and [`lean-agent-security/evals/scenarios.md`](lean-agent-security/evals/scenarios.md) have short tests, such as asking for a function that doesn't exist, a broken test, a made-up package, and pushback on a correct answer. The design skill has no tests yet, because judging a design takes a person. Run each test with and without these files, using the same model, and open an issue with what you saw.

[`lean-agent/references/aspect-map.md`](lean-agent/references/aspect-map.md) lists the 14 model quality areas this project started from, and which ones instructions can and can't affect.

## Contributing

Issues and pull requests are welcome. Keep the rules short and direct, since every word costs a small model context. If you add a rule, add a test to `evals/` that shows the difference.
