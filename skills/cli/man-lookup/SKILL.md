---
name: man-lookup
description: Look up Linux/Unix command documentation using the man command
license: MIT
author: elee
compatibility: opencode
metadata:
  audience: developers
  workflow: local
---

## What I do

- Look up documentation for Linux/Unix commands using the `man` command
- Help understand command syntax, options, and behavior
- Search for related commands when the exact name is unknown

## When to use me

Use this when you encounter unfamiliar Linux/Unix commands and need to understand their usage.

## Usage

```bash
man <command>
```

## Guidelines

- Use `man` to understand command syntax, options, and behavior before using unfamiliar commands
- If a man page doesn't exist (exit code 16 or "No manual entry"), try `--help` or web search
- For commands with multiple sections, specify the section if needed: `man 5 passwd` (config files) vs `man 1 passwd` (command)
- Use `man -k <keyword>` to search for related commands when unsure of the exact command name

## Common Sections

- 1: User commands
- 5: File formats and config files
- 8: System administration commands

## Graceful Failure

Not all commands have man pages. If `man` fails:
1. Try `<command> --help` or `<command> -h`
2. Continue with the task - missing documentation is not a blocker
