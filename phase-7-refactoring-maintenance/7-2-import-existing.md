# 7-2 Import Existing Resource

## Overview

Bring existing AWS resources under Terraform management safely, without recreating them.

## Code Example

Define the resource in Terraform to match the existing infrastructure:

    resource "aws_s3_bucket" "imported" {
      bucket = "existing-bucket-name"
    }

Import the existing resource into Terraform state:

    terraform import aws_s3_bucket.imported existing-bucket-name

Verify state list:

    terraform state list

Example output:

    aws_s3_bucket.imported

Plan and apply to confirm no unintended changes:

    terraform plan
    terraform apply

## Expected Output

* Existing resource added to Terraform state
* Terraform plan shows no changes
* Resource can now be managed with Terraform safely

## Insights

* **Why this demo exists:** Allows management of pre-existing infrastructure without disruption
* **Key points:** Importing does not modify resources; configuration must match existing resource
* **Common mistakes / pitfalls:** Resource name mismatches; forgetting to define matching configuration
