# GUIDING PRINCIPLES

This document defines the **North Star principles** for the `terraform-explained` repo.
It guides a clear, structured, zero-to-hero learning experience for Terraform on AWS.

---

## 1. Clarity Over Cleverness

* Every demo and explanation prioritizes **understanding first**.
* Avoid overly clever solutions that may confuse learners.

## 2. Mental Models First

* Explain concepts and reasoning **before code**.
* Learners should understand *why* Terraform behaves a certain way, not just *how* to run commands.

## 3. Safe, Incremental Learning

* Introduce **one major concept per demo**.
* AWS resources should be safe to create and destroy, minimizing risk.
* Failures are learning opportunities and noted in **Insights**.

## 4. Insights in Every Demo

Each demo includes an **Insights** section covering:

* **Why this demo exists** — the concept or problem being taught
* **Key points** — reasoning behind code choices
* **Common mistakes / pitfalls** — what could break or confuse
* **Reflection / next steps** — questions to explore and connect to future demos

## 5. Incremental, Phased Progression

* Learning is structured in **phases (0–8)**:

  0. Setup & Orientation
  1. Single AWS Resources
  2. Variables & Outputs
  3. Multiple Resources & Dependencies
  4. Modules & Reusability
  5. Environments & Workspaces
  6. Remote State & Collaboration
  7. Refactoring & Maintenance
  8. Hero Challenges / Optional Advanced

* Each phase builds on the previous, creating a **zero-to-hero journey**.

## 6. Forkable and Reusable

* The repo can be safely **forked, modified, and shared**.
* Learners and teams can adapt demos to their own projects.

## 7. Beginner and Experienced Friendly

* Beginners can follow along from the first demo.
* Experienced engineers gain value from **Insights**, safe examples, and best practices.

---

> **Summary:** Every file and demo in this repo should serve a clear purpose, teach concepts effectively, and be easy to follow — from someone new to Terraform to someone confidently deploying AWS infrastructure using Terraform.
