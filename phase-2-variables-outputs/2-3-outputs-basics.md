# 2-3 Outputs Basics

## Overview

Learn how to define **outputs** in Terraform to expose resource information.
Outputs make it easier to reference created resources in other modules, scripts, or future workflows.

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

### 2. Create `outputs.tf` File

Create a file named `outputs.tf` in your working folder:

```hcl
output "bucket_arn" {
  description = "The ARN of the S3 bucket"
  value       = aws_s3_bucket.example.arn
}

output "bucket_name" {
  description = "The name of the S3 bucket"
  value       = aws_s3_bucket.example.bucket
}
```

**Tip:** Outputs can also be marked `sensitive = true` if you don’t want them displayed in the terminal (e.g., passwords or secrets).

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working folder
terraform apply   # create resources
terraform output  # display output values
terraform state list  # verify resources in state
terraform destroy # remove resources
```

**Optional Verification with AWS CLI:**

```bash
aws s3 ls
```

Expected output:

```
bucket_arn = arn:aws:s3:::terraform-demo-bucket-phase2
bucket_name = terraform-demo-bucket-phase2
```

---

## Insights

* **Why this demo exists:** Demonstrates how to expose key resource information for downstream use.
* **Key points:**
  - Outputs are accessible via `terraform output`
  - Can be marked `sensitive` to hide sensitive data
  - Useful for cross-module references and scripts
* **Common mistakes / pitfalls:**
  - Referencing outputs before `apply` (resource must exist)
  - Missing `depends_on` when necessary in complex setups
* **Reflection / next steps:**
  - Combine outputs with `terraform_remote_state` (Phase 5) to share information between modules or workspaces.
