# 2-2 Override Variables

## Overview

Learn how to override variables using CLI arguments and `.tfvars` files.

## Code Example

Create `terraform.tfvars`:

```hcl
bucket_name = "terraform-demo-bucket-overridden"
region      = "us-east-1"
```

Apply with overridden variables:

```bash
terraform plan -var="bucket_name=terraform-demo-bucket-cli"
terraform apply -var="bucket_name=terraform-demo-bucket-cli"
```

## Expected Output

* Terraform uses variable values from CLI or `terraform.tfvars`
* Bucket name reflects overridden value
* `terraform destroy` removes the bucket

## Insights

* **Why this demo exists:** Shows flexible configuration for multiple environments.
* **Key points:** `.tfvars` is automatically loaded; CLI `-var` overrides take precedence.
* **Common mistakes / pitfalls:** Conflicting variable values; forgetting to plan before apply.
* **Reflection / next steps:** Use for multiple environments (dev/test/prod).
