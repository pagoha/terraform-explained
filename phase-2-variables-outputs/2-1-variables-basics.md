# 2-1 Variables Basics

## Overview

Learn how to define and use **variables** in Terraform to make configurations dynamic.
This demo shows how changing variables can modify resources safely.

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

### 2. Create Terraform Configuration Files

**Create `variables.tf`:**

```hcl
variable "bucket_name" {
  description = "The name of the S3 bucket"
  type        = string
  default     = "terraform-demo-bucket-phase2"
}

variable "region" {
  description = "AWS region to deploy resources"
  type        = string
  default     = "us-east-1"
}
```

**Create `main.tf`:**

```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
  acl    = "private"
}
```

**Tip:** Both files should live in the same working folder.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working folder
terraform plan    # preview S3 bucket creation using variables
terraform apply   # create the S3 bucket
terraform state list  # verify resource in state
terraform destroy # remove the bucket
```

**Optional Verification with AWS CLI:**

```bash
aws s3 ls
```

Expected output: Bucket created with the name from `bucket_name` variable.

---

### 4. Overriding Variables

**Override via CLI:**

```bash
terraform apply -var="bucket_name=my-custom-bucket"
```

**Override via `terraform.tfvars` file:**

```hcl
bucket_name = "my-custom-bucket"
region      = "us-east-1"
```

Terraform automatically picks up values from `terraform.tfvars`.

---

## Insights

* **Why this demo exists:** Introduces dynamic configuration with variables.
* **Key points:**
  - Variables can have defaults or be overridden
  - Always reference variables using `var.<name>`
* **Common mistakes / pitfalls:**
  - Forgetting `var.` when using a variable
  - Changing variable values without reviewing plan, which may overwrite existing resources
* **Reflection / next steps:**
  - Explore variable types: `string`, `number`, `bool`, `list`, `map`, and `object`. Use overrides for flexible deployments.
