# 2-1 Variables Basics

## Overview

Learn how to define and use variables in Terraform to make configurations dynamic.

## Code Example

`variables.tf`:

```hcl
variable "bucket_name" {
  description = "The name of the S3 bucket"
  type        = string
  default     = "terraform-demo-bucket-phase2"
}

variable "region" {
  description = "AWS region to deploy resources"
  type        = string
  default     = "us-east-1"
}
```

`main.tf`:

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
  acl    = "private"
}
```

Commands:

```bash
terraform init
terraform plan
terraform apply
terraform destroy
```

## Expected Output

* Bucket created with the name from `bucket_name` variable
* Changing the variable updates the resource on next `apply`
* `terraform destroy` removes the resource

## Insights

* **Why this demo exists:** Introduces dynamic configuration with variables.
* **Key points:** Variables can have defaults or be overridden via CLI or `terraform.tfvars`.
* **Common mistakes / pitfalls:** Forgetting to reference variables with `var.<name>`; overwriting existing resources with new variable values without planning.
* **Reflection / next steps:** Explore variable types: string, number, bool, list, map, and object.
