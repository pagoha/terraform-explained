# 1-1 Create S3 Bucket

## Overview

Learn how to create an **S3 bucket** using Terraform with additional properties like **versioning** and **tags**.
This demo builds on the Phase 0 workflow and shows how to add metadata to AWS resources.

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

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-unique-001" # must be globally unique
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

**Tip:** Replace `unique-001` with a unique number or initials to avoid bucket name collisions.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview resource creation
terraform apply   # create the S3 bucket
terraform state list  # verify resource in state
terraform destroy # remove the bucket
```

**Optional Verification with AWS CLI:**

```bash
aws s3 ls
```

Expected output: Your bucket should appear in the list.

---

## Insights

* **Why this demo exists:** Demonstrates adding properties (versioning) and metadata (tags) to AWS resources using Terraform.
* **Key points:**
  - Versioning is enabled via a nested block
  - Tags help organize and identify resources
* **Common mistakes / pitfalls:**
  - Bucket name collisions (must be globally unique)
  - Incorrect versioning block syntax
* **Reflection / next steps:**
  - Experiment with different ACLs, encryption, and lifecycle rules. Continue with Phase 1 demos for EC2, Security Groups, and DynamoDB.
