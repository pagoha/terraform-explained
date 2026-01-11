# 0-1 Install Terraform

## Overview

This demo guides learners to **install Terraform** on their machine and verify that it is set up correctly. The instructions are OS-specific and include a step to create a dedicated working folder for Terraform projects.

## Steps

### 1. Create a Working Folder

Choose a location on your computer where you will store all Terraform configurations. For example:

**Windows (PowerShell):**

```powershell
mkdir C:\TerraformProjects
cd C:\TerraformProjects
```

**macOS / Linux (Terminal):**

```bash
mkdir -p ~/TerraformProjects
cd ~/TerraformProjects
```

This ensures all Terraform files are organized in a single location.

---

### 2. Install Terraform

#### macOS (Homebrew)

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
terraform -version
```

#### Windows (Chocolatey)

```powershell
choco install terraform
terraform -version
```

#### Linux (apt)

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
sudo apt-add-repository "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
terraform -version
```

---

## Expected Output

* Terraform version prints in terminal, e.g.:

```
Terraform v1.7.3
on darwin_amd64
```

* Confirms Terraform is installed, executable, and your working folder is ready for projects.

---

## Insights

* **Why this demo exists:** You cannot use Terraform without installing it. Ensures a consistent environment for future demos.
* **Key points:** Installation steps vary by OS. Make sure Terraform is **added to PATH**.
* **Common mistakes / pitfalls:**
  - Forgetting to add Terraform to PATH
  - Using outdated versions that may not support certain features
  - Not verifying installation before proceeding
  - Forgetting to navigate to a dedicated working folder
* **Reflection / next steps:**
  - Verify installation in PowerShell, terminal, or shell. Once confirmed, proceed to configure AWS credentials.
