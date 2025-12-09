---
title: "Worklog Tuần 10"
date: "2025-11-14"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Hoàn thiện 100% Backend CRUD bằng .NET chạy trên Aspire AppHost.
* Xây dựng và kiểm thử mô hình dữ liệu DynamoDB trên môi trường local (Docker).
* Tích hợp DynamoDB Local với NoSQL Workbench để validate mô hình.
* Làm việc cùng nhóm FE để hoàn thiện giao diện cơ bản và kết nối API local.
* Chuẩn bị nền tảng vững chắc trước khi chuyển sang tuần 11 (chuyển code lên Lambda + API Gateway).


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------- |
| 2   | - Kiểm tra & cài đặt lại môi trường BE: .NET SDK, Docker Desktop, NoSQL Workbench <br> - Nắm sơ đồ kiến trúc hệ thống và luồng xử lý backend | 10/11/2025   | 10/11/2025      |
| 3   | - Setup DynamoDB Local bằng Docker <br> - Kết nối & trực quan hóa bằng NoSQL Workbench, test CRUD thủ công                                   | 11/11/2025   | 11/11/2025      |                |
| 4   | - Code DAL/Repository bằng .NET + AWSSDK.DynamoDBv2 <br> - Tích hợp DI vào Aspire AppHost <br> - Viết logic nghiệp vụ tại BLL                | 12/11/2025   | 12/11/2025      |                |
| 5   | - Viết API Controllers CRUD  <br> - Test unit & integration trên môi trường local  <br>                                                      | 13/11/2025   | 13/11/2025      |                |
| 6   | - Làm việc chung với nhóm FE <br> - Build giao diện sơ bộ (List/Create) <br> - FE kết nối API Local, test end-to-end                         | 14/11/2025   | 14/11/2025      |                |


### Kết quả đạt được tuần 10:

* Tổng quát:
  * Trong tuần này tôi đã hoàn thiện toàn bộ phần backend chạy local bằng Aspire AppHost, xây dựng mô hình dữ liệu DynamoDB, test CRUD và tích hợp với frontend. Nhờ đảm bảo kiến trúc và code local hoàn chỉnh, tôi có nền tảng vững chắc để chuyển sang Lambda/API Gateway ở tuần 11.

* Lý thuyết đã học:
  * Thiết kế dữ liệu DynamoDB theo Single-Table Design, Access Pattern, PK/SK.
  * Kiến thức về DynamoDB Local, NoSQL Workbench, Docker setup.
  * Cách sử dụng AWSSDK.DynamoDBv2 trong .NET và tích hợp DI.
  * Cấu trúc Backend ASP.NET (Controller -> BLL -> Repository).
  * Cách FE gọi API local, xử lý response và render dữ liệu.

* Thực hành / Sản phẩm:
  * Tạo DynamoDB Local bằng Docker và quản lý schema qua NoSQL Workbench.
  * Build Repository + BLL + Controllers bằng .NET 8 / Aspire AppHost.
  * Hoàn thiện 5–6 API CRUD (POST/GET/PUT/DELETE/List).
  * Viết unit test cho BLL và integration test cho API.
  * FE team triển khai giao diện List + Create và test thành công với API local.