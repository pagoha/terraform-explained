# Why Terraform Modules Exist

Terraform modules are **reusable building blocks** for your infrastructure.
They help you organize, simplify, and standardize infrastructure code.

Understanding modules before you create them ensures that your infrastructure remains maintainable, scalable, and consistent.

> Read this first, so you know why the Phase 4 demos use modules.

---

## What Is a Module?

A module is a container for multiple resources that are used together.

- Every `.tf` file is technically part of a module
- The **root module** is the main folder of your configuration
- **Child modules** are reusable subdirectories called by the root module

Modules help:

- Reduce code repetition
- Encapsulate complexity
- Promote best practices

---

## Built-in vs Custom Modules

### Built-in Modules

- Modules that come from Terraform Registry
- Pre-built for common patterns, e.g., VPC, S3 bucket

### Custom Modules

- Created by you to standardize infrastructure
- Can be reused across projects or environments
- Stored in local folders or remote repositories

---

## Why Modules Exist

1. **Reusability**
   Avoid duplicating the same code across multiple environments or projects.

2. **Abstraction**
   Hide complex resource setups behind a simple interface with variables and outputs.

3. **Consistency**
   Standardize how resources are created and configured.

4. **Maintainability**
   Updates to a module automatically propagate to all places it’s used.

---

## Anatomy of a Module

A typical module folder contains:

```text
my-module/
  main.tf        # resources
  variables.tf   # input variables
  outputs.tf     # output values
  README.md      # explanation
```

> This structure helps learners and teams understand what a module does without digging through every resource.

---

## Using a Module

In the root module:

```hcl
module "example_bucket" {
  source = "./my-module"
  bucket_name = "my-unique-bucket"
}
```

- `source` points to the module location
- Inputs are passed as variables
- Outputs can be used elsewhere

---

## Common Mistakes with Modules

```text
- Not using modules for repeated patterns
- Hardcoding values inside modules instead of using variables
- Making modules too complex (violates clarity)
- Ignoring documentation for inputs/outputs
```

---

## How This Repo Uses Modules

Phase 4 demos introduce modules gradually:

```text
1. Start with simple reusable modules
2. Add variables and outputs
3. Combine multiple modules
4. Highlight best practices
```

This approach ensures learners understand **why** each module exists and **how** to use it safely.

---

## Key Takeaways

```text
- Modules are reusable, maintainable, and scalable building blocks
- They help reduce code duplication and enforce consistency
- Always use variables and outputs to make modules flexible
- Documentation within modules improves clarity for teams
```
