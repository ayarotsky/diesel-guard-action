# diesel-guard-action

GitHub Action for [diesel-guard](https://github.com/ayarotsky/diesel-guard) — a Postgres migration safety linter that catches dangerous patterns before they cause downtime.

No database connection required. Works with [Diesel](https://diesel.rs/) and [SQLx](https://github.com/launchbadge/sqlx) migration frameworks.

## Usage

```yaml
- uses: ayarotsky/diesel-guard-action@v1
```

Add a `diesel-guard.toml` to your repo root to configure the framework:

```toml
framework = "diesel"  # or "sqlx"
```

## Inputs

| Input  | Description                                          | Required | Default       |
|--------|------------------------------------------------------|----------|---------------|
| `path` | Path to migrations directory or a single `.sql` file | No       | `migrations/` |

## Examples

**Basic — check the default migrations directory:**

```yaml
steps:
  - uses: actions/checkout@v6
  - uses: ayarotsky/diesel-guard-action@v1
```

**Custom path:**

```yaml
steps:
  - uses: actions/checkout@v6
  - uses: ayarotsky/diesel-guard-action@v1
    with:
      path: db/migrate/
```


## Configuration

diesel-guard reads `diesel-guard.toml` from the working directory. Example:

```toml
framework = "diesel"

# Skip migrations created before this timestamp
# start_after = "20240101000000"

# Disable specific checks
# disable_checks = ["AddColumnCheck"]

# Target Postgres version (skips version-specific checks)
# postgres_version = 16
```

Run `diesel-guard init` locally to generate a fully documented config file.
