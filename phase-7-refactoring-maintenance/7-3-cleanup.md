# 7-3 Cleanup

## Overview

Learn how to remove unused or obsolete resources from Terraform state safely, ensuring that your infrastructure and state remain aligned and drift-free.

## Code Example

List current resources in state:

    terraform state list

Example output:

    aws_s3_bucket.active_bucket
    aws_s3_bucket.unused
    aws_instance.example

Remove an unused resource from state:

    terraform state rm aws_s3_bucket.unused

Verify the updated state:

    terraform state list

Example updated output:

    aws_s3_bucket.active_bucket
    aws_instance.example

Plan and apply to confirm no unintended changes:

    terraform plan
    terraform apply

## Expected Output

* The unused resource (`aws_s3_bucket.unused`) is removed from Terraform state
* Terraform plan shows no pending changes for removed resources
* Active infrastructure remains unchanged
* State file reflects only current managed resources

## Insights

* **Why this demo exists:** Maintains a clean Terraform state and prevents configuration drift
* **Key points:**
  * Only remove resources that are truly unused or intentionally unmanaged
  * Removing from state does not delete the actual infrastructure unless explicitly applied
* **Common mistakes / pitfalls:**
  * Accidentally removing active resources from state
  * Forgetting to plan and verify changes after removal
* **Reflection / next steps:** Regularly audit Terraform state and remove obsolete resources to keep projects manageable
