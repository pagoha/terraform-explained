# 0-3 Terraform Workflow

## Overview

Introduce Terraform workflow: `init`, `plan`, `apply`, `destroy`.

## Code Example

Create a simple `main.tf`:

```hcl
terraform {
  required_version = ">= 1.0.0"
}

provider "aws" {
  region = "us-east-1"
}
```

Commands to run:

```bash
terraform init    # initialize working directory
terraform plan    # preview changes
terraform apply   # apply changes
terraform destroy # remove resources
```

## Expected Output

* `terraform init` downloads AWS provider
* `terraform plan` shows no resources yet
* `terraform apply` applies your configuration (empty for now)
* `terraform destroy` cleans up safely

## Insights

* **Why this demo exists:** Understanding the workflow is critical for all future Terraform usage.
* **Key points:** `init` must be run first; `plan` is your safety check; `apply` makes changes; `destroy` removes resources.
* **Common mistakes / pitfalls:** Forgetting `init`; applying changes without reviewing plan; manually deleting resources instead of `destroy`.
* **Reflection / next steps:** Add your first resource to see changes in plan and apply.
