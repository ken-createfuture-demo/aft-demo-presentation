# AFT Deployment Architecture

## Deploying the AFT Stack

In the Management Account, AFT provisions:

**Request Framework** - EventBridge, Lambda validators, DynamoDB  
**Provisioning Framework** - Step Functions, Service Catalog, IAM roles  
**Customisation Framework** - CodePipeline, CodeBuild, S3 state

---

## Where AFT Operates

![AFT operates in Management account](assets/account-types.png)

AFT runs in the Management account and uses cross-account IAM roles to provision target accounts.

---

## The Automated Workflow

![Automated workflow](assets/automated-workflow.png)

---

## How It Works

**Request** - Engineer commits HCL → EventBridge → Lambda validates

**Provision** - Step Functions → Service Catalog creates account → Control Tower baseline

**Customise** - CodePipeline → Terraform applies configs → Account ready

Multiple accounts can provision concurrently.
