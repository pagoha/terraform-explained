# 8-2 Optional AWS Features

## Overview

Integrate optional AWS features such as IAM policies, CloudWatch alarms, and Lambda functions to enhance infrastructure automation, security, and observability.

## Code Example

Example root module additions for optional features:

    # IAM Policy module
    module "iam_policy" {
      source       = "./modules/iam_policy"
      policy_name  = "optional-ec2-access"
      description  = "Optional IAM policy for EC2 monitoring"
    }

    # CloudWatch Alarm for EC2 CPU
    module "cloudwatch_alarm" {
      source      = "./modules/cloudwatch_alarm"
      alarm_name  = "ec2-high-cpu-${terraform.workspace}"
      metric_name = "CPUUtilization"
      namespace   = "AWS/EC2"
      threshold   = 80
      evaluation_periods = 2
      period      = 300
      statistic   = "Average"
    }

    # Lambda function for automation
    module "lambda_function" {
      source       = "./modules/lambda_function"
      function_name = "auto-cleanup-${terraform.workspace}"
      handler       = "index.handler"
      runtime       = "nodejs18.x"
      s3_bucket     = module.s3_bucket.bucket_name
      s3_key        = "lambda-code.zip"
    }

Commands:

    terraform init
    terraform plan
    terraform apply

## Expected Output

* Optional features deployed successfully alongside core architecture
* IAM policies attached correctly
* CloudWatch alarms active and monitoring resources
* Lambda functions available for automation tasks
* `terraform state list` includes optional modules

## Insights

* **Why this demo exists:** Demonstrates how to safely add optional enhancements without affecting core infrastructure.
* **Key points:** Keep optional features modular and parameterized to avoid tightly coupling them to the main architecture.
* **Common mistakes / pitfalls:** Overcomplicating the core infrastructure; hardcoding resource names; not using workspaces for environment isolation.
* **Reflection / next steps:** Add additional optional modules (SNS notifications, S3 lifecycle rules, CloudTrail) while maintaining modularity and workspace-awareness.
