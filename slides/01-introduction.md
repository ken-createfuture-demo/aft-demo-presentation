# Agenda

&nbsp;

**1** &nbsp; Introduction & Control Tower Foundation

**2** &nbsp; The Journey — Zero to Deployed AFT

**3** &nbsp; Architecture — How AFT Operates Under the Hood

**4** &nbsp; Demo — Account Provisioning & Customisation

**5** &nbsp; What We Delivered — Outcomes & Cost

**6** &nbsp; Summary & Questions

---

## What is AFT?

**Account Factory for Terraform** — an orchestration layer on top of AWS Control Tower that replaces manual account provisioning with a GitOps workflow.

Engineer commits HCL → pipeline validates & provisions → hardened account lands in the correct OU with security baseline applied.

**Why we adopted it:**

- **Consistency** — every account is identical by design, no snowflakes
- **Speed** — provision ten accounts as easily as one, in parallel
- **Auditability** — full trail in Git history and DynamoDB
- **Self-service** — engineers raise a PR, no tickets required

---

## Control Tower Prerequisite

Control Tower must be active before deploying AFT. One-time setup:

1. Your existing account becomes the **Management Account**
2. Control Tower provisions two accounts automatically:
   - **Log Archive** — centralised CloudTrail and config logs
   - **Audit** — GuardDuty, Security Hub, cross-account read-only access

**You supply:** two unique email addresses
**Control Tower creates:** both accounts, baseline guardrails, OU structure

---

## Three-Account Architecture

![Three-account architecture](assets/three-account-architecture.png)

**Management** — AFT stack, Step Functions, CodePipeline
**Log Archive** — CloudTrail, Config logs, centralised S3
**Audit** — GuardDuty, Security Hub, cross-account audit role
