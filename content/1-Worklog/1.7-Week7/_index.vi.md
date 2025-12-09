---
title: "Worklog Tuần 7"
date: "2025-10-24"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:

* Tìm hiểu toàn bộ IAM: user, group, role, policy, permission boundary.
* Tìm hiểu cơ chế xác thực và phân quyền trong AWS, cách viết policy JSON và cách evaluate.
* Làm quen AWS Organizations, OU, Service Control Policy (SCP).
* Thực hành lab IAM + Organization để hình dung cách quản lý tài khoản ở quy mô lớn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                  |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | --------------------------------------------------------------------------------------------------------------- |
| 2   | - Tìm hiểu tổng quan IAM: user, group, role, policy <br> - Nắm cách hoạt động của policy evaluation: explicit deny, implicit deny, allow                                                                      | 20/10/2025   | 20/10/2025      | <https://youtu.be/tsobAlSg19g?si=9f3mlIWPtrCcNuKg> <br><br> <https://youtu.be/N_vlJGAqZxo?si=e8oiWCObco95CoKh>  |
| 3   | - **Thực hành:** <br>&emsp; + Create user/group/role <br>&emsp; + Gán inline policy & managed policy <br>&emsp; + Test truy cập S3/EC2 theo từng policy <br> - Tìm hiểu permission boundary và session policy | 21/10/2025   | 21/10/2025      | <https://000028.awsstudygroup.com>                                                                              |
| 4   | - Tìm hiểu AWS Organizations: cấu trúc OU, tạo nhiều account <br> - Khái niệm SCP, deny list, allow list                                                                                                      | 22/10/2025   | 22/10/2025      | <https://youtu.be/5oQY8Rogz9Y?si=h8DlUb8ZLI4HbbvM>  <br><br> <https://youtu.be/NW1xrMkNMjU?si=dhT0T3y2JYVK8QwT> |
| 5   | - **Thực hành:** <br>&emsp; + Create Organization + OU <br>&emsp; + Áp dụng SCP deny Ec2 / deny S3 <br>&emsp; + Kiểm tra hiệu lực SCP kết hợp IAM polic <br>&emsp; + Sắp xếp lại OU, remove SCP               | 23/10/2025   | 23/10/2025      | <https://000030.awsstudygroup.com> <br><br> <https://000044.awsstudygroup.com/>                                 |
| 6   | - **Làm việc nhóm:** <br>&emsp; + Thảo luận ý tưởng về workshop <br>&emsp; + Cách thực hiện <br>&emsp; + Chia phần cho workshop                                                                               | 24/10/2025   | 24/10/2025      |                                                                                                                 |


### Kết quả đạt được tuần 7:

* Tổng quát: 
  * Trong tuần này tôi đã nắm được nền tảng quản lý truy cập AWS, bao gồm IAM và Organizations. Hiểu cách vận hành của policy, cách viết, cách đánh giá quyền, và cách áp dụng SCP trong môi trường nhiều account.
  

* Lý thuyết đã học:
  * Khái niệm về User – Group – Role – Policy và cơ chế evaluate
  * Inline policy, managed policy, permission boundary
  * Cấu trúc AWS Organizations, OU
  * Khái niệm SCP và sự khác biệt so với IAM policy
  * Landing Zone – Control Tower overview

  
* Thực hành với bài lab:
  * Tạo user/group/role và test truy cập
  * Viết policy JSON và thử deny/allow theo từng hành vi
  * Tạo Organization, OU và áp SCP
  * Kiểm tra sự kết hợp SCP + IAM policy trong thực tế