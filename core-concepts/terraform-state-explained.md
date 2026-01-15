# Terraform State Explained

Terraform uses something called **state** to understand what infrastructure
exists and how it relates to your configuration.

If you don’t understand Terraform state, Terraform will often feel confusing,
dangerous, or unpredictable.

This document explains **what Terraform state is, who creates it, why it exists,
when it changes, and how it’s used**, before you run your first real demo.

---

## What Is Terraform State?

Terraform state is Terraform’s **memory**.

It is how Terraform knows:

- What resources already exist
- What Terraform created
- How real infrastructure maps to your code

Without state, Terraform would have no idea whether it needs to:

- Create something new
- Update something existing
- Leave something alone

---

## Who Creates and Owns the State File?

Terraform state is created and maintained by **Terraform itself**.

- Humans **do not write** state files
- Humans **do not edit** state files
- Terraform is the only system that should manage state

You influence state **indirectly** by:

- Writing configuration (`.tf` files)
- Running Terraform commands (`apply`, `import`, etc.)

Terraform then observes real infrastructure and records the result in state.

State is Terraform’s **record of reality**, not your intent.

---

## Why Terraform Needs State

Terraform is declarative. You describe **what you want**, not **how to do it**.

To figure out *what to change*, Terraform compares:

1. Your configuration (`.tf` files)
2. The current state (what Terraform last recorded)
3. The real infrastructure (what actually exists)

State is the bridge between your code and the real world.

---

## When and How State Files Are Created

Terraform creates or updates state during these operations:

- `terraform apply` → records what was created or changed
- `terraform import` → records existing infrastructure
- `terraform refresh` → updates state from real infrastructure
- `terraform state` commands → manipulate state safely

State is updated **only after Terraform confirms reality**.

Terraform never guesses — it observes.

---

## Local State vs Remote State

### Local State

By default, Terraform stores state locally in:

```
terraform.tfstate
```

Local state is:

- Simple
- Easy to inspect
- Ideal for learning and solo work

This repo intentionally starts with local state.

---

### Remote State

In team or production environments, state is stored remotely (for example in S3).

Remote state:

- Enables collaboration
- Prevents concurrent changes
- Adds locking and safety controls

Remote state is introduced later, once the mental model is solid.

---

## A Concrete Example of a Terraform State File

Below is a **simplified example** of a Terraform state file after creating
a single AWS EC2 instance.

> Real state files are larger and may contain sensitive data.

```json
{
  "version": 4,
  "terraform_version": "1.6.0",
  "serial": 3,
  "lineage": "9c2e1d6b-8f9a-4d8b-a8a5-2f4b3c1a9e12",
  "outputs": {},
  "resources": [
    {
      "mode": "managed",
      "type": "aws_instance",
      "name": "example",
      "provider": "provider[\"registry.terraform.io/hashicorp/aws\"]",
      "instances": [
        {
          "schema_version": 1,
          "attributes": {
            "id": "i-0abc1234def567890",
            "ami": "ami-0a123456789abcdef",
            "instance_type": "t3.micro",
            "availability_zone": "us-east-1a",
            "private_ip": "10.0.1.25",
            "tags": {
              "Name": "terraform-example"
            }
          }
        }
      ]
    }
  ]
}
```

---

## How to Read This State File

### Metadata

- **version** – internal state format
- **terraform_version** – last Terraform version used
- **serial** – increments on every state change
- **lineage** – unique identity for this state’s history

### Resources

The `resources` section records **real infrastructure**.

- Resource type and name map directly to your `.tf` code
- Provider shows who manages it
- Attributes store observed reality (IDs, IPs, metadata)

This is how Terraform knows *what already exists*.

---

## Different State Scenarios You Will Encounter

- **New project** → state starts empty, grows over time
- **Changed configuration** → state updates after apply
- **Deleted resource** → state removes the entry
- **Imported resource** → state records pre-existing infra
- **Drift detected** → state differs from reality until refreshed

Understanding these scenarios prevents fear and surprises.

---

## Why State Must Be Protected

State may contain:

- Resource IDs
- Infrastructure topology
- Sensitive values

If state is:

- Deleted → Terraform may recreate everything
- Modified → Terraform may destroy the wrong resources
- Committed to Git → secrets may leak

This is why state is usually:

- Ignored by Git
- Stored remotely in real projects
- Locked during changes

---

## Key Takeaways

- Terraform state is Terraform’s source of truth
- Terraform creates and owns the state file
- State records reality, not intent
- Humans never edit state manually
- Understanding state makes Terraform predictable

---

## What to Do Next

Proceed to **Phase 0 – Setup & Orientation** and observe how Terraform
creates and updates state as you run your first commands.
