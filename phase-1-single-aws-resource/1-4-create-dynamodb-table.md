# 1-4 Create DynamoDB Table

## Overview

Deploy a **DynamoDB table** using Terraform to introduce non-relational AWS resources.
This demo builds on previous Phase 1 resources and shows how to manage AWS databases with Terraform.

---

## Steps

### 1. Navigate to Your Terraform Working Folder

**Windows (PowerShell):**

```powershell
cd C:\TerraformProjects
```

**macOS / Linux (Terminal):**

```bash
cd ~/TerraformProjects
```

---

### 2. Create Terraform Configuration File

Create a file named `main.tf` with the following content:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_dynamodb_table" "example" {
  name         = "terraform-demo-table" # must be globally unique
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

**Tip:** Add a unique suffix (e.g., your initials) to the table name to avoid collisions.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview table creation
terraform apply   # create the DynamoDB table
terraform state list  # verify resource in state
terraform destroy # remove the table
```

**Optional Verification with AWS CLI:**

```bash
aws dynamodb list-tables
```

Expected output: Your table appears in the list.

---

## Insights

* **Why this demo exists:** Introduces DynamoDB and demonstrates Terraform’s management of database resources.
* **Key points:**
  - `PAY_PER_REQUEST` avoids charges for low-volume testing
  - `hash_key` defines the partition key
* **Common mistakes / pitfalls:**
  - Forgetting the `attribute` block
  - Table name collisions (must be unique globally)
* **Reflection / next steps:**
  - Explore read/write capacity settings, global secondary indexes, and more complex DynamoDB features in later phases.
