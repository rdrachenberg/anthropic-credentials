---
description: Add an Anthropic course credential to index.html
argument-hint: <course name> <verification-id> [#accent]
allowed-tools: Read, Edit
---

Add a new credential to `index.html` in this repo.

Input: $ARGUMENTS

Parse it as follows:
- The last token beginning with `#` is the accent hex colour. If absent, pick one
  yourself that is visually distinct from every accent already in the array and
  legible against the `--panel` background (`#10151C`).
- The last remaining token is the Skilljar verification ID (lowercase alphanumeric,
  typically 12 characters).
- Everything before that is the course name. Do not re-case or abbreviate it — use
  it exactly as given, since it must match the certificate.

Then:

1. Read `index.html` and locate the `<script id="certsData">` block containing
   `window.CERTS`.
2. Append one entry to the end of that array, matching the existing formatting
   exactly — two-space indent, the same key order (`course`, `id`, `accent`, `url`),
   and the line break before `url:`. Build the URL as
   `https://verify.skilljar.com/c/<id>`.
3. Do not touch anything else. `renderAll()` regenerates the verify lines, the cert
   cards, and the count badge from this array at load time, so the prerendered
   markup further up the file does not need editing.
4. Before finishing, confirm the ID does not already appear anywhere in the file. If
   it does, stop and tell me rather than adding a duplicate.

Report back with just the entry you added and the new total count.
