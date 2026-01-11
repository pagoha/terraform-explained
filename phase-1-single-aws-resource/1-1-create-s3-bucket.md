# 1-1 Create S3 Bucket

## Overview

Learn how to create an S3 bucket using Terraform with additional properties like versioning and tags.

## Code Example

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-unique-001"
  acl    = "private"

  versioning {
    enabled = true
  }

  tags = {
    Environment = "Phase1"
    Project     = "TerraformExplained"
  }
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

* `terraform plan` shows 1 S3 bucket with versioning and tags
* `terraform apply` creates the bucket with specified properties
* `terraform state list` shows `aws_s3_bucket.example`
* `terraform destroy` deletes the bucket safely

## Insights

* **Why this demo exists:** Demonstrates adding properties and metadata to a resource.
* **Key points:** Versioning is enabled via a nested block; tags help organize resources.
* **Common mistakes / pitfalls:** Bucket name collisions; forgetting versioning block syntax.
* **Reflection / next steps:** Experiment with different ACLs and encryption options.
