# 0-3 Terraform Workflow

## Overview

This demo introduces the core Terraform workflow:

1. `terraform init` – initialize the working directory
2. `terraform plan` – preview infrastructure changes
3. `terraform apply` – apply configuration changes
4. `terraform destroy` – remove resources

You will create a simple working folder and a `main.tf` to follow along.

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

### 2. Create a Simple Terraform Configuration

Create a file named `main.tf` in your working folder with the following content:

```hcl
terraform {
  required_version = ">= 1.0.0"
}

provider "aws" {
  region = "us-east-1"
}
```

This config sets the required Terraform version and defines the AWS provider with your configured region.

---

### 3. Run the Terraform Workflow Commands

```bash
terraform init    # initialize working directory
terraform plan    # preview changes
terraform apply   # apply changes
terraform destroy # remove resources
```

**Command Notes / Expected Output:**

- `terraform init` – downloads the AWS provider, sets up backend (empty project for now).
- `terraform plan` – shows **no resources yet**, confirms your configuration is valid.
- `terraform apply` – applies your configuration (nothing to create yet, so safe).
- `terraform destroy` – removes any resources if created (safe to run on empty project).

---

## Insights

* **Why this demo exists:** Understanding the full Terraform workflow is critical for all future usage.
* **Key points:**
  - `init` must be run first to set up the working folder
  - `plan` previews changes before applying
  - `apply` makes actual changes
  - `destroy` safely removes resources
* **Common mistakes / pitfalls:**
  - Forgetting to run `init` first
  - Applying changes without reviewing the plan
  - Manually deleting resources instead of using `destroy`
* **Reflection / next steps:**
  - Add your first resource (e.g., an `aws_s3_bucket`) to see changes in `plan` and `apply`.
