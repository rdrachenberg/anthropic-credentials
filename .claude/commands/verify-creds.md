---
description: Audit index.html for credential data drift before deploying
allowed-tools: Read, Grep, Bash(grep:*), Bash(git status:*)
---

## Current state

Entries in `window.CERTS`:
!`grep -c 'course:"' index.html`

Prerendered verify lines in the static fallback markup:
!`grep -o 'class="line verify-line' index.html | wc -l`

Prerendered cert cards:
!`grep -o 'class="cert shown"' index.html | wc -l`

Verify-line indices as written in the static markup:
!`grep -o '\[[0-9]*/[0-9]*\]' index.html | tr '\n' ' '`

Hardcoded count badge and count line:
!`grep -o 'id="countBadge">[0-9]*\|>[0-9]* credentials found' index.html`

Working tree:
!`git status --short`

## Checks

Using the output above and the `window.CERTS` array in `index.html`, verify:

1. **Counts agree.** The number of entries in `window.CERTS`, the number of
   prerendered verify lines, and the number of prerendered cert cards should all
   match, and both hardcoded counts should equal that number.
2. **Indices are coherent.** Every `[n/total]` in the static markup should use the
   same `total`, and `n` should run 1..total with no gaps or repeats.
3. **URLs match IDs.** For each entry, `url` should end with exactly the value of
   `id`. Flag any mismatch — a wrong ID means the verification link 404s, which is
   the one failure that makes the whole page pointless.
4. **No duplicate IDs or duplicate course names.**
5. **Accents are distinct.** Flag any two entries sharing the same accent hex.

## Output

List only what is wrong, one line each, most severe first. If everything passes, say
so in one line and nothing more. Do not fix anything unless I ask — this command is
read-only by design.

Note that the prerendered markup is only a no-JS fallback, so drift there is cosmetic
rather than user-facing. Say so when you report it, and rank it below any URL or ID
problem.
