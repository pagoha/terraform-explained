# 5-1 Introduction to Workspaces

## Overview

Learn how Terraform workspaces allow you to manage multiple environments from the same codebase safely.

## Code Example

### Workspace commands

```bash
# List existing workspaces
terraform workspace list

# Create new workspaces
terraform workspace new dev
terraform workspace new prod

# Switch to a workspace
terraform workspace select dev
```

### Terraform configuration (`main.tf`)

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-${terraform.workspace}-bucket"
  acl    = "private"
}
```

### Apply resources in different workspaces

```bash
terraform init
terraform plan
terraform apply          # Applies to dev workspace
terraform workspace select prod
terraform plan
terraform apply          # Applies to prod workspace
terraform workspace list # Shows default, dev, prod
terraform destroy        # Destroys resources in current workspace
```

## Expected Output

* Separate S3 buckets for each workspace (`dev`, `prod`)
* `terraform workspace list` shows `default`, `dev`, and `prod`
* `terraform destroy` removes only the resources in the current workspace

## Insights

* **Why this demo exists:** Demonstrates safe separation of environments using the same Terraform code.
* **Key points:**
  - Workspaces isolate state files
  - Resources in one workspace do not affect others
  - Same Terraform code can deploy multiple environments
* **Common mistakes / pitfalls:**
  - Forgetting which workspace is selected before applying/destroying
  - Assuming resources share state across workspaces
* **Reflection / next steps:** Combine workspaces with variables and modules to deploy fully parameterized multi-environment infrastructure.
