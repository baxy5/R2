---
name: checkpointer-development
description: Break a non-trivial implementation into small sequential todos, completing ONE at a time and pausing for explicit user confirmation before continuing. Use when implementing a multi-step change that spans multiple steps or files.
---

Implement the requested change incrementally, checkpointing with the user between every step.

## When to use

- Any implementation that spans multiple steps or multiple files
- Refactors, feature builds, migrations, or wiring that cannot be done in a single trivial edit
- Skip for one-line fixes or single, self-contained edits

## Procedure

1. **Decompose** the task into a short, ordered list of todos. Each todo should be a small, independently reviewable unit of work.
2. **Present** the full todo list to the user up front so they see the plan.
3. **Implement exactly ONE todo** — the next not-started item.
4. **Summarize** what changed and how it was verified (tests, build, or diff).
5. **STOP and ask the user to continue.** Wait for explicit confirmation before starting the next todo.
6. **Repeat** from step 3 until every todo is complete.

## Rules

- One todo at a time — never batch multiple todos into a single step.
- Always pause and wait for the user's explicit go-ahead between todos.
- Keep each chunk small enough to review on its own.
- If new work surfaces mid-task, add it to the todo list rather than silently expanding the current step.
- Do not skip the summary or the confirmation prompt, even for quick todos.
