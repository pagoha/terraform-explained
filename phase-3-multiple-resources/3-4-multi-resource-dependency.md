# 3-4 Multi-Resource Dependency

## Overview

Deploy multiple AWS resources together — **S3 bucket, Security Group, and EC2 instance** —
to demonstrate Terraform’s dependency graph and resource ordering.

## Code Example

Create `main.tf`:

    provider "aws" {
      region = "us-east-1"
    }

    # S3 bucket
    resource "aws_s3_bucket" "example" {
      bucket = "terraform-demo-bucket-multi"
      acl    = "private"
    }

    # Security group
    resource "aws_security_group" "example_sg" {
      name        = "terraform-demo-sg-multi"
      description = "Allow SSH inbound"

      ingress {
        from_port   = 22
        to_port     = 22
        protocol    = "tcp"
        cidr_blocks = ["0.0.0.0/0"]
      }

      egress {
        from_port   = 0
        to_port     = 0
        protocol    = "-1"
        cidr_blocks = ["0.0.0.0/0"]
      }
    }

    # EC2 instance referencing SG and depending on S3
    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2
      instance_type = "t2.micro"

      vpc_security_group_ids = [aws_security_group.example_sg.id]

      depends_on = [aws_s3_bucket.example]

      tags = {
        Name = "MultiResourceEC2"
      }
    }

Run the Terraform commands:

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* Resources created in order: S3 → Security Group → EC2
* `terraform state list` shows:
  - aws_s3_bucket.example
  - aws_security_group.example_sg
  - aws_instance.example
* `terraform destroy` removes EC2 → SG → S3

## Insights

* **Why this demo exists:** Demonstrates Terraform’s dependency graph and how multiple resources interact.
* **Key points:** Terraform automatically resolves most dependencies; `depends_on` is used for explicit ordering.
* **Common mistakes / pitfalls:** Circular dependencies, referencing resources before they exist, misconfigured IDs.
* **Reflection / next steps:** Combine multiple resources into modules, and later deploy in separate environments using workspaces (Phase 4/6).
