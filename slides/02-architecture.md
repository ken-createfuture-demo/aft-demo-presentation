# AFT Architecture & Deployment

## Deploying the AFT Stack

**In the Management Account, AFT provisions:**

* **Request Framework:** EventBridge, Lambda validators, DynamoDB
* **Provisioning Framework:** Step Functions, Service Catalog, IAM roles
* **Customisation Framework:** CodePipeline, CodeBuild, S3 state

---

## Where AFT Operates

![AFT operates in Management account](assets/aft-operates.png)

AFT runs in the Management account and uses cross-account IAM roles to provision target accounts.

---

## The Automated Workflow

![Automated workflow](assets/automated-workflow.png)

---

## How It Works

**1. Request**
- Engineer commits HCL to Git
- EventBridge detects commit
- Lambda validates request

**2. Provision**
- Step Functions orchestrate
- Service Catalog creates account
- Control Tower applies baseline

**3. Customise**
- CodePipeline spawned per account
- Terraform applies configurations
- Account ready for use

**Parallel Processing:** Multiple accounts provision concurrently

---

## Security

**State Isolation:** Dedicated S3 bucket + DynamoDB lock per account  
**Access Model:** Cross-account IAM roles, temporary STS credentials  
**Compliance:** Control Tower guardrails, CloudTrail logs, Security Hub findings