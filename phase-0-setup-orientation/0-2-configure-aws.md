# 0-2 Configure AWS

## Overview

Configure AWS credentials so Terraform can manage AWS resources.

## Code Example

```bash
aws configure
```

You will be prompted for:

* AWS Access Key ID
* AWS Secret Access Key
* Default region name (e.g., us-east-1)
* Default output format (e.g., json)

## Expected Output

* Credentials saved in `~/.aws/credentials`
* Configuration in `~/.aws/config`

## Insights

* **Why this demo exists:** Terraform requires AWS credentials to create resources.
* **Key points:** Use IAM user with limited permissions for learning; never use root account credentials.
* **Common mistakes / pitfalls:** Misconfiguring region; forgetting to set credentials; credentials file permissions issues.
* **Reflection / next steps:** Test with `aws s3 ls` to ensure credentials are valid. Ready for Terraform workflow demo.
