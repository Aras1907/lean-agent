# Aspect map

How each model-quality aspect maps to this skill. A skill is a set of instructions: it changes **behavior at run time**, not the model's weights, training data, or serving stack. Aspects marked "out of scope" need model, infrastructure, or research work instead.

| # | Aspect | Covered? | Where / what a skill can do |
|---|--------|----------|-----------------------------|
| 1 | Training methodology (Constitutional AI, RLAIF, SFT, reward models, curriculum) | Partial | The *idea* of a constitution becomes the runtime principle hierarchy (SKILL §1) and the critique-and-revise loop (§7). Actual training is out of scope. |
| 2 | Data quality & curation | Partial | Knowledge-cutoff management: trust the repo and docs over memory (§2, §5). Dataset filtering is out of scope. |
| 3 | Alignment & safety | **Yes** | Safety-first hierarchy (§1), honest uncertainty (§2), prompt-injection resistance (§1), anti-sycophancy (§3). |
| 4 | Reasoning | **Yes** | Think-plan-act, done criteria, edge-case listing (§4), self-critique (§7). Extended-thinking modes are a tool setting; turn them on for hard tasks if available. |
| 5 | Context management | Partial | Targeted retrieval, re-reading the original request against "lost in the middle", progress notes, summaries (§7, §8). Window size and attention are out of scope. |
| 6 | Coding-specific | **Yes** | Repo mapping (§4), static analysis + types + tests loop (§6), dependency security scanning (§6), API grounding against installed versions (§5). |
| 7 | Interpretability (circuit tracing, SAEs, steering) | Out of scope | Needs model internals. The closest behavioral analog: state what was verified vs. inferred (§2, §10). |
| 8 | Agentic capabilities | **Yes** | Tool use over guessing (§5, §6), bounded retries (§6), sub-agent delegation (§8), memory/progress notes (§8, §9). Sandbox setup is the tool's job. |
| 9 | Evaluation & benchmarking | Partial | Per-task done criteria (§4) and `evals/scenarios.md` for measuring the skill. SWE-bench / HumanEval runs need a harness, out of scope. |
| 10 | Inference optimization | Out of scope | Speculative decoding, KV cache, MoE, quantization are serving-stack concerns. |
| 11 | User experience | **Yes** | Structured output validation, result-first reports, error recovery, summarization (§6, §8, §10). LoRA personalization is out of scope; project rules files are the runtime analog (§9). |
| 12 | Deployment & accessibility | Partial | The skill itself is portable: plain markdown that works in any tool (see README). Model hosting is out of scope. |
| 13 | Documentation & community | Partial | Contribution notes in the repo README. Model cards are out of scope. |
| 14 | Continuous improvement | Partial | Learning from corrections via memory/rules files (§9). A/B testing, drift detection, rollback are platform features. |

## Sources consulted for extra practices

- Verification as the main control loop, static checks after each edit: [Verification-First Engineering](https://se-ml.github.io/agentic_patterns/07-verification-first/)
- Feed the exact failure reason into the retry: [Closed-loop agent that catches its own hallucinations](https://regolo.ai/how-to-build-a-closed-loop-ai-agent-that-catches-its-own-hallucinations/)
- Grounded repo context as the defense against invented APIs; keep root rules files short: [How to make agentic coding actually work](https://rikkisnah.github.io/posts/how-to-make-agentic-coding-actually-work)
- Skill structure (concise body, details in references/, specific trigger description): [Gemini CLI skill best practices](https://geminicli.com/docs/cli/skills-best-practices/)
