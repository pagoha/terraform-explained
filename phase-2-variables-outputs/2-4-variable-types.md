# 2-4 Variable Types

## Overview

Learn about **advanced variable types** in Terraform: `list`, `map`, `bool`, `number`, and `object`.
This demo shows how structured variables improve reusability and maintainability.

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

**Create `main.tf`:**

```hcl
resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-types" # must be globally unique
  acl    = "private"

  versioning {
    enabled = var.enable_versioning
  }

  tags = var.env_tags
}
```

**Tip:** Both files should live in the same working folder. Adjust bucket name to avoid collisions.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working folder
terraform plan    # preview resource creation with variables
terraform apply   # create the S3 bucket
terraform state list  # verify resource in state
terraform destroy # remove the bucket
```

**Optional Verification with AWS CLI:**

```bash
aws s3 ls
```

Expected output: Bucket created with versioning enabled and tags applied.

---

### 4. Experimenting with Variable Values

**Override `enable_versioning` via CLI:**

```bash
terraform apply -var="enable_versioning=false"
```

**Override `env_tags` via `terraform.tfvars`:**

```hcl
env_tags = {
  Environment = "test"
  Project     = "TerraformDemo"
}
```

Terraform updates resources accordingly.

---

## Insights

* **Why this demo exists:** Demonstrates best practices for reusable configurations using advanced variable types.
* **Key points:**
  - Maps, lists, and objects allow structured data
  - Boolean variables can toggle features on/off
* **Common mistakes / pitfalls:**
  - Incorrect type usage (e.g., assigning string to bool)
  - Forgetting to update variable references in resources
* **Reflection / next steps:**
  - Use complex objects for multi-resource modules in Phase 4 and advanced configurations.
