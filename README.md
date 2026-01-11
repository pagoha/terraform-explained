# Terraform Explained – Complete Zero-to-Hero Guide

## Overview

This repository is designed to take a learner from **never having touched Terraform** to being able to confidently deploy, maintain, and scale Terraform-managed AWS infrastructure. It includes **working demos, best practices, and insights** for each stage.

The repo is organized into **phases**, each building upon the previous, with optional advanced challenges for a complete zero-to-hero experience.

---

## Repository Structure

```
terraform-explained/
├─ README.md
├─ guiding-principles.md  # North Star principles
├─ phase-0-setup-orientation/
│  ├─ 0-1-install-terraform.md
│  ├─ 0-2-configure-aws.md
│  ├─ 0-3-terraform-workflow.md
│  └─ 0-4-first-local-resource.md
├─ phase-1-single-aws-resource/
│  ├─ 1-1-create-s3-bucket.md
│  ├─ 1-2-create-ec2-instance.md
│  ├─ 1-3-add-security-group.md
│  └─ 1-4-create-dynamodb-table.md
├─ phase-2-variables-outputs/
│  ├─ 2-1-variables-basics.md
│  ├─ 2-2-override-variables.md
│  ├─ 2-3-outputs-basics.md
│  └─ 2-4-variable-types.md
├─ phase-3-multiple-resources/
│  ├─ 3-1-s3-with-ec2.md
│  ├─ 3-2-security-group-with-ec2.md
│  ├─ 3-3-ec2-with-iam-role.md
│  └─ 3-4-multi-resource-dependency.md
├─ phase-4-modules-reusability/
│  ├─ 4-1-simple-module.md
│  ├─ 4-2-module-with-variables-outputs.md
│  ├─ 4-3-multiple-modules.md
│  └─ 4-4-module-best-practices.md
├─ phase-5-environments-workspaces/
│  ├─ 5-1-intro-to-workspaces.md
│  ├─ 5-2-workspace-variables.md
│  ├─ 5-3-workspaces-with-modules.md
│  └─ 5-4-workspace-best-practices.md
├─ phase-6-remote-state-collaboration/
│  ├─ 6-1-intro-remote-state.md
│  ├─ 6-2-backend-workspaces.md
│  ├─ 6-3-team-collaboration.md
│  └─ 6-4-remote-state-best-practices.md
├─ phase-7-refactoring-maintenance/
│  ├─ 7-1-rename-resource.md
│  ├─ 7-2-import-existing.md
│  ├─ 7-3-cleanup.md
│  └─ 7-4-version-upgrades.md
├─ phase-8-hero-challenges/
│  ├─ 8-1-multi-resource-architecture.md
│  ├─ 8-2-optional-aws-features.md
│  ├─ 8-3-error-handling-drift.md
│  └─ 8-4-terraform-ci-cd.md
├─ .gitignore
├─ LICENSE
└─ README.md
```

---

## Phase Roadmap

### Phase 0: Setup & Orientation

* Install Terraform and AWS CLI
* Configure AWS credentials
* Run your first local resource

### Phase 1: Single AWS Resource

* Create and manage basic AWS resources (S3, EC2, Security Groups, DynamoDB)

### Phase 2: Variables & Outputs

* Learn variables, overrides, output usage, and types
* Begin parameterizing infrastructure

### Phase 3: Multiple Resources & Dependencies

* Deploy interdependent resources
* Manage dependencies, data sources, and resource order

### Phase 4: Modules & Reusability

* Create and use modules
* Combine multiple modules for larger infra
* Learn module best practices

### Phase 5: Environments & Workspaces

* Use workspaces to separate dev/test/prod environments
* Apply workspace-specific variables and outputs
* Combine modules with workspaces for isolated deployments

### Phase 6: Remote State & Collaboration

* Store Terraform state remotely in S3 and lock with DynamoDB
* Enable safe multi-user collaboration
* Follow remote state best practices

### Phase 7: Refactoring & Maintenance (Advanced)

* Rename Terraform resources safely
* Import existing AWS resources into state
* Clean up unused resources
* Safely upgrade Terraform and provider versions

### Phase 8: Hero Challenges (Advanced)

* Deploy multi-resource architectures using modules and workspaces
* Integrate optional AWS features (IAM, CloudWatch, Lambda)
* Handle drift, errors, and failed applies
* Implement CI/CD pipelines for automated Terraform deployments

---

## Learning Workflow

1. Start at **Phase 0** and progress sequentially.
2. Read **Overview** to understand the concept.
3. Run the **Code Example** in your AWS environment.
4. Compare results to **Expected Output**.
5. Reflect on **Insights** to understand key points, common pitfalls, and next steps.
6. Advance through phases until confident managing Terraform professionally.

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
* Add Insights for every new demo

---

This repository provides a complete, structured, and hands-on path to learning Terraform on AWS. Follow the step-by-step demos and best practices to progress from beginner concepts to advanced multi-environment and production-ready deployments.
