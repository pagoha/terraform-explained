# 7-4 Version Upgrades

## Overview

Upgrade Terraform CLI and provider versions safely.

## Code Example

```hcl
terraform {
  required_version = ">= 1.6.0"
  required_providers {
    aws = ">= 5.0"
  }
}
```

Commands:

```bash
terraform init -upgrade
terraform plan
terraform apply
```

## Expected Output

* Terraform and provider versions updated
* Plan shows no unintended changes

## Insights

* **Why this demo exists:** Maintain up-to-date Terraform environment.
* **Key points:** Always plan and review before applying upgrades.
* **Common mistakes / pitfalls:** Skipping `terraform plan`; provider incompatibilities.
