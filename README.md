# 🚀 aws-eks-terraform-jenkins project

## 📌 Project Overview

This project demonstrates how to provision an **Amazon EKS (Elastic Kubernetes Service)** cluster using **Terraform Modules**, automate the infrastructure deployment with a **Jenkins CI/CD Pipeline**, and deploy applications to Kubernetes.

The project follows Infrastructure as Code (IaC) principles and provisions AWS infrastructure in a repeatable and automated manner.

---

# 🎯 Project Objectives

The primary goals of this project are:

- Provision AWS infrastructure using Terraform
- Organize Terraform code using reusable modules
- Store Terraform state remotely using Amazon S3
- Enable state locking using DynamoDB
- Automate Terraform deployment through Jenkins
- Create an Amazon EKS Cluster
- Deploy Kubernetes resources to the EKS cluster
- Follow DevOps best practices for Infrastructure as Code

---

# 🏗️ Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ├── Terraform fmt
    ├── Terraform validate
    ├── Terraform init
    ├── Terraform plan
    ├── Manual Approval
    └── Terraform apply
           │
           ▼
         AWS
         ├── VPC
         ├── IAM
         ├── Amazon EKS
         ├── Amazon ECR
         ├── Application Load Balancer
         └── S3 Backend + DynamoDB Lock
                │
                ▼
      aws eks update-kubeconfig
                │
                ▼
           Kubernetes Cluster
                │
                ▼
          Deploy Application
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|------------|---------|
| AWS | Cloud Platform |
| Terraform | Infrastructure as Code |
| Jenkins | CI/CD Pipeline |
| Amazon EKS | Kubernetes Cluster |
| Kubernetes | Container Orchestration |
| Amazon ECR | Container Image Registry |
| Amazon S3 | Terraform Remote Backend |
| DynamoDB | Terraform State Locking |
| Git | Version Control |
| GitHub | Source Code Repository |

---

# 📁 Project Structure

```text
hospital-devops-project
│
├── Jenkinsfile
├── kubernetes
│   ├── namespace.yaml
│   ├── deployment.yaml
│   └── service.yaml
│
└── terraform
    ├── backend
    │   └── dev.hcl
    │
    ├── modules
    │   ├── vpc
    │   ├── iam
    │   ├── eks
    │   ├── ecr
    │   ├── alb
    │   └── jenkins
    │
    ├── main.tf
    ├── providers.tf
    ├── variables.tf
    ├── outputs.tf
    ├── versions.tf
    └── dev.tfvars
```

---

# 📦 Terraform Modules

This project uses reusable Terraform modules.

| Module | Purpose |
|---------|---------|
| vpc | Creates VPC, Subnets, Internet Gateway, NAT Gateway and Route Tables |
| iam | Creates IAM Roles and Policies required by EKS |
| eks | Creates the Amazon EKS Cluster and Managed Node Group |
| ecr | Creates an Amazon ECR Repository |
| alb | Creates an Application Load Balancer |
| jenkins | (Optional) Creates a Jenkins EC2 instance |

---

# 🔄 Jenkins Pipeline

The Jenkins pipeline automates the infrastructure deployment.

Pipeline stages:

1. Checkout
2. Terraform Format
3. Terraform Validate
4. Terraform Init
5. Terraform Plan
6. Manual Approval
7. Terraform Apply
8. Configure kubeconfig
9. Deploy Application to EKS

---

# 🚀 Deployment Workflow

1. Push code to GitHub.
2. Jenkins checks out the latest code.
3. Terraform validates the configuration.
4. Terraform initializes the backend.
5. Terraform generates an execution plan.
6. Manual approval is requested before applying changes.
7. Terraform provisions the AWS infrastructure.
8. Jenkins configures `kubectl` to connect to the EKS cluster.
9. Kubernetes manifests are applied to deploy the application.

---

# 📋 Prerequisites

- AWS Account
- AWS CLI
- Terraform
- Jenkins
- kubectl
- Git
- GitHub Repository
- S3 Bucket for Terraform State
- DynamoDB Table for State Locking

---

# ▶️ Running the Project Locally

```bash
cd terraform

terraform init -backend-config=backend/dev.hcl

terraform validate

terraform plan -var-file=dev.tfvars

terraform apply -var-file=dev.tfvars
```

---

# 🧹 Cleanup

To delete all AWS resources created by Terraform:

```bash
terraform destroy -var-file=dev.tfvars
```

---

# 📖 Documentation

Detailed documentation will be available in the `docs/` directory.

Examples:

- Project Overview
- Terraform Fundamentals
- Terraform Modules
- Terraform Backend
- Jenkins Pipeline
- Kubernetes
- Troubleshooting
- Interview Notes

---

# 👨‍💻 Author

**Vikash Suman**

DevOps | AWS | Terraform | Kubernetes | Jenkins

---

# ⭐ Future Enhancements

- Multi-environment support (dev, test, prod)
- GitHub Actions integration
- Terraform Cloud backend
- Helm-based Kubernetes deployments
- Monitoring with Prometheus and Grafana
- Logging with EFK/ELK Stack
- ArgoCD for GitOps deployments
