# Terraform Providers & Versions Explained

Terraform interacts with cloud platforms and other services through **providers**.
Providers are plugins that know how to create, read, update, and delete resources.

Understanding providers and versioning is critical so your Terraform runs reliably and safely.

> Read this first before running demos — it explains the bridge between Terraform and AWS.

---

## What Is a Provider?

A provider is a **plugin** that knows how to manage resources for a specific platform.

For example:

- `aws` → AWS resources
- `azurerm` → Azure resources
- `google` → GCP resources

Without a provider, Terraform cannot manage any infrastructure.

---

## Specifying Providers in Terraform

In your `.tf` configuration, providers are declared like this:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  required_version = ">= 1.5.0"
}
```

Explanation:

- `source`: Where Terraform should download the provider
- `version`: Which version of the provider to use
- `required_version`: Minimum Terraform version required

> Pinning versions ensures stability and predictable behavior.

---

## Why Provider Versions Matter

Providers change over time. New versions may:

- Add features
- Fix bugs
- Change default behavior

Without version constraints:

- Your configuration may break unexpectedly
- Terraform may behave differently on different machines
- Collaborators may see different results

---

## Installing Providers

Terraform automatically downloads required providers during `terraform init`.

- No manual installation is needed
- Provider binaries are stored in your system cache
- This ensures consistent versions across runs

---

## Checking Provider Versions

Run:

```bash
terraform providers
```

This shows:

- Providers used in your configuration
- Installed versions
- Source locations

---

## Common Mistakes

- Not specifying provider versions → breaks reproducibility
- Using outdated providers → may lack features or have bugs
- Committing provider binaries to Git → unnecessary and risky

---

## How This Repo Uses Providers

All demos in this repo:

- Use `aws` provider only
- Specify provider version to maintain consistency
- Ensure Terraform version compatibility

This keeps all examples safe and predictable for learners.

---

## Key Takeaways

- Terraform cannot manage resources without providers
- Always pin provider versions
- `terraform init` handles provider installation
- Checking providers helps ensure reproducibility
- This repo uses a single AWS provider for simplicity
