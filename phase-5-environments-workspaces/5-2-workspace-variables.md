# 5-2 Workspace-Specific Variables

## Overview

Use workspace-specific variables for different environments.

## Code Example

`variables.tf`:

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

`main.tf`:

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-${var.bucket_suffix}-bucket"
  acl    = "private"
}
```

Commands:

```bash
terraform init
terraform workspace select dev
terraform apply
terraform workspace select prod
terraform apply
```

## Expected Output

* Buckets created with names reflecting workspace (`dev`, `prod`)
* Workspace variables allow environment-specific configuration
* Destroying resources in one workspace doesn’t affect others

## Insights

* **Why this demo exists:** Demonstrates variable usage per environment.
* **Key points:** `terraform.workspace` can be used to dynamically adjust resources.
* **Common mistakes / pitfalls:** Not using workspace-specific identifiers; overwriting resources.
* **Reflection / next steps:** Add outputs to reference workspace-specific resources.
