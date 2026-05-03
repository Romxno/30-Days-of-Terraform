# Day 3: Creating Your First S3 Bucket
From writing a resource block to provisioning real infrastructure ~ your first full Terraform cycle

> Full Story: __[Read on Medium](#)__

---

## 📖 Overview

Welcome to Day 3 of **#30DaysOfAWSTerraform**! Yesterday, we explored Terraform Providers ~ the interpreters that let Terraform talk to AWS. Today, we take the next step and actually *create something real*. We'll provision our first AWS resource ~ an S3 bucket ~ and walk through the complete Terraform lifecycle from start to finish.

By the end of this day, you'll have gone from an empty folder to a live bucket in your AWS account, modified it, and cleanly destroyed it. All without touching the console.

---

## 🗂️ Setting Up Today's Workspace

Create a new folder for today's work. I'm using `Day-03`. Inside it, create a single file:

```
Day-03/
└── main.tf
```

Terraform isn't strict about filenames, but keeping it simple helps as your projects grow. We start with the familiar provider block ~ this tells Terraform we're working with AWS in the `ap-south-1` region.

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}
```

---

## 🪣 What is an S3 Bucket Resource Block?

Before writing code, it helps to understand how Terraform thinks about resources. Every piece of infrastructure you want Terraform to manage ~ an EC2 instance, a VPC, a database ~ is declared as a **resource block**.

Think of it like this:

> **Provider** = The interpreter between Terraform and AWS  
> **Resource Block** = The blueprint for a specific piece of infrastructure  
> **State File** = Terraform's memory of what it has already built

When you run `terraform apply`, Terraform reads your resource blocks, compares them against its state file, and calls the AWS API to make reality match your configuration. No manual clicks. No SDK code. Just HCL.

---

## ✍️ Writing the S3 Bucket Resource

The [Terraform AWS provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) tells us exactly which fields are required, which are optional, and how to safely customize resources. For today, we're following the "private bucket with tags" pattern.

Here's our complete `main.tf`:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "day3_bucket" {
  bucket = "arnab-day3-terraform"

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}
```

Breaking down the resource block:

| Part | What it means |
|------|---------------|
| `resource` | Keyword that opens a resource declaration |
| `"aws_s3_bucket"` | The resource type ~ tells Terraform this is an S3 bucket |
| `"day3_bucket"` | Internal Terraform label ~ used to reference this resource within your config |
| `bucket` | The actual bucket name in AWS ~ must be globally unique across all accounts and regions |
| `tags` | Key-value metadata to organise and identify your resources |

> 💡 **Note:** `"day3_bucket"` is only meaningful inside your Terraform code. It does not become the bucket name in AWS ~ that's what the `bucket` argument is for.

---

## 🚀 The Terraform Lifecycle

With the configuration saved, we're ready to let Terraform do the work. This four-command workflow is the foundation of everything you'll do with Terraform.

### 1 ~ Initialize

```bash
terraform init
```

Downloads the AWS provider plugin and prepares Terraform to communicate with AWS. Think of it as placing all the props on stage before a play begins. Run this once whenever you start a new project or add a new provider.

---

### 2 ~ Plan (Dry Run)

```bash
terraform plan
```

Terraform reads your configuration, checks its state file, and shows you exactly what it *will* do ~ without changing anything. You should see **1 resource to add**. This step is your safety net before any real changes happen.

---

### 3 ~ Apply (Create)

```bash
terraform apply
```

Terraform will prompt you for confirmation:

```
Do you want to perform these actions?
```

Type `yes` to create the bucket. To skip the prompt entirely:

```bash
terraform apply --auto-approve
```

After a few seconds, the bucket is live. Open **AWS Console → S3** and you'll see it listed. ✅

---

### 4 ~ Modify (Update)

Terraform makes updates just as easy as creation. Change the bucket name or update a tag in `main.tf`:

```hcl
tags = {
  Name        = "My bucket 2.0"
  Environment = "Dev"
}
```

Then run plan and apply again:

```bash
terraform plan   # shows: 0 to add, 1 to update
terraform apply
```

Terraform compares your new configuration against its state file and applies only what changed. No console work, no guesswork ~ just a predictable, controlled update.

---

### 5 ~ Destroy

```bash
terraform destroy
```

Terraform will confirm before removing resources:

```
Do you really want to destroy these resources?
```

Type `yes` and the bucket is gone in seconds. To skip the prompt:

```bash
terraform destroy --auto-approve
```

Gentle, predictable, and safe.

---

## 📋 Command Reference

| Command | Purpose |
|---------|---------|
| `terraform init` | Initialize provider plugins and backend |
| `terraform plan` | Preview changes ~ no resources are touched |
| `terraform apply` | Create or update resources |
| `terraform apply --auto-approve` | Apply without the confirmation prompt |
| `terraform destroy` | Remove all managed resources |
| `terraform destroy --auto-approve` | Destroy without the confirmation prompt |

---

## 💡 Key Concepts

- **Resource Block** ~ The fundamental building block in Terraform. Every AWS resource starts with `resource "type" "local_name" { }`.
- **State File** ~ Terraform stores infrastructure state in `terraform.tfstate`. It uses this to determine what needs to change on every plan and apply.
- **S3 Bucket Naming** ~ Names must be globally unique across all AWS accounts and all regions. Choose carefully.
- **Tags** ~ Always tag resources with at minimum `Name` and `Environment`. It makes cost tracking and resource management significantly easier as your infrastructure grows.

---

## 🎯 What's Next?

Day 3 gave us the full picture ~ writing a resource block, understanding the lifecycle, and completing a real provisioning cycle from scratch. In **Day 4**, we'll go deeper into Terraform concepts and start building more complex infrastructure on AWS.

---

## 📚 Resources

- [Terraform AWS S3 Bucket Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)
- [AWS S3 Bucket Naming Rules](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html)
- [Official Terraform Documentation](https://developer.hashicorp.com/terraform/docs)

---

*Part of the [#30DaysOfAWSTerraform](#) series*