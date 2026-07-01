# 🚀 Hospital DevOps Project

> End-to-End Infrastructure Automation using Terraform, Jenkins, Amazon EKS, Kubernetes and AWS

---

# 📖 Project Overview

This project demonstrates how a complete AWS infrastructure can be provisioned using **Infrastructure as Code (IaC)** with **Terraform**, automated using **Jenkins CI/CD**, and deployed onto **Amazon Elastic Kubernetes Service (EKS)**.

The repository follows real-world DevOps practices such as:

- Terraform Modules
- Remote State Backend
- State Locking
- Jenkins Pipeline
- Infrastructure Validation
- Infrastructure Planning
- Automated Infrastructure Provisioning
- Kubernetes Deployment

The entire infrastructure can be deployed by triggering a Jenkins pipeline without manually creating AWS resources.

---

# 🎯 Project Objectives

The objective of this project is to automate the provisioning of a production-style Kubernetes infrastructure.

Instead of manually creating AWS resources from the AWS Console, Terraform creates them automatically.

The Jenkins Pipeline automates the complete deployment process.

The infrastructure includes:

- Amazon VPC
- Public Subnets
- Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- IAM Roles
- Amazon EKS Cluster
- Managed Node Group
- Amazon ECR
- Application Load Balancer

---

# 🏗 High Level Architecture

```text
               Developer

                    │

                    ▼

            GitHub Repository

                    │

              Git Push / Webhook

                    │

                    ▼

             Jenkins Pipeline

                    │

      ┌─────────────┴──────────────┐

      │                            │

 Terraform Validate          Terraform Plan

      │

      ▼

 Terraform Apply

      │

      ▼

┌──────────────────────────────────────────────┐

│                    AWS                       │

│                                              │

│  VPC                                         │

│   ├── Public Subnets                         │

│   ├── Private Subnets                        │

│   ├── Internet Gateway                       │

│   ├── NAT Gateway                            │

│                                              │

│  IAM Roles                                   │

│  ECR Repository                              │

│  Amazon EKS                                  │

│  Managed Node Group                          │

│  Application Load Balancer                   │

└──────────────────────────────────────────────┘

                    │

                    ▼

       aws eks update-kubeconfig

                    │

                    ▼

            kubectl apply

                    │

                    ▼

          Kubernetes Deployment

                    │

                    ▼

           Running Application
```

---

# 🛠 Technology Stack

| Technology | Purpose |
|------------|---------|
| AWS | Cloud Provider |
| Terraform | Infrastructure as Code |
| Jenkins | Continuous Integration / Continuous Delivery |
| Amazon EKS | Kubernetes Cluster |
| Kubernetes | Container Orchestration |
| Amazon ECR | Docker Image Repository |
| Amazon S3 | Terraform Remote Backend |
| DynamoDB | Terraform State Locking |
| Git | Version Control |
| GitHub | Source Code Repository |

---

# 📁 Repository Structure

```text
hospital-devops-project-

│

├── Jenkinsfile

├── kubernetes

│   ├── namespace.yaml

│   ├── deployment.yaml

│   └── service.yaml

│

└── terraform

    ├── backend

    │      dev.hcl

    │

    ├── envs

    │      dev

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

# 📚 Documentation

The project documentation is split into multiple files.

| Document | Description |
|----------|-------------|
| docs/01-project-overview.md | Complete Project Explanation |
| docs/02-terraform-fundamentals.md | Learn Terraform |
| docs/03-terraform-modules.md | Terraform Modules |
| docs/04-terraform-backend.md | Remote Backend |
| docs/05-vpc-module.md | VPC Module |
| docs/06-iam-module.md | IAM Module |
| docs/07-eks-module.md | EKS Module |
| docs/08-ecr-module.md | ECR Module |
| docs/09-alb-module.md | ALB Module |
| docs/10-jenkins-pipeline.md | Jenkins Pipeline |
| docs/11-kubernetes.md | Kubernetes |
| docs/12-deployment-flow.md | Complete Deployment Flow |
| docs/13-troubleshooting.md | Troubleshooting |
| docs/14-interview-notes.md | DevOps Interview Questions |

---

# 🚀 Features

- Infrastructure as Code
- Reusable Terraform Modules
- Remote Backend
- State Locking
- Automated Infrastructure Deployment
- Infrastructure Validation
- Infrastructure Planning
- Kubernetes Deployment
- Automated EKS Creation
- Jenkins Approval Stage
- GitHub Integration

---

# 👨‍💻 Author

**Vikash Suman**

DevOps Engineer
