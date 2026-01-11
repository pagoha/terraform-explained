# 2-2 Override Variables

## Overview

Learn how to **override Terraform variables** using CLI arguments and `.tfvars` files.
This allows flexible configuration for different environments without changing your main code.

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

### 2. Create `terraform.tfvars` File

Create a file named `terraform.tfvars` in your working folder:

```hcl
bucket_name = "terraform-demo-bucket-overridden"
region      = "us-east-1"
```

Terraform will automatically load values from this file during `plan` and `apply`.

---

### 3. Apply Terraform with CLI Variable Override

**Override variables directly from CLI:**

```bash
terraform plan -var="bucket_name=terraform-demo-bucket-cli"
terraform apply -var="bucket_name=terraform-demo-bucket-cli"
```

**Expected behavior:** The bucket name in Terraform will reflect the overridden value.

---

### 4. Run Full Workflow

```bash
terraform init    # initialize working folder
terraform state list  # verify resource in state
terraform destroy # remove the bucket
```

Optional verification with AWS CLI:

```bash
aws s3 ls
```

Expected output: Bucket created matches the overridden value.

---

## Insights

* **Why this demo exists:** Demonstrates flexible configuration using overrides for multiple environments.
* **Key points:**
  - `.tfvars` files are automatically loaded
  - CLI `-var` overrides always take precedence
* **Common mistakes / pitfalls:**
  - Conflicting values between `.tfvars` and CLI
  - Forgetting to run `terraform plan` before `apply`
* **Reflection / next steps:**
  - Use variable overrides to safely deploy to multiple environments (dev/test/prod) without modifying the main code.
