# Aspect map

This table goes through the 14 model-quality areas the skill was built from and says what the skill does about each. A skill is a set of instructions, so it can only change how the agent works while it runs. Training data, model weights, and the serving stack are out of its reach, and the areas that depend on them need model or infrastructure work.

Section numbers (§) refer to `SKILL.md`.

| # | Area | Covered | What the skill does |
|---|------|---------|---------------------|
| 1 | Training methods (Constitutional AI, RLAIF, SFT, reward models, curriculum) | Partly | The priority list in §1 plays the role of a constitution at run time, and the self-review in §7 is a critique-and-revise pass. Training itself is out of scope. |
| 2 | Data quality and curation | Partly | §2 and §5 tell the agent to trust the repo and docs over its memory, which helps with the knowledge cutoff. Filtering training data is out of scope. |
| 3 | Alignment and safety | Yes | Safety comes first in §1, §2 covers stating uncertainty, §1 covers instructions planted in data, and §3 covers pushback. |
| 4 | Reasoning | Yes | §4 covers planning, done conditions, and edge cases; §7 covers self-review. Extended thinking is a tool setting, so turn it on for hard tasks if your tool has it. |
| 5 | Context management | Partly | §8 covers targeted reading, progress notes, and summaries. §7 asks the agent to re-read the original request, since models tend to lose details in the middle of a long context. Context window size and attention are out of scope. |
| 6 | Coding | Yes | §4 covers mapping the repo, §6 the lint, type, test, and security check loop, and §5 confirming APIs against the installed version. |
| 7 | Interpretability (circuit tracing, SAEs, steering) | No | This needs access to model internals. The closest a skill gets is asking the agent to say what it checked and what it inferred (§2, §10). |
| 8 | Agent capabilities | Yes | §5 and §6 have the agent use tools to check things, §6 caps retries, §8 covers sub-agents and progress notes, and §9 covers memory. Setting up a sandbox is the tool's job. |
| 9 | Evaluation and benchmarks | Partly | §4 sets done conditions for each task, and `evals/scenarios.md` tests the skill. Running SWE-bench or HumanEval needs a separate harness. |
| 10 | Inference optimization | No | Speculative decoding, KV caching, MoE routing, and quantization happen in the serving stack. |
| 11 | User experience | Yes | §10 covers valid structured output and putting the result first, §6 covers recovering from errors, and §8 covers summaries. Fine-tuning with LoRA is out of scope; a project rules file (§9) is the closest substitute. |
| 12 | Deployment and access | Partly | The skill is a markdown file that works in any tool (see the README). Hosting a model is out of scope. |
| 13 | Documentation and community | Partly | The repo README has contribution notes. Model cards are out of scope. |
| 14 | Continuous improvement | Partly | §9 saves the user's corrections to memory or a rules file. A/B testing, drift detection, and rollback are platform features. |

## Sources for the added practices

- Run checks after every edit and treat verification as the main loop: [Verification-First Engineering](https://se-ml.github.io/agentic_patterns/07-verification-first/)
- Pass the exact failure into the next attempt: [How to build a closed-loop AI agent that catches its own hallucinations](https://regolo.ai/how-to-build-a-closed-loop-ai-agent-that-catches-its-own-hallucinations/)
- Ground the agent in the repo so it doesn't invent APIs, and keep the root rules file short: [How to make agentic coding actually work](https://rikkisnah.github.io/posts/how-to-make-agentic-coding-actually-work)
- Keep the skill body short, move detail into reference files, and give the description specific triggers: [Gemini CLI skill best practices](https://geminicli.com/docs/cli/skills-best-practices/)
