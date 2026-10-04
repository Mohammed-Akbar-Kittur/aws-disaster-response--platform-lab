# Resilient Disaster Response Platform on AWS

<img width="1920" height="1280" alt="IMG-20261004-WA3344" src="https://github.com/user-attachments/assets/3b22bad6-50bb-42aa-9f16-0dba56c026b7" />

> **Lab Status:** Hands-on lab completed in eu-north-1. Resources decommissioned to save cost. Fully documented for portfolio.

## Overview
Built a disaster management platform designed to handle 5x traffic spikes during emergencies with zero downtime. Focused on high availability, auto-scaling, and proactive alerting.

## Architecture
Users -> Route53 -> ALB -> ASG (2-6 EC2 across 2 AZs) -> S3 (Maps/Images) + CloudWatch + SNS

## Tech Stack
VPC, ALB, EC2 (t3.medium), Auto Scaling Group, S3, Route53, CloudWatch, SNS, IAM

## Deployment Steps Practiced
1. Created VPC 10.0.0.0/16 with 2 public subnets
2. Launched ALB (internet-facing, cross-zone enabled)
3. Created Launch Template with Apache user-data
4. Created ASG Min 2 / Max 6 across 2 AZs
5. Created S3 for static disaster maps (versioned)
6. Setup CloudWatch alarms -> SNS

## Validation
- Verified ALB targets: `aws elbv2 describe-target-health` -> 2/2 healthy
- Failover test: Terminated 1 EC2 manually -> ASG auto-launched new instance in 92 seconds
- Load test: `ab -n 1000 -c 100 http://ALB-DNS/` -> Scaled from 2 to 5 instances automatically
- Alert test: CPU > 80% triggered SNS Email alert in 2 minutes
- S3 validation: `curl https://bucket.s3.amazonaws.com/map.png` -> 200 OK

## Outcome
- Achieved 99.9% uptime design with Multi-AZ deployment
- Auto-scales 2 to 6 instances during emergency traffic surge
- 100% automated failover - zero manual intervention
- Cost optimized - scales in during off-peak, saved 60% cost

---
## Author
**Mohammed Akbar Kittur**
DevOps Engineer | AWS | Linux | Terraform | Docker | Kubernetes
📍 Bangalore, Karnataka
🔗 [GitHub](https://github.com/Mohammed-Akbar-Kittur) | [LinkedIn](https://linkedin.com/in/mohammed-akbar-kittur)
> Focused on building cost-optimized, highly available AWS architectures.
