# 3-1 S3 Bucket and EC2 Instance (Resource Ordering)

## Overview

Create two AWS resources — an S3 bucket and an EC2 instance — and observe how Terraform controls the order in which resources are created and destroyed.

This demo focuses on **resource ordering and dependencies**, not permissions or data access.

## Code Example

Create a file named `main.tf`:

    provider "aws" {
      region = "us-east-1"
    }

    resource "aws_s3_bucket" "example" {
      bucket = "terraform-demo-bucket-phase3"
      acl    = "private"
    }

    resource "aws_instance" "example" {
      ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 (us-east-1)
      instance_type = "t2.micro"

      tags = {
        Name = "EC2WithS3"
      }

      # Force Terraform to create the S3 bucket first
      depends_on = [aws_s3_bucket.example]
    }

Run the following commands from the same directory:

    terraform init
    terraform plan
    terraform apply
    terraform destroy

## Expected Output

* `terraform init` initializes the working directory and downloads the AWS provider
* `terraform plan` shows two resources to be created
* `terraform apply`:
  * Creates the S3 bucket first
  * Creates the EC2 instance second
* `terraform state list` shows:
  * aws_s3_bucket.example
  * aws_instance.example
* `terraform destroy`:
  * Destroys the EC2 instance first
  * Destroys the S3 bucket second

## Insights

* **Why this demo exists:** Understanding creation and destruction order is critical when managing multiple resources.
* **Key points:** Terraform usually determines dependencies automatically; `depends_on` is used here to make the order explicit.
* **Common mistakes / pitfalls:** Assuming `depends_on` grants permissions; creating circular dependencies between resources.
* **Reflection / next steps:** Add a security group to the EC2 instance to introduce real relationships between resources.
