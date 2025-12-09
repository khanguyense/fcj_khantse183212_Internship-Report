---
title: "Nhật ký Tuần 4"
date: "2025-09-30"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4:

* Hiểu cách khởi tạo và quản lý EC2 Windows và Linux.
* Thực hành triển khai ứng dụng trên EC2 (Node.js & AWS User Management App).
* Hiểu IAM governance và quản lý chi phí EC2 thông qua IAM.
* Hiểu cách ứng dụng truy cập dịch vụ AWS qua IAM Role thay cho Access Key.
* Thực hành gán IAM Role cho EC2 và kiểm tra quyền truy cập của ứng dụng.

---

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                                           | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                         |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ---------------- | ------------------------------------------ |
| 1    | - Tìm hiểu giới thiệu EC2 & bước chuẩn bị <br>&emsp; + Khái niệm EC2 <br>&emsp; + Các tài nguyên cần thiết <br>&emsp; + Yêu cầu IAM & networking                                                          | 09/30/2025   | 09/30/2025       | <https://000004.awsstudygroup.com/>        |
| 2    | - **Khởi tạo EC2:** <br>&emsp; + Tạo Windows Server 2022 instance <br>&emsp; + Tạo Amazon Linux instance <br>&emsp; + Kết nối và kiểm tra truy cập                                                         | 10/01/2025   | 10/01/2025       | <https://000004.awsstudygroup.com/>        |
| 3    | - **Triển khai ứng dụng:** <br>&emsp; + Triển khai AWS User Management App trên Amazon Linux 2 <br>&emsp; + Triển khai Node.js App trên Windows EC2                                                        | 10/02/2025   | 10/02/2025       | <https://000004.awsstudygroup.com/>        |
| 4    | - **IAM Governance & Authorization:** <br>&emsp; + Hiểu governance chi phí & sử dụng với IAM <br>&emsp; + So sánh Access Key vs IAM Role <br>&emsp; + Rủi ro của việc dùng Access Key lâu dài              | 10/03/2025   | 10/03/2025       | <https://000048.awsstudygroup.com/>        |
| 5    | - **Thực hành IAM Role cho EC2:** <br>&emsp; + Tạo IAM Role cho EC2 <br>&emsp; + Gán Role vào EC2 instance <br>&emsp; + Kiểm tra ứng dụng truy cập AWS qua Role <br>&emsp; + Clean up resource sau bài học | 10/04/2025   | 10/04/2025       | <https://000048.awsstudygroup.com/>        |

---

### Thành tựu Tuần 4:

* Khởi tạo thành công EC2 Windows và Linux.
* Hiểu cách chuẩn bị môi trường EC2 để triển khai ứng dụng.
* Triển khai thành công 2 ứng dụng:
  * AWS User Management App (Linux)
  * Node.js App (Windows)
* Hiểu rõ IAM governance & ảnh hưởng của IAM tới chi phí và bảo mật.
* Nắm được lý do không nên dùng Access Key cho ứng dụng.
* Tạo và gán IAM Role cho EC2, giúp ứng dụng truy cập AWS service an toàn.
* Kiểm tra thành công quyền truy cập dựa trên IAM Role.
* Dọn dẹp tài nguyên để tránh phát sinh chi phí.
