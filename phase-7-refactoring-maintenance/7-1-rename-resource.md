# 7-1 Rename Resource

## Overview

Learn how to safely rename a Terraform resource without destroying it, ensuring the infrastructure remains intact and state is consistent.

## Code Example

Original resource:

    resource "aws_s3_bucket" "old_name" {
      bucket = "terraform-demo-old"
    }

Renamed resource:

    resource "aws_s3_bucket" "new_name" {
      bucket = "terraform-demo-old"
      lifecycle {
        prevent_destroy = true
      }
    }

Rename the resource in state:

    terraform state mv aws_s3_bucket.old_name aws_s3_bucket.new_name

Verify state list:

    terraform state list

Example output:

    aws_s3_bucket.new_name

Plan and apply to confirm no unintended changes:

    terraform plan
    terraform apply

## Expected Output

* Resource renamed in state without destruction
* Terraform plan shows no changes to the actual infrastructure
* State file now reflects the new resource name

## Insights

* **Why this demo exists:** Avoids accidental destruction when renaming resources
* **Key points:** Always use `terraform state mv` when renaming
* **Common mistakes / pitfalls:** Forgetting `prevent_destroy`; renaming resource in code without updating state
