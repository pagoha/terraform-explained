# 7-3 Cleanup

## Overview

Remove unused resources and clean up state.

## Code Example

```bash
terraform state list
terraform state rm aws_s3_bucket.unused
terraform plan
terraform apply
```

## Expected Output

* Unused resources removed from state
* Infrastructure matches code

## Insights

* **Why this demo exists:** Maintain clean state and prevent drift.
* **Key points:** Only remove resources you truly intend to delete from state.
* **Common mistakes / pitfalls:** Accidentally removing active resources.
