# 0-2 Configure AWS

## Overview

Configure AWS credentials so Terraform can manage AWS resources.
This demo includes creating a working folder (if not done already) and verifying credentials.

## Steps

### 1. Navigate to your Terraform Working Folder

**Windows (PowerShell):**

```powershell
cd C:\TerraformProjects
```

**macOS / Linux (Terminal):**

```bash
cd ~/TerraformProjects
```

---

### 2. Configure AWS Credentials

Run the AWS CLI configure command:

```bash
aws configure
```

You will be prompted for:

* AWS Access Key ID
* AWS Secret Access Key
* Default region name (e.g., `us-east-1`)
* Default output format (e.g., `json`)

**Tip:** For learning, use an IAM user with limited permissions. Do **not** use root account credentials.

---

### 3. Verify Configuration

**List your S3 buckets** to confirm credentials work:

```bash
aws s3 ls
```

Expected output:

```
2026-01-01 example-bucket
2026-01-02 my-other-bucket
```

**Credential files created:**

- Windows: `%UserProfile%\.aws\credentials` and `%UserProfile%\.aws\config`
- macOS/Linux: `~/.aws/credentials` and `~/.aws/config`

---

## Insights

* **Why this demo exists:** Terraform requires valid AWS credentials to create and manage resources.
* **Key points:**
  - Use IAM users with limited permissions
  - Set the correct default region (`us-east-1` for these demos)
* **Common mistakes / pitfalls:**
  - Misconfiguring the region
  - Forgetting to set credentials
  - Incorrect file permissions
* **Reflection / next steps:**
  - Test with `aws s3 ls` to ensure credentials are valid. Once verified, you’re ready for the Terraform workflow demo (`0-3 Terraform Workflow`).
