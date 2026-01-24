# What We Built

## The Setup

Built complete AFT implementation with:
- Global customisations for security
- Approval gates everywhere
- Full audit trail

---

## Global Customisations

Applied to all accounts:

**Security:**
- GuardDuty (threat detection)
- Security Hub (compliance checks)
- CloudWatch logs (centralised)

**Compliance:**
- IAM password policy
- CloudTrail configuration
- Standard tagging

**Monitoring:**
- CloudWatch alarms (root login alerts)
- SNS notifications
- Centralised logging

---

## Pipeline in Action

![Global Customisations Pipeline](./assets/Screenshot_2025-10-01_at_11.29.19-bee0b708-b466-4122-98e0-c4fef181e3e0.png)

**Flow:** Source → Plan → **Approval** → Apply

Manual approval before anything changes.

---

## Account Pipeline Example

![Account Customisations](./assets/Screenshot_2025-10-01_at_11.28.50-4254ce05-880c-46d7-9046-3c2691ae2d46.png)

Multiple accounts, each with own pipeline.

**Status:**
- ✓ Source done
- ✓ Plan done  
- ⏸️ Waiting for approval
- ⏳ Apply pending

---

## Multiple Accounts Running

![Pipeline List](./assets/Screenshot_2025-09-25_at_15.46.08-b5606b6d-1e69-4729-a4f3-6416c87c63d4.png)

All accounts get provisioned in parallel.

---

## Successful Execution

![Success](./assets/Screenshot_2025-09-29_at_10.32.36-4e999e06-a17d-432e-82d1-daa395e490d4.png)

**Complete flow:**
- Source ✓
- Plan ✓
- Approval ✓
- Global customisations ✓
- Account customisations ✓

**Time:** ~10 minutes total

---

## Cost Reality

![Route 53 Costs](./assets/Screenshot_2025-09-25_at_15.46.29-78682f1b-e121-4b74-b432-5de11db13d31.png)

**Route 53:** $1.02 over 2 months ($0.02/day)

![Total Costs](./assets/Screenshot_2025-09-25_at_15.47.30-32d6c247-06a4-4c19-b838-c189f7a80985.png)

**Total:** $52.45 over 2 months ($0.86/day)

Spikes = provisioning events

---

## What Changed

**Before:**
- Days of manual work
- Different setup each time
- No approval process
- No audit trail

**After:**
- 30-60 minutes automated
- Exact same setup every time
- Approval gates enforced
- Complete audit in DynamoDB
