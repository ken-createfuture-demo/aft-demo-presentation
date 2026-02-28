# Agenda

**1.** &ensp; Introduction & Control Tower Foundation

**2.** &ensp; The Journey — Zero to Deployed AFT

**3.** &ensp; Architecture — How AFT Works

**4.** &ensp; Demo — Account Provisioning

**5.** &ensp; What We Delivered — Outcomes & Cost

**6.** &ensp; Summary & Questions

---

## What is AFT?

**Account Factory for Terraform**<br>GitOps-driven account provisioning on Control Tower.

Commit HCL → pipeline runs → account ready.

- **Consistency** — no snowflake accounts
- **Speed** — parallel provisioning
- **Auditability** — tracked in Git + DynamoDB
- **Self-service** — PR-based, no tickets

---

## Control Tower Prerequisite

Control Tower must be active before deploying AFT.

1. Your existing account becomes **Management**
2. Control Tower auto-creates two accounts:
   - **Log Archive** — CloudTrail and config logs
   - **Audit** — GuardDuty, Security Hub

**You supply:** two emails (Log Archive + Audit)<br>
**Control Tower creates:** accounts, guardrails, OU structure

---

![Three-account architecture](assets/three-account-architecture.svg)
