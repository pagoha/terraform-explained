# Common Terraform Mistakes

This document highlights **frequent mistakes in Terraform** and how to avoid them. Use it as a quick reference for best practices.

---

## 1. Hardcoding Values

**Problem:**
Embedding values directly in your configuration (like AMI IDs, regions, or passwords) makes your code **less portable and harder to maintain**.

**Example of a mistake:**

```hcl
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

**Better approach:** Use **variables** or **data sources**:

```hcl
variable "ami_id" {
  type        = string
  description = "AMI ID for the web server"
}

resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = "t2.micro"
}
```

---

## 2. Ignoring State Management

**Problem:**
Not using **remote state** can cause conflicts when multiple people work on the same infrastructure.

**Mistakes:**

- Using only local state (`terraform.tfstate`)
- Not locking state during operations

**Best Practice:**

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "global/s3/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

---

## 3. Not Using `terraform fmt` or `terraform validate`

**Problem:**
Unformatted or invalid Terraform code that leads to errors and poor readability.

**Solution:**

```bash
terraform fmt -recursive
terraform validate
```

---

## 4. Overcomplicating Modules

**Problem:**
Creating modules for everything—even trivial resources—can add unnecessary complexity.

**Solution:**

- Use modules **only when reusability is clear**
- Keep module inputs/outputs simple

---

## 5. Overwriting Managed Resources

**Problem:**
Changing resource attributes outside Terraform can lead to **drift** or accidental destruction.

**Example Mistake:**

- Editing EC2 instance tags directly in AWS
- Changing resource names managed by Terraform

**Solution:**

```hcl
resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = "t2.micro"

  lifecycle {
    prevent_destroy = true
  }
}
```

---

## 6. Forgetting Dependencies

**Problem:**
Resources created out of order because Terraform didn’t know about dependencies can cause errors.

**Solution:**

- Use **explicit dependencies** (`depends_on`) when needed
- Prefer Terraform's **implicit graph-based dependencies**:

```hcl
resource "aws_security_group" "web_sg" {
  name = "web_sg"
}

resource "aws_instance" "web" {
  ami                    = var.ami_id
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.web_sg.id]
}
```

---

## 7. Using `count` and `for_each` Incorrectly

**Problem:**
Mixing `count` and `for_each` on resources or modules can create **confusing outputs**.

**Solution:**

- Stick with one strategy per resource/module
- Use `for_each` when you need **keyed access**, `count` for simple lists

```hcl
variable "servers" {
  type = map(string)
  default = {
    app1 = "t2.micro"
    app2 = "t2.small"
  }
}

resource "aws_instance" "web" {
  for_each      = var.servers
  ami           = var.ami_id
  instance_type = each.value
}
```

---

## 8. Not Planning Changes

**Problem:**
Running `terraform apply` without checking changes can cause **unintended destruction or downtime**.

**Solution:**

```bash
terraform plan
```

- Review the plan carefully before applying changes
- Use `-target` cautiously if needed

---

## 9. Not Versioning Providers

**Problem:**
Terraform will use the **latest provider version** if not pinned, which can break your code.

**Solution:**

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

---

## 10. Ignoring Security Best Practices

**Problem:**
Sensitive data in code (like passwords, API keys, or secrets) can lead to **security breaches**.

**Solution:**

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

- Store secrets in **Vault, SSM, or environment variables**, not in code.

---

> 💡 **Pro Tip:** Regularly review your Terraform configurations and practices. Even small changes can prevent major headaches in production.
