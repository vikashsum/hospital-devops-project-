# 🚀 Hospital DevOps Project

## 📌 Project Overview

This project demonstrates how to provision an Amazon EKS cluster using **Terraform Modules** with a **remote backend** (S3 + DynamoDB) and deploy the infrastructure through a **Jenkins CI/CD Pipeline**.

The project follows Infrastructure as Code (IaC) principles and can provision the complete AWS infrastructure with a single pipeline execution.

---

## 🏗 Architecture

```text
Developer
     │
     ▼
GitHub Repository
     │
     ▼
Jenkins Pipeline
     │
     ▼
Terraform
     │
     ▼
AWS
├── VPC
├── IAM
├── EKS
├── ALB
└── ECR
     │
     ▼
Kubernetes
     │
     ▼
Application
```

---

## 📂 Project Structure

```text
hospital-devops-project-
│
├── Jenkinsfile
├── kubernetes
│   ├── deployment.yaml
│   ├── service.yaml
│   └── namespace.yaml
│
└── terraform
    ├── backend
    │   └── dev.hcl
    │
    ├── envs
    │   └── dev
    │       ├── main.tf
    │       ├── variables.tf
    │       ├── outputs.tf
    │       ├── providers.tf
    │       ├── versions.tf
    │       └── dev.tfvars
    │
    └── modules
        ├── vpc
        ├── iam
        ├── eks
        ├── alb
        ├── ecr
        └── jenkins
```

---

## ⚙️ Technologies Used

- Terraform
- AWS
- Amazon EKS
- Amazon VPC
- Amazon IAM
- Amazon ECR
- Amazon ALB
- Amazon S3
- DynamoDB
- Jenkins
- Kubernetes
- Git & GitHub
