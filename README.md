# 30 Days of Terraform

![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)

> A 30-day systematic journey through Infrastructure as Code and Terraform

[📝 Blog Series](#) • [📂 Code Examples](./Day-01) • [🚀 Quick Start](#quick-start)

---

## Progress

| Day | Topic | Status | Links |
|-----|-------|--------|-------|
| **01** | IaC & Terraform Fundamentals | ✅ | [Blog](#) • [Code](./Day-01) |
| **02** | First Configuration & Providers | ⏳ | Coming Soon |
| **03** | Resources & State | ⏳ | Coming Soon |
| **04** | Variables & Outputs | ⏳ | Coming Soon |
| **05** | Modules | ⏳ | Coming Soon |
| ... | ... | ... | ... |
| **30** | Production Architecture | ⏳ | Coming Soon |

---

## Day 01: Introduction to IaC & Terraform

**Full Blog Post:** [Day 01: Terraform — The Foundation of Modern Infrastructure](#)

### What is Infrastructure as Code?

Traditional cloud setup means clicking through consoles, copying settings, and hoping you remember what you did. IaC treats infrastructure like software—written in code, version-controlled, and reproducible.

**Why it matters:**
- **Consistency** → Same infrastructure every time
- **Speed** → Deploy in seconds, not hours
- **Reliability** → No manual errors
- **Scalability** → 1 resource or 1,000, same effort

### How Terraform Works

Terraform uses `.tf` files written in HCL (HashiCorp Configuration Language) to define infrastructure.

**The Workflow:**

```bash
terraform init      # Initialize and download providers
terraform plan      # Preview what will change
terraform apply     # Create/update resources
terraform destroy   # Clean up everything
```

Behind the scenes, Terraform talks to cloud APIs (AWS, Azure, GCP) to provision your infrastructure exactly as defined.

### Installation

**macOS**
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

**Linux**
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```

**Verify:**
```bash
terraform version
```

---

## Quick Start

```bash
# Clone repository
git clone https://github.com/Romxno/30-Days-of-Terraform.git
cd 30-Days-of-Terraform/Day-01

# Run Terraform
terraform init
terraform plan
terraform apply

# Clean up
terraform destroy
```

---

## Learning Path

**Week 1** → Foundations (IaC, providers, resources, state)  
**Week 2** → Core concepts (variables, modules, backends)  
**Week 3** → Advanced patterns (remote state, workspaces, functions)  
**Week 4** → Production (CI/CD, security, real-world projects)

---

## Important

⚠️ **Security:** Never commit `.tfvars` files or credentials  
💰 **Cost:** Always run `terraform destroy` after testing  
📝 **State:** Never manually edit `.tfstate` files

---

## Resources

- [Terraform Docs](https://developer.hashicorp.com/terraform/docs)
- [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Best Practices](https://www.terraform-best-practices.com/)

---

## Acknowledgments

**Piyush Sachdeva** • [#30DaysOfTerraform Challenge](https://github.com/piyushsachdeva/30DaysOfTerraform)  
**DevOps Community** • Continuous inspiration and support

---

<div align="center">

**[Shubham](https://github.com/Romxno)** • DevOps Engineer

📝 [Medium](#) • 💼 [LinkedIn](#)

**Day 1/30** ✅ • *Learning infrastructure the modern way*

</div> 