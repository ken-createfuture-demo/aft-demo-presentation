# The Provisioning Workflow

## What You Actually Write

One Terraform file per account:

```hcl
# aft-account-request/dev-account.tf

module "dev_account" {
  source = "./modules/aft-account-request"
  
  control_tower_parameters = {
    AccountName               = "dev-project-alpha"
    AccountEmail              = "dev-alpha@example.com"
    ManagedOrganizationalUnit = "Development"
    SSOUserEmail              = "admin@example.com"
    SSOUserFirstName          = "Dev"
    SSOUserLastName           = "Admin"
  }
  
  account_tags = {
    Environment = "development"
    Team        = "platform"
  }
}
```

Commit it. AFT handles the rest.

---

## What Happens Automatically

![The complete workflow](assets/automated-workflow-main.png)

**The complete flow:**

**Git commit** - Engineer pushes HCL account request  
**EventBridge detects** - Picks up the commit event  
**Lambda validates** - Checks email, OU, account name  
**Service Catalog provisions** - Creates the AWS account  
**Control Tower baseline** - Applies guardrails and security policies  
**CodePipeline customises** - Runs Terraform configurations  
**Account ready** - SSO access configured, ready for use

---

## Validation Stage

**Email format and uniqueness** - No duplicate emails allowed  
**OU exists and is accessible** - Confirms the organisational unit is valid  
**Account name not already taken** - Ensures unique account names

---

## Provisioning Stage

**Service Catalog creates the AWS account** - New account provisioned in AWS Organizations  
**Control Tower applies baseline guardrails** - Preventive and detective controls enabled  
**Account placed in specified OU** - Moved to correct organisational unit

---

## Customisation Stage

**CodePipeline spawned for this account** - Dedicated pipeline created  
**Global customisations run first** - Security baseline applied to all accounts  
**Account-specific configs applied** - Project-specific resources deployed  
**SSO access configured** - Identity Centre access enabled

---
