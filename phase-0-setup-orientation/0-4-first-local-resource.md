# 0-4 First Local Resource

## Overview

Deploy your first real AWS resource using Terraform — an S3 bucket.

## Code Example

`main.tf`:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-12345"
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

* `terraform plan` shows 1 resource to be created
* `terraform apply` creates the S3 bucket in AWS
* `terraform state list` shows `aws_s3_bucket.example`
* `terraform destroy` removes the bucket

## Insights

* **Why this demo exists:** Provides hands-on experience creating AWS resources. Shows plan vs apply in action.
* **Key points:** Bucket name must be globally unique; ACL settings control access.
* **Common mistakes / pitfalls:** Bucket name collisions; forgetting to destroy resources leading to unexpected charges.
* **Reflection / next steps:** Experiment with versioning, tags, and other S3 properties. Phase 1 demos will introduce additional AWS resources.
