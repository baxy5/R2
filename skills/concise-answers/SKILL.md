---
name: concise-answers
description: Instructs agents to answer questions, explain code, and provide information with extreme brevity while preserving correctness. Use when the goal is to inform rather than modify — "how does X work", "why is this failing", "where is Y defined", "what's the best way to do Z", "explain this function". Trigger for any question-answering, code explanation, debugging guidance, architecture questions, or API/library usage. Enforces short, direct, read-only responses.
argument-hint: <question or topic>
---

## Workflow

1. **Understand** the question — identify the exact information needed, nothing more.
2. **Research** only if necessary — use search/read tools to gather the minimum relevant context; skip if you already know.
3. **Clarify** only if ambiguity blocks a correct answer — ask one concise question.
4. **Answer** — lead with the answer, append only the minimum supporting detail required for correctness; stop immediately after.

## Output format

- **Default**: 1–3 short sentences.
- **Bullets**: only when clearly shorter than prose; 2–4 items max.
- **Code snippet**: only when it is the clearest possible answer; no prose padding around it.
- **Headings**: only when the answer has distinct parts that would otherwise be hard to scan.
- Never include introductions, restatements, summaries, background, caveats, or unprompted follow-up detail.
- When answering about a codebase, reference specific files and symbols.

## When to use

- Code explanation: how code works, what a function does
- Architecture: project structure, how components interact
- Debugging: why an error occurs, what could cause a behavior
- Best practices: recommended approach, how to structure something
- API / library usage: how to call a method, what parameters it expects
- Codebase navigation: where something is defined or used
- General programming: language features, algorithms, design patterns

## Do NOT use

- When the task requires modifying files, running commands, or applying changes — explain what changes would be needed, but do not make them.
- When the user needs a long-form document, report, or structured deliverable rather than a direct answer.
