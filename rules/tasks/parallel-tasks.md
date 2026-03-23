# Global Agent Rules

Prefer parallelism in both the planning of your work and the execution. This document outlines both guidelines to follow and directions to ensure there is good parallelization

## General Guidelines

- Bias toward delegation: if in doubt, spawn a subagent.
- Keep the main conversation focused on coordination, planning, and presenting results -- offload execution to subagents.
- When splitting work, aim for roughly equal-sized chunks per subagent to balance load.
- After all parallel subagents complete, synthesize their results in the main session before proceeding.

## Prefer Background Subagents

- **Always prefer background subagents** over running tasks inline when the task will take more than a few seconds or involves multiple steps.
- For long-running tasks (builds, test suites, large refactors, migrations), delegate to a background subagent so the main session remains responsive.

## Parallelize with Multiple Subagents

- When a task is naturally parallelizable, **split it across multiple background subagents running in parallel** rather than writing a single fragile script.
- Examples of when to parallelize across subagents:
  - Modifying syntax or updating API usage patterns across many files (give each subagent a subset of files).
  - Running independent test suites or lint checks simultaneously.
  - Performing bulk renames, refactors, or migrations that touch many independent locations.
  - Searching or analyzing multiple directories or modules concurrently.
- Each subagent should receive a clear, self-contained task description with explicit file lists or scope boundaries so work doesn't overlap or conflict.

## Why Subagents Over Scripts

- Subagents can reason about each change individually, handling edge cases that a regex or sed script would miss or break.
- Subagents can verify their own work (e.g., check syntax, run a local build) before reporting back.
- If one subagent fails, the others are unaffected -- this is more resilient than a monolithic script that aborts on the first error.

## Prefer Parallel Subagents for Task Execution

- **Default to running tasks in parallel subagents** rather than executing them sequentially in the main session.
- Even when tasks seem small or quick, prefer dispatching them as parallel subagents if there are multiple independent units of work.
- When the user asks you to do something, look for opportunities to decompose it into independent subtasks and run them concurrently via subagents.
- Examples:
  - Reading and analyzing multiple files: spawn a subagent per file or group of files rather than reading them one by one.
  - Implementing multiple independent changes: give each change to its own subagent.
  - Researching a question that touches multiple areas of the codebase: dispatch parallel exploration subagents for each area.
- Only run tasks sequentially when there is a true data dependency between them (e.g., one task's output is another's input).
