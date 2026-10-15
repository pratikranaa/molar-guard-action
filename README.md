# Molar Guard action

Runs your Molar Guard scenario on every pull request and posts the result as a GitHub check.

```yaml
name: Molar Guard
on: [pull_request]
permissions:
  contents: read
  checks: write
  pull-requests: write
jobs:
  guard:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pratikranaa/molar-guard-action@v1
        with:
          api-key: ${{ secrets.MOLAR_API_KEY }}
          scenario-id: ${{ vars.MOLAR_SCENARIO_ID }}
          mode: advisory   # or "required" to block the merge on failure
```

Create an API key at https://app.molar.it (Settings → API keys) and save it as the `MOLAR_API_KEY`
repository secret. `molar-guard init` writes this workflow for you. All inputs are documented in
[`action.yml`](action.yml). Source: the Molar monorepo (`molar-guards/apps/action`). MIT licensed.
