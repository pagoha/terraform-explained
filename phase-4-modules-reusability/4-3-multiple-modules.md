# 4-3 Multiple Modules

## Overview

Learn how to **combine multiple modules** to deploy EC2, Security Group, and S3 bucket together, demonstrating module composition and inter-module references.

## Code Example

**Folder structure:**

    terraform-explained/
    ├─ modules/
    │  ├─ s3_bucket/
    │  ├─ ec2_instance/
    │  └─ security_group/
    └─ main.tf

**Root configuration (`main.tf`):**

    module "app_bucket" {
      source      = "./modules/s3_bucket"
      bucket_name = "terraform-demo-module-multi-s3"
    }

    module "app_sg" {
      source = "./modules/security_group"
      name   = "terraform-demo-module-sg"
    }

    module "app_ec2" {
      source                 = "./modules/ec2_instance"
      ami                    = "ami-0c55b159cbfafe1f0"
      instance_type          = "t2.micro"
      vpc_security_group_ids = [module.app_sg.security_group_id]
      depends_on             = [module.app_bucket]
    }

**Terraform commands:**

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* S3 bucket, security group, and EC2 instance created using modules
* `terraform state list` shows module resources:
  - `module.app_bucket.aws_s3_bucket.this`
  - `module.app_sg.aws_security_group.this`
  - `module.app_ec2.aws_instance.this`
* Dependencies handled automatically (`depends_on` ensures correct order)
* `terraform destroy` removes resources in the correct order

## Insights

* **Why this demo exists:** Shows **combining modules** to manage real-world, reusable infrastructure.
* **Key points:**
  - Modules can reference outputs from other modules (`module.app_sg.security_group_id`)
  - Simplifies infrastructure management and scaling
* **Common mistakes / pitfalls:**
  - Forgetting to output values from modules
  - Circular dependencies between modules
* **Reflection / next steps:** Parameterize modules for multiple environments, regions, or AWS accounts.
