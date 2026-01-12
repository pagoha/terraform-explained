# 8-1 Multi-Resource Architecture

## Overview

Deploy multiple interdependent AWS resources across environments using modules and workspaces. This demonstrates a real-world scenario where infrastructure is modular, environment-aware, and maintainable.

## Code Example

Assume modules exist for VPC, EC2, RDS, and S3. The root module combines them using workspace-specific configurations.

Root `main.tf` example:

    module "vpc" {
      source = "./modules/vpc"
      cidr_block = "10.0.0.0/16"
    }

    module "s3_bucket" {
      source      = "./modules/s3_bucket"
      bucket_name = "terraform-demo-${terraform.workspace}-bucket"
    }

    module "ec2_instance" {
      source                = "./modules/ec2_instance"
      instance_type         = "t2.micro"
      ami                   = "ami-0c55b159cbfafe1f0"
      vpc_security_group_ids = [module.vpc.default_sg_id]
      depends_on            = [module.s3_bucket]
    }

    module "rds_instance" {
      source      = "./modules/rds"
      db_name     = "appdb"
      username    = "admin"
      password    = "P@ssw0rd123"
      subnet_ids  = module.vpc.private_subnets
      depends_on  = [module.vpc]
    }

Commands:

    terraform init
    terraform workspace new dev
    terraform workspace select dev
    terraform apply
    terraform workspace select prod
    terraform apply

## Expected Output

* Full AWS architecture deployed per workspace/environment
* Modules deployed in correct dependency order
* Outputs display resource IDs, ARNs, and environment-specific references
* `terraform state list` shows all resources and module instances

## Insights

* **Why this demo exists:** Provides a realistic multi-resource deployment scenario combining modules, variables, and workspaces.
* **Key points:** Properly structuring modules, using workspace-aware variables, and managing dependencies ensures maintainable and repeatable infrastructure.
* **Common mistakes / pitfalls:** Misconfigured dependencies, resource naming conflicts, hardcoding values instead of using variables or workspace interpolation.
* **Reflection / next steps:** Expand with additional AWS services (IAM, CloudWatch, Lambda); integrate with CI/CD pipelines for automated multi-environment deployments.
