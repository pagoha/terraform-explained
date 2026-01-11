# 8-4 Terraform CI/CD

## Overview

Implement automated pipelines for Terraform deployments.

## Code Example

* GitHub Actions or GitLab CI pipeline YAML

```yaml
name: Terraform
on:
  push:
    branches:
      - main
jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v2
      - name: Terraform Init
        run: terraform init
      - name: Terraform Plan
        run: terraform plan
      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve
```

## Expected Output

* Automatic plan and apply on push to main branch
* CI/CD pipeline enforces collaboration and repeatable deployments

## Insights

* **Why this demo exists:** Shows modern automation of Terraform workflows.
* **Key points:** CI/CD pipelines reduce manual errors and enforce best practices.
* **Common mistakes / pitfalls:** Not securing secrets; skipping plan step.
