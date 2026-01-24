# AFT Implementation - Complete Guide

Walkthrough of deploying AWS Control Tower Account Factory for Terraform (AFT) from scratch.

## Quick Links

- [View Presentation](https://YOUR-USERNAME.github.io/YOUR-REPO/presentation.html)
- [Browse Slides](slides/)

## What This Covers

We'll walk through the complete AFT journey:

1. **Control Tower Setup** - The foundation (creates Log Archive and Audit accounts automatically)
2. **Git Repository Preparation** - Setting up your four repos
3. **AFT Deployment** - Deploying the AFT infrastructure
4. **Account Provisioning** - How to provision accounts via Git
5. **Customisations** - Tailoring accounts to your needs
6. **Real Implementation** - What we actually built and what it cost

## The Four Phases

### Phase 1: Control Tower (60-90 minutes, one-time)

Enable AWS Control Tower in your management account. This automatically creates two new AWS accounts:
- **Log Archive Account** - For centralised CloudTrail logs
- **Audit Account** - For security and compliance tooling

You don't create these manually. Control Tower creates them for you.

**Cost:** ~£10-15/month

### Phase 2: Preparation (15 minutes, one-time)

Create four Git repositories:
- `aft-account-request` - Where you request new accounts
- `aft-global-customisations` - Security baseline (all accounts)
- `aft-account-customisations` - Environment-specific configs
- `aft-account-provisioning-customisations` - Pre-baseline setup

Collect your three account IDs (Management, Log Archive, Audit).

**Cost:** £0

### Phase 3: Deploy AFT (30-45 minutes, one-time)

Deploy the AFT infrastructure in your management account. This creates:
- Lambda functions (validation, processing)
- Step Functions (orchestration)
- EventBridge rules (Git triggers)
- DynamoDB tables (state tracking)
- CodePipeline/CodeBuild (customisations)

**Cost:** ~£3-5/month

### Phase 4: Provision Accounts (30-60 minutes each, ongoing)

Write a simple Terraform file, commit to Git, and AFT provisions the account automatically with all your customisations.

**Cost:** ~£1-2 per account provisioned

## Key Points

- Control Tower creates the Log Archive and Audit accounts **automatically**
- You only provide the email addresses
- Total one-time setup: ~2-3 hours
- Then: 30-60 minutes per account
- Everything version-controlled in Git
- Complete audit trail in DynamoDB
- Security baseline included by default

## Before and After

| | Before AFT | With AFT |
|---|---|---|
| **Time** | Days | 30-60 minutes |
| **Process** | Manual | Automated |
| **Consistency** | Variable | Identical every time |
| **Audit trail** | Maybe | Complete in Git + DynamoDB |
| **Security** | Manual setup | Baseline included |
| **Scale** | Painful | Trivial |

## Cost Breakdown

| Component | Monthly Cost |
|-----------|--------------|
| Control Tower | £10-15 |
| AFT Infrastructure | £3-5 |
| Per Account Provisioned | £1-2 each |
| **Example: 10 accounts** | **£30-35/month** |

## Related Repositories

The actual AFT code referenced in this presentation:

- [AFT Account Requests](LINK-TO-YOUR-AFT-ACCOUNT-REQUEST-REPO)
- [Global Customisations](LINK-TO-YOUR-AFT-GLOBAL-CUSTOMISATIONS-REPO)
- [Account Customisations](LINK-TO-YOUR-AFT-ACCOUNT-CUSTOMISATIONS-REPO)
- [Provisioning Customisations](LINK-TO-YOUR-AFT-PROVISIONING-CUSTOMISATIONS-REPO)

## Presentation Navigation

### Using the HTML Presentation

Open [presentation.html](https://YOUR-USERNAME.github.io/YOUR-REPO/presentation.html) and use:
- Arrow keys to navigate
- `F` for fullscreen
- `Esc` for overview
- `?` for help

### Reading the Slides

Navigate through the markdown slides directly:
- [00 - Prerequisites](slides/01-aft-overview)
- [01 - Introduction](slides/01-introduction.md)
- [02 - Architecture](slides/02-architecture.md)
- [03 - Workflow](slides/03-workflow.md)
- [04 - Customisations](slides/04-customisations.md)
- [05 - Demo](slides/05-demo.md)
- [06 - What We Built](slides/06-work-done.md)

## Common Questions

**Do I need to manually create the Log Archive and Audit accounts?**
No. Control Tower creates these automatically when you enable it. You just provide the email addresses.

**How many AWS accounts will I have after Control Tower setup?**
Three: Your original management account, plus the Log Archive and Audit accounts created by Control Tower.

**Can I use existing accounts for Log Archive or Audit?**
No. Control Tower must create these fresh during setup.

**What if I want to change the Log Archive email address later?**
You can't. It's set during Control Tower setup and can't be changed.

**How long does the complete setup take?**
About 2-3 hours total (one-time). Then 30-60 minutes per account going forward.

**What's the minimum I need to get started?**
An AWS account with admin access, two email addresses for the new accounts, and a decision on which region to use.

## Quick Start

```bash
# 1. Enable Control Tower (AWS Console)
#    Provide two email addresses
#    Wait 60-90 minutes

# 2. Create four Git repositories
#    (Can be empty initially)

# 3. Collect account IDs from AWS Organizations

# 4. Deploy AFT infrastructure
terraform init
terraform apply
# Wait 30-45 minutes

# 5. Start provisioning accounts
#    Write Terraform file → Commit → Done
```

## What We Actually Built

Our implementation includes:
- GuardDuty enabled on all accounts
- Security Hub with default standards
- CloudWatch Logs with 90-day retention
- IAM password policy enforcement
- VPC Flow Logs
- Environment-specific configurations (dev vs staging vs prod)
- Manual approval gates in pipelines
- Complete audit trail

**Total cost:** ~£21/month for base infrastructure + provisioned accounts

## Support

For questions about AFT:
- [AWS Documentation](https://docs.aws.amazon.com/controltower/latest/userguide/aft-overview.html)
- [GitHub Issues](https://github.com/aws-ia/terraform-aws-control_tower_account_factory/issues)

---

**Presented by:** [Your Name]  
**Date:** [Presentation Date]  
**Organisation:** [Your Organisation]
