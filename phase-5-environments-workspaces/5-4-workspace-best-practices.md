# 5-4 Workspace Best Practices

## Overview

Learn best practices for managing multiple environments using workspaces.

## Key Guidelines

* Always name workspaces clearly (`dev`, `test`, `prod`)
* Use `terraform.workspace` in resource names or variables
* Avoid mixing environments in the same workspace
* Consider remote backends per workspace for team collaboration
* Use outputs to track workspace-specific resources

## Insights

* **Why this demo exists:** Ensures safe and organized multi-environment deployments.
* **Reflection / next steps:** Combine with remote state and locking in Phase 6 for team collaboration.
