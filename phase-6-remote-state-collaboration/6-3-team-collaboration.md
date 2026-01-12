# 6-3 Team Collaboration

## Overview
Best practices for collaborating with a team on Terraform projects using remote state.

## Key Guidelines

* Enable backend locking (DynamoDB or Terraform Cloud)
* Use version-controlled `.tf` files
* Always run `terraform init` before switching branches or workspaces
* Communicate workspace and environment selections with team members
* Consider automated CI/CD pipelines to plan/apply safely

## Insights

* **Why this demo exists:** Ensures safe, collaborative Terraform usage.
* **Reflection / next steps:** Explore Terraform Cloud or Terraform Enterprise for advanced collaboration features.
