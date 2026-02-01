# GitHub Action: Keep Workflow Alive

GitHub Action to prevent GitHub from [disabling scheduled workflows due to
repository inactivity][1].

[1]: https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration#disabling-and-enabling-workflows

It uses the GitHub API to preemptively re-enable the workflow, thus preventing it from being automatically disabled.

## Usage:

Invoke this action in all scheduled workflows that you need to continue running even if there's no activity in the repo:

```yaml
name: Tests

on:
  schedule:
    - cron: "0 0 * * *"

jobs:
  tests:
    name: Run integration tests
    steps:
      - uses: actions/checkout@v4
      # ... whatever other steps you need to run your tests
  keepalive:
    name: Keep workflow alive
    runs-on: ubuntu-slim
    permissions:
      actions: write
    steps:
      - name: Keep workflow alive
        uses: darktohka/keepalive-workflow@v1
```
