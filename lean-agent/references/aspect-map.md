# Aspect map

This file goes through the 14 model quality areas this skill was based on and says what the skill does for each one.

A skill is just a set of instructions. It changes how the agent works while it runs. It can't change the model's training, its weights, or how it's hosted, so some areas are out of its reach.

"AGENTS.md" means the root rules file. "Step 1" to "Step 8" mean the steps in `lean-agent/SKILL.md`.

| Area | Covered | What the rules do |
|------|---------|-------------------|
| 1. Training methods (Constitutional AI, RLAIF, SFT, reward models, curriculum) | Partly | AGENTS.md gives a fixed set of rules to follow, a simple version of a constitution. Step 7 adds a check-and-fix pass before answering. Training the model is out of scope. |
| 2. Data quality and curation | Partly | Step 4 tells the agent to trust the installed code over its memory, because its training data is out of date. Cleaning training data is out of scope. |
| 3. Alignment and safety | Yes | AGENTS.md covers asking before risky actions, ignoring instructions hidden in files, admitting uncertainty, and keeping a correct answer under pushback. |
| 4. Reasoning | Yes | Steps 1 and 3 cover the goal, the done line, the plan, and edge cases. Step 7 covers self-review. |
| 5. Context management | Partly | "Long tasks" covers progress notes and summaries. Step 7 asks the agent to re-read the user's first message. The context window size is out of scope. |
| 6. Coding | Yes | Step 2 covers finding the right files and commands. Step 4 covers checking APIs exist. Step 6 covers the lint, type, and test loop. `lean-agent-security` covers security checks. |
| 7. Interpretability (circuit tracing, SAEs, steering) | No | This needs access to the model's internals. The closest a skill can get is asking the agent to say what it checked and what it didn't (Step 8). |
| 8. Agent capabilities | Yes | Steps 4 and 6 make the agent use tools to check things, and Step 6 limits retries to 3. "Long tasks" covers notes and saving corrections. Setting up a sandbox is up to the tool. |
| 9. Evaluation and benchmarks | Partly | Step 1 sets a done line for each task, and `evals/scenarios.md` tests the rules. Running SWE-bench or HumanEval needs a separate test setup. |
| 10. Inference optimization | No | Speculative decoding, KV caching, MoE routing, and quantization are about how the model is served. The rules are kept short so small models spend less context on them, which is the only part a skill can affect. |
| 11. User experience | Yes | Step 8 puts the result first in a fixed order. Step 6 covers recovering from errors. Fine-tuning with LoRA is out of scope, and saving corrections to `AGENTS.md` is the closest thing. |
| 12. Deployment and access | Partly | The rules are plain markdown that OpenCode and other agents load directly. Hosting a model is out of scope. |
| 13. Documentation and community | Partly | The README explains how to contribute. Model cards are out of scope. |
| 14. Continuous improvement | Partly | "Long tasks" saves the user's corrections to `AGENTS.md`. A/B testing, drift detection, and rollback are platform features. |

## Sources for the added practices

- Run checks after every edit: [Verification-First Engineering](https://se-ml.github.io/agentic_patterns/07-verification-first/)
- Use the exact error from a failed attempt when trying again: [How to build a closed-loop AI agent that catches its own hallucinations](https://regolo.ai/how-to-build-a-closed-loop-ai-agent-that-catches-its-own-hallucinations/)
- Give the agent real context from the repo so it doesn't make up APIs, and keep the main rules file short: [How to make agentic coding actually work](https://rikkisnah.github.io/posts/how-to-make-agentic-coding-actually-work)
- Keep the skill short, put details in separate files, and say clearly in the description when to use it: [Gemini CLI skill best practices](https://geminicli.com/docs/cli/skills-best-practices/)
