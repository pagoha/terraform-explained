# 5-1 Introduction to Workspaces

## Overview

Learn how Terraform workspaces allow multiple environments from the same codebase.

## Code Example

```bash
terraform workspace list
terraform workspace new dev
terraform workspace new prod
terraform workspace select dev
```

`main.tf`:

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-${terraform.workspace}-bucket"
  acl    = "private"
}
```

Commands:

```bash
terraform init
terraform plan
terraform apply
terraform workspace select prod
terraform apply
terraform workspace list
terraform destroy
```

## Expected Output

* Separate buckets for `dev` and `prod` workspaces
* `terraform workspace list` shows `default`, `dev`, `prod`
* `terraform destroy` removes resources in the current workspace

## Insights

* **Why this demo exists:** Illustrates safe environment separation.
* **Key points:** Workspaces isolate state files; same code can deploy multiple environments.
* **Common mistakes / pitfalls:** Forgetting which workspace is selected; assuming resources share state.
* **Reflection / next steps:** Combine with variables and modules for full multi-environment setups.
