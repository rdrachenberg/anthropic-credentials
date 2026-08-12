---
description: Commit and push index.html to trigger the Vercel deploy
argument-hint: [commit message]
allowed-tools: Read, Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*)
disable-model-invocation: true
---

## Working tree

!`git status --short`

## Staged and unstaged changes

!`git diff --stat HEAD`

## Recent commit messages, for style

!`git log --oneline -8`

## Task

Commit and push the changes above to `main`, which triggers the Vercel deploy.

1. If the working tree is clean, stop and say so. Do not create an empty commit.
2. If any file other than `index.html`, `README.md`, or `favicon.ico` is modified,
   stop and show me what changed before going further.
3. Read the actual diff to `window.CERTS` and confirm it is a well-formed addition or
   edit — no truncated array, no unbalanced braces, no accidentally deleted entries.
   If the diff removes an entry and I did not ask for a removal, stop and ask.
4. Use my commit message if I supplied one: $ARGUMENTS
   Otherwise write one in the style of the recent log above. Name the credential when
   the change adds one, e.g. `Add MCP: Advanced Topics credential`.
5. Stage, commit, and push to `origin main`. Report the commit SHA and the message.

Do not amend, force-push, rebase, or touch any branch other than `main`.
