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
```

**macOS / Linux (Terminal):**

```bash
cd ~/TerraformProjects
```

---

### 2. Create Terraform Configuration File

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

**Tip:** Verify the AMI ID is available in your region. `t2.micro` is free-tier eligible.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview EC2 instance creation
terraform apply   # create the EC2 instance
terraform state list  # verify resource in state
terraform destroy # terminate the EC2 instance
```

**Optional Verification with AWS CLI:**

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,Tags]' --output table
```

Expected output: Shows the instance ID, state, and tags.

---

## Insights

* **Why this demo exists:** Introduces EC2 instances and shows Terraform state mapping.
* **Key points:**
  - Check AMI ID for your region
  - `t2.micro` is free-tier eligible
* **Common mistakes / pitfalls:**
  - Using an AMI unavailable in your region
  - Forgetting to destroy the instance, which can incur AWS charges
* **Reflection / next steps:**
  - Learn how to associate a **security group** and **key pair** with this instance. Continue with Phase 1 demos to add networking and security resources.
