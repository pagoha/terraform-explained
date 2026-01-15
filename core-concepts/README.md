# Core Terraform Concepts (Read First)

Welcome 👋

Before you start running Terraform demos, this section explains the **core concepts** that Terraform is built on.

You **do not need to memorize everything here**.

Instead, think of these documents as:

- A **mental map** for why Terraform behaves the way it does
- A **reference** you can return to when something feels confusing
- A way to understand *what problem Terraform is solving* before writing code

Many Terraform frustrations come from skipping this step.
This repo intentionally separates **concept understanding** from **hands-on demos** so learning feels clear, not overwhelming.

---

## How to Use This Section

### Recommended Approach

1. **Skim these documents once** before starting the demos
2. Start Phase 0 and Phase 1 demos
3. Come back here whenever something “clicks” or doesn’t make sense yet

Terraform rewards understanding *why* more than memorizing *how*.

---

## Reading Order (Suggested)

You can read these in order, but it’s okay to jump around.

---

### 1️⃣ Terraform State (Most Important)

📄 **[terraform-state-explained.md](terraform-state-explained.md)**

Terraform state is the **foundation** of everything Terraform does.

This document explains:

- What state is
- Why Terraform needs it
- Why losing or sharing state incorrectly causes problems
- The difference between local and remote state

👉 If Terraform ever feels “scary,” it’s usually a state issue.

---

### 2️⃣ Terraform Workflow: init → plan → apply

📄 **[terraform-init-plan-apply-explained.md](terraform-init-plan-apply-explained.md)**

This explains the **Terraform lifecycle**:

- What `terraform init` really does
- Why `terraform plan` exists
- Why you should never blindly run `terraform apply`

After reading this, Terraform stops feeling like magic and starts feeling predictable.

---

### 3️⃣ Providers and Versioning

📄 **[providers-and-versions-explained.md](providers-and-versions-explained.md)**

Terraform doesn’t create infrastructure by itself — providers do.

This document explains:

- What providers are
- Why version pinning matters
- How provider upgrades can break working code

This knowledge becomes critical as projects grow and teams collaborate.

---

### 4️⃣ Why Modules Exist

📄 **[why-modules-exist.md](why-modules-exist.md)**

Modules are often introduced too early and feel confusing.

This document explains:

- What modules really are
- When they help (and when they don’t)
- Why Terraform considers *every folder* a module
- How this repo introduces modules gradually in Phase 4

If modules ever feel “overkill,” this will explain why they exist.

---

### 5️⃣ Common Terraform Mistakes

📄 **[common-terraform-mistakes.md](common-terraform-mistakes.md)**

This is a **battle-tested checklist** of mistakes people make in real projects.

It covers:

- Hardcoding values
- Ignoring state and locking
- Overusing modules
- Forgetting `terraform plan`
- Provider version issues
- Security pitfalls

👉 Even experienced engineers revisit this list.

---

## How These Concepts Connect to the Demos

Each demo in this repo is intentionally designed to reinforce **one or more concepts** from this section.

As you move through the phases:

- Early demos reinforce **state** and **workflow**
- Middle phases reinforce **variables, outputs, and dependencies**
- Later phases reinforce **modules, refactoring, and collaboration**

If a demo ever feels confusing, come back here — the answer is almost always conceptual, not syntactic.

---

## Final Note to the Learner

Terraform is not hard — it’s **misunderstood**.

This repo exists to:

- Remove mystery
- Build correct mental models
- Help you deploy infrastructure **confidently and safely**

You don’t need to rush.
Understanding compounds quickly.

---

## Next Step

Once you’re comfortable with these ideas:
➡️ Go to **Phase 0 – Setup & Orientation** and start your first demo.

You’re ready.
