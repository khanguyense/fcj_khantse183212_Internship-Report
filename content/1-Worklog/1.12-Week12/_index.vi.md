---
title: "Nhật ký công việc"
date: "2025-12-09"
weight: 12
chapter: false
pre: " <b> 12. </b> "
---
# Worklog Tuần 12

## Mục tiêu Tuần 12
- Nắm vững quy trình triển khai hạ tầng AWS bằng CDK và hiểu rõ mối quan hệ giữa các stack (VPC, RDS, Lambda, S3, API Gateway).
- Hoàn thiện logic backend cho module admin, bao gồm xử lý dữ liệu, analytics và cơ chế lưu trữ/archiving từ RDS → S3.
- Tối ưu cấu trúc hệ thống, refactor code backend và dashboard theo hướng tách riêng business layer – dễ bảo trì – dễ mở rộng.
- Nghiên cứu và triển khai các cải tiến để xử lý dữ liệu hiệu quả hơn (checksum, giới hạn dữ liệu load, tối ưu logic đồng bộ).
- Thành thạo quản lý tài nguyên AWS thông qua CLI và Console, đảm bảo có thể chạy nhiều lần deploy mà không bị xung đột.

## Các công việc cần thực hiện trong tuần

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | ---------------- | ------------------ |
| 2 | Refactor quy trình deploy và comment các thành phần analytics không sử dụng.<br>Điều chỉnh `app.py` để luôn deploy VPC, RDS và DB Init Stack; bật `DashboardStack` với dependency đúng.<br>Comment toàn bộ tài nguyên Glue, archive và analytics (Lambda/EventBridge + API) trong `dashboard_stack.py`.<br>Giảm kích thước instance RDS (SMALL → MICRO) và đặt storage = 20GB. | 24/11/2025 | 24/11/2025 |  |
| 3 | Bắt đầu deploy `AppStack`, `DashboardStack` và `DBInitStack` để hỗ trợ backend cho admin.<br>Sửa lỗi do cấu hình max AZ = 1 khi tạo RDS (AWS yêu cầu tối thiểu 2 AZ). Mặc dù tạo 2 AZ, nhưng chế độ Multi-AZ **không** được bật, chỉ thêm subnet – nên không phát sinh thêm chi phí.<br>Refactor API: xử lý body dạng string trả về từ API Gateway, cập nhật đường dẫn endpoint, cải thiện logging.<br>Cập nhật CDK: dùng secret đúng cho Lambda, cập nhật VPC/subnet, thêm rule SG cho HTTPS, comment endpoint Bedrock không dùng.<br>Cập nhật cơ chế đóng gói asset (dùng `cp -r` thay cho `cp -au`).<br>Tổ chức lại luồng nghiệp vụ admin: quản lý lịch hẹn, gán consultant cho timeslot và tạo báo cáo tổng hợp lịch hẹn hằng ngày.<br>Admin upload file SQL → `ArchiveData` lưu vào S3 → các lần deploy sau sẽ load từ S3 thay vì phải upload lại.<br>Định hướng tương lai: cho phép Lambda `index.py` đọc schema khi deploy và load dữ liệu từ S3 – khả thi.<br>Định hướng dài hạn: migrate toàn bộ dữ liệu on-premise lên S3; Lambda sẽ đẩy dữ liệu khởi tạo vào RDS ở lần deploy đầu tiên; các cập nhật dữ liệu mới sẽ do `ArchiveData` xử lý. | 25/11/2025 | 25/11/2025 |  |
| 4 | Hardcode schema trong `index.py` và xóa các file schema khỏi thư mục project.<br>Xử lý data mới và lưu CSV phục vụ cho việc tạo DDL Athena sau này.<br>Thêm API và UI tổng quan cho dashboard; refactor lại logic database cho admin.<br>Thêm API thống kê tổng hợp: tổng quan, khách hàng, consultant, lịch hẹn, chương trình cộng đồng; cập nhật UI dashboard để hiển thị các số liệu này.<br>Refactor `DatabasePage`: loại bỏ tính năng chạy raw SQL, tập trung vào schema + analytics.<br>Cập nhật CDK + IAM role cho S3 bucket mới và phân quyền phù hợp.<br>Di chuyển toàn bộ business logic của admin dashboard vào một service class riêng (`code/services/admin.py`).<br>Đổi tên `AdminStack` → `FrontendStack` cho đúng với trách nhiệm; cập nhật toàn bộ tham chiếu. | 26/11/2025 | 26/11/2025 |  |
| 5 | Họp team để thiết kế chiến lược load dữ liệu từ S3 vào RDS mỗi khi RDS được khởi động.<br>Yêu cầu: tránh load toàn bộ dataset mỗi lần. Dữ liệu động (lịch hẹn, lịch làm việc) thay đổi thường xuyên → không thể reload tất cả.<br>Giải pháp: giới hạn dữ liệu được load. Dữ liệu tĩnh (thông tin consultant) nên load toàn bộ. Dữ liệu động theo thời gian (lịch hẹn) chỉ nên load có điều kiện, ví dụ: trong khoảng thời gian liên quan đến thao tác của admin.<br>Cách làm hiện tại: load dữ liệu trong khoảng ±1 ngày so với ngày hiện tại.<br>Cập nhật `vpc_stack` để import S3 bucket được tạo thủ công bằng CLI.<br>Lệnh CLI:<br>`aws s3 mb s3://meetassist-data-<account-id>-ap-southeast-1 --region ap-southeast-1`<br>Dọn dẹp `DashboardStack`, loại bỏ các đoạn code Glue & analytics đã lỗi thời.<br>Cập nhật API cho customer và consultant; cải thiện logging cho Lambda `AdminManager`. | 27/11/2025 | 27/11/2025 |  |
| 6 | Quản lý rule EventBridge cho Lambda `ArchiveData` (bật/tắt/kiểm tra trạng thái/gọi thủ công).<br><br>Disable: `aws events disable-rule --name MeetAssist-ArchiveSchedule`<br>Enable: `aws events enable-rule --name MeetAssist-ArchiveSchedule`<br>Check status: `aws events describe-rule --name MeetAssist-ArchiveSchedule`<br>Invoke: `aws lambda invoke --function-name DashboardStack-ArchiveData --payload "{}" --cli-binary-format raw-in-base64-out NUL`<br><br>Sửa lỗi CSV UTF-8 khi mở bằng Excel; `index.py` hiện hỗ trợ cả UTF-8 và UTF-8 BOM.<br>Triển khai logic checksum cho `ArchiveData` để tránh upload lại CSV không đổi → giảm chi phí S3 PUT.<br>Phương án 1: Không dùng checksum (luôn overwrite) – đơn giản nhưng timestamp “ồn ào” và chi phí cao hơn.<br>Phương án 2 (khuyến nghị): Dùng checksum (MD5). Nếu không đổi → bỏ qua; nếu khác → upload.<br>Tạo `archive_info.json` trong S3 để:<br>- Theo dõi trạng thái archiving<br>- Lưu checksum<br>- Ghi lại metrics, lỗi, thời gian cập nhật gần nhất<br>- Có thể dùng về sau trong dashboard<br>Triển khai cơ chế archiving RDS → S3 bằng Lambda chạy theo lịch:<br>- Tạo `ArchiveService` để export CSV + upload lên S3 + ghi metadata<br>- `archive_handler` chạy theo lịch (5 phút/lần, mặc định tắt)<br>- Tự động bỏ qua các bảng không thay đổi dựa trên checksum<br>Cập nhật CDK để deploy Lambda + IAM + rule EventBridge.<br>Cải thiện xử lý lỗi cho các luồng consultant/appointment/program.<br>Cập nhật docstring của `dashboard_handler` để mô tả rõ ràng ranh giới giữa luồng CRUD và luồng archiving. | 28/11/2025 | 28/11/2025 |  |

## Thành tựu Tuần 12
- Refactor toàn bộ backend & hạ tầng để tối ưu hơn và dễ bảo trì hơn.
- Nắm vững cách deploy và cấu hình VPC, RDS, S3, Lambda và EventBridge bằng CDK.
- Hoàn thành toàn bộ API cho dashboard và admin phục vụ analytics và nghiệp vụ quản lý.
- Tối ưu luồng import & archive dữ liệu giữa RDS ↔ S3.
- Xây dựng cơ chế checksum để giảm chi phí S3 và cải thiện hiệu quả xử lý dữ liệu.
- Tách biệt rõ ràng business logic vào các service class để dễ test và mở rộng.
- Cải thiện logging, debugging và cấu trúc tích hợp giữa API Gateway – Lambda.
- Hoàn tất quá trình migrate dữ liệu từ on-premise lên cloud và đảm bảo xử lý đúng trong các lần redeploy.
