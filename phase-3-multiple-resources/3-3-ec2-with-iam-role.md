# 3-3 EC2 Instance with IAM Role

## Overview

Attach an IAM role to an EC2 instance to grant permissions to access AWS services.

## Code Example

`main.tf`:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_iam_role" "example_role" {
  name = "terraform-demo-role-phase3"

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      }
    ]
  })
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  iam_instance_profile = aws_iam_role.example_role.name

  tags = {
    Name = "EC2WithIAM"
  }
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

* IAM role created and attached to EC2
* EC2 instance can assume role permissions
* `terraform destroy` removes EC2 then IAM role

## Insights

* **Why this demo exists:** Shows how to integrate IAM with compute resources.
* **Key points:** Roles can provide temporary credentials; EC2 must use instance profile.
* **Common mistakes / pitfalls:** Using role name instead of instance profile; forgetting policies.
* **Reflection / next steps:** Use role to allow EC2 to interact with S3 or DynamoDB.
