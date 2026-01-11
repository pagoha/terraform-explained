# Terraform State Explained

Terraform uses something called **state** to understand what infrastructure
exists and how it relates to your configuration.

If you don’t understand Terraform state, Terraform will often feel confusing,
dangerous, or unpredictable.

This document explains **what Terraform state is, why it exists, how it’s used,
and why it must be protected**, before you run your first real demo.

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

## What’s Inside the State?

Conceptually, Terraform state contains:
- Resource IDs (for example, AWS instance IDs)
- Resource attributes (names, regions, settings)
- Relationships between resources
- Metadata Terraform needs to make decisions

The state file is **not your infrastructure**, and it is **not your configuration**.

It is a **record of reality**.

---

## Why Terraform Needs State

Terraform is declarative. You describe **what you want**, not **how to do it**.

To figure out *what to change*, Terraform compares:
1. Your configuration (`.tf` files)
2. The current state (what Terraform last knew)
3. The real infrastructure (what actually exists)

State is the bridge between your code and the real world.

---

## Local State vs Remote State

### Local State

By default, Terraform stores state locally in a file called:

```
terraform.tfstate
```

This is what you will use at the beginning of this repo.

Local state is:
- Simple
- Easy to understand
- Perfect for learning and solo work

---

### Remote State

In team or production environments, state is stored remotely (for example in S3).

Remote state:
- Allows collaboration
- Prevents conflicts
- Protects critical infrastructure data

This repo introduces remote state **later**, once the fundamentals are clear.

---

## Why Terraform State Must Be Protected

Terraform state often contains:
- Resource identifiers
- Infrastructure structure
- Potentially sensitive data

If state is:
- Deleted → Terraform may try to recreate everything
- Modified manually → Terraform may behave unpredictably
- Committed to Git → Sensitive data may leak

This is why:
- State files are usually **ignored by Git**
- Access to state is tightly controlled in real projects

---

## State Is Not Configuration

A very common mistake is confusing state with configuration.

| Configuration (`.tf`) | State (`.tfstate`) |
|----------------------|-------------------|
| Desired infrastructure | Recorded reality |
| Human-written          | Machine-managed |
| Safe to edit           | Never edit manually |

You change infrastructure by changing **configuration**, not state.

---

## Why This Repo Starts With Local State

This repository intentionally starts with:
- Local state
- Simple examples
- Safe resources

This allows you to:
- See how state changes
- Understand Terraform behavior
- Build confidence before adding complexity

Once the mental model is solid, remote state and collaboration are introduced.

---

## Key Takeaways

- Terraform state is Terraform’s source of truth
- State connects your code to real infrastructure
- State must be protected
- You do not edit state manually
- Understanding state makes Terraform predictable

---

## What to Do Next

After reading this document:
1. Proceed to **Phase 0 – Setup & Orientation**
2. Run your first Terraform commands
3. Observe how Terraform creates and updates state

As you progress through the demos, come back to this document whenever Terraform’s
behavior feels unclear — the answer is often in the state.
