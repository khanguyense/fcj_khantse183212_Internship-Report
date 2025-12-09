---
title: "Week 9 Worklog"
date: "2025-11-07"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:

* Learn the overall Serverless architecture and its core components: API Gateway, Lambda, DynamoDB.
* Design the full application architecture: backend, frontend, authentication, security, and integrations.
* Explore the security and edge layer: CloudFront, Route 53, WAF.
* Learn the authentication system with Amazon Cognito and how tokens are issued for APIs.
* Analyze how CI/CD is implemented using CodePipeline, CodeBuild, GitLab, and IaC (CloudFormation).
* Learn AWS observability and monitoring systems: CloudWatch, X-Ray, SNS.
  
### Tasks to be carried out this week:
| Day | Task                                                                                                       | Start Date | End Date   | Reference Materials |
| --- | ---------------------------------------------------------------------------------------------------------- | ---------- | ---------- | ------------------- |
| 2   | - Learn Serverless architecture <br> - API Gateway, Lambda, DynamoDB & integration mechanisms              | 03/11/2025 | 03/11/2025 |                     |
| 3   | - Design full architecture (BE + FE + Auth + Edge) <br> - Draw architecture diagram & request flow         | 04/11/2025 | 04/11/2025 |                     |
| 4   | - Learn CloudFront, Route 53, WAF <br> - Design security layer in front of API Gateway                     | 05/11/2025 | 05/11/2025 |                     |
| 5   | - Learn Cognito (User Pool, Token) <br> - Analyze how API Gateway validates JWT tokens                     | 06/11/2025 | 06/11/2025 |                     |
| 6   | - Learn CI/CD: CloudFormation, CodePipeline, CodeBuild <br> - Observability system: CloudWatch, X-Ray, SNS | 07/11/2025 | 07/11/2025 |                     |

### Week 9 Achievements:

* Overview:  
  * This week, I focused on understanding and designing the Serverless architecture for the application. I gained a solid understanding of how API Gateway – Lambda – DynamoDB work together, and explored the security layer using CloudFront/WAF as well as authentication via Cognito. I also learned the CI/CD workflow and logging/monitoring mechanisms to prepare for the coding phases in the upcoming weeks.

* Theory Learned:
  * Serverless architecture, pay-per-use model, and autoscaling principles.  
  * API Gateway REST API, Lambda integration, and DynamoDB table workflow.  
  * CloudFront + WAF + Route 53 for API protection.  
  * Cognito User Pool & Tokens (ID/Access), JWT flow through API Gateway authorizer.  
  * CI/CD with CodePipeline + CodeBuild + CloudFormation.  
  * CloudWatch logs/metrics, SNS alerts, tracing using X-Ray.

* Practice / Deliverables:
  * Full system architecture diagram (BE – FE – Auth – Edge).  
  * Request flow from client -> CloudFront -> API Gateway -> Lambda -> DynamoDB.  
  * Security diagram: CDN, DNS, WAF, throttling & protection at API Gateway.  
  * Preliminary CI/CD pipeline design using CloudFormation & CodePipeline.  
  * Authentication flow design: Cognito -> API Gateway JWT Authorizer.
