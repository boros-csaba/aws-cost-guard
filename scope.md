# v1 scope: GitHub Actions–only

## Inputs (how it’s configured)
Configuration sources (only these)
- Repo file: cost-guard.yaml committed
- GitHub Actions:
    vars for non-secrets (e.g. thresholds)
    secrets for webhooks
- CLI flags (optional but minimal) — mainly --config and --date

## Explicitly not supported in v1
- interactive prompts
- multiple config formats
- local profiles / credential setups docs

## Required inputs
- AWS_ROLE_ARN (GitHub secret or variable)
- AWS_REGION (variable)

## Outputs (what it produces)
### Required outputs
- out/report.json
- out/report.md
### Workflow behavior
- Upload both as artifacts
- Print a short summary to logs (so you don’t have to download artifacts to understand)

### Exit codes
- 0 = no anomaly
- 2 = anomaly detected (useful for branching/alerting)
- 1 = error (fail the workflow)

## Detection features (keep it tight but useful)
### What v1 detects
- Daily spend anomalies over a lookback window (default 14 days)
- Baseline: moving average (default 7 days)
- Trigger: both
  - min absolute delta (default $200)
  - min percent delta (default 30%)

### What v1 explains (top contributors)
For any day flagged anomalous:
- Top contributors grouped by:
  - SERVICE
  - LINKED_ACCOUNT (if org/payer setup)
  - REGION
Skip tags for v1.

### What v1 does NOT do
- forecasting
- budget comparisons
- AWS Anomaly Detection integration
- CUR ingestion
- per-team routing
- ticket creation