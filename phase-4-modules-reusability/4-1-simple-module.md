# 4-1 Simple Module

## Overview

Learn how to create a **simple reusable module** for S3 buckets so it can be used across multiple environments or projects.

## Code Example

**Folder structure:**

    terraform-explained/
    ├─ modules/
    │  └─ s3_bucket/
    │     ├─ main.tf
    │     ├─ variables.tf
    │     └─ outputs.tf
    └─ main.tf

**Module variables (`modules/s3_bucket/variables.tf`):**

    variable "bucket_name" {
      description = "Name of the S3 bucket"
      type        = string
    }

    variable "acl" {
      description = "ACL for the bucket"
      type        = string
      default     = "private"
    }

**Module resource (`modules/s3_bucket/main.tf`):**

    resource "aws_s3_bucket" "this" {
      bucket = var.bucket_name
      acl    = var.acl
    }

**Module outputs (`modules/s3_bucket/outputs.tf`):**

    output "bucket_id" {
      value = aws_s3_bucket.this.id
    }

**Root configuration (`main.tf`):**

    module "example_bucket" {
      source      = "./modules/s3_bucket"
      bucket_name = "terraform-demo-module-001"
    }

**Terraform commands:**

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* S3 bucket created via the module
* `terraform state list` shows the module and its resource:
  - `module.example_bucket.aws_s3_bucket.this`
* `terraform destroy` removes the bucket safely

## Insights

* **Why this demo exists:** Demonstrates **modularization** to reuse Terraform code.
* **Key points:** Modules help organize infrastructure code, isolate functionality, and simplify larger deployments.
* **Common mistakes / pitfalls:** Incorrect `source` path; forgetting to pass required variables; name collisions.
* **Reflection / next steps:** Create additional modules for EC2, Security Groups, and other AWS resources for full modularized architecture.
