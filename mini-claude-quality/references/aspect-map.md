# Aspect map

This file goes through the 14 model quality areas this skill was based on and says what the skill does for each one.

A skill is just a set of instructions. It changes how the agent works while it runs. It can't change the model's training, its weights, or how it's hosted, so some areas are out of its reach.

The section names below match the headings in `SKILL.md`.

| Area | Covered | What the skill does |
|------|---------|---------------------|
| 1. Training methods (Constitutional AI, RLAIF, SFT, reward models, curriculum) | Partly | "When goals conflict" gives the agent a priority list to follow, which is a simple version of a constitution. "Review your own work" adds a check-and-fix pass before answering. Training the model is out of scope. |
| 2. Data quality and curation | Partly | "Say how sure you are" and "Confirm an API exists" tell the agent to trust the repo and the docs over its memory, because its training data is out of date. Cleaning training data is out of scope. |
| 3. Alignment and safety | Yes | "When goals conflict" puts safety first and tells the agent to ignore instructions hidden in files or web pages. "Say how sure you are" covers admitting uncertainty. "Don't just agree" covers holding a correct answer when the user pushes back. |
| 4. Reasoning | Yes | "Plan before you edit" covers planning, writing down what done looks like, and listing edge cases. "Review your own work" covers checking the result. Extended thinking is a tool setting, so turn it on for hard tasks if your tool has it. |
| 5. Context management | Partly | "Long sessions" covers reading only what's needed, keeping progress notes, and writing summaries. "Review your own work" asks the agent to re-read the original request, because models tend to forget details in long conversations. The size of the context window is out of scope. |
| 6. Coding | Yes | "Plan before you edit" covers finding the right files. "Test-and-fix loop" covers linting, type checks, tests, and security checks. "Confirm an API exists" covers checking functions against the installed version. |
| 7. Interpretability (circuit tracing, SAEs, steering) | No | This needs access to the model's internals. The closest a skill can get is asking the agent to say what it checked and what it guessed. |
| 8. Agent capabilities | Yes | "Confirm an API exists" and "Test-and-fix loop" make the agent use tools to check things instead of guessing, and the loop limits retries. "Long sessions" covers sub-agents and progress notes. "Corrections" covers memory. Setting up a sandbox is up to the tool. |
| 9. Evaluation and benchmarks | Partly | "Plan before you edit" sets a finish line for each task, and `evals/scenarios.md` tests the skill itself. Running SWE-bench or HumanEval needs a separate test setup. |
| 10. Inference optimization | No | Speculative decoding, KV caching, MoE routing, and quantization are about how the model is served. A skill can't touch them. |
| 11. User experience | Yes | "Your reply" covers valid JSON or YAML output and putting the result first. "Test-and-fix loop" covers recovering from errors. "Long sessions" covers summaries. Fine-tuning with LoRA is out of scope, and a project rules file ("Corrections") is the closest thing. |
| 12. Deployment and access | Partly | The skill is a plain markdown file, so it works in any tool. See the README for where to put it. Hosting a model is out of scope. |
| 13. Documentation and community | Partly | The README explains how to contribute. Model cards are out of scope. |
| 14. Continuous improvement | Partly | "Corrections" saves the user's corrections to memory or a rules file. A/B testing, drift detection, and rollback are platform features. |

## Sources for the added practices

- Run checks after every edit: [Verification-First Engineering](https://se-ml.github.io/agentic_patterns/07-verification-first/)
- Use the exact error from a failed attempt when trying again: [How to build a closed-loop AI agent that catches its own hallucinations](https://regolo.ai/how-to-build-a-closed-loop-ai-agent-that-catches-its-own-hallucinations/)
- Give the agent real context from the repo so it doesn't make up APIs, and keep the main rules file short: [How to make agentic coding actually work](https://rikkisnah.github.io/posts/how-to-make-agentic-coding-actually-work)
- Keep the skill short, put details in separate files, and say clearly in the description when to use it: [Gemini CLI skill best practices](https://geminicli.com/docs/cli/skills-best-practices/)
