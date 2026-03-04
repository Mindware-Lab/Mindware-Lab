# GitHub Actions Workflows

Planned workflows:
- CI checks for pull requests
- scheduled Zotero sync
- scheduled OSF metadata sync
- scheduled research scout runs
- nightly embedding refresh

Safety defaults:
- scheduled jobs run in read/sync mode by default
- publishing or write-back actions require manual workflow dispatch and approval
- write operations should open pull requests when possible