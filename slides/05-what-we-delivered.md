# What We Delivered

## What We Delivered at Evoke

- **Control Tower Landing Zone** — fully configured
- **AFT Framework** — deployed in Management account
- **Four Git repos** — connected and operational
- **Pipeline Approval Gates** — manual approvals on customisations
- **Quota Increment Service** — auto-requests across regions
- **Account Provisioning** — end-to-end automated workflow

---

## Pipeline Approval Gates

Added manual approval stages to AFT pipelines:

- **Global Customisations** — approval before applying to all accounts
- **Account Customisations** — approval before per-account changes
- **Safety net** — prevents unreviewed Terraform from reaching production
- **Audit trail** — approver identity logged per deployment

---

## Quota Increment Service

Built a Lambda to auto-request AWS service quota increases:

- **Multi-region** — targets all required regions in one invocation
- **Idempotent** — skips quotas already at target value
- **Monitoring** — polls request status, sends SNS on approval
- **Example** — Elastic IPs 5 → 20, Security Groups 60 → 200

Runs as a post-provisioning customisation via CodeBuild.

---

## Operational Benefits

- **Provisioning time** — days → under an hour
- **Consistent configs** — no manual setup, no snowflakes
- **Full audit trail** — every change tracked in Git
- **Self-service** — engineers request accounts via PR
