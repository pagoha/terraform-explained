# 8-4 Capstone: Terraform CI/CD

## Overview

This phase demonstrates **advanced Terraform automation** using CI/CD pipelines.
We explore three progressively complex examples that combine:

* Modules
* Workspaces
* Optional AWS features (IAM, CloudWatch, Lambda)
* Slack notifications
* Safe multi-environment deployment

This is **self-contained**: all definitions, commands, and setup instructions are included.
External tools like Git, GitHub, Terraform CLI, AWS CLI, and Slack are referenced with links where relevant.

---

## Prerequisites

* Terraform CLI >= 1.6 ([download](https://developer.hashicorp.com/terraform/downloads))
* AWS CLI >= 2 ([download](https://aws.amazon.com/cli/))
* Git ([download](https://git-scm.com/downloads))
* GitHub account with a repository
* Optional: Slack workspace for notifications

Verify installations:

```
terraform version
aws --version
git --version
```

---

## Example 1: Basic GitHub Actions Pipeline (Single Module, Multi-Workspace)

**Goal:** Deploy a single S3 bucket module to multiple workspaces (dev/prod) automatically on push to GitHub.

### Step 1: Repository Setup

```
git init terraform-capstone
cd terraform-capstone
git branch -M main
```

Folder structure:

```
terraform-capstone/
├─ modules/
│  └─ s3_bucket/
│     ├─ main.tf
│     ├─ variables.tf
│     └─ outputs.tf
├─ main.tf
└─ .github/
   └─ workflows/
      └─ terraform.yml
```

**Notes:**

* `modules/s3_bucket` reuses your Phase 4 module.
* Workspaces (`dev`, `prod`) allow environment separation.

---

### Step 2: Terraform Module (S3 Bucket)

`modules/s3_bucket/variables.tf`:

```
variable "bucket_name" { type = string }
variable "versioning" { type = bool, default = true }
```

`modules/s3_bucket/main.tf`:

```
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name

  versioning {
    enabled = var.versioning
  }
}
```

`modules/s3_bucket/outputs.tf`:

```
output "bucket_arn" {
  value = aws_s3_bucket.this.arn
}
```

---

### Step 3: Root Module

`main.tf`:

```
module "example_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "capstone-${terraform.workspace}-bucket"
}

output "s3_bucket_arn" {
  value = module.example_bucket.bucket_arn
}
```

---

### Step 4: GitHub Actions Workflow

`.github/workflows/terraform.yml`:

```
name: Terraform CI/CD

on:
  push:
    branches:
      - main

jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
        with:
          terraform_version: 1.6.0

      - name: Terraform Init
        run: terraform init

      - name: Select Workspace
        run: |
          terraform workspace new dev || true
          terraform workspace select dev

      - name: Terraform Plan
        run: terraform plan

      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve
```

**Notes:**

* Workspace `dev` created automatically; modify for `prod` similarly.
* `if: github.ref` ensures only main branch triggers applies.

---

### Step 5: Expected Output

* Dev workspace bucket deployed
* `terraform state list` shows S3 bucket under module
* Safe separation of dev/prod environments

---

## Example 2: Multi-Module Deployment with Slack Notifications

**Goal:** Deploy multiple modules (S3, EC2, SG) with Slack notifications on plan/apply.

### Step 1: Modules

Reuse `s3_bucket`, add `ec2_instance` and `security_group` modules (Phase 4).

`modules/ec2_instance/main.tf`:

```
resource "aws_instance" "this" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  vpc_security_group_ids = var.security_group_ids
  tags = { Name = "CI_CD_EC2" }
}
```

`modules/ec2_instance/variables.tf`:

```
variable "security_group_ids" { type = list(string) }
```

`modules/security_group/main.tf`:

```
resource "aws_security_group" "this" {
  name        = var.name
  description = "Managed by Terraform"
  ingress { from_port = 22; to_port = 22; protocol = "tcp"; cidr_blocks = ["0.0.0.0/0"] }
  egress  { from_port = 0; to_port = 0; protocol = "-1"; cidr_blocks = ["0.0.0.0/0"] }
}
```

`modules/security_group/variables.tf`:

```
variable "name" { type = string }
```

---

### Step 2: Root Module

`main.tf`:

```
module "app_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "capstone-${terraform.workspace}-bucket"
}

module "app_sg" {
  source = "./modules/security_group"
  name   = "capstone-sg-${terraform.workspace}"
}

module "app_ec2" {
  source             = "./modules/ec2_instance"
  security_group_ids = [module.app_sg.this.id]
  depends_on         = [module.app_bucket]
}
```

---

### Step 3: Slack Notification Setup

1. Create a Slack Incoming Webhook ([guide](https://api.slack.com/messaging/webhooks))
2. Store webhook in GitHub Actions secret `SLACK_WEBHOOK_URL`

Workflow snippet:

```
- name: Notify Slack
  run: |
    curl -X POST -H 'Content-type: application/json' \
    --data '{"text":"Terraform apply completed successfully for $GITHUB_REF"}' \
    ${{ secrets.SLACK_WEBHOOK_URL }}
```

**Notes:** Slack notification runs after apply to inform the team of changes.

---

### Step 4: Commands

```
terraform workspace new dev || true
terraform workspace select dev
terraform init
terraform plan
terraform apply
```

---

### Step 5: Expected Output

* Dev environment: S3, SG, EC2 deployed
* Slack notification posted
* Safe separation per workspace

---

### Diagram: Multi-Module CI/CD

```
GitHub Actions
       |
       v
[Checkout & Init Terraform]
       |
       v
[Workspace: dev] --> [Module: S3 Bucket]
       |                   |
       |                   v
       |              [AWS S3 Bucket]
       |
       v
[Module: Security Group] --> [AWS SG]
       |
       v
[Module: EC2 Instance] --> [AWS EC2]
       |
       v
[Slack Notification]
```

---

## Example 3: Optional AWS Features (IAM, CloudWatch, Lambda)

**Goal:** Build optional enhancements without breaking main architecture.

### Step 1: IAM Role for EC2

```
resource "aws_iam_role" "ec2_role" {
  name = "capstone-ec2-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [{
      Effect = "Allow",
      Principal = { Service = "ec2.amazonaws.com" },
      Action = "sts:AssumeRole"
    }]
  })
}
```

### Step 2: CloudWatch Alarm

```
resource "aws_cloudwatch_metric_alarm" "cpu_high" {
  alarm_name          = "CPUHigh"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "CPUUtilization"
  namespace           = "AWS/EC2"
  period              = 300
  statistic           = "Average"
  threshold           = 70
}
```

### Step 3: Lambda Automation

```
resource "aws_lambda_function" "cleanup" {
  filename      = "lambda.zip"
  function_name = "capstone-cleanup"
  handler       = "index.handler"
  runtime       = "nodejs18.x"
  role          = aws_iam_role.ec2_role.arn
}
```

**Notes:** Optional features can be toggled using variables or separate modules to keep core infrastructure stable.

---

### Step 4: Commands

```
terraform init
terraform plan
terraform apply
terraform output
```

---

### Step 5: Expected Output

* IAM role attached to EC2
* CloudWatch alarms deployed
* Lambda automation available
* Outputs verify resource creation

---

## Insights & Best Practices

* **Why this phase exists:** Combine all learned skills into advanced, automated deployments.
* **Key points:**

  * Modules + Workspaces + Remote State + CI/CD
  * Notifications inform team
  * Optional features are modular and parameterized
* **Common mistakes / pitfalls:**

  * Forgetting workspace selection
  * Overwriting state in remote backend
  * Missing dependencies between modules
* **Reflection / next steps:** Extend CI/CD to multiple accounts, multi-region deployments, policy-as-code, Terraform Cloud/Enterprise.

---

## References

* [Terraform CLI](https://developer.hashicorp.com/terraform/downloads)
* [AWS CLI](https://aws.amazon.com/cli/)
* [GitHub Actions](https://docs.github.com/en/actions)
* [Slack Incoming Webhooks](https://api.slack.com/messaging/webhooks)
* [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
