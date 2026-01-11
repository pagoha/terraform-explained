# 5-3 Workspaces with Modules

## Overview

Combine workspaces with modules to deploy identical infrastructure in multiple environments.

## Code Example

`main.tf`:

```hcl
module "s3_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "terraform-demo-${terraform.workspace}-module"
}
```

Commands:

```bash
terraform init
terraform workspace select dev
terraform apply
terraform workspace select prod
terraform apply
terraform output
terraform destroy
```

## Expected Output

* Dev and Prod S3 buckets created using the same module
* Outputs reflect correct workspace-specific resources
* Destroying resources in one workspace only affects that workspace

## Insights

* **Why this demo exists:** Combines modularity with environment separation.
* **Key points:** Modules and workspaces together create maintainable multi-environment infrastructure.
* **Common mistakes / pitfalls:** Forgetting to select workspace; module variables not dynamic.
* **Reflection / next steps:** Scale to multiple modules and resources for full environment setups.
