# aws-cost-guard
This project is designed to run as a scheduled GitHub Actions workflow, building and executing the C# CLI using ephemeral AWS credentials via GitHub OIDC.

### Non-goals for v1
- Running locally (no local setup docs)
- Supporting multiple clouds
- Complex anomaly detection models
- Full FinOps platform features (budgets, forecasting, ticketing)
- Tag-based routing and org-wide governance features