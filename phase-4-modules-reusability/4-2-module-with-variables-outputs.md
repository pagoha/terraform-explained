# 4-2 Module with Variables & Outputs

## Overview

Learn how to use **variables and outputs inside modules** to create dynamic, reusable Terraform code.

## Code Example

**Module variables (`modules/s3_bucket/variables.tf`):**

    variable "bucket_name" {
      description = "Name of the S3 bucket"
      type        = string
    }

    variable "versioning" {
      description = "Enable versioning on the bucket"
      type        = bool
      default     = true
    }

**Module resource (`modules/s3_bucket/main.tf`):**

    resource "aws_s3_bucket" "this" {
      bucket = var.bucket_name

      versioning {
        enabled = var.versioning
      }
    }

**Module outputs (`modules/s3_bucket/outputs.tf`):**

    output "bucket_arn" {
      description = "The ARN of the S3 bucket"
      value       = aws_s3_bucket.this.arn
    }

**Root configuration (`main.tf`):**

    module "example_bucket" {
      source      = "./modules/s3_bucket"
      bucket_name = "terraform-demo-module-002"
      versioning  = true
    }

    output "s3_bucket_arn" {
      description = "Expose the ARN from the module"
      value       = module.example_bucket.bucket_arn
    }

**Terraform commands:**

    terraform init
    terraform plan
    terraform apply
    terraform output
    terraform destroy

## Expected Output

* Module creates **versioned S3 bucket**
* `terraform output` displays the bucket ARN
* `terraform state list` shows:
  - `module.example_bucket.aws_s3_bucket.this`
* `terraform destroy` removes the bucket safely

## Insights

* **Why this demo exists:** Demonstrates passing **variables into modules** and exposing **outputs** back to the root module.
* **Key points:** Outputs allow modules to communicate with the root module or other modules.
* **Common mistakes / pitfalls:** Forgetting to define outputs; mismatched variable types; not passing required variables.
* **Reflection / next steps:** Combine multiple modules to build a complete environment with reusable components.
