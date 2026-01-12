# 4-4 Module Best Practices

## Overview

Learn **best practices for designing and structuring Terraform modules** to ensure reusability, clarity, and maintainability.

## Key Guidelines

* Keep modules **small and focused**—each module should do one thing well
* Use **variables** for all configurable options instead of hardcoding values
* Use **outputs** to expose useful information for the root module or other modules
* Avoid **hardcoding values**; allow flexibility for different environments
* Include a **README.md** inside each module explaining:
  - Purpose of the module
  - Variables and their defaults
  - Outputs
  - Example usage

## Insights

* **Why this demo exists:** Provides guidance for writing **clean, reusable, and maintainable Terraform modules**
* **Key points:** Consistent structure and documentation make modules easier to reuse and share
* **Common mistakes / pitfalls:** Overly large modules; missing outputs; hardcoded values
* **Reflection / next steps:** Apply these best practices in Phase 5 (Environments & Workspaces) and Phase 6 (Remote State & Collaboration)
