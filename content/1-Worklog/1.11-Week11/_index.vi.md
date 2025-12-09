---
title: "Worklog Tuần 11"
date: "2025-11-21"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---


### Mục tiêu tuần 11:

* Hoàn thiện giao diện FE cùng nhóm Frontend.
* Phối hợp kiểm thử end-to-end giữa FE và BE.
* Tìm hiểu quy trình deploy tổng thể hệ thống (API, FE, cơ sở dữ liệu, hạ tầng) để nắm kiến thức chung, dù không phải người chịu trách nhiệm chính.
* Chuẩn bị các ghi chú cần thiết cho tuần 12 (viết tài liệu & tổng kết).
  
### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------- |
| 2   | - Làm việc chung với nhóm FE để hoàn thiện giao diện còn thiếu <br> - - Rà soát lại API contract giữa FE và BE                                    | 17/11/2025   | 17/11/2025      |
| 3   | - FE tích hợp API đầy đủ các luồng CRUD <br> - Fix lỗi sai schema, payload, status code trong quá trình FE test                                   | 18/11/2025   | 18/11/2025      |                |
| 4   | - Test end-to-end toàn bộ luồng: List -> Create -> Update -> Delete từ FE tới BEI <br> - Cập nhật lại response model/validation cho phù hợp FE    | 19/11/2025   | 19/11/2025      | <              |
| 5   | - Tìm hiểu quy trình deploy của nhóm (CI/CD, API Gateway, Lambda, S3 + CloudFront) <br> - Ghi chú các bước để chuẩn bị cho tuần 12 viết tài liệu  | 20/11/2025   | 20/11/2025      |                |
| 6   | - Tổng hợp issue FE và BE trong tuần <br>&emsp; + - Rà soát lại toàn bộ phần BE để chuẩn bị cho môi trường deploy (dù không trực tiếp triển khai) | 21/11/2025   | 21/11/20255     |                |


### Kết quả đạt được tuần 11:

* Tổng quát:
  * Trong tuần này tôi chủ yếu phối hợp với nhóm FE để hoàn thiện giao diện và tích hợp API. Sau khi BE đã xong ở tuần 10, tôi hỗ trợ fix lỗi, chuẩn hóa contract API và kiểm thử end-to-end. Ngoài ra, tôi cũng tìm hiểu quy trình deploy của nhóm (Lambda, API Gateway, S3/CloudFront, CI/CD) để chuẩn bị cho việc viết tài liệu ở tuần 12.

* Lý thuyết đã học:
  * Cách FE gọi API CRUD và debug request.
  * API Contract: schema input/output, error format, status code.
  * Quy trình deploy: .NET -> Lambda, API Gateway routing, FE build -> S3/CloudFront.
  * Tổng quan CI/CD pipeline và chuẩn bị code cho deploy (config, logging).

* Thực hành / Sản phẩm:
  * Phối hợp FE hoàn thiện màn hình List/Create/Update/Delete.
  * Điều chỉnh backend theo yêu cầu FE (schema, validation, status code).
  * Test end-to-end toàn bộ luồng FE ↔ BE trên local.
  * Ghi chú quy trình deploy để dùng cho tuần 12.
  * Tổng hợp lỗi FE và BE và cập nhật backlog nhóm.