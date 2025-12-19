
# CloudBase
## AWS EKS Shared Cluster Infrastructure Project

CloudBase is a Terraform-based academic project focused on designing and deploying a shared Kubernetes environment on AWS.  
The project demonstrates how multiple workloads can securely coexist within a single Amazon EKS cluster using infrastructure automation and DevOps pipelines.



## Project Overview

The objective of CloudBase is to showcase cloud-native infrastructure design using Infrastructure as Code (IaC).  
It provisions networking, compute, and CI/CD components required to operate a shared Amazon EKS cluster where workloads are logically separated using Kubernetes and AWS-native controls.

This project is intended for learning and demonstration purposes and highlights best practices in AWS DevOps, Terraform automation, and Kubernetes operations.

---

## Technologies and Tools

- Amazon Web Services (AWS)
- Amazon EKS
- Terraform
- AWS CodePipeline, CodeBuild, and CodeCommit
- Kubernetes
- GitOps tooling

---

## Repository Layout

The repository is organized into modular components to support clarity and reuse:

.
├── bootstrap        # Backend initialization for Terraform state
├── demo             # Sample environment configuration
│   ├── compute      # EKS and Kubernetes-related resources
│   │   └── k8s
│   │       └── cfg-namespace-mgmt
│   │           └── templates
│   ├── network      # VPCs, subnets, and routing
│   └── pipeline     # CI/CD pipeline definitions
├── modules          # Reusable Terraform modules
│   ├── codebuild
│   ├── codecommit
│   ├── codepipeline
│   ├── gitops
│   ├── iam-role
│   ├── kms
│   ├── s3
│   ├── transit_gw
│   └── vpc
└── templates
└── scripts

---

## Terraform Backend Initialization

CloudBase uses Amazon S3 to store Terraform state files and DynamoDB for state locking.

A helper script is provided to bootstrap these backend resources.

From the `bootstrap` directory, execute:

```sh
./bootstrap.sh

This step must be completed before running Terraform in any other module.

⸻

Deployment Workflow

Infrastructure components are deployed in a specific sequence to ensure dependency integrity:
	1.	CI/CD Pipeline
	2.	Network Resources
	3.	Compute and EKS Resources

The pipeline layer is initialized manually. All subsequent layers are deployed automatically through AWS CodePipeline.

⸻

Running Terraform

A wrapper script is included to standardize Terraform execution across environments.

Example commands for initializing and deploying the pipeline module:

./run.sh -m pipeline -env demo -region us-west-2 -tfcmd init
./run.sh -m pipeline -env demo -region us-west-2 -tfcmd plan
./run.sh -m pipeline -env demo -region us-west-2 -tfcmd apply

Once the pipeline is active, network and compute components are deployed automatically.

⸻

Provisioned AWS Resources

After a successful deployment, the following infrastructure is created:
	•	A centralized egress VPC with public and private subnets
	•	A dedicated VPC hosting the Amazon EKS cluster
	•	Separate private VPCs for isolated workloads
	•	Transit Gateway connecting all VPCs with appropriate routing
	•	A fully configured CI/CD pipeline for infrastructure automation

⸻

CI/CD Pipeline Stages

The CloudBase pipeline is composed of multiple stages to ensure safe and repeatable deployments:
	•	Validation Stage
Initializes Terraform and performs static analysis using security scanning tools.
	•	Planning Stage
Generates and stores Terraform execution plans for review.
	•	Apply Stage
Applies the approved infrastructure changes to AWS.
	•	Destroy Stage (Optional)
Allows manual teardown of all deployed resources when enabled.

⸻

Common Issues and Resolution

Source Repository Checkout Failure

If the pipeline fails during source checkout with an authentication-related error, the issue is typically caused by an incomplete or empty application repository.

Resolution Steps
	1.	Confirm that the application repository contains valid source code.
	2.	Temporarily disable the deployment flag in the namespace configuration module.
	3.	Apply the change, then re-enable the deployment flag and apply again.
	4.	Verify resource status using Kubernetes and GitOps tooling.

If issues persist, inspect pipeline logs and GitOps controller logs for additional details.

