# 1-3 Add Security Group

## Overview

Add a **security group (SG)** to control inbound and outbound traffic for an EC2 instance.
This demo shows how Terraform manages AWS networking resources safely.

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

**Tip:**
- In real environments, avoid `"0.0.0.0/0"` for SSH; restrict to your IP.
- This SG can be attached to EC2 instances in later demos.

---

### 3. Run Terraform Workflow

```bash
terraform init    # initialize working directory
terraform plan    # preview SG creation
terraform apply   # create the security group
terraform state list  # verify resource in state
terraform destroy # remove the security group
```

**Optional Verification with AWS CLI:**

```bash
aws ec2 describe-security-groups --group-names terraform-demo-sg --query 'SecurityGroups[*].[GroupId,GroupName,IpPermissions]' --output table
```

Expected output: Shows SG ID, name, and rules.

---

## Insights

* **Why this demo exists:** Shows how to secure resources and manage networking using Terraform.
* **Key points:**
  - `ingress` and `egress` blocks define traffic rules
  - Use restrictive CIDR blocks in production
* **Common mistakes / pitfalls:**
  - Leaving SSH open to the world (`0.0.0.0/0`)
  - Forgetting to destroy SG before EC2, which may block deletions
* **Reflection / next steps:**
  - Attach this SG to EC2 instances in later demos. Phase 1 will continue with DynamoDB and more complex resources.
