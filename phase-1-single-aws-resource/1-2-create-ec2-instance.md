# 1-2 Create EC2 Instance

## Overview

Deploy a **simple EC2 instance** using Terraform and understand how resources map to Terraform state.
This demo builds on the Phase 0 workflow and teaches basic AWS compute management.

---

## Steps

### 1. Navigate to Your Terraform Working Folder

**Windows (PowerShell):**

```powershell
cd C:\TerraformProjects
````

**macOS / Linux (Terminal):**

```bash
cd ~/TerraformProjects
```

---

### 2. Original Terraform Configuration File (Static AMI)

Create a file named `main.tf` with the following content:

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

**Note:** This AMI may **not exist in your region**, and running `terraform apply` with this file could result in:

```
Error: InvalidAMIID.NotFound: The image id '[ami-0c55b159cbfafe1f0]' does not exist
```

This shows why AMIs can differ by region and why dynamic lookups are useful.

---

### 3. Updated Terraform Configuration File (Dynamic AMI Lookup)

Create a second file named `main.tf` (or update the first) with the following content:

```hcl
provider "aws" {
  region = "us-east-1"
}

# Lookup the latest Amazon Linux 2 AMI in us-east-1
data "aws_ami" "amazon_linux_2" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

resource "aws_instance" "example" {
  ami           = data.aws_ami.amazon_linux_2.id
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformDemoInstance"
  }
}
```

This ensures the EC2 instance will use the latest Amazon Linux 2 AMI dynamically.

---

### 4. Run Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview EC2 instance creation
terraform apply   # create the EC2 instance
terraform state list  # verify resource in state
terraform destroy # terminate the EC2 instance
```

---

### 5. Optional Verification with AWS CLI

Check your EC2 instance status and tag:

**Windows (PowerShell):**

```powershell
aws ec2 describe-instances --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name,Type:InstanceType,AZ:Placement.AvailabilityZone}" --output table
```

**Linux / macOS (Terminal):**

```bash
aws ec2 describe-instances --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name,Type:InstanceType,AZ:Placement.AvailabilityZone}" --output table
```

Expected output for the dynamic AMI example:

| ID           | Name                  | State   | Type     | AZ         |
| ------------ | --------------------- | ------- | -------- | ---------- |
| i-0abcdef123 | TerraformDemoInstance | running | t2.micro | us-east-1a |

---

## Insights

* **Why this demo exists:** Introduces EC2 instances, Terraform state mapping, and AMI regional differences.
* **Key points:**

  * Original AMI may fail depending on your region
  * Using `data "aws_ami"` ensures you always get a valid, current AMI
  * `t2.micro` is free-tier eligible
* **Common mistakes / pitfalls:**

  * Using an AMI unavailable in your region
  * Forgetting to destroy the instance, which can incur AWS charges
* **Reflection / next steps:**

  * Learn how to associate a **security group** and **key pair** with this instance
  * Continue with Phase 1 demos to add networking and security resources
