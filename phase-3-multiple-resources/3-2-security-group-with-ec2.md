# 3-2 Security Group with EC2

## Overview

Attach a security group to an EC2 instance, demonstrating inter-resource relationships.

## Code Example

`main.tf`:

```hcl
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
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  vpc_security_group_ids = [aws_security_group.example_sg.id]

  tags = {
    Name = "EC2WithSG"
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

* Security group created, EC2 instance created with the SG attached
* Can SSH into instance if key pair is configured
* `terraform destroy` removes EC2 then SG

## Insights

* **Why this demo exists:** Demonstrates how resources can reference each other.
* **Key points:** `vpc_security_group_ids` links EC2 to SG; Terraform resolves dependencies automatically.
* **Common mistakes / pitfalls:** Forgetting `depends_on` when necessary; mismatched region or VPC.
* **Reflection / next steps:** Add multiple SGs or multiple EC2 instances sharing a SG.
