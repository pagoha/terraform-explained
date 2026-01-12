# 8-3 Error Handling & Drift

## Overview

Learn how to detect drift between Terraform state and actual infrastructure, and safely handle failed applies or resource errors.

## Code Example

Example workflow to detect and correct drift:

    # Refresh current state
    terraform plan
    terraform refresh

    # Apply changes safely
    terraform apply

    # Inspect current resources in state
    terraform state list

Commands:

    terraform init
    terraform plan
    terraform refresh
    terraform apply
    terraform state list

## Expected Output

* Terraform detects drift between state and real resources
* Changes applied only where necessary
* Failed applies can be retried safely without destroying other resources
* `terraform state list` accurately reflects current infrastructure

## Insights

* **Why this demo exists:** Prepares learners to manage real-world infrastructure drift and errors safely.
* **Key points:** Regularly refresh state; validate resources before applying; rely on outputs for verification.
* **Common mistakes / pitfalls:** Ignoring drift; manually editing state files; skipping `terraform refresh`.
* **Reflection / next steps:** Combine with CI/CD pipelines and automated monitoring to catch drift proactively.
