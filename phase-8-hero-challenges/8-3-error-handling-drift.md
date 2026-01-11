# 8-3 Error Handling & Drift

## Overview

Detect drift and handle failed applies or resource errors.

## Code Example

```bash
terraform plan
terraform refresh
terraform apply
terraform state list
```

## Expected Output

* Detects drift between state and actual resources
* Failed applies are safely retried

## Insights

* **Why this demo exists:** Prepare learners to manage real-world drift and errors.
* **Key points:** Regularly refresh state; use outputs for verification.
* **Common mistakes / pitfalls:** Ignoring drift; manual edits to state.
