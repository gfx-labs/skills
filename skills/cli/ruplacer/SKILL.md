---
name: ruplacer
description: Use ruplacer to find and replace text across multiple files in a codebase. Invoke this skill when the user asks to replace, rename, or refactor text patterns across files, or when they mention ruplacer directly.
author: elee
---

# Ruplacer Text Replacement Skill

Use the `ruplacer` CLI tool for efficient find-and-replace operations across codebases.

## When to Use This Skill

- User asks to replace text across multiple files
- User wants to rename a variable, function, class, or identifier globally
- User requests a codebase-wide refactor of a term or pattern
- User mentions "ruplacer" directly
- User wants to find and replace with regex patterns

## Instructions

### 1. Preview First (Dry Run)

Always run ruplacer **without** `--go` first to preview changes:

```bash
ruplacer 'old_pattern' 'new_replacement' /path/to/search
```

This shows what would be changed without modifying files.

### 2. Apply Changes

After user confirms the preview looks correct, run with `--go` to apply:

```bash
ruplacer --go 'old_pattern' 'new_replacement' /path/to/search
```

### 3. Common Options

| Option | Description |
|--------|-------------|
| `--go` | Actually write changes to disk (required to make changes) |
| `--no-regex` | Treat pattern as literal string, not regex |
| `-w, --word-regex` | Match whole words only (prevents partial matches) |
| `--preserve-case` | Replace all case variants (snake_case, CamelCase, etc.) |
| `-t, --type <type>` | Only search specific file types (e.g., `-t go`, `-t py`, `-t '*.tsx'`) |
| `-T, --type-not <type>` | Exclude file types |
| `--hidden` | Also search hidden files |
| `--ignored` | Also search gitignored files |
| `-e, --allow-empty` | Don't error if no matches found |

### 4. Example Workflows

**Simple literal replacement:**
```bash
# Preview
ruplacer --no-regex 'oldName' 'newName' src/

# Apply
ruplacer --go --no-regex 'oldName' 'newName' src/
```

**Rename with case preservation (snake_case, CamelCase, etc.):**
```bash
# Preview - will replace OldName, oldName, old_name, OLD_NAME, etc.
ruplacer --preserve-case OldName NewName src/

# Apply
ruplacer --go --preserve-case OldName NewName src/
```

**Word-boundary matching (avoid partial matches):**
```bash
# Preview - only matches 'foo' as a word, not 'foobar'
ruplacer -w 'foo' 'bar' src/

# Apply
ruplacer --go -w 'foo' 'bar' src/
```

**Regex replacement with capture groups:**
```bash
# Preview - swap 'LastName, FirstName' to 'FirstName LastName'
ruplacer '(\w+), (\w+)' '$2 $1' src/

# Apply
ruplacer --go '(\w+), (\w+)' '$2 $1' src/
```

**Filter by file type:**
```bash
# Only Go files
ruplacer -t go 'oldFunc' 'newFunc' .

# Only TypeScript/JavaScript
ruplacer -t ts -t js 'oldVar' 'newVar' .

# Glob pattern
ruplacer -t '*.tsx' 'Component' 'NewComponent' src/
```

**Exclude file types:**
```bash
# Exclude test files
ruplacer -T '*_test.go' 'pattern' 'replacement' .
```

### 5. Safety Guidelines

1. **Always preview first** - Never run with `--go` without showing the user what will change
2. **Use `--no-regex` for literals** - When replacing literal strings with special regex chars
3. **Use `-w` for identifiers** - Prevents replacing partial matches inside other words
4. **Use `--preserve-case` for renames** - Handles all naming conventions automatically
5. **Scope appropriately** - Specify a path to limit the search scope
6. **Check git status after** - Run `git diff` to verify changes look correct

### 6. Troubleshooting

**Only ONE path argument allowed:**
```bash
# WRONG - ruplacer does not accept multiple paths
ruplacer 'old' 'new' pkg/cli/ pkg/repository/

# CORRECT - run separately for each directory
ruplacer 'old' 'new' pkg/cli/
ruplacer 'old' 'new' pkg/repository/

# OR use a common parent directory
ruplacer 'old' 'new' pkg/
```

**Pattern starts with dashes:**
```bash
# Use -- to separate options from pattern
ruplacer -- --old-flag --new-flag src/
```

**No matches found:**
```bash
# Use -e to not error on empty results
ruplacer -e 'pattern' 'replacement' src/
```

**List available file types:**
```bash
ruplacer --type-list
```
