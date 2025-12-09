---
title: "Event 4"
date: "2025-11-16"
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---
# Summary Report: "AWS Cloud Mastery Series #2: DevOps on AWS"

### Purpose of the Workshop
- Provide a comprehensive overview of DevOps culture, principles, and practices on AWS.
- Demonstrate how to build a complete CI/CD pipeline—from source control to automated deployment.
- Introduce major Infrastructure as Code (IaC) tools on AWS and their practical applications.
- Equip attendees with knowledge on containerization, observability, and operational best practices.

### Speakers / Main Instructors (Expected)
- **Đỗ Huy Thắng** – DevOps Lead, VNG  
- **Nguyễn Thị Thu Hà** – Senior DevOps Engineer, AWS  
- **Phạm Tuấn Anh** – Solutions Architect, AWS  

---

### Key Topics & Learnings

#### 1. DevOps Culture & Core Principles
- DevOps is not just about tools—it represents a **collaborative culture** between Development and Operations.
- DORA metrics (Deployment Frequency, Lead Time, MTTR, Change Failure Rate) are **critical indicators** of DevOps performance.
- **Shift-left Testing & Security** helps detect issues earlier and reduce remediation cost.

#### 2. CI/CD Pipeline on AWS
- AWS DevTools (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) enable **fully automated** release workflows.
- Deployment strategies include **Blue/Green**, **Canary**, and **Rolling Updates**.
- Live demonstration: commit → build → test → deploy to EC2/ECS.

#### 3. Infrastructure as Code (IaC)
- **AWS CloudFormation**: declarative IaC using YAML/JSON templates.
- **AWS CDK**: imperative IaC using languages like Python or TypeScript, offering strong reusability.
- **Drift Detection** ensures infrastructure remains consistent with defined configurations.

#### 4. Containers & Microservices
- Docker packages applications into lightweight, portable, isolated containers.
- Comparison of **Amazon ECS vs Amazon EKS** to choose the right orchestration tool.
- **AWS App Runner** offers serverless container deployment with minimal operational overhead.

#### 5. Monitoring & Observability
- **Amazon CloudWatch**: metrics, logs, alarms, dashboards for real-time system health.
- **AWS X-Ray**: distributed tracing to analyze performance and identify latency bottlenecks.
- Best practices include meaningful alerts, dashboards aligned with SLOs, and a structured postmortem process.

---

### Key Takeaways

#### Mindset & Culture
- DevOps is a continuous improvement journey.
- Automation is the backbone of DevOps.
- Adopt a “blameless postmortem” mindset to learn from failures.

#### Technical Knowledge
- CI/CD is about creating a **reliable delivery workflow**, not just running scripts.
- IaC enables consistency, version control, and environment reproducibility.
- Observability provides deeper insights into root cause analysis.

#### Career Skills
- DevOps engineers need broad knowledge: networking, security, coding, system operations.
- Advanced debugging skills are essential for distributed systems.

---

### Personal Action Plan
1. Build a personal CI/CD pipeline using CodeCommit & CodePipeline.  
2. Practice AWS CDK using Python to deploy core AWS resources.  
3. Package a small application into Docker and deploy it on ECS Fargate.  
4. Create a CloudWatch dashboard with essential metrics and alarms.

---

### Personal Reflection

This workshop offered highly practical insights that developers often overlook.  
**The CI/CD and IaC demonstrations were particularly impressive**, showing how automation reduces risk and accelerates release cycles.  
Real-world case studies from VNG and AWS emphasized the critical role of monitoring and DevOps culture.

---


