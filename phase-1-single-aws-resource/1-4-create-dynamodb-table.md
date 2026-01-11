# 1-4 Create DynamoDB Table

## Overview

Deploy a simple DynamoDB table to introduce non-relational AWS resources.

## Code Example

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_dynamodb_table" "example" {
  name         = "terraform-demo-table"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "id"

  attribute {
    name = "id"
    type = "S"
  }

  tags = {
    Environment = "Phase1"
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

* Table created with PAY_PER_REQUEST billing
* Can be referenced in future demos
* `terraform destroy` deletes the table

## Insights

* **Why this demo exists:** Introduces DynamoDB and Terraform’s resource handling for databases.
* **Key points:** PAY_PER_REQUEST avoids charges for low-volume testing; hash_key defines partition key.
* **Common mistakes / pitfalls:** Forgetting attribute block; table name collisions.
* **Reflection / next steps:** Explore adding read/write capacity, global secondary indexes in Phase 3.
