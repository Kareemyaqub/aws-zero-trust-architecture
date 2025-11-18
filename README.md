# Zero Trust Architecture Demo on AWS

This repository contains a simple example of a **Zero Trust style architecture** on **Amazon Web Services (AWS)** using **CloudFormation**.

## What it deploys

- A **VPC** (isolated network).
- A **public subnet** with an Application Load Balancer (ALB).
- A **private subnet** with an EC2 instance (web server) that:
  - Has **no public IP**.
  - Is only reachable through the ALB.
- **Security groups** to restrict traffic:
  - ALB: accepts inbound HTTPS (port 443) from the internet.
  - EC2: accepts inbound HTTP (port 80) *only* from the ALB.
- **IAM role** attached to the EC2 instance instead of static credentials.

This is a simplified teaching example of how Zero Trust ideas can be mapped to AWS:

- **Verify explicitly** – Users hit the ALB endpoint (you can later add Cognito, OIDC, etc.).
- **Least privilege access** – Only specific ports and paths are allowed between components.
- **Assume breach** – The EC2 instance has no direct internet exposure and is segmented.

## Files

- `infra/zero-trust-vpc.yaml` – CloudFormation template for the core network and resources.
- `docs/architecture-overview.md` – High-level description of the architecture and Zero Trust concepts.

## How to deploy

You can deploy using the **AWS Management Console** (no command line needed):

1. Log in to the AWS console.
2. Go to **CloudFormation** → **Create stack** → *With new resources (standard)*.
3. Choose **Upload a template file** and upload `infra/zero-trust-vpc.yaml`.
4. Follow the wizard and click **Create stack**.
5. Wait for the stack status to become **CREATE_COMPLETE**.

See the `docs/architecture-overview.md` file for more details.
