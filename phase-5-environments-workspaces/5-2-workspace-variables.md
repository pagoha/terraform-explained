# 5-2 Workspace-Specific Variables

## Overview

Use workspace-specific variables to configure resources differently for each environment.

## Code Example

### Variables (`variables.tf`)

```hcl
variable "region" {
  type    = string
  default = "us-east-1"
}

variable "bucket_suffix" {
  type    = string
  default = terraform.workspace
}
```

### Terraform configuration (`main.tf`)

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-${var.bucket_suffix}-bucket"
  acl    = "private"
}
```

### Commands

```bash
terraform init

# Apply resources in dev workspace
terraform workspace select dev
terraform plan
terraform apply

# Apply resources in prod workspace
terraform workspace select prod
terraform plan
terraform apply

# Optional: list workspaces
terraform workspace list

# Destroy resources in current workspace
terraform destroy
```

## Expected Output

* S3 buckets created with names reflecting the workspace (`dev`, `prod`)
* Workspace-specific variables allow environment-specific configurations
* Destroying resources in one workspace does not affect other workspaces

## Insights

* **Why this demo exists:** Demonstrates how to use workspace-aware variables to manage multiple environments safely.
* **Key points:**
  - `terraform.workspace` provides a dynamic identifier per environment
  - Workspace-specific values help prevent resource name collisions
  - Apply/destroy operations affect only the current workspace
* **Common mistakes / pitfalls:**
  - Forgetting to include workspace identifiers in resource names
  - Overwriting resources across workspaces by not using dynamic values
* **Reflection / next steps:** Add outputs for workspace-specific resources; combine with modules to build full multi-environment infrastructure.
