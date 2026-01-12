# 7-4 Version Upgrades

## Overview

Upgrade Terraform CLI and provider versions safely, ensuring infrastructure is compatible and no unintended changes occur.

## Code Example

Specify required Terraform and provider versions:

    terraform {
      required_version = ">= 1.6.0"
      required_providers {
        aws = ">= 5.0"
      }
    }

Upgrade providers and CLI:

    terraform init -upgrade

Plan and apply to confirm no breaking changes:

    terraform plan
    terraform apply

Example output:

    Initial provider version: aws 4.66.0
    Upgrading to provider version: aws 5.3.0
    Terraform CLI version upgraded to 1.6.2
    Plan: 0 to add, 0 to change, 0 to destroy

## Expected Output

* Terraform and provider versions updated
* Terraform plan shows no unintended changes
* State and infrastructure remain consistent

## Insights

* **Why this demo exists:** Keeps Terraform environment up-to-date and compatible
* **Key points:** Always run `terraform plan` before `apply` when upgrading
* **Common mistakes / pitfalls:** Skipping `init -upgrade`; applying upgrades without verifying compatibility; breaking provider version constraints
* **Reflection / next steps:** Repeat this process regularly; test upgrades in isolated environments first
