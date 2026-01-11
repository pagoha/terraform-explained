# 1-2 Create EC2 Instance

## Overview

Deploy a simple EC2 instance and understand how Terraform maps AWS resources to state.

## Code Example

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2 (us-east-1)
  instance_type = "t2.micro"
  tags = {
    Name = "TerraformDemoInstance"
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

* `terraform plan` shows 1 EC2 instance to be created
* `terraform apply` creates the instance
* `terraform state list` shows `aws_instance.example`
* `terraform destroy` terminates the EC2 instance

## Insights

* **Why this demo exists:** Introduces EC2 instances and basic AWS compute management.
* **Key points:** Always check AMI ID for your region; t2.micro is free-tier eligible.
* **Common mistakes / pitfalls:** Using AMIs not available in your region; forgetting to destroy leads to charges.
* **Reflection / next steps:** Learn how to associate a security group and key pair with the instance.
