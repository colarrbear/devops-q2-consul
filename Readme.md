# Consul Crash Course Demo Project

This repository accompanies the [Consul crash course video](https://www.youtube.com/watch?v=s3I1kKKfjtQ) on YouTube.

It demonstrates deploying [Consul](https://www.consul.io/) on AWS EKS using Terraform, and includes a sample microservices application from [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo).

---

## Directory Structure

```
.
├── kubernetes/
│   ├── config-consul.yaml
│   ├── config.yaml
│   ├── consul-mesh-gateway.yaml
│   ├── consul-values.yaml
│   ├── debug-pod.yaml
│   ├── exported-service.yaml
│   ├── intentions.yaml
│   ├── service-resolver.yaml
│   └── values-examples-with-explanation.yaml
├── microservices-demo/           # Source: https://github.com/GoogleCloudPlatform/microservices-demo
├── terraform/
│   ├── .terraform/
│   ├── .terraform.lock.hcl
│   ├── .terraform.tfstate.lock.info
│   ├── data.tf
│   ├── main.tf
│   ├── providers.tf
│   ├── terraform.tfstate
│   ├── terraform.tfstate.backup
│   ├── terraform.tfvars
│   └── variables.tf
├── .gitignore
├── .gitmodules
└── Readme.md
```

---

## Source Code

- The `microservices-demo` directory contains the [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo) application, used here as a sample workload for Consul service mesh.

---

## Terraform Usage

Initialize, plan, and apply your infrastructure with the following commands:

```sh
# Initialize project & download providers
terraform init

# Preview what will be created
terraform plan

# Apply with variable file (with preview)
terraform apply -var-file=terraform.tfvars

# Apply without preview
terraform apply -var-file=terraform.tfvars -auto-approve

# Destroy all resources
terraform destroy

# List resources in current state
terraform state list
```

---

## Accessing the EKS Cluster

```sh
# Install and configure AWS CLI with your credentials
aws configure

# List existing EKS clusters
aws eks list-clusters --region eu-central-1 --output table --query 'clusters'

# Describe a specific cluster (check VPC config)
aws eks describe-cluster --region eu-central-1 --name myapp-eks-cluster --query 'cluster.resourcesVpcConfig'

# Create kubeconfig for the cluster
aws eks update-kubeconfig --region eu-central-1 --name myapp-eks-cluster

# Test your configuration
kubectl get svc
```

---
