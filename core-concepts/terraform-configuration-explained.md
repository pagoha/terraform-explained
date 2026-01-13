# Terraform Configuration Explained

Terraform configuration files (`.tf`) define **what you want your infrastructure to look like**.

They represent **desired intent**, not execution steps or recorded reality.

If Terraform state is Terraform’s **memory**, configuration files are Terraform’s **instructions**.

---

## What Is Terraform Configuration?

Terraform configuration is a collection of `.tf` files in a directory that describe:

- What infrastructure should exist
- How resources relate to each other
- What values are configurable
- What information should be exposed as outputs

Terraform does **not** run files sequentially.

Instead, it:
- Loads *all* `.tf` files in a directory
- Merges them into a single configuration
- Uses that configuration to calculate changes

> **Mental model:** Terraform loads a configuration — it does not execute scripts.

---

## What Lives in Configuration Files

Configuration may include:

- `resource` — infrastructure to create or manage
- `variable` — inputs for flexibility
- `output` — exposed values
- `provider` — API configuration (AWS, etc.)
- `terraform` — versions and backends
- `data` — read-only references
- `locals` — computed reuse values
- `module` — reusable configuration units

These blocks describe **intent**, not outcomes.

---

## What Does *Not* Belong in Configuration

Configuration should never contain:

- Resource IDs
- Execution history
- Dependency ordering logic
- Manual timing assumptions
- State data

Those belong to **state**, not configuration.

---

## Configuration vs State

| Configuration (`.tf`) | State (`.tfstate`) |
|----------------------|-------------------|
| Desired intent | Recorded reality |
| Human-written | Machine-managed |
| Safe to edit | Never edit manually |
| Version controlled | Never committed |
| Describes what *should exist* | Tracks what *does exist* |

You change infrastructure by changing **configuration**, not state.

---

## How Terraform Uses Configuration

- **`terraform init`**  
  Validates configuration, downloads providers/modules

- **`terraform plan`**  
  Compares configuration to state and reality

- **`terraform apply`**  
  Uses configuration as instructions and updates state

Configuration is always the **source of intent**.

---

## File Names and Layout

Terraform ignores file names.

These are equivalent:
- `main.tf`
- `network.tf`
- `ec2.tf`

Terraform loads **all `.tf` files in the directory** as one configuration.

What matters:
- Directory boundaries (modules)
- Clear separation of concerns
- Readability for humans

---

## Simple Configuration Example

```hcl
provider "aws" {
  region = "us-east-1"
}

variable "bucket_name" {
  description = "Name of the S3 bucket"
  type        = string
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
}

output "bucket_name" {
  value = aws_s3_bucket.example.bucket
}
```

This configuration:
- Declares intent
- Contains no state
- Is safe to commit
- Is reusable

---

## Common Configuration Mistakes

- Thinking file order matters
- Treating Terraform like a script
- Editing state instead of configuration
- Hardcoding values instead of using variables
- Expecting Terraform to infer intent

Terraform reacts to **configuration changes only**.

---

## Key Takeaways

- Configuration defines desired infrastructure
- Terraform loads all `.tf` files together
- Configuration is safe to edit and version control
- State is never edited manually
- Understanding configuration removes Terraform “magic”

---

## What to Do Next

After reading this document:

1. Continue with **Phase 0 – Setup & Orientation**
2. Pair this document with **Terraform State Explained**
3. Observe how configuration changes affect plans and state

As Terraform becomes more complex, always return to this mental model:
**Configuration defines intent. State records reality.**
