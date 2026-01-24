# How It Works

## Three Main Parts

```mermaid
graph TB
    A[1. Account Request<br/>Write Terraform, commit to Git] --> B[2. Provisioning<br/>AWS creates account automatically]
    B --> C[3. Customisation<br/>Your configs get applied]
    
    style A fill:#e1f5ff
    style B fill:#fff4e1
    style C fill:#e8f5e9
```

**Flow:** Request → Provision → Customise

---

## The Components

```mermaid
graph LR
    A[Git Commit] --> B[EventBridge]
    B --> C[Lambda<br/>Validator]
    C --> D[DynamoDB<br/>Storage]
    C --> E[Step Functions<br/>Orchestrator]
    E --> F[Service Catalog<br/>Account Creation]
    F --> G[CodePipeline<br/>Customisations]
    
    style A fill:#e1f5ff
    style E fill:#fff4e1
    style G fill:#e8f5e9
```

**Request Handler:**
- DynamoDB stores requests
- Lambda validates everything
- EventBridge triggers the workflow

**Provisioning:**
- Step Functions runs the show
- Service Catalog creates account
- Takes about 10 minutes

**Customisation:**
- CodePipeline per account
- Terraform applies your configs
- Takes 20-40 minutes

---

## What Actually Happens

```
You: git commit + push
     ↓
EventBridge: "New request detected"
     ↓
Lambda: "Validating request"
     ↓
DynamoDB: "Details stored"
     ↓
Step Functions: "Starting workflow"
     ↓
AWS: Creates your account
     ↓
Pipelines: Apply your customisations
     ↓
Done: Account ready
```

**Total time: 30-60 minutes**

---

## The Git Repos You Need

Four repos total:

1. **aft-account-request** - Where you request accounts
2. **aft-global-customisations** - Applied to ALL accounts
3. **aft-account-customisations** - Specific account stuff
4. **aft-account-provisioning-customisations** - Pre-setup configs

GitHub, GitLab, or CodeCommit all work.

---

## Security & State

**Terraform state:**
- Lives in S3 (encrypted)
- DynamoDB locks it
- Separate per account

**Security:**
- Everything encrypted
- IAM roles for access
- CloudTrail logs everything
- Control Tower guardrails active
