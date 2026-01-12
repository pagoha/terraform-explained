# 6-2 Remote Backend with Workspaces

## Overview
Use remote backends in combination with Terraform workspaces to manage isolated environments safely and consistently.

## Code Example
Configure an S3 backend with a DynamoDB table for locking, using workspace-specific keys:

    terraform {
      backend "s3" {
        bucket         = "terraform-demo-remote-state"
        key            = "workspace-${terraform.workspace}/terraform.tfstate"
        region         = "us-east-1"
        dynamodb_table = "terraform-state-lock"
        encrypt        = true
      }
    }

Commands:

    terraform init
    terraform workspace new dev
    terraform workspace select dev
    terraform apply
    terraform workspace new prod
    terraform workspace select prod
    terraform apply
    terraform workspace list

## Expected Output

* Separate state files for dev and prod in the S3 bucket
* DynamoDB locks prevent simultaneous modifications to the same state
* Workspace isolation ensures resources don’t collide while sharing the same backend

## Insights

* **Why this demo exists:** Demonstrates safe multi-environment deployments with centralized state.
* **Key points:** Workspace-specific keys organize state per environment; DynamoDB locking avoids conflicts.
* **Common mistakes / pitfalls:** Overwriting state files by misconfiguring keys or regions; forgetting to select the correct workspace.
* **Reflection / next steps:** Combine with modules and CI/CD pipelines for collaborative and automated deployments.
