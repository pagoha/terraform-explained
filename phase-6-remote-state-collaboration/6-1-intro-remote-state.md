# 6-1 Introduction to Remote State

## Overview

Learn why remote state is critical for team collaboration and safe deployments.

## Code Example

Configure an S3 backend with a DynamoDB table for state locking:

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-demo-remote-state"
    key            = "global/s3/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-lock"
    encrypt        = true
  }
}
```

Commands:

```bash
terraform init
terraform plan
terraform apply
terraform state list
terraform destroy
```

## Expected Output

* Terraform state stored in S3 bucket
* DynamoDB table used for locking during operations
* State file encrypted and shared for team collaboration

## Insights

* **Why this demo exists:** Centralizes state for team collaboration.
* **Key points:** Prevents conflicts with `dynamodb_table` locking; ensures consistent deployments.
* **Common mistakes / pitfalls:** Forgetting to initialize backend; using same key for multiple environments.
* **Reflection / next steps:** Combine with workspaces for multiple environments.
