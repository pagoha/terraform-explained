# 2-3 Outputs Basics

## Overview

Learn how to define outputs in Terraform to expose resource information.

## Code Example

`outputs.tf`:

```hcl
output "bucket_arn" {
  description = "The ARN of the S3 bucket"
  value       = aws_s3_bucket.example.arn
}

output "bucket_name" {
  description = "The name of the S3 bucket"
  value       = aws_s3_bucket.example.bucket
}
```

Commands:

```bash
terraform init
terraform apply
terraform output
terraform destroy
```

## Expected Output

* Outputs displayed in terminal:

```
bucket_arn = arn:aws:s3:::terraform-demo-bucket-phase2
bucket_name = terraform-demo-bucket-phase2
```

## Insights

* **Why this demo exists:** Outputs are useful for referencing resources in other modules or scripts.
* **Key points:** Outputs can be sensitive (e.g., passwords), default formatting is human-readable.
* **Common mistakes / pitfalls:** Trying to reference outputs before `apply`; missing `depends_on` in some scenarios.
* **Reflection / next steps:** Combine with `terraform_remote_state` in Phase 5 for cross-module communication.
