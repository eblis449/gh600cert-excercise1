---
name: update-github-info
description: Refresh GitHub information for Mona from the latest GitHub Blog updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  edit: true
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

## Task

Read `notes/mona-notes.md` for Mona's context and fetch these public sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Use GitHub repository API tools to read repository guidance and reference files when needed. Update `site/content/github-info.md` with accurate, relevant GitHub information for Mona.

When a material update is needed, use the configured `create-pull-request` safe output to open a pull request for Mona to review. Do not write directly to the default branch.

If the existing content is already current or no relevant updates are available, use `noop` with a brief explanation.