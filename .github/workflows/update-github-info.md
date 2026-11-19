---
name: update-github-info
description: Review recent GitHub Blog and Changelog updates and propose practical updates to Mona's GitHub Info page.
intent: Keep Mona's GitHub Info page current with concise, practical, officially sourced updates for developers.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
  skip-if-match: 'is:pr is:open in:title "[Mona] GitHub Info update"'
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[Mona] GitHub Info update: "
    branch-prefix: "mona/github-info/"
    draft: false
    if-no-changes: ignore
    allowed-files:
      - "site/content/github-info.md"
  noop:
---

# Update GitHub Info for Mona

1. Read `notes/mona-notes.md` and `site/content/github-info.md` before researching. Follow Mona's editorial notes and preserve the page's existing structure and useful content.
2. Use web-fetch to read all three sources:
   - https://github.blog/latest/
   - https://github.blog/changelog/
   - https://awesome-copilot.github.com/workflows/
3. Consider only specific, recent updates that are useful to developers and not already covered by the page. Verify details and publication dates where available from the fetched official pages; do not infer missing facts or include unsupported claims.
4. If there are meaningful updates, edit only `site/content/github-info.md`. Keep additions short and practical, connect them to the page's existing themes, and cite the relevant source with a link.
5. Open a non-draft pull request for Mona to review using the configured `create-pull-request` safe output. Give it a clear summary and include the source links. Do not write to the default branch directly, use other write mechanisms, or merge the pull request.
6. If none of the sources contains a useful, verified update, the page is already current, or there is otherwise no change to propose, use `noop` with a brief reason.
