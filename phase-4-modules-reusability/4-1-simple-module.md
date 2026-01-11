# 4-1 Simple Module

## Overview

Create a simple module for S3 buckets to reuse across environments.

## Code Example

Folder structure:

```
terraform-explained/
├─ modules/
│  └─ s3_bucket/
│     ├─ main.tf
│     ├─ variables.tf
│     └─ outputs.tf
└─ main.tf
```

`modules/s3_bucket/variables.tf`:

```hcl
variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}

variable "acl" {
  description = "ACL for the bucket"
  type        = string
  default     = "private"
}
```

`modules/s3_bucket/main.tf`:

```hcl
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name
  acl    = var.acl
}
```

`modules/s3_bucket/outputs.tf`:

```hcl
output "bucket_id" {
  value = aws_s3_bucket.this.id
}
```

`main.tf`:

```hcl
module "example_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "terraform-demo-module-001"
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

* Module creates S3 bucket using reusable code
* `terraform state list` shows module and resource
* `terraform destroy` removes the bucket

## Insights

* **Why this demo exists:** Demonstrates modularization for reuse.
* **Key points:** Modules help organize code, isolate functionality, and simplify large deployments.
* **Common mistakes / pitfalls:** Forgetting `source` path; not passing required variables.
* **Reflection / next steps:** Create modules for EC2, SG, and other resources.
