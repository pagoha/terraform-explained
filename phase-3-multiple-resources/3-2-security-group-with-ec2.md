# 3-2 Security Group with EC2 Instance

## Overview

Create a security group and attach it to an EC2 instance.
This demo shows how Terraform automatically understands **relationships between resources** when one resource references another.

## Code Example

Create a file named `main.tf`:

    provider "aws" {
      region = "us-east-1"
    }

    resource "aws_security_group" "example_sg" {
      name        = "terraform-demo-sg-phase3"
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

    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 (us-east-1)
      instance_type = "t2.micro"

      # Attach the security group to the EC2 instance
      vpc_security_group_ids = [aws_security_group.example_sg.id]

      tags = {
        Name = "EC2WithSecurityGroup"
      }
    }

Run the following commands from the same directory:

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* `terraform init` initializes the working directory
* `terraform plan` shows two resources to be created
* `terraform apply`:
  * Creates the security group
  * Creates the EC2 instance with the security group attached
* `terraform state list` shows:
  * aws_security_group.example_sg
  * aws_instance.example
* `terraform destroy`:
  * Destroys the EC2 instance first
  * Destroys the security group second

## Insights

* **Why this demo exists:** Shows how Terraform links resources together through references.
* **Key points:** Referencing another resource’s attribute automatically creates a dependency.
* **Common mistakes / pitfalls:** Assuming `depends_on` is always required; forgetting that security groups belong to a VPC.
* **Reflection / next steps:** Add multiple security groups or reuse one security group across multiple EC2 instances.
