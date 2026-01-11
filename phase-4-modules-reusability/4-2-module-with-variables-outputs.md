# 4-2 Module with Variables & Outputs

## Overview

Use variables and outputs inside modules for dynamic, reusable code.

## Code Example

`modules/s3_bucket/variables.tf`:

```hcl
variable "bucket_name" { type = string }
variable "versioning" { type = bool, default = true }
```

`modules/s3_bucket/main.tf`:

```hcl
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name

  versioning {
    enabled = var.versioning
  }
}
```

`modules/s3_bucket/outputs.tf`:

```hcl
output "bucket_arn" {
  value = aws_s3_bucket.this.arn
}
```

`main.tf`:

```hcl
module "example_bucket" {
  source     = "./modules/s3_bucket"
  bucket_name = "terraform-demo-module-002"
  versioning  = true
}

output "s3_bucket_arn" {
  value = module.example_bucket.bucket_arn
}
```

Commands:

```bash
terraform init
terraform plan
terraform apply
terraform output
terraform destroy
```

## Expected Output

* Module creates versioned S3 bucket
* Output exposes bucket ARN
* `terraform destroy` removes the bucket

## Insights

* **Why this demo exists:** Shows passing variables into modules and exposing outputs.
* **Key points:** Outputs allow modules to communicate with root module or other modules.
* **Common mistakes / pitfalls:** Forgetting to output values; mismatch variable types.
* **Reflection / next steps:** Combine multiple modules to build a full environment.
