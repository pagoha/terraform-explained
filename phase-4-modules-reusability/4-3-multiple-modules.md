# 4-3 Multiple Modules

## Overview

Combine multiple modules to deploy EC2, Security Group, and S3 bucket together.

## Code Example

Folder structure:

```
terraform-explained/
├─ modules/
│  ├─ s3_bucket/
│  ├─ ec2_instance/
│  └─ security_group/
└─ main.tf
```

`main.tf`:

```hcl
module "app_bucket" {
  source      = "./modules/s3_bucket"
  bucket_name = "terraform-demo-module-multi-s3"
}

module "app_sg" {
  source = "./modules/security_group"
  name   = "terraform-demo-module-sg"
}

module "app_ec2" {
  source                = "./modules/ec2_instance"
  ami                   = "ami-0c55b159cbfafe1f0"
  instance_type         = "t2.micro"
  vpc_security_group_ids = [module.app_sg.security_group_id]
  depends_on            = [module.app_bucket]
}
```

Commands:

```bash
terraform init
terraform plan
terraform apply
terraform destroy
```

## Expected Output

* Resources created through modules
* Dependency ordering handled automatically
* `terraform destroy` removes resources in correct order

## Insights

* **Why this demo exists:** Demonstrates combining modules for real-world reusable infrastructure.
* **Key points:** Modules can reference each other using outputs; simplifies management.
* **Common mistakes / pitfalls:** Forgetting output references; circular dependencies.
* **Reflection / next steps:** Parameterize modules for multiple environments or accounts.
