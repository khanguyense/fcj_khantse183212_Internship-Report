---
title: "Nhật ký Tuần 3"
date: "2025-09-23"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3:

* Hiểu sâu hơn về kiểm soát truy cập với AWS IAM: User, Group, Policy, Role.
* Biết cách thiết kế mô hình phân quyền an toàn dựa trên IAM Role và nguyên tắc “least privilege”.
* Thực hành tạo IAM Group, IAM User, IAM Role và kịch bản Switch Role.
* Nắm các khái niệm mạng cơ bản trong Amazon VPC: Subnet, Route Table, Internet Gateway, NAT Gateway.
* Thực hành xây dựng VPC, cấu hình Security Group, Network ACL và làm quen với Site-to-Site VPN.

---

### Các nhiệm vụ thực hiện trong tuần:

| Ngày | Nhiệm vụ                                                                                                                                                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                         |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | ---------------- | ------------------------------------------ |
| 1    | - Tìm hiểu tổng quan về IAM Access Control <br>&emsp; + IAM User & IAM Group <br>&emsp; + IAM Policy <br>&emsp; + IAM Role <br> - Ôn lại mục tiêu bảo mật và nguyên tắc least privilege                                                                       | 09/23/2025   | 09/23/2025       | <https://000002.awsstudygroup.com/>        |
| 2    | - **Thực hành IAM (1):** <br>&emsp; + Tạo Admin IAM Group <br>&emsp; + Tạo Admin User và thêm vào group <br>&emsp; + Đăng nhập bằng Admin User và kiểm tra quyền                                                      | 09/24/2025   | 09/24/2025       | <https://000002.awsstudygroup.com/>        |
| 3    | - **Thực hành IAM (2):** <br>&emsp; + Tạo Admin Role <br>&emsp; + Tạo OperatorUser <br>&emsp; + Cấu hình trust relationship cho Switch Role <br>&emsp; + Test Switch Role từ OperatorUser <br>&emsp; + Rà soát & dọn dẹp cấu hình không cần thiết | 09/25/2025   | 09/25/2025       | <https://000002.awsstudygroup.com/>        |
| 4    | - Học lý thuyết về Amazon VPC: <br>&emsp; + Subnet <br>&emsp; + Route Table <br>&emsp; + Internet Gateway <br>&emsp; + NAT Gateway <br> - So sánh và hiểu vai trò: <br>&emsp; + Security Group <br>&emsp; + Network ACL                                  | 09/26/2025   | 09/26/2025       | <https://000003.awsstudygroup.com/>        |
| 5    | - **Thực hành VPC & Networking:** <br>&emsp; + Tạo VPC, Subnet, Internet Gateway, Route Table, Security Group <br>&emsp; + Bật VPC Flow Logs <br>&emsp; + Tạo EC2 trong VPC và test kết nối <br>&emsp; + Đọc và hiểu các bước cấu hình Site-to-Site VPN   | 09/27/2025   | 09/27/2025       | <https://000003.awsstudygroup.com/>        |

---

### Thành tựu Tuần 3:

* Hiểu rõ hơn về các thành phần IAM trong kiểm soát truy cập:
  * IAM User, IAM Group  
  * IAM Policy và cách gán quyền  
  * IAM Role và trust relationship  

* Xây dựng được cấu trúc IAM cơ bản cho quản trị:
  * Tạo Admin Group, Admin User  
  * Kiểm tra quyền dựa trên group thay vì gán trực tiếp  

* Thực hành mô hình phân quyền nâng cao:
  * Tạo Admin Role và OperatorUser  
  * Cấu hình và test Switch Role trong Console  
  * Áp dụng nguyên tắc least privilege khi phân quyền  

* Nắm được các khái niệm chính của Amazon VPC:
  * Subnet, Route Table, Internet Gateway, NAT Gateway  
  * Phân biệt Security Group và Network ACL  

* Tự tay xây dựng một môi trường VPC nhỏ:
  * Tạo VPC, subnet, routing, lớp bảo mật  
  * Khởi tạo EC2 trong VPC và kiểm tra kết nối  
  * Bật VPC Flow Logs để quan sát traffic  

* Nắm được luồng tổng quát để thiết lập AWS Site-to-Site VPN cho môi trường hybrid.
