# AFT: Technical Mission Briefing

## The Objective

**AWS Account Factory for Terraform (AFT)** automates AWS account provisioning through Control Tower.

Replace manual ticket-ops with a **GitOps** workflow: commit HCL, trigger the pipeline, receive a fully hardened, compliant account.

---

## Why This Matters

* **Standardised Delivery:** No more "snowflake" accounts; every VPC and IAM role is identical by design
* **Rapid Scaling:** Provision ten project accounts as easily as one
* **Immutable Audit Trail:** Every change documented in Git and DynamoDB
* **Engineer Autonomy:** Teams request accounts via Pull Request

---

## Control Tower: The Foundation

AWS Control Tower governs multi-account environments. Enable it once before deploying AFT:

1. Your existing AWS account becomes the **Management Account**
2. Control Tower **automatically creates** two accounts:
   - **Log Archive** — centralised logging
   - **Audit** — security and compliance

**You provide:** Email addresses for each account
**Control Tower handles:** Account creation, baseline policies, OU configuration

---

## The Three-Account Architecture

![Three-account architecture](assets/three-account-architecture.png)

**Management:** AFT stack and orchestration  
**Log Archive:** CloudTrail and API logs  
**Audit:** GuardDuty and Security Hub

---

## The Four-Phase Journey

![Four-phase journey](assets/four-phase-journey.png)

**Phase 1:** Enable Control Tower (creates Log Archive + Audit accounts)  
**Phase 2:** Create four Git repositories  
**Phase 3:** Deploy AFT infrastructure in Management account  
**Phase 4:** Provision accounts via Git commits (ongoing)
---

## The Four Mandatory Repositories

AFT requires these four Git repositories (can be empty initially):

1. **aft-account-request** — entry point for new account HCL files
2. **aft-global-customisations** — resources applied to all accounts
3. **aft-account-customisations** — account-specific configurations
4. **aft-account-provisioning-customisations** — pre-baseline setup

