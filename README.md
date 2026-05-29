# ProdVerdict GitHub Action

Deterministic production contract checks for AI-assisted SaaS — Stripe vs database access, env var coverage, PR comments.

**Website:** https://prodverdict.com  
**SDK & examples:** https://github.com/prodv-dev/prodverdict-sdk

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

      - uses: prodv-dev/prodverdict-action@v0.1.0
        with:
          config: ./prodverdict.yml
          contract: access
        env:
          STRIPE_SECRET_KEY: ${{ secrets.STRIPE_TEST_KEY }}
          DATABASE_URL: ${{ secrets.DATABASE_URL }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input | Default | Description |
|-------|---------|-------------|
| `config` | `./prodverdict.yml` | Path to ProdVerdict config |
| `contract` | `access` | `access` or `config` |
| `strict` | `false` | Fail on warn-level findings |

## License

MIT
