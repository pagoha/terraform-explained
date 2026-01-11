# 1-3 Add Security Group

## Overview

Add a security group to control inbound and outbound traffic for an EC2 instance.

## Code Example

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_security_group" "example_sg" {
  name        = "terraform-demo-sg"
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

  tags = {
    Project = "TerraformExplained"
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

* Security group created with SSH inbound rule
* Can attach to EC2 instances in later demos
* `terraform destroy` removes the security group

## Insights

* **Why this demo exists:** Shows how to secure resources and configure networking.
* **Key points:** Ingress/egress blocks define rules; use restrictive CIDR for real environments.
* **Common mistakes / pitfalls:** Leaving 0.0.0.0/0 open in production; forgetting to destroy SG before EC2.
* **Reflection / next steps:** Learn how to attach this SG to EC2 instances in Phase 3.
