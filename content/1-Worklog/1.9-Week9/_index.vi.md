---
title: "Worklog Tuần 9"
date: "2025-11-07"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---



### Mục tiêu tuần 9:

* Tìm hiểu tổng quan kiến trúc Serverless và các thành phần chính: API Gateway, Lambda, DynamoDB.
* Thiết kế kiến trúc tổng thể cho ứng dụng: backend, frontend, xác thực, bảo mật và tích hợp.
* Nghiên cứu lớp bảo mật (Edge & Security): CloudFront, Route 53, WAF.
* Tìm hiểu hệ thống xác thực với Amazon Cognito và cách cấp token cho API.
* Phân tích cách triển khai CI/CD với CodePipeline, CodeBuild, GitLab và IaC (CloudFormation).
* Tìm hiểu hệ thống quan sát/giám sát: CloudWatch, X-Ray, SNS.
  
### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                  | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------- |
| 2   | - Tìm hiểu kiến trúc Serverless <br> - API Gateway, Lambda, DynamoDB & cơ chế tích hợp                     | 03/11/2025   | 03/11/2025      |
| 3   | - Thiết kế kiến trúc tổng thể (BE + FE + Auth + Edge) <br> - Vẽ sơ đồ kiến trúc & luồng request            | 04/11/2025   | 04/11/2025      |
|     |
| 4   | - Tìm hiểu CloudFront, Route 53, WAF <br> - Thiết kế lớp bảo mật trước API Gateway                         | 05/11/2025   | 05/11/2025      |                |
| 5   | - Tìm hiểu Cognito (User Pool, Token) <br> - Phân tích cách API Gateway validate JWT token                 | 06/11/2025   | 06/11/2025      |                |
| 6   | - Tìm hiểu CI/CD: CloudFormation, CodePipeline, CodeBuild <br> - Hệ thống quan sát: CloudWatch, X-Ray, SNS | 07/11/2025   | 07/11/2025      |                |


### Kết quả đạt được tuần 9:

* Tổng quát:
  * Trong tuần này tôi tập trung hiểu và thiết kế kiến trúc Serverless cho ứng dụng. Tôi đã nắm rõ luồng hoạt động của API Gateway – Lambda – DynamoDB, đồng thời nghiên cứu lớp bảo mật bằng CloudFront/WAF và hệ thống xác thực bằng Cognito. Tôi cũng nắm được quy trình CI/CD và cơ chế logging/monitoring để chuẩn bị cho các tuần code tiếp theo.
  
* Lý thuyết đã học:
  * Kiến trúc Serverless, nguyên tắc pay-per-use và autoscaling.
  * API Gateway REST API, Lambda integration, DynamoDB table workflow.
  * CloudFront + WAF + Route 53 để bảo vệ API.
  * Cognito User Pool & Token (ID/Access), JWT flow qua API Gateway authorizer.
  * CI/CD với CodePipeline + CodeBuild + CloudFormation.
  * CloudWatch logs/metrics, SNS alert, tracing bằng X-Ray.

* Thực hành / Sản phẩm:
  * Sơ đồ kiến trúc tổng thể ứng dụng (BE – FE – Auth – Edge).
  * Luồng request từ client -> CloudFront -> API Gateway -> Lambda -> DynamoDB.
  * Diagram bảo mật: CDN, DNS, WAF, throttling & protection tại API Gateway.
  * Phác thảo pipeline tự động triển khai bằng CloudFormation & CodePipeline.
  * Thiết kế flow xác thực Cognito -> API Gateway JWT Authorizer.