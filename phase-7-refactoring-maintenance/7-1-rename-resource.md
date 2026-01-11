# 7-1 Rename Resource

## Overview

Learn how to safely rename a Terraform resource without destroying it.

## Code Example

```hcl
# Original resource
resource "aws_s3_bucket" "old_name" {
  bucket = "terraform-demo-old"
}

# Renamed resource
resource "aws_s3_bucket" "new_name" {
  bucket = "terraform-demo-old"
  lifecycle {
    prevent_destroy = true
  }
}
```

Commands:

```bash
terraform state mv aws_s3_bucket.old_name aws_s3_bucket.new_name
terraform plan
terraform apply
```

## Expected Output

* Resource renamed in state without destruction
* Terraform plan shows no changes to the actual infrastructure

## Insights

* **Why this demo exists:** Avoid accidental destruction when renaming resources.
* **Key points:** Use `terraform state mv` for safe renames.
* **Common mistakes / pitfalls:** Forgetting to prevent destroy; renaming without state updates.
