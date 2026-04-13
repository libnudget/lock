# lock

Reusable GitHub Action for locking merged pull requests after a configurable delay.

## Usage

```yaml
name: Lock Merged PRs

on:
  pull_request:
    types: [closed]
  workflow_dispatch:

permissions:
  pull-requests: write
  contents: write

jobs:
  lock-merged:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - uses: libnudget/lock@v1
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Name | Required | Default | Notes |
|------|----------|---------|-------|
| `token` | yes | | GitHub token with PR write access |
| `days-before-lock` | no | 0 | Days after merge before locking |
| `lock-reason` | no | `resolved` | Reason for locking (resolved, off-topic, duplicated, spam) |
| `delete-branch` | no | `true` | Delete the branch after merging |

## What it does

- Triggers when a PR is merged
- Waits for the configured delay (default 1 day)
- Locks the PR with the specified reason
- Optionally deletes the merged branch

## Notes

- Uses `workflow_dispatch` for manual triggering
- Requires `pull-requests: write` and `contents: write` permissions (write needed for branch deletion)

## License

MIT
