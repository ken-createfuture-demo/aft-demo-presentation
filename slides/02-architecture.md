# AFT Deployment Architecture

## Deploying the AFT Stack

**In the Management Account, AFT provisions:**

* **Request Framework:** EventBridge, Lambda validators, DynamoDB
* **Provisioning Framework:** Step Functions, Service Catalog, IAM roles
* **Customisation Framework:** CodePipeline, CodeBuild, S3 state

---

## Where AFT Operates

![AFT operates in Management account](assets/account-types.png)

AFT runs in the Management account and uses cross-account IAM roles to provision target accounts.

---

## The Automated Workflow

![Automated workflow](assets/automated-workflow.png)

---

## How It Works

**1. Request:** Engineer commits HCL → EventBridge → Lambda validates

**2. Provision:** Step Functions → Service Catalog creates account → Control Tower baseline

**3. Customise:** CodePipeline → Terraform applies configs → Account ready

**Note:** Multiple accounts provision concurrently

**Parallel Processing:** Multiple accounts provision concurrently

---

## Security

**State Isolation:** Dedicated S3 bucket + DynamoDB lock per account  
**Access Model:** Cross-account IAM roles, temporary STS credentials  
**Compliance:** Control Tower guardrails, CloudTrail logs, Security Hub findings