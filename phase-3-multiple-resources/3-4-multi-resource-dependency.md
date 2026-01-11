# 3-4 Multi-Resource Dependency

## Overview

Deploy multiple AWS resources together (S3, EC2, SG) demonstrating Terraform dependency graph.

## Code Example

`main.tf`:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-multi"
  acl    = "private"
}

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

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  vpc_security_group_ids = [aws_security_group.example_sg.id]

  depends_on = [aws_s3_bucket.example]

  tags = {
    Name = "MultiResourceEC2"
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

* Resources created in order: S3 → SG → EC2
* `terraform state list` shows all resources
* `terraform destroy` removes EC2 → SG → S3

## Insights

* **Why this demo exists:** Demonstrates complex dependency handling.
* **Key points:** Terraform builds resource graph; `depends_on` ensures explicit ordering.
* **Common mistakes / pitfalls:** Circular dependencies; misconfigured references.
* **Reflection / next steps:** Expand to modules and multiple environments in Phase 4/6.
