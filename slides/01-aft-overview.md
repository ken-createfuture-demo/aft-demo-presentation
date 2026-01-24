# AFT: Technical Mission Briefing

## The Objective
**AWS Account Factory for Terraform (AFT)** is our dedicated orchestration engine for AWS Control Tower. We are moving from manual "ticket-ops" to a pure **GitOps** workflow: commit HCL, trigger the pipeline, and have a fully hardened, compliant account ready.

---

## Why This Matters
* **Standardised Delivery:** No more "snowflake" accounts; every VPC and IAM role is identical by design
* **Rapid Scaling:** Provision ten project accounts as easily as one
* **Immutable Audit Trail:** Every change documented in Git and DynamoDB
* **Engineer Autonomy:** Teams request accounts via Pull Request

---

## Control Tower: The Foundation

Before deploying AFT, enable AWS Control Tower (one-time setup):

1. Your existing AWS account becomes the **Management Account**
2. Control Tower **automatically creates** two new accounts:
   - **Log Archive** - centralised logging
   - **Audit** - security and compliance

**What you provide:** Email addresses for Log Archive and Audit  
**What Control Tower does:** Creates accounts, applies baseline, configures OUs

---

## The Three-Account Architecture

![Three-account architecture](assets/three-account-architecture.png)

**Management:** AFT stack and orchestration  
**Log Archive:** CloudTrail and API logs  
**Audit:** GuardDuty and Security Hub

---

## The Four-Phase Journey

![The Four-Phase Journey](assets/four-phase-journey.png)

**One-time setup:** Phases 1-3 | **Ongoing:** Phase 4

---

## The Four Mandatory Repositories

AFT requires four Git repositories before deployment:

1. **aft-account-request**: Entry point for new account HCL files
2. **aft-global-customisations**: Resources applied to all accounts
3. **aft-account-customisations**: Account-specific configurations
4. **aft-account-provisioning-customisations**: Pre-baseline configurations

Repositories can be empty initially but must exist before deploying AFT.

---

## Engineer Checklist

**Before deploying AFT:**
* [ ] **Control Tower Landing Zone active**
* [ ] **Three account IDs collected**
* [ ] **Four Git repositories created**
* [ ] **Git integration configured**
* [ ] **AWS IAM Identity Centre active**
* [ ] **Terraform environment ready**

**Once ready, deploy AFT.**