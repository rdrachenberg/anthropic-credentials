# Credentials

A terminal-styled page verifying Anthropic course completions.

## Deploy

Connected to Vercel — pushes to `main` deploy automatically.

## Updating

The site is static, so credentials are hard-coded. To add one:

1. Append an entry to the `window.CERTS` array in the `<script id="certsData">` block of `index.html`
   (or run `/add-cred <course name> <skilljar id>` in Claude Code).
2. Commit and push:
   ```
   git add index.html
   git commit -m "Add <course> credential"
   git push
   ```
