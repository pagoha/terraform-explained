![Terraform](https://img.shields.io/badge/Terraform-1.x-623CE4?logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Focused-FF9900?logo=amazon-aws&logoColor=white)
![Learning](https://img.shields.io/badge/Learning-Zero--to--Hero-blue)
![Infrastructure as Code](https://img.shields.io/badge/IaC-Best%20Practices-2ea44f)
![Status](https://img.shields.io/badge/Status-Stable-success)

# Terraform Explained – Complete Zero-to-Hero Guide

## Overview

This repository is designed to take a learner from **never having touched Terraform** to confidently deploying, maintaining, and scaling Terraform-managed AWS infrastructure. It includes **hands-on demos, best practices, and insights** for each stage.

The repository is organized into **phases**, each building on the previous, with optional advanced challenges for a complete zero-to-hero experience.

---

### Who This Repo Is For

- Beginners who want to learn Terraform from the ground up, without skipping foundational concepts
- Engineers who already know Terraform but want to strengthen mental models and best practices
- Anyone who wants to deploy infrastructure safely, predictably, and repeatably

---

## Read This First (Strongly Recommended)

Before starting the hands-on demos, review the **Core Terraform Concepts** section:

📘 **[`core-concepts/README.md`](core-concepts/README.md)**

This section explains the *mental models* Terraform is built on, including:

- What Terraform state is and why it matters
- How the `init → plan → apply` workflow actually works
- Providers, versioning, and why upgrades can be risky
- Why modules exist and when they help (or hurt)
- Common Terraform mistakes seen in real-world projects

You **do not need to memorize everything** in this section.

Instead:

- Skim it once before starting Phase 0
- Return to it whenever something feels confusing
- Use it as a reference as the demos become more advanced

This repository intentionally separates concept understanding from hands-on execution demos so learning Terraform feels clear, safe, and predictable — not overwhelming.

---

## Repository Structure

```
terraform-explained/
├─ README.md                  # Root guide and learning roadmap (this file)
├─ guiding-principles.md      # North Star principles for the repo
├─ core-concepts/
│  ├─ README.md               # Core Terraform mental models (read first)
│  ├─ terraform-state-explained.md
│  ├─ terraform-init-plan-apply-explained.md
│  ├─ providers-and-versions-explained.md
│  ├─ why-modules-exist.md
│  └─ common-terraform-mistakes.md
├─ phase-0-setup-orientation/
├─ phase-1-single-aws-resource/
├─ phase-2-variables-outputs/
├─ phase-3-multiple-resources/
├─ phase-4-modules-reusability/
├─ phase-5-environments-workspaces/
├─ phase-6-remote-state-collaboration/
├─ phase-7-refactoring-maintenance/
├─ phase-8-hero-challenges/
├─ .gitignore
├─ LICENSE
└─ assets/
   └─ terraform-zero-to-hero-roadmap.png
```

---

## Phase Roadmap

![Terraform Explained Zero-to-Hero Roadmap](assets/terraform-zero-to-hero-roadmap.png)

*Visual roadmap illustrating the sequential phases from setup to hero challenges.*

### Phase 0: Setup & Orientation

* Install Terraform CLI and AWS CLI
* Configure AWS credentials and profiles
* Learn Terraform workflow basics
* Deploy your first local resource safely

### Phase 1: Single AWS Resource

* Create and manage basic AWS resources: S3, EC2, Security Groups, DynamoDB
* Understand core resource configuration and lifecycle

### Phase 2: Variables & Outputs

* Learn Terraform variables, overrides, outputs, and types
* Begin parameterizing your infrastructure for reuse
* Understand how outputs expose resource information

### Phase 3: Multiple Resources & Dependencies

* Deploy interdependent resources in a controlled order
* Manage resource dependencies and data sources
* Understand Terraform’s dependency graph and `depends_on` usage

### Phase 4: Modules & Reusability

* Create and use Terraform modules to organize and reuse code
* Combine multiple modules for larger infrastructure
* Learn best practices for module design and maintainability

### Phase 5: Environments & Workspaces

* Use Terraform workspaces to separate dev, test, and prod environments
* Apply workspace-specific variables and outputs
* Combine modules with workspaces for safe, isolated deployments

### Phase 6: Remote State & Collaboration

* Store Terraform state remotely in S3 and lock with DynamoDB
* Enable safe multi-user collaboration with remote backends
* Apply remote state best practices for secure and maintainable infrastructure

### Phase 7: Refactoring & Maintenance (Advanced)

* Safely rename Terraform resources using `terraform state mv`
* Import existing AWS resources into Terraform state
* Clean up unused resources to maintain state hygiene
* Upgrade Terraform CLI and provider versions safely

### Phase 8: Capstone / Hero Challenges (Advanced)

* Deploy complex multi-resource architectures using modules and workspaces
* Integrate optional AWS features like IAM policies, CloudWatch, and Lambda
* Detect drift and handle failed applies or errors
* Implement CI/CD pipelines for automated, collaborative Terraform deployments
* Phase 8 serves as the **culmination of all prior phases**, providing advanced, real-world scenarios

---

## Learning Workflow

1. Start at **Phase 0** and progress sequentially.
2. Read **Overview** to understand the concept.
3. Run the **Code Example** in your AWS environment.
4. Compare results to **Expected Output**.
5. Reflect on **Insights** to understand key points, common pitfalls, and next steps.
6. Continue through all phases until you are confident managing Terraform professionally.

---

## Guiding Principles (North Star)

Refer to `guiding-principles.md`:

* Clarity over cleverness
* Mental models first
* Safe, incremental learning
* Insights in every demo
* Incremental, phased progression
* Forkable and reusable
* Beginner and experienced friendly

---

## Tools & Recommendations

* VS Code with Terraform & YAML extensions
* Terraform CLI (latest stable)
* AWS CLI configured with profiles
* Optional: cspell and markdownlint for documentation quality

---

## Contributing

* Follow the **phase and insights structure**
* Keep file naming consistent (lowercase with hyphens)
* Maintain clarity and safety in demos
* Add insights for every new demo

---

This repository provides a **complete, structured, hands-on path** to learning Terraform on AWS. By following the phased demos, insights, and best practices, learners progress from beginner concepts to advanced, multi-environment, production-ready deployments.

Throughout the journey, the **Core Concepts** section remains an essential reference for understanding *why* Terraform behaves the way it does — helping learners make confident, informed decisions rather than just memorizing commands.

Made with ❤️ by [pagoha]
