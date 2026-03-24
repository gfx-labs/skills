# GitHub MCP Rules

## Primary Directive

Always prefer the GitHub MCP tools over local git commands, filesystem operations, curl/wget, or web fetching when interacting with GitHub repositories. Never use `curl`, `wget`, the WebFetch tool, or raw API calls to access GitHub content — the GitHub MCP provides typed, authenticated access to all of it.

## Reading Code

- Use `get_file_contents` to read files from repositories instead of cloning and reading locally.
- Use `search_code` to find code across repositories instead of local grep or ripgrep.
- Use `get_commit` to inspect commit details and diffs instead of `git log` or `git show`.
- Use `list_commits` to browse commit history instead of `git log`.
- Use `get_file_contents` with a `ref` parameter to read files at specific branches, tags, or commits.

## Pull Requests

- Use `pull_request_read` with the appropriate method (`get`, `get_diff`, `get_files`, `get_review_comments`, `get_reviews`, `get_comments`, `get_check_runs`, `get_status`) to inspect PRs.
- Use `list_pull_requests` to browse PRs. If filtering by author, use `search_pull_requests` instead.
- Use `create_pull_request` to open new PRs.
- Use `update_pull_request` to modify existing PRs.
- Use `pull_request_review_write` to create, submit, or delete reviews.
- Use `add_comment_to_pending_review` for inline review comments on specific lines.
- Use `add_reply_to_pull_request_comment` to reply to existing review threads.
- Use `request_copilot_review` for automated review before requesting human reviewers.

## Issues

- Use `issue_read` to get issue details, comments, sub-issues, and labels.
- Use `issue_write` to create or update issues.
- Use `list_issues` or `search_issues` to find issues.
- Use `add_issue_comment` to comment on issues or PRs.
- Use `sub_issue_write` to manage sub-issue relationships.

## Repository Operations

- Use `search_repositories` to discover repositories.
- Use `list_branches`, `list_tags`, `list_releases` to explore repository structure.
- Use `create_branch` to create branches remotely.
- Use `create_or_update_file` and `push_files` for remote file changes when local edits are not needed.
- Use `delete_file` to remove files remotely.
- Use `fork_repository` and `create_repository` for repo management.

## Never Use These for GitHub Content

Do not use any of the following to read repositories, code, issues, PRs, or any other GitHub-hosted content:

- `curl` or `wget` against `api.github.com` or `raw.githubusercontent.com`
- The WebFetch tool pointed at `github.com` URLs
- `gh api` via Bash (the MCP tools wrap this already)
- Cloning a repo just to read a file

The GitHub MCP tools handle authentication, pagination, and structured responses. Use them.

## When to Fall Back to Local Git

Only use local git commands (`git` via Bash) when:

- You need to make multi-file edits that are easier to do locally.
- You need to run tests, builds, or other local tooling before pushing.
- You are working on the current repository's working tree (staged/unstaged changes, local commits).
- The GitHub MCP tool does not support the operation you need.

For everything else — reading remote code, browsing history, managing PRs/issues, searching across repos — use the GitHub MCP.
