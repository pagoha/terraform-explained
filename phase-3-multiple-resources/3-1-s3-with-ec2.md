# 3-1 S3 Bucket with EC2 Instance

## Overview

Deploy an EC2 instance that interacts with an S3 bucket, demonstrating dependencies between resources.

## Code Example

`main.tf`:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "example" {
  bucket = "terraform-demo-bucket-phase3"
  acl    = "private"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2
  instance_type = "t2.micro"

  tags = {
    Name = "EC2WithS3"
  }

  depends_on = [aws_s3_bucket.example]
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

* S3 bucket created first, EC2 instance created second
* `terraform state list` shows both resources
* `terraform destroy` removes EC2 first, then the bucket

## Insights

* **Why this demo exists:** Shows how to manage resource dependencies with `depends_on`.
* **Key points:** Terraform automatically handles many dependencies; explicit `depends_on` is sometimes required.
* **Common mistakes / pitfalls:** Circular dependencies; forgetting `depends_on` for ordering critical resources.
* **Reflection / next steps:** Experiment with additional resources like security groups or IAM roles.
