# 7-2 Import Existing Resource

## Overview

Bring existing AWS resources under Terraform management.

## Code Example

```hcl
resource "aws_s3_bucket" "imported" {
  bucket = "existing-bucket-name"
}
```

Commands:

```bash
terraform import aws_s3_bucket.imported existing-bucket-name
terraform plan
terraform apply
```

## Expected Output

* Existing resource added to Terraform state
* Plan shows no changes

## Insights

* **Why this demo exists:** Manage pre-existing infrastructure safely.
* **Key points:** Importing does not modify resources.
* **Common mistakes / pitfalls:** Resource name mismatches; forgetting to define matching configuration.
