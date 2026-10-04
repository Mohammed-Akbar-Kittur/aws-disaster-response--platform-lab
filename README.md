# Resilient Disaster Response Platform on AWS

<img width="1920" height="1280" alt="IMG-20261004-WA3344" src="https://github.com/user-attachments/assets/54f2bf2d-38bc-4f48-8920-0cf8610ecaff" />

> **Lab Status:** Hands-on lab completed in eu-north-1. Resources decommissioned to avoid AWS charges. Architecture, configs, and learnings documented here.

## Overview
Built a highly available disaster management website designed to handle 5x traffic spikes during emergency events. Focused on availability, auto-scaling, and proactive alerting.

## Architecture Flow
`Users -> Route53 (DNS + Health Checks) -> Application Load Balancer (ALB) -> Auto Scaling Group (2-6 EC2 across 2 AZs) -> S3 (Static Maps/Images/Docs) -> CloudWatch -> SNS (Email/SMS Alerts)`

## Key Implementations
- **High Availability:** Multi-AZ deployment across eu-north-1a & eu-north-1b, no single point of failure
- **Auto Scaling:** ASG Min 2 / Max 6 / Desired 2, Target Tracking on CPU 70% + RequestCount
- **Static Assets:** S3 bucket versioned, secured, serving disaster maps and documents
- **Monitoring:** CloudWatch metrics for ALB Latency, 5xx errors, EC2 CPU/Memory, UnhealthyHostCount
- **Alerting:** SNS topics -> Email, SMS, Ops pager on alarm breach

## Tech Stack
AWS - VPC, ALB, EC2 (t3.medium), Auto Scaling Group, S3, Route53, CloudWatch, SNS, IAM

## Deployment Steps Practiced
```bash
1. Create VPC 10.0.0.0/16 with 2 Public Subnets
2. Launch ALB (internet-facing, cross-zone enabled)
3. Create Launch Template with user-data (Apache)
4. Create ASG spanning 2 AZs
5. Create S3 bucket for static assets
6. Setup CloudWatch Alarms -> SNS
