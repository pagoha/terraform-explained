# 6-1 Introduction to Remote State

## Overview
Learn why remote state is critical for team collaboration, safe deployments, and consistent Terraform management across multiple users.

## Code Example
Configure an S3 backend with a DynamoDB table for state locking:

terraform {
  backend "s3" {
    bucket         = "terraform-demo-remote-state"
    key            = "global/s3/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-lock"
    encrypt        = true
  }
}

Commands:

terraform init
terraform plan
terraform apply
terraform state list
terraform destroy

## Expected Output
- Terraform state is stored in the specified S3 bucket
- DynamoDB table enforces locking during operations to prevent conflicts
- State file is encrypted and shared for safe multi-user collaboration

## Insights
- **Why this demo exists:** Centralizes Terraform state to avoid local-only limitations and enable team collaboration
- **Key points:**
  - `dynamodb_table` prevents simultaneous conflicting changes
  - `key` defines the path of the state file in the S3 bucket
  - `encrypt = true` ensures the state file is stored securely
- **Common mistakes / pitfalls:**
  - Forgetting to run `terraform init` after configuring the backend
  - Using the same `key` for multiple environments without isolation
  - Not enabling encryption for sensitive infrastructure
- **Reflection / next steps:** Combine with workspaces to manage multiple environments and separate state files safely
