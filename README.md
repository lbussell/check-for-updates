# check-for-updates action

GitHub Action that checks https://endoflife.date and automatically opens issues
when new software versions are released.

## Features

- 🔍 Checks for new software releases using the endoflife.date API
- 🎫 Automatically creates GitHub issues for new releases

## Usage

```yaml
name: Check for Updates

on:
  schedule:
    - cron: '0 9 * * *'  # Daily at 9 AM UTC
  workflow_dispatch:

permissions:
  contents: read
  issues: write

jobs:
  check-updates:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@...

      - name: Check for Ubuntu updates
        uses: lbussell/check-for-updates@...
        with:
          # https://endoflife.date product ID
          product: ubuntu
          # (optional) Comma-separated list of labels that will be added to the issue
          # labels: 'your-label-here'
          # (optional) GitHub token for creating issues. Uses ${{ github.token }} if not set.
          # token: '...'
```

### Outputs

| Output | Description |
|--------|-------------|
| `new-version` | The new version if one was found, empty string otherwise |
| `issue-number` | The issue number created if a new version was found, empty string otherwise |

### Available Products

The action uses the [endoflife.date](https://endoflife.date) API. You can check
any product available in [`api/v1/products`](https://endoflife.date/api/v1/products).
