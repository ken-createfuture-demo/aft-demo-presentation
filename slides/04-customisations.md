# Customisations

## Three Types

![Three types of customisations](assets/three-types-customisations.png)

**Provisioning Customisations:** Run before Control Tower baseline (one-time setup)  
**Global Customisations:** Applied to ALL accounts after baseline  
**Account Customisations:** Last step, specific accounts only

---

## Global Customisations Example

Applied to every account:

```hcl
# aft-global-customisations/terraform/main.tf

# Enable GuardDuty everywhere
resource "aws_guardduty_detector" "main" {
  enable = true
}

# Enable Security Hub with default standards
resource "aws_securityhub_account" "main" {
  enable_default_standards = true
}

# Centralised CloudWatch logs
resource "aws_cloudwatch_log_group" "central" {
  name              = "/aws/central-logs"
  retention_in_days = 90
}

# SNS topic for alerts
resource "aws_sns_topic" "security_alerts" {
  name = "security-alerts"
}
```

One change here updates all accounts.

---

## Account Customisations Example

Only for specific accounts:

```hcl
# aft-account-customisations/dev-account/terraform/main.tf

# Dev-specific S3 bucket
resource "aws_s3_bucket" "dev_artifacts" {
  bucket = "dev-artifacts-${data.aws_caller_identity.current.account_id}"
  
  tags = {
    Environment = "development"
    Purpose     = "Build artifacts"
  }
}

# Dev IAM role for deployments
resource "aws_iam_role" "dev_deploy" {
  name = "DevDeployRole"
  
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Action = "sts:AssumeRole"
      Principal = {
        Service = "codepipeline.amazonaws.com"
      }
      Effect = "Allow"
    }]
  })
}

# Dev VPC with public subnet
resource "aws_vpc" "dev" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  
  tags = {
    Name = "dev-vpc"
  }
}
```

One change here updates only this account.

---

## How Updates Work

![Git commit routing](assets/git-commit-routing.png)

**Global customisations repo:** Triggers pipelines for ALL accounts  
**Account customisations repo:** Triggers pipeline for that specific account only

Each pipeline runs: **plan → approve → apply**