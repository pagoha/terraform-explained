# 5-4 Workspace Best Practices

## Overview

Learn best practices for managing multiple environments using Terraform workspaces. Following these guidelines ensures safe, predictable, and maintainable deployments across `dev`, `test`, and `prod` environments.

## Key Guidelines

* **Name workspaces clearly:** Use descriptive names like `dev`, `test`, `prod` to avoid confusion.
* **Use `terraform.workspace`:** Reference `terraform.workspace` in resource names, variables, or outputs to dynamically distinguish environments.
* **Avoid mixing environments:** Keep each workspace isolated; do not manually share resources between workspaces.
* **Consider remote backends:** For team collaboration, configure a remote backend per workspace to manage state and enable locking (e.g., S3 + DynamoDB).
* **Leverage outputs:** Use workspace-specific outputs to track and reference resources safely across environments.
* **Document workspace usage:** Keep notes or a README for each workspace, especially when multiple environments share the same codebase.

## Insights

* **Why this demo exists:** Ensures safe, organized, and repeatable multi-environment deployments.
* **Key points:** Proper workspace management prevents accidental cross-environment changes and enables team collaboration.
* **Common mistakes / pitfalls:** Overwriting resources by applying the wrong workspace; manually sharing state files; hardcoding environment names.
* **Reflection / next steps:** Combine these best practices with remote state, modules, and variables in Phase 6 for robust team workflows.
