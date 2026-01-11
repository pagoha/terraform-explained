# 6-4 Remote State Best Practices

## Overview

Learn best practices when using remote state for collaboration and production environments.

## Key Guidelines

* Always enable state locking
* Encrypt sensitive data in the backend
* Separate state per environment (workspaces or buckets)
* Version control all Terraform code, but never commit `terraform.tfstate`
* Use outputs to reference remote resources safely

## Insights

* **Why this demo exists:** Ensures maintainable, secure, and collaborative infrastructure as code.
* **Reflection / next steps:** Combine with Terraform modules and workspaces for full team-ready deployments.
