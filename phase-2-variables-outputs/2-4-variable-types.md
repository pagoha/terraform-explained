# 2-4 Variable Types

## Overview

Learn about advanced variable types in Terraform: list, map, bool, number, object.

## Code Example

`variables.tf`:

```hcl
variable "env_tags" {
  description = "Tags for environment"
  type = map(string)
  default = {
    Environment = "dev"
    Project     = "TerraformExplained"
  }
}

variable "enable_versioning" {
  description = "Enable bucket versioning"
  type        = bool
  default     = true
}
```

`main.tf`:

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-types"
  acl    = "private"

  versioning {
    enabled = var.enable_versioning
  }

  tags = var.env_tags
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

* Bucket created with versioning enabled and tags applied
* Changing variable values modifies resource accordingly
* `terraform destroy` removes the bucket

## Insights

* **Why this demo exists:** Demonstrates best practices for reusable configurations using advanced types.
* **Key points:** Lists, maps, and objects allow structured data; boolean variables toggle features.
* **Common mistakes / pitfalls:** Incorrect type usage; forgetting to update references.
* **Reflection / next steps:** Use complex objects for multi-resource modules in Phase 4.
