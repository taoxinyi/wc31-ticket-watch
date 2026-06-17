# WC31 Ticket Watch: GitHub Actions

Fast 5-minute GitHub Actions monitor for match #31, Turkiye vs Paraguay.

The workflow is intentionally optimized for runtime:

- public repository
- standard `ubuntu-latest` runner
- no checkout step
- no setup-node step
- no npm install
- inline Node.js using built-in `fetch`
- job timeout: 1 minute
- fetch timeout: 12 seconds
- Discord timeout: 8 seconds

## Schedule

The workflow runs every 5 minutes:

```yaml
cron: "2/5 * * * *"
```

GitHub's shortest scheduled interval is 5 minutes. Scheduled runs can be delayed
or dropped under high load, so this is best-effort monitoring rather than a hard
real-time guarantee.

## Alerts

By default, it reports every run in the workflow summary and sends Discord only
when at least one 2-seat non-wheelchair adjacent pair is under `$450`.

To enable Discord, add a repository secret:

```text
DISCORD_WEBHOOK_URL
```

## Billing/limits notes

This repo should stay public. GitHub says standard GitHub-hosted runners are free
in public repositories. In private repositories, GitHub Free includes 2,000
Actions minutes per month, and exceeding included amounts can bill unless budgets
stop usage.

At 5-minute cadence there are about 288 runs per day. In a private repo, even a
very fast job can be accounted against the monthly allowance, so public is the
safer free setup.
