# 0-4 First Local Resource

## Overview

Deploy your first real AWS resource using Terraform — an **S3 bucket**.
This demo shows the full workflow with `plan`, `apply`, and `destroy` so learners can see Terraform in action.

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

Ensure you are in your dedicated working folder for all Terraform projects.

---

### 2. Create Terraform Configuration File

Create a file named `main.tf` in your working folder:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-12345" # must be globally unique
  acl    = "private"
}
```

**Tip:** Replace `12345` with a unique number or your initials to avoid bucket name collisions.

---

### 3. Run the Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview resource creation
terraform apply   # create S3 bucket
terraform state list  # verify resource in state
terraform destroy # remove the bucket
```

**Command Notes / Expected Output:**

- `terraform plan` – shows **1 resource to be created**
- `terraform apply` – creates the S3 bucket in AWS
- `terraform state list` – lists `aws_s3_bucket.example`
- `terraform destroy` – safely deletes the bucket

Optional: verify in AWS CLI:

```bash
aws s3 ls
```

---

## Insights

* **Why this demo exists:** Provides hands-on experience creating AWS resources. Demonstrates plan vs apply.
* **Key points:**
  - S3 bucket names must be **globally unique**
  - ACL settings control access (private vs public)
* **Common mistakes / pitfalls:**
  - Bucket name collisions
  - Forgetting to destroy resources, which can incur charges
* **Reflection / next steps:**
  - Experiment with versioning, tags, and other S3 properties. Phase 1 demos will introduce additional AWS resources.
