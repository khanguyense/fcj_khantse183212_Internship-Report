---
title: "Translated Blogs"
date: "2025-10-5"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã dịch. Ví dụ:

###  [Blog 1 - Tăng cường deployment guardrails với tính năng rolling update cho inference component trên Amazon SageMaker AI inference](3.1-Blog1/)
Amazon SageMaker AI hiện đã hỗ trợ triển khai cuộn (rolling updates) cho inference components, giúp giải quyết các vấn đề chính của mô hình triển khai blue/green truyền thống—như chi phí GPU cao, hạn chế về dung lượng và rủi ro khi chuyển toàn bộ lưu lượng cùng lúc—đặc biệt đối với các mô hình LLM lớn chạy trên những phiên bản GPU đắt tiền. Inference component vốn đã giúp tối ưu bằng cách “right-size” tài nguyên và mở rộng theo từng mô hình, và rolling updates mở rộng lợi ích này bằng cách cập nhật các bản sao của mô hình theo từng lô có thể cấu hình, chỉ tạm thời bổ sung vừa đủ tài nguyên cho mỗi bước, chuyển lưu lượng sang phiên bản mới rồi giải phóng dần tài nguyên của phiên bản cũ. Bạn có thể kiểm soát kích thước batch, thời gian chờ, chiến lược rollback và khoảng thời gian đợi giữa các bước thông qua RollingUpdatePolicy trong UpdateInferenceComponent, trong khi các cảnh báo CloudWatch có thể kích hoạt rollback tự động, có kiểm soát nếu có sự cố xảy ra. Ví dụ, với ba phiên bản đơn GPU, SageMaker có thể cập nhật từng bản sao một bằng cách khởi chạy một instance mới, xác thực hoạt động, rồi loại bỏ một bản sao cũ, lặp lại cho đến khi tất cả được cập nhật—đạt được khả năng không gián đoạn dịch vụ, kiểm thử an toàn hơn và triển khai tiết kiệm chi phí, đáng tin cậy hơn cho nhiều kích cỡ mô hình khác nhau.
###  [Blog 2 - Nâng cao hiệu quả đào tạo phân tích bộ gen vi khuẩn với Amazon WorkSpaces](3.2-Blog2/)
Trung tâm Nghiên cứu Y khoa Siriraj với chuỗi hội thảo “Nanopore workshop: bacterial genome bioinformatics series” cần môi trường tính toán mạnh mẽ, đồng nhất cho hơn 60 nhà nghiên cứu, nhưng gặp phải nhiều trở ngại lớn: người tham gia sử dụng laptop cá nhân rất khác nhau về hệ điều hành, cấu hình CPU và RAM, nhiều máy không đủ mạnh cho các tác vụ phân tích bộ gen vi khuẩn nặng; việc cài đặt và cấu hình các công cụ tin sinh học phức tạp như EPI2ME trên từng thiết bị cá nhân tốn thời gian và dễ phát sinh lỗi; và hạ tầng tại chỗ hạn chế khiến việc mở rộng quy mô hay hỗ trợ các buổi đào tạo hybrid/online gặp nhiều khó khăn. Bằng cách sử dụng Amazon WorkSpaces—các desktop ảo trên đám mây có thể chạy nhiều hệ điều hành Windows hoặc Linux khác nhau và truy cập từ nhiều thiết bị—họ có thể cung cấp tập trung các môi trường mạnh, được cấu hình sẵn, tránh nhu cầu mua sắm phần cứng và cài đặt riêng lẻ cho từng người, từ đó mang lại trải nghiệm đào tạo thực hành về vi sinh bộ gen mượt mà, linh hoạt và dễ mở rộng hơn.
###  [Blog 3 - Thông báo kết thúc hỗ trợ và khả năng khám phá nâng cao cho Amazon EKS](3.3-Blog3/)
Trong thế giới ứng dụng container hóa đang phát triển nhanh chóng, việc duy trì khả năng chịu lỗi (resilience) và quan sát (observability) trên các môi trường Kubernetes trở thành một thách thức quan trọng. Khi các tổ chức ngày càng sử dụng Amazon Elastic Kubernetes Service (Amazon EKS) để quản lý khối lượng công việc chạy trên container, nhu cầu về quản lý vòng đời phiên bản cụm (cluster version lifecycle) và cơ chế khám phá (discovery) trở nên thiết yếu. Khi các môi trường Amazon EKS ngày càng phức tạp và mở rộng ra nhiều Vùng (Region) và tài khoản AWS khác nhau, người dùng thường gặp khó khăn trong việc theo dõi phiên bản cụm, vòng đời hỗ trợ và trạng thái triển khai tổng thể.

Việc giám sát chủ động vòng đời và thời điểm kết thúc hỗ trợ của các cụm EKS là rất quan trọng để đảm bảo tính bảo mật, ổn định và tuân thủ cho các triển khai Kubernetes. Bên cạnh đó, việc có được khả năng quan sát rõ ràng đối với các cụm EKS trên toàn bộ một AWS Organization là điều cần thiết cho quản lý tài nguyên hiệu quả, lập kế hoạch chiến lược và duy trì một “inventory” chính xác.
