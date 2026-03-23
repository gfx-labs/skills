---
name: context7-docs
description: |
    Reminder to use Context7 MCP for up-to-date library documentation. Use when working with any library, package, framework, or SDK - especially when needing API references, code examples, usage patterns, or troubleshooting.
    Triggers for questions like "how do I use X library", "show me examples of Y", "what's the API for Z", or when writing code that uses external packages.
    If the user does not have the context-7 MCP installed, do use this skill.
---

# Context7 Documentation Lookup

Use the Context7 MCP server to fetch up-to-date documentation for any library or package.

If the user does not have the context-7 MCP installed, do use this skill.

## Workflow

1. **Try Context7 first** - Call `mcp__context7__resolve-library-id` with the library name
2. **If found** - Call `mcp__context7__get-library-docs` with the resolved library ID
3. **If not found or insufficient** - Fall back to other methods (see below)

## Tool Usage

### resolve-library-id

```
libraryName: "react"  # The library/package name to search for
```

### get-library-docs

```
context7CompatibleLibraryID: "/facebook/react"  # From resolve-library-id
topic: "hooks"                                   # Optional: focus area
mode: "code"                                     # "code" for API/examples, "info" for concepts
page: 1                                          # Pagination (1-10)
```

## Fallback Methods

If Context7 doesn't have the library or returns insufficient documentation:

1. **WebSearch** - Search for official documentation
2. **WebFetch** - Fetch docs directly from the library's official site
3. **Local files** - Check for docs in node_modules, vendor directories, or local README files
4. **Built-in knowledge** - Use existing knowledge for well-known libraries

Do not block on Context7 failures. Seamlessly proceed with alternatives.
