# 6-2 Remote Backend with Workspaces

## Overview

Use remote backends in combination with Terraform workspaces for isolated environments.

## Code Example

```hcl
terraform {
  backend "s3" {
    bucket         = "terraform-demo-remote-state"
    key            = "workspace-${terraform.workspace}/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-lock"
    encrypt        = true
  }
}
```

Commands:

```bash
terraform init
terraform workspace new dev
terraform workspace select dev
terraform apply
terraform workspace new prod
terraform workspace select prod
terraform apply
terraform workspace list
```

## Expected Output

* Separate state files for `dev` and `prod` in S3
* Locks prevent multiple users from editing the same state concurrently
* Workspaces isolated while sharing the same backend

## Insights

* **Why this demo exists:** Combines workspaces and remote state for robust environment management.
* **Key points:** Key paths define workspace-specific state; team members share the same backend.
* **Common mistakes / pitfalls:** Overwriting state files; misconfigured keys or regions.
* **Reflection / next steps:** Automate using CI/CD pipelines for collaborative deployments.
