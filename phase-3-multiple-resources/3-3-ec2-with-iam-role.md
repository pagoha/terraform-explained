# 3-3 EC2 Instance with IAM Role

## Overview

Attach an IAM role to an EC2 instance using an instance profile.
This demo introduces **IAM roles**, **instance profiles**, and how Terraform links permissions to compute resources.

## Code Example

Create a file named `main.tf`:

    provider "aws" {
      region = "us-east-1"
    }

    # IAM role that EC2 can assume
    resource "aws_iam_role" "example_role" {
      name = "terraform-demo-role-phase3"

      assume_role_policy = jsonencode({
        Version = "2012-10-17"
        Statement = [
          {
            Effect = "Allow"
            Action = "sts:AssumeRole"
            Principal = {
              Service = "ec2.amazonaws.com"
            }
          }
        ]
      })
    }

    # Instance profile required to attach the role to EC2
    resource "aws_iam_instance_profile" "example_profile" {
      name = "terraform-demo-profile-phase3"
      role = aws_iam_role.example_role.name
    }

    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 (us-east-1)
      instance_type = "t2.micro"

      # Attach IAM role via instance profile
      iam_instance_profile = aws_iam_instance_profile.example_profile.name

      tags = {
        Name = "EC2WithIAMRole"
      }
    }

Run the following commands from the same directory:

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* `terraform init` initializes the working directory
* `terraform plan` shows IAM role, instance profile, and EC2 instance
* `terraform apply`:
  * Creates the IAM role
  * Creates the instance profile
  * Launches the EC2 instance with the role attached
* `terraform state list` shows:
  * aws_iam_role.example_role
  * aws_iam_instance_profile.example_profile
  * aws_instance.example
* `terraform destroy` removes the EC2 instance, then the IAM resources

## Insights

* **Why this demo exists:** IAM roles are the safest way to grant AWS permissions to EC2 instances.
* **Key points:** EC2 cannot use a role directly; an instance profile is required.
* **Common mistakes / pitfalls:** Skipping the instance profile; assuming a role grants permissions without policies.
* **Reflection / next steps:** Attach an IAM policy and allow the EC2 instance to access S3 or DynamoDB.
