---
name: update-github-info
description: Keep Mona's GitHub Info content current using official GitHub Blog and Changelog sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - defaults
    - github.blog
    - github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    max: 1
    base-branch: main
    draft: false
    reviewers: [mona]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info for Mona

Read `notes/mona-notes.md` and `site/content/github-info.md` before making changes.

Use the `web-fetch` tool to fetch and review both official sources:
- https://github.blog/latest/
- https://github.blog/changelog/

Identify recent, useful updates that help developers learn GitHub faster and fit Mona's editorial focus. Do not duplicate themes or information already covered in the existing content. Use only facts supported by the fetched pages, keep summaries short and practical, and include a direct source link for every item derived from the GitHub Blog or Changelog. Do not invent dates, features, or claims. If neither source has a relevant update, leave the content unchanged and explain why no pull request is warranted.

Update only `site/content/github-info.md`, preserving its existing structure and voice. Keep the diff focused on the selected update or updates.

When there is a useful, source-backed change, propose it through the configured `create-pull-request` safe output with a concise title and a body summarizing the changes and linking to their sources. Request review from Mona. Never write directly to `main`, push changes to `main`, or merge the pull request.
