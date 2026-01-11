# Terraform init / plan / apply Explained

Terraform is powerful, but many beginners simply memorize commands:
`init`, `plan`, and `apply`.  
When you do that without understanding, mistakes and confusion happen quickly.

This document explains **what each command actually does**, why Terraform separates them, and how they work together to safely manage infrastructure.

> Read this first, before running any demo, so you understand *why* you are doing each step.

---

## Terraform’s Core Workflow

Terraform follows a deliberate workflow to ensure safety and predictability:

1. Initialize the working directory
2. Preview proposed changes
3. Apply approved changes

Separation is intentional — it prevents mistakes and ensures transparency.

---

## terraform init

### Purpose

`terraform init` prepares a directory to be used with Terraform.

It:
- Downloads required providers (like AWS)
- Configures backends (state storage)
- Prepares modules (if any)

> Terraform **cannot** run without initialization.

### What It Does Not Do

- Does **not** create resources
- Does **not** modify state
- Does **not** read variables yet

Think of `init` as **setting up your toolbox**, not building anything.

### When to Run

- First time in a directory
- After adding/changing providers
- After changing backend configuration
- After pulling code with new dependencies

---

## terraform plan

### Purpose

`terraform plan` previews what Terraform will do.

It:
- Reads your configuration (`.tf` files)
- Reads current state (`.tfstate`)
- Compares desired vs actual infrastructure
- Produces an **execution plan**

> No changes are made yet — this is a safe review step.

### Why It Matters

- Catch mistakes early
- Avoid accidental changes
- Share proposed changes with teammates

Professional workflows require **plan approval before apply**.

### What to Review

- Resources to be created, updated, or destroyed
- Unexpected replacements
- Changes you didn’t intend

---

## terraform apply

### Purpose

`terraform apply` executes the plan and makes changes real.

It:
- Creates, updates, or deletes resources
- Updates Terraform state
- Implements your configuration

> Only `apply` modifies infrastructure.

### Confirmation

By default, Terraform asks for confirmation to prevent accidental changes.  
In automation or CI/CD, this can be handled programmatically.

---

## terraform destroy

`terraform destroy` removes all resources managed by Terraform in the workspace.

- Uses planning logic to safely destroy
- Updates state accordingly
- Should be run intentionally and carefully

Destroying is **not inherently dangerous** — running it accidentally is.

---

## Why Terraform Separates init / plan / apply

Separation provides:

- **Safety**: no unintended infrastructure changes
- **Transparency**: clear review of proposed changes
- **Automation**: CI/CD pipelines can run plan and apply independently

Teams benefit from:
- Generating plans automatically
- Reviewing changes safely
- Applying changes consistently

---

## Common Beginner Mistakes

- Skipping `plan`
- Running `apply` without checking plan
- Assuming `init` creates infrastructure
- Ignoring destroy outputs
- Not connecting state changes back to configuration

> Terraform does exactly what you tell it to — even if you didn’t mean it.

---

## How This Repo Uses the Workflow

Each demo in this repo follows the workflow:

1. Initialize once (`init`)
2. Preview changes (`plan`)
3. Apply intentionally (`apply`)
4. Observe state updates

> Linking every step back to workflow ensures understanding before touching real resources.

---

## Key Takeaways

- `init` = prepare Terraform environment  
- `plan` = preview changes safely  
- `apply` = make changes real  
- Terraform’s workflow is **designed for predictability and safety**  

Understanding these commands will make the Phase 0 and Phase 1 demos click immediately.
