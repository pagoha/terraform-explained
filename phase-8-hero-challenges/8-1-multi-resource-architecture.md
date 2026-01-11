# 8-1 Multi-Resource Architecture

## Overview

Deploy multiple interdependent AWS resources using modules and workspaces.

## Code Example

* Modules for VPC, EC2, RDS, S3
* Root module combines all modules using workspace-specific configurations

Commands:

```bash
terraform init
terraform workspace new dev
terraform workspace select dev
terraform apply
terraform workspace select prod
terraform apply
```

## Expected Output

* Complete architecture deployed per environment
* Outputs show correct references

## Insights

* **Why this demo exists:** Real-world scenario combining multiple resources.
* **Key points:** Use modules, variables, workspaces for maintainable infra.
* **Common mistakes / pitfalls:** Dependency misconfiguration, resource naming conflicts.
