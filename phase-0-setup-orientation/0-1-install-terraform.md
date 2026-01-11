# 0-1 Install Terraform

## Overview

This demo guides learners to install Terraform on their machine and verify that it is set up correctly.

## Code Example

Check Terraform version after installation:

```bash
terraform -version
```

## Expected Output

* Terraform version prints in terminal, e.g.:

```
Terraform v1.7.3
on darwin_amd64
```

* Confirms Terraform is installed and executable

## Insights

* **Why this demo exists:** You cannot use Terraform without installing it. This ensures a consistent environment for future demos.
* **Key points:** Installation steps vary by OS. For Windows, use the MSI installer or Chocolatey. For macOS, use Homebrew.
* **Common mistakes / pitfalls:** Forgetting to add Terraform to PATH; using outdated versions that may not support certain features.
* **Reflection / next steps:** Verify installation in PowerShell or terminal, then proceed to configure AWS credentials.
