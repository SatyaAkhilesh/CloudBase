# CloudBase

## AWS EKS Shared Cluster Infrastructure Project

CloudBase is a comprehensive academic Infrastructure as Code (IaC) project that focuses on the design, automation, and management of a shared Kubernetes platform on Amazon Web Services (AWS).  
The project leverages Terraform and AWS DevOps services to provision a secure, scalable, and repeatable Amazon EKS environment capable of hosting multiple isolated workloads within a single cluster.

This repository serves as a practical demonstration of modern cloud-native infrastructure principles, DevOps automation, and Kubernetes operational patterns.

---

## 🎯 Project Objectives

The primary objectives of CloudBase are:

- To demonstrate real-world cloud infrastructure provisioning using Terraform  
- To design a shared Amazon EKS environment with logical workload isolation  
- To implement automated CI/CD pipelines for infrastructure lifecycle management  
- To apply AWS networking best practices for secure inter-service communication  
- To gain hands-on experience with DevOps workflows and GitOps-based operations  

CloudBase is intended for educational and demonstration purposes, making it suitable for coursework, labs, or capstone projects in cloud computing and DevOps domains.

---

## 🧠 Conceptual Background

Modern cloud platforms often rely on shared infrastructure models to optimize cost, simplify operations, and improve scalability.  
In Kubernetes-based environments, this is commonly achieved by running multiple workloads within a single cluster while enforcing isolation through namespaces, IAM policies, and network controls.

CloudBase explores this architectural model by implementing:

- A **single Amazon EKS cluster** hosting multiple workloads  
- **Logical separation** of workloads using Kubernetes constructs  
- **Independent networking boundaries** using AWS VPCs  
- **Automated pipelines** that control infrastructure changes  

This approach reflects real-world cloud platform design while remaining approachable for academic study.

---

## 🧱 High-Level Architecture

CloudBase provisions a complete AWS infrastructure stack composed of the following layers:

### 🕸️ Networking Layer
- Multiple Virtual Private Clouds (VPCs)
- Public and private subnets distributed across availability zones
- Internet Gateway and NAT Gateway for controlled outbound access
- AWS Transit Gateway to enable secure connectivity between VPCs

### ⚙️ Compute Layer
- Amazon EKS cluster deployed in a dedicated VPC
- Kubernetes worker nodes running in private subnets
- Namespace-based separation for workloads
- Integration with GitOps tooling for workload management

### 🔄 Automation Layer
- CI/CD pipelines built using AWS CodePipeline
- Build and validation stages powered by AWS CodeBuild
- Source control integration using AWS CodeCommit
- Automated Terraform plan and apply workflows

All layers are fully defined using Terraform, ensuring consistent and repeatable deployments.

---

## 🛠️ Technologies and Tools

CloudBase uses the following tools and services:

- **Amazon Web Services (AWS)** – Core cloud infrastructure  
- **Amazon EKS** – Managed Kubernetes service  
- **Terraform** – Infrastructure as Code automation  
- **AWS CodePipeline** – CI/CD orchestration  
- **AWS CodeBuild** – Build and validation execution  
- **AWS CodeCommit** – Source code management  
- **Kubernetes** – Container orchestration platform  
- **GitOps Tooling** – Declarative workload synchronization  

---

## 💾 Terraform State Management

To ensure safe collaboration and prevent state conflicts, CloudBase uses a remote Terraform backend:

- **Amazon S3** for storing Terraform state files  
- **Amazon DynamoDB** for state locking and concurrency control  

