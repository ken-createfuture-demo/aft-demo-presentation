# The Journey

## The Four-Phase Journey

![Four-phase journey](assets/four-phase-journey.png)

**Phase 1** - Enable Control Tower (creates Log Archive + Audit)  
**Phase 2** - Create four Git repositories  
**Phase 3** - Deploy AFT in Management account  
**Phase 4** - Provision accounts via Git commits (ongoing)

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
