---
name: update-github-info
description: Keep the GitHub Info page useful with concise, sourced updates from official GitHub news.
intent: Keep Mona's GitHub Info page practically useful with accurate, sourced updates from the official GitHub Blog and Changelog.
model: gpt-6-luna
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` before drafting.
Fetch both https://github.blog/latest/ and https://github.blog/changelog/ and
fetch https://awesome-copilot.github.com/workflows/. Look for recent, verified
information from these sources that would make the page more useful to
developers.

Keep any update short and practical, preserve the page's focus and existing
themes, and cite the exact source article or changelog entry with a link. Do
not add speculative claims, duplicate existing information, or edit any file
other than `site/content/github-info.md`.

If a source cannot be fetched, do not infer its contents; use verified
information from the other source only. If neither source provides a relevant
update, no actual page change is needed, or the evidence is insufficient, use
`noop` with a brief reason. When the page has a worthwhile change, edit it and
open one reviewable pull request for Mona using the configured safe output.
Never write directly to the default branch or create the pull request through
another tool.
