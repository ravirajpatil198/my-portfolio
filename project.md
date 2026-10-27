# Retail Store on Amazon EKS

**Portfolio project | Cloud infrastructure, Kubernetes, and GitOps**

**Repository:** [github.com/ravirajpatil198/retail-store](https://github.com/ravirajpatil198/retail-store)

## Project Summary

I configured an AWS deployment platform for a containerized retail application using Terraform, Amazon EKS Auto Mode, Kubernetes Helm charts, and Argo CD. The infrastructure and deployment configuration demonstrate how a multi-service application can be provisioned and managed with infrastructure as code and GitOps.

The retail application is based on the [AWS Containers Retail Store sample](https://github.com/aws-containers/retail-store-sample-app). My project focus is the AWS infrastructure and deployment setup documented in this repository, not original authorship of the upstream application services.

## What I Worked On

- Defined Terraform infrastructure for an AWS VPC with public and private subnets across three availability zones.
- Configured an Amazon EKS cluster with EKS Auto Mode and a unique generated suffix for cluster naming.
- Integrated EKS Blueprints Add-ons for NGINX Ingress and cert-manager.
- Deployed Argo CD with Terraform and configured an Argo CD project and individual applications.
- Connected the application Helm charts to the `retail-store` Kubernetes namespace using Argo CD sync policies.
- Documented deployment, cluster access, application checks, and infrastructure teardown.

## Architecture

```text
AWS account
└── Terraform
    ├── VPC: public and private subnets across three AZs
    ├── Amazon EKS Auto Mode cluster
    ├── NGINX Ingress + Network Load Balancer
    ├── cert-manager
    └── Argo CD
        └── Helm applications in the retail-store namespace
            ├── UI
            ├── Catalog
            ├── Cart
            ├── Checkout
            └── Orders
```

Argo CD manages the Kubernetes application resources from Git. The NGINX ingress service is exposed through an AWS Network Load Balancer. Terraform outputs provide cluster details and useful commands for connecting to and inspecting the deployment.

## Technology Stack

- **Cloud:** AWS, Amazon EKS Auto Mode, VPC, IAM
- **Infrastructure as code:** Terraform
- **Containers and orchestration:** Docker, Kubernetes, Helm
- **GitOps:** Argo CD
- **Cluster add-ons:** NGINX Ingress Controller, cert-manager
- **Application services:** Java, Go, and Node.js

## Design Notes

The Terraform configuration selects three available availability zones and creates public and private subnets. It enables a single NAT Gateway by default to reduce cost; this is a cost-conscious development setup, not a highly available production network design. The cluster name receives a random suffix to reduce naming conflicts.

## Current Scope

Argo CD synchronization is configured, but this repository does not include a GitHub Actions workflow or automated container image build-and-publish pipeline. The checked-in Argo CD manifests currently reference the upstream sample repository; update their repository URLs to this project before using Argo CD to sync charts from this fork.

No deployment performance, availability, or cost measurements are claimed here; add verified results if you collect them from a real deployment.

## Suggested Portfolio Blurb

> Built an AWS deployment platform for a multi-service retail application using Terraform, Amazon EKS Auto Mode, and Argo CD. Provisioned a three-AZ VPC, integrated ingress and certificate-management add-ons, and configured GitOps delivery of five Helm-packaged services. The application is based on the AWS Containers Retail Store sample; my work focused on its infrastructure and deployment configuration.
