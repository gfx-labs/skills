# Prefer ripgrep (`rg`) Over `grep`

- **Always use `rg` (ripgrep) instead of `grep`** for searching file contents from the command line.
- `rg` is faster, respects `.gitignore` by default, and provides cleaner output with better defaults for code search.
- Use `rg` flags as needed (e.g., `--type`, `--glob`, `-i`, `-C` for context lines).
- Never fall back to `grep` unless `rg` is explicitly unavailable.
