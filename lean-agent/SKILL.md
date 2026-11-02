---
name: lean-agent
description: Step-by-step workflow for coding tasks with more than one step. Use for building features, fixing bugs, refactoring, debugging, or reviewing code. Covers planning, checking APIs exist, a capped test-and-fix loop, self-review, and how to report results.
---

# Coding workflow

Follow the steps in order. Don't skip a step.

## Step 1. Understand the task

1. Write the goal in one sentence.
2. Write how you will know it is done. Example: "`npm test` passes and `/login` returns 200."
3. If the user's request is based on a wrong fact, tell them before you start.
4. Ask a question only if the answer changes what you build. Otherwise pick the simple default and say which one you picked.

## Step 2. Read the code

1. Search for the files involved. Read them.
2. Search for every caller of any function you will change.
3. Find the test, lint, type check, and build commands. Look in `package.json`, `Makefile`, `pyproject.toml`, CI config, or the README.
4. Check the dependency file before you assume a library is installed.

## Step 3. Plan

1. Write a short checklist of steps.
2. List the edge cases: empty input, very large input, missing values, wrong types, errors from the network or disk, and two users at the same time.
3. For a bug, first write a test or command that shows the bug.

## Step 4. Check every API before you use it

Small models often invent functions that don't exist. Before you use a function, method, flag, config key, or package:

- Search the repo for it, or
- read the installed source (`node_modules/`, `site-packages/`, `vendor/`), or
- run the command with `--help`.

Use the installed version. It may be older than the one you remember. If you can't confirm something exists, don't use it.

## Step 5. Edit

- Do one checklist item at a time.
- Reuse code the project already has. Then the standard library. Then installed packages. Write new code last.
- Keep the diff small. No unrelated renames, reformatting, or cleanups.
- Comments explain why, not what.

## Step 6. Test-and-fix loop

Run the checks, fastest first: linter, type checker, tests for what you changed, all tests, build.

If a check fails:

1. Read the exact error message.
2. Fix the cause, not the symptom. Don't add `@ts-ignore`, `# type: ignore`, or an empty `catch`.
3. Run the check again.
4. After 3 failed tries with the same idea, stop. Re-read the code and try a different idea, or tell the user what you tried.

Never delete, skip, or weaken a test. Never hardcode an expected value to pass a test.

## Step 7. Review your own diff

Read your diff and answer each question:

- Does it meet the "done" line from Step 1?
- Did you handle the edge cases from Step 3?
- Is there anything the user didn't ask for? Remove it.
- Is there a debug print, commented-out code, or a secret? Remove it.
- Could another caller break?
- Re-read the user's first message. Did you miss anything?

## Step 8. Report

Write the reply in this order:

1. The result in one or two sentences.
2. What changed, with `file:line`.
3. Commands you ran and whether they passed.
4. What you did not check.
5. Any risk the user should know.

## Long tasks

- Keep a short note with: goal, done line, finished steps, next step. Keep it outside the repo.
- Before the context gets full, write a summary of where you are.
- When the user corrects you, follow the correction for the rest of the session. Offer to add it to `AGENTS.md` so it lasts.

## Git, only when asked

- Run `git status` and `git diff` first. Stage only files for this task.
- Short summary line. Body says why.
- On the default branch, make a new branch first.
- Never use `--no-verify` or force-push without asking.
