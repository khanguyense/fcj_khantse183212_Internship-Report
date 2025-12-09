---
title: "Worklog Tuần 5"
date: "2025-10-10"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---


### Mục tiêu tuần 5:

* Tìm hiểu các thành phần chính của EC2 và cách vận hành compute trong AWS.
* Nắm cơ chế Auto Scaling, EBS, Instance Store, User Data, Metadata.
* Thực hành backup, Storage Gateway và triển khai EC2 phục vụ cho lưu trữ.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                                                                                                                                                                                                                                                                                                                             |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - Tìm hiểu về EC2, các loại instance, AMI, key pair <br> - Biết được EBS, Instance Store, User Data, Metadata                                                                                                                                          | 06/10/2025   | 06/10/2025      | <https://youtu.be/-t5h4N6vfBs?si=GeVdhO9IEDjzzS_D> <br><br> <https://youtu.be/e7XeKdOVq40?si=T3I4pgPoEfVytcU3> <br><br> <https://youtu.be/yAR6QRT3N1k?si=GQghyBwLCpijrDON> <br><br> <https://youtu.be/hKr_TfGP7NY?si=gR2MqaLAFrqL-KBo> <br><br> <https://youtu.be/6IHNDJ85aoQ?si=M0puk6DJpliO7ahf> <br><br> <https://youtu.be/_v_43Wi7zjo?si=qNDVWzKcQFNO2mGh> <br><br> <https://youtu.be/Ew3QRaKJQSA?si=xNvXvD8yFhnSMJby> |
| 3   | - Nắm bắt được EC2 Auto Scaling và cách scale VM <br> -  tìm hiểu về các dịch vụ lưu trữ và compute (EFS/FSx, Lightsail, MGN overview)                                                                                                                 | 07/10/2025   | 07/10/2025      | <https://youtu.be/bbLcPitXJSY?si=eyVnxvL9ho0LpUYy> <br><br> <https://youtu.be/hFVYG8WqfU0?si=9Px4wmR4IRZxk15n>                                                                                                                                                                                                                                                                                                             |
| 4   | - **Thực hành:** <br>&emsp; +  Deploy AWS Backup  <br>&emsp; + Create backup plan <br>&emsp; + Test restore & cleanup <br>&emsp; + Dọn dẹp backup                                                                                                      | 08/10/2025   | 08/10/2025      | <https://000013.awsstudygroup.com>                                                                                                                                                                                                                                                                                                                                                                                         |
| 5   | - **Thực hành:** <br>&emsp; + Create S3 bucket để làm Storage Gateway <br>&emsp; + Create EC2 cho Storage Gateway <br>&emsp; + Create Storage Gateway + File Share <br>&emsp; + Dọn dẹp Storage Gateway                                                | 09/10/2025   | 09/10/20255     | <https://000024.awsstudygroup.com>                                                                                                                                                                                                                                                                                                                                                                                         |
| 6   | - **Thực hành:** <br>&emsp; + Create bucket, upload dữ liệu <br>&emsp; + Enable static website hosting <br>&emsp; + Cấu hình public access block <br>&emsp; + Cấu hình CloudFront và test website  <br>&emsp; +  Dọn dẹp website + CloudFront + bucket | 10/10/2025   | 10/10/2025      | <https://000057.awsstudygroup.com>                                                                                                                                                                                                                                                                                                                                                                                         |


### Kết quả đạt được tuần 5:

* Tổng quát: 
  * Trong tuần này tôi đã hiểu cơ chế vận hành EC2, các loại storage của instance, Auto Scaling và backup. Đồng thời làm quen Storage Gateway và triển khai S3 static website

* Lý thuyết đã học:
  * Khái niệm về kiến trúc EC2, AMI, key pair
  * EBS vs Instance Store
  * User Data / Metadata
  * EC2 Auto Scaling
  * Storage Gateway và nền tảng về Backup

  
* Thực hành với bài lab:
  * Tạo backup plan + test restore
  * Tạo Storage Gateway + file share
  * Tạo static website bằng S3 + CloudFront

