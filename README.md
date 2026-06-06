# ProdVerdict GitHub Action

Deterministic production contract checks for AI-assisted SaaS — billing vs database access, env var drift, unsafe migrations. PR comments + optional dashboard upload.

**Website:** https://prodverdict.com  
**SDK & examples:** https://github.com/prodv-dev/prodverdict-sdk  
**npm CLI:** https://www.npmjs.com/package/prodverdict

## Usage

```yaml
name: ProdVerdict

on:
  pull_request:

jobs:
  prodverdict:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: prodv-dev/prodverdict-action@v0.5.0
        with:
          config: ./prodverdict.yml
          contract: access
        env:
          STRIPE_SECRET_KEY: ${{ secrets.STRIPE_SECRET_KEY }}
          DATABASE_URL: ${{ secrets.DATABASE_URL }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Paddle + Postgres

```yaml
      - uses: prodv-dev/prodverdict-action@v0.5.0
        with:
          config: ./prodverdict.yml
          contract: access
        env:
          PADDLE_API_KEY: ${{ secrets.PADDLE_API_KEY }}
          PADDLE_ENVIRONMENT: sandbox
          DATABASE_URL: ${{ secrets.DATABASE_URL }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### All contracts in one job

Run separate jobs per contract, or use the CLI in a step: `npx prodverdict check all`.

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `config` | `./prodverdict.yml` | Path to ProdVerdict config |
| `contract` | `access` | `access`, `config`, or `migration` |
| `strict` | `false` | Fail on warn-level findings |
| `slack_webhook_url` | | Optional Slack notify on fail/warn |

## Demo (no credentials)

```bash
npx prodverdict check access --fixtures \
  --config examples/paddle-stripe/prodverdict.yml \
  --fixtures-dir examples/paddle-stripe/scenarios/fail-revenue-leak
```

## License

MIT
