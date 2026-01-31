# Table of Contents

**1. Introduction**  
What is AFT and why we're using it

**2. The Journey**  
From zero to deployed AFT

**3. Architecture**  
How AFT works under the hood

**4. The Demo**  
Our actual implementation walkthrough

**5. Customisations**  
Tailoring accounts to project needs

**6. What We Delivered**  
Concrete outcomes and business value

**7. Summary & Questions**

---

## The Objective

**AWS Account Factory for Terraform (AFT)** automates AWS account provisioning through Control Tower.

We're moving from manual ticket-based account requests to **GitOps**: commit HCL, pipeline runs, account ready. Simple as that.

---

## Why This Matters

**Standardised delivery** - No more one-off account configurations  
**Rapid scaling** - Provision ten accounts as easily as one  
**Audit trail** - Every change tracked in Git  
**Engineer autonomy** - Teams request accounts via Pull Request

---

## Control Tower: The Foundation

AWS Control Tower is a managed service for multi-account governance.

**Before deploying AFT, enable Control Tower (one-time setup):**

Your existing AWS account becomes the **Management Account**. Control Tower then automatically creates two additional accounts:
- **Log Archive** - Centralised logging
- **Audit** - Security and compliance monitoring

You provide the email addresses, Control Tower handles the rest.

---

## The Three-Account Architecture

![Three-account architecture](assets/three-account-architecture.png)

**Management Account:** Where AFT infrastructure runs  
**Log Archive:** CloudTrail and API logs  
**Audit Account:** GuardDuty and Security Hub

---

## The Four-Phase Journey

![Four-phase journey](assets/four-phase-journey.png)

**Phase 1:** Enable Control Tower (creates Log Archive + Audit)  
**Phase 2:** Create four Git repositories  
**Phase 3:** Deploy AFT in Management account  
**Phase 4:** Provision accounts via Git commits (ongoing)

---

## The Four Mandatory Repositories

AFT requires four Git repositories before deployment:

**aft-account-request** - Entry point for new account HCL files  
**aft-global-customisations** - Resources applied to all accounts  
**aft-account-customisations** - Account-specific configurations  
**aft-account-provisioning-customisations** - Pre-baseline configurations

Repositories can be empty initially but must exist.

---

## Engineer Checklist

Before deploying AFT, make sure you have:

- Control Tower Landing Zone active
- Three account IDs collected (Management, Log Archive, Audit)
- Four Git repositories created
- Git integration configured (GitHub/GitLab/CodeCommit)
- AWS IAM Identity Centre active
- Terraform environment ready

Once these are sorted, you're ready to deploy.

---

## What's Next

Now that you understand the foundation, we'll cover:

**Architecture** - How AFT operates in the Management account  
**Workflow** - The automated journey from commit to ready account  
**Customisations** - How to tailor accounts to project requirements  
**Demo** - Walkthrough of our actual implementation
