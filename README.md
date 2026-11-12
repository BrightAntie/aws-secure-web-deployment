# aws-secure-web-deployment

A secure, scalable web application deployed on AWS using CloudFront, an Application Load Balancer, and EC2, built within the AWS Free Tier.

This is a solo rebuild of an end-to-end cloud solution design and deployment capstone originally completed as a group project. The goal is to understand the *why* behind each architectural decision, not just to get it working.

## Problem Statement

A fast-growing startup has launched a web application, but users face slow page loads, inconsistent availability during peak traffic, and security concerns. The company also lacks a structured deployment process. They need a secure, highly available, and scalable solution on a limited budget.

## Planned Architecture

```
Browser (HTTPS) -> CloudFront -> Application Load Balancer -> EC2
                       |
                       +-> S3 (static assets, via Origin Access Control)
```

| Component | Purpose |
|---|---|
| CloudFront | CDN, HTTPS enforcement, faster global delivery |
| Application Load Balancer | Distributes traffic, runs health checks |
| EC2 (t2.micro) | Hosts the web application |
| S3 | Stores static assets (kept private, served via CloudFront) |
| ACM | Free SSL/TLS certificates |
| IAM | Least-privilege access |
| CloudWatch | Logs and alarms |
| GitLab/GitHub CI/CD | Automated deployments |

## Tools

- **Cloud:** AWS (Free Tier)
- **Version control:** Git
- **CI/CD:** GitLab CI/CD (or GitHub Actions)
- **Build method:** AWS Console first, Terraform rebuild later

## Environment

| Setting | Value |
|---|---|
| AWS region | `<your-region>` |
| CloudFront certificate region | `us-east-1` |
| Domain | `<your-domain>` |
| EC2 instance type | t2.micro |

## Branching Strategy

- `main`: production, protected, merge requests only
- `develop`: integration branch
- `feature/*`: one branch per task, merged into `develop`

## Progress

### Phase 1: Project Setup & Environment Configuration
- [x] Git repository with `main`, `develop`, and feature branches
- [x] README started
- [ ] AWS account, MFA, and budget alert
- [ ] IAM user with least-privilege permissions
- [ ] EC2 instance and security group
- [ ] S3 bucket (Block Public Access on)
- [ ] ACM certificate

### Phase 2: Web Application Development & Deployment
- [ ] Simple web app (HTML/CSS/JS) hosted on EC2
- [ ] Target group and Application Load Balancer
- [ ] HTTP to HTTPS redirect
- [ ] Health checks showing healthy
- [ ] Static assets in S3

### Phase 3: Security Hardening & CloudFront Integration
- [ ] CloudFront distribution with ALB as origin
- [ ] ACM certificate attached
- [ ] EC2 security group restricted to CloudFront
- [ ] S3 Origin Access Control
- [ ] Full HTTPS flow tested

### Phase 4: CI/CD, Monitoring & Cost Management
- [ ] CI/CD pipeline deploying to EC2
- [ ] CloudWatch alarms and logs
- [ ] Deployment checklist



## Setup Notes

Record every console setting here as you build (AMI, security group rules, bucket settings, listener rules). This becomes the specification for the Terraform rebuild.

### Phase 1
- _Add notes as you go._

## Future Work

- Rebuild the whole infrastructure with Terraform
- Replace SSH-based deployments with AWS Systems Manager (SSM)

## Teardown

When finished, delete the resources to avoid charges: CloudFront distribution, ALB, target group, EC2 instance, Elastic IPs, S3 bucket, and any unused certificates.
