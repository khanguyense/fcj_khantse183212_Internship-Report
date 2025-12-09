---
title: "Event 3"
date: "2025-11-16"
weight: 4
chapter: false
pre: " <b> 4.3. </b> "
---
# Báo cáo tóm tắt: "AWS Cloud Mastery Series #2: DevOps on AWS"

## Mục đích của Workshop

- Cung cấp cái nhìn tổng quan toàn diện về văn hóa, nguyên tắc và thực hành DevOps trên AWS.  
- Minh họa cách xây dựng một pipeline CI/CD hoàn chỉnh — từ quản lý mã nguồn đến triển khai tự động.  
- Giới thiệu các công cụ Infrastructure as Code (IaC) chính trên AWS và cách ứng dụng thực tế.  
- Trang bị cho người tham dự kiến thức về containerization, observability và các thực hành vận hành tốt nhất.  

## Diễn giả / Giảng viên chính (Dự kiến)

- **Đỗ Huy Thắng** – DevOps Lead, VNG  
- **Nguyễn Thị Thu Hà** – Senior DevOps Engineer, AWS  
- **Phạm Tuấn Anh** – Solutions Architect, AWS  

---

## Các chủ đề & nội dung học chính

### 1. Văn hóa DevOps & Các nguyên tắc cốt lõi

- DevOps không chỉ là công cụ — đó là một văn hóa hợp tác giữa Development và Operations.  
- Các chỉ số DORA (Tần suất triển khai, Thời gian đưa thay đổi vào sản xuất, MTTR, Tỷ lệ thay đổi lỗi) là những chỉ báo quan trọng về hiệu quả DevOps.  
- Shift-left Testing & Security giúp phát hiện vấn đề sớm hơn và giảm chi phí khắc phục.  

### 2. CI/CD Pipeline trên AWS

- AWS DevTools (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) cho phép xây dựng quy trình phát hành tự động hoàn toàn.  
- Các chiến lược triển khai gồm **Blue/Green**, **Canary** và **Rolling Updates**.  
- Demo trực tiếp: `commit → build → test → deploy` lên EC2/ECS.  

### 3. Infrastructure as Code (IaC)

- **AWS CloudFormation**: IaC theo kiểu khai báo bằng template YAML/JSON.  
- **AWS CDK**: IaC theo kiểu lập trình (imperative) dùng các ngôn ngữ như Python hoặc TypeScript, hỗ trợ tái sử dụng mạnh.  
- **Drift Detection** giúp đảm bảo hạ tầng luôn nhất quán với cấu hình đã định nghĩa.  

### 4. Containers & Microservices

- Docker đóng gói ứng dụng thành các container nhẹ, di động, tách biệt.  
- So sánh **Amazon ECS** và **Amazon EKS** để lựa chọn công cụ điều phối phù hợp.  
- **AWS App Runner** cung cấp triển khai container dạng serverless với chi phí vận hành tối thiểu.  

### 5. Monitoring & Observability

- **Amazon CloudWatch**: metrics, logs, alarms, dashboards để theo dõi sức khỏe hệ thống theo thời gian thực.  
- **AWS X-Ray**: distributed tracing để phân tích hiệu năng và xác định các nút thắt độ trễ.  
- Thực hành tốt bao gồm cảnh báo có ý nghĩa, dashboard gắn với SLO, và quy trình postmortem có cấu trúc.  

---

## Những điều rút ra chính

### Tư duy & Văn hóa

- DevOps là một hành trình cải tiến liên tục.  
- Tự động hóa là xương sống của DevOps.  
- Áp dụng tư duy “blameless postmortem” để học từ thất bại.  

### Kiến thức kỹ thuật

- CI/CD là xây dựng một quy trình phân phối đáng tin cậy, không chỉ là chạy script.  
- IaC mang lại tính nhất quán, khả năng quản lý phiên bản và tái tạo môi trường.  
- Observability cung cấp góc nhìn sâu hơn để phân tích nguyên nhân gốc rễ.  

### Kỹ năng nghề nghiệp

- Kỹ sư DevOps cần nền tảng rộng: networking, security, coding, vận hành hệ thống.  
- Kỹ năng debug nâng cao là thiết yếu trong môi trường hệ thống phân tán.  

---

## Kế hoạch hành động cá nhân

1. Xây dựng một CI/CD pipeline cá nhân dùng CodeCommit & CodePipeline.  
2. Thực hành AWS CDK với Python để triển khai các tài nguyên AWS cốt lõi.  
3. Đóng gói một ứng dụng nhỏ bằng Docker và deploy trên ECS Fargate.  
4. Tạo một CloudWatch dashboard với các metrics và alarms quan trọng.  

---

## Cảm nhận cá nhân

Workshop mang lại nhiều góc nhìn thực tế mà lập trình viên thường dễ bỏ qua.  
**Phần demo CI/CD và IaC đặc biệt ấn tượng**, cho thấy tự động hóa giúp giảm rủi ro và tăng tốc vòng đời phát hành như thế nào.  
Các case study thực tế từ VNG và AWS nhấn mạnh vai trò then chốt của monitoring và văn hóa DevOps.
