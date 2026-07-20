---
name: command-explainer
description: Explain in 1-2 plain sentences what a shell/terminal command you are about to run does and its side effects, before running it. Invoke whenever you propose or run a non-trivial terminal command so the user understands it first.
argument-hint: <the command to explain>
---

## Workflow

1. Take the command you are about to run (or were asked about).
2. Identify the program, key flags, targets, and any side effects (writes, deletes, network, state changes).
3. Output a 1-2 sentence plain-language explanation. No step-by-step breakdown, no flag-by-flag table.
4. Flag any destructive or irreversible effect (delete, force push, reset, overwrite) explicitly in the explanation.

## Output format

One or two sentences, plain language, no preamble. Example:
`Removes all stopped Docker containers to free disk space — irreversible for those containers.`

## When to use

- Before running any non-trivial terminal command.
- When the user asks "what does this command do?"

## Do NOT use

- For trivial, obviously safe commands (`ls`, `cd`, `pwd`).
- When the user wants a deep, line-by-line teardown — give that directly instead.
