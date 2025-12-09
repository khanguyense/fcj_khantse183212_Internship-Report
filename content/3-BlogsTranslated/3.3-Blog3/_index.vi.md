---
title: "Blog 3"
date: "2025-10-16"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
**Nâng cao hiệu quả đào tạo phân tích bộ gen vi khuẩn với Amazon WorkSpaces**

**Tác giả:** Satsawat Natakarnkitkul, Charlie Lee, và Sikharin Kongpaiboon

**Ngày đăng:** ngày 04 tháng 04 năm 2025|

**Danh mục:** [Amazon WorkSpaces](https://aws.amazon.com/blogs/publicsector/category/end-user-computing/amazon-workspaces/), [Education](https://aws.amazon.com/blogs/publicsector/category/public-sector/education/),  [Healthcare](https://aws.amazon.com/blogs/publicsector/category/public-sector/healthcare-public-sector/),  [Higher education](https://aws.amazon.com/blogs/publicsector/category/public-sector/education/higher-education/),  [Public Sector](https://aws.amazon.com/blogs/publicsector/category/public-sector/education/higher-education/) | [Permalink](https://aws.amazon.com/blogs/publicsector/empowering-bacterial-genomics-education-with-amazon-workspaces/)|

![AWS Branded Background with text "Empowering bacterial genomics education with Amazon WorkSpaces"](data:image/jpeg;base64...)

Các hội thảo phân tích bộ gen vi khuẩn yêu cầu các công cụ bioinformatics chuyên biệt và sức mạnh tính toán lớn để xử lý dữ liệu giải trình tự. Khi Trung tâm Nghiên cứu Y khoa Siriraj lên kế hoạch tổ chức “Hội thảo Nanopore: chuỗi hội thảo tin sinh học về bộ gen vi khuẩn” cho hơn 60 nhà nghiên cứu, họ đã gặp phải thách thức phổ biến: làm thế nào để cung cấp môi trường tính toán hiệu suất cao, đồng nhất cho các phân tích bộ gen phức tạp. Amazon Web Services (AWS) đã giải quyết vấn đề này thông qua [Amazon WorkSpaces](https://aws.amazon.com/workspaces-family/workspaces/), thay đổi cách Trung tâm Nghiên cứu Y khoa Siriraj cung cấp đào tạo thực hành về bộ gen vi khuẩn.

Bạn có thể sử dụng Amazon WorkSpaces để cấp phát các máy tính để bàn ảo trên nền tảng đám mây, gọi là *WorkSpaces*, cho người dùng của mình. Những máy tính để bàn này có thể chạy Microsoft Windows, Amazon Linux 2, Ubuntu Linux, Rocky Linux hoặc Red Hat Enterprise Linux. WorkSpaces loại bỏ nhu cầu mua sắm và triển khai phần cứng hoặc cài đặt phần mềm phức tạp. Bạn có thể nhanh chóng thêm hoặc bớt người dùng khi nhu cầu thay đổi. Người dùng có thể truy cập máy tính để bàn ảo của mình từ nhiều thiết bị hoặc trình duyệt web khác nhau. Với những lợi ích này, người dùng có thể làm việc hiệu quả mà không cần phải lo lắng về máy tính để bàn của họ.

# **Thách thức**

Các hội thảo đào tạo về bộ gen vi khuẩn do Trung tâm Nghiên cứu Y khoa Siriraj tổ chức thường gặp phải nhiều khó khăn tài nguyên tính toán, cài đặt phần mềm, cũng như khả năng tiếp cận và mở rộng cơ sở hạ tầng.

Một trong những thách thức lớn nhất là sự khác biệt về cấu hình phần cứng giữa các học viên. Nhiều người dùng phải sử dụng laptop cá nhân với hệ điều hành, tốc độ xử lý, bộ nhớ khác nhau, dẫn đến hiệu suất không đồng đều. Sự khác biệt này thường gây ra lỗi hệ thống, tốc độ xử lý chậm và không thể chạy các phân tích genome đòi hỏi tài nguyên lớn hiệu quả.

Việc cài đặt và cấu hình phần mềm là trở ngại chính. Các công cụ bioinformatics như [EPI2ME](https://epi2me.nanoporetech.com/), phổ biến trong việc lắp ráp và phân tích bộ gen vi khuẩn, yêu cầu các gói phụ thuộc (dependencies) và cấu hình đặc thù. Đảm bảo tương thích trên nhiều thiết bị khác nhau thường làm gián đoạn tiến độ, khiến giảng viên mất thời gian xử lý sự cố thay vì tập trung vào thực hành.

Xử lý dữ liệu bộ gen vi khuẩn cần máy tính mạnh mà phần đông học viên không có sẵn. Thiếu tài nguyên tính toán dẫn đến việc không hoàn thành bài tập, gây thất vọng và làm giảm hiệu quả học tập. Laptop cá nhân thường không đủ khả năng xử lý các phép tính phức tạp trong phân tích dữ liệu DNA, làm hạn chế việc thực hành.

Phương pháp giảng dạy truyền thống cũng giới hạn số lượng học viên mà tổ chức có thể đào tạo. Nhiều tổ chức thiếu cơ sở hạ tầng cần thiết để đáp ứng nhu cầu đào tạo ngày càng tăng, đặc biệt cho các buổi đào tạo kết hợp hoặc trực tuyến.

# **Xây dựng môi trường học tập trên nền tảng đám mây**

[Oxford Nanopore Centre of Excellence (Thái Lan)](https://www.longreadlab.com/), [Yip In Tsoi ( Đối tác AWS)](https://partners.amazonaws.com/partners/001E000001HPK4zIAH/YIP%20IN%20TSOI) và AWS đã phối hợp khởi xướng và tổ chức một hội thảo nhằm giải quyết những thách thức cấp bách này trong đào tạo tin sinh học, đặc biệt liên quan đến giới hạn phần cứng, vấn đề tương thích phần mềm, và sức mạnh tính toán. Hội thảo hợp tác này sử dụng WorkSpaces như một môi trường tính toán tập trung trên đám mây cho tất cả học viên, cung cấp một môi trường học tập tiêu chuẩn trên đám mây. WorkSpaces là dịch vụ máy tính để bàn ảo được quản lý toàn phần, cung cấp tài nguyên tính toán đã được cấu hình sẵn, giúp đảm bảo mọi học viên có cùng môi trường làm việc.

Một trong những lợi ích chính của WorkSpaces là loại bỏ sự trì hoãn do cài đặt và cấu hình phần mềm. Tất cả các công cụ bioinformatics cần thiết cho hội thảo—bao gồm EPI2ME—đã được cài đặt sẵn và tối ưu, giúp học viên bắt đầu thực hành ngay lập tức.

Sức mạnh tính toán của WorkSpaces đóng vai trò quan trọng nâng cao trải nghiệm hội thảo. Nhờ truy cập nguồn tài nguyên đám mây mạnh mẽ, học viên có thể thực hiện lắp ráp bộ gen, căn chỉnh trình tự, và phân tích so sánh genome mà không gặp giới hạn về hiệu suất. Sự đồng đều trong tài nguyên tính toán giúp mọi học viên hoàn thành bài tập cùng tiến độ, tạo môi trường học tập hiệu quả hơn.

Khả năng mở rộng và tiếp cận cũng là điểm mạnh của WorkSpaces. Học viên có thể đăng nhập WorkSpaces từ bất kỳ thiết bị nào, loại bỏ giới hạn về địa lý và phần cứng. Tính linh hoạt của WorkSpaces cũng giúp tổ chức dễ dàng đáp ứng số lượng học viên lớn mà không phải lo lắng về hạ tầng tính toán.

# **Kết quả hội thảo**

Trong ba ngày hội thảo, WorkSpaces được sử dụng rộng rãi. Học viên tham gia các bài tập như giải trình tự bằng công nghệ Oxford Nanopore (ONT), lắp ráp bộ gen bằng EPI2ME, và phân tích so sánh bộ gen gồm cgMLST và nghiên cứu ổ dịch.

Việc triển khai WorkSpaces giúp hội thảo diễn ra suôn sẻ mà không gặp khó khăn kỹ thuật, cải thiện đáng kể so với các lần trước khi việc cài đặt và khắc phục lỗi có thể mất đến 3 giờ đồng hồ. Hiệu suất tính toán được giữ ổn định, giúp học viên tập trung phân tích dữ liệu thay vì gặp sự cố hoặc xử lý chậm.

Phản hồi từ học viên cho thấy WorkSpaces đã giúp nâng cao hiệu quả đào tạo tin sinh học. Nhiều học viên cho biết môi trường tính toán tiêu chuẩn giúp họ tập trung vào nội dung học mà không phải lo ngại về hạn chế phần cứng hay lỗi phần mềm. Giảng viên cũng nhận thấy hiệu quả giảng dạy được cải thiện rõ rệt khi không phải mất thời gian xử lý các vấn đề kỹ thuật.

# **Tương lai phát triển**

Việc tích hợp thành công WorkSpaces với hội thảo Nanopore cho thấy công nghệ đám mây có thể thay đổi cách đào tạo. Bởi vì các rào cản công nghệ truyền thống đã được loại bỏ, học viên có thể tập trung hơn vào phân tích bộ gen vi khuẩn.

Trong tương lai, có tiềm năng mở rộng sử dụng WorkSpaces trong các chương trình đào tạo genomics khác—đặc biệt là các dự án quy mô lớn—như:

* Nâng cao khả năng phân tích bộ gen với [AWS HealthOmics](https://aws.amazon.com/healthomics/)
* Xử lý và phân tích bộ dữ liệu lớn với [AWS Batch](https://aws.amazon.com/batch)
* Tự động hóa quy trình phân tích genome với [AWS Lambda](https://aws.amazon.com/lambda)

Những giải pháp này có thể cải thiện hơn nữa giáo dục tin sinh học bằng cách tối ưu hóa quy trình phân tích dữ liệu. Các tổ chức cũng đang nghiên cứu tích hợp WorkSpaces vào các mô hình học từ xa, giúp mở rộng sự tham gia của sinh viên và nhà nghiên cứu trên toàn cầu.

Để tìm hiểu thêm và bắt đầu, hãy liên hệ với nhóm tài khoản AWS của bạn hoặc nhóm hỗ trợ [AWS Public Sector team.](https://aws.amazon.com/government-education/contact/)

# **Tài nguyên bổ sung**

* [Genomics on AWS](https://aws.amazon.com/health/genomics/)
* [Amazon WorkSpaces Documentation](https://docs.aws.amazon.com/workspaces/)
* [Siriraj Long-read Lab (Si-LoL), Oxford Nanopore Centre of Excellence (Thailand)](https://www.longreadlab.com/)

Được đồng viết bởi Oxford Nanopore Centre of Excellence (Thailand), YIP In Tsoi (Đối tác AWS), và AWS.

TAGS : [Amazon Workspaces](https://aws.amazon.com/blogs/publicsector/tag/amazon-workspaces/),[AWS education](https://aws.amazon.com/blogs/publicsector/tag/aws-education/),[AWS for higher education](https://aws.amazon.com/blogs/publicsector/tag/aws-for-higher-education/),[AWS healthcare](https://aws.amazon.com/blogs/publicsector/tag/aws-healthcare/), [genomics](https://aws.amazon.com/blogs/publicsector/tag/genomics/), [healthcare](https://aws.amazon.com/blogs/publicsector/tag/healthcare/)

# **Tác giả:** ![](data:image/png;base64...)

**Satsawat Natakarnkitkul:** Trưởng nhóm dữ liệu và AI cho khu vực ASEAN tại AWS Thái Lan, dẫn dắt các sáng kiến AI tạo sinh trên khắp Đông Nam Á. Với hơn một thập kỷ kinh nghiệm trong chuyển đổi số và các giải pháp AI/ML, ông là chuyên gia đầu ngành trong trí tuệ nhân tạo, khoa học dữ liệu, và kiến trúc đám mây. Ông thường xuyên phát biểu tại các sự kiện công nghệ khu vực ASEAN, và nhiệt huyết sử dụng công nghệ mới như AI tạo sinh để tạo giá trị thực tế trong khu vực công.

![](data:image/png;base64...)

**Charlie Lee:** Chuyên gia hàng đầu về ngành genomics khu vực châu Á - Thái Bình Dương và Nhật Bản của AWS, có bằng tiến sĩ khoa học máy tính chuyên sâu về tin sinh học. Ông là nhà lãnh đạo trong lĩnh vực tin sinh học, genomics, và chẩn đoán phân tử, đam mê thúc đẩy nghiên cứu và cải thiện chăm sóc sức khỏe qua genomics với các công nghệ giải trình tự tiên tiến và điện toán đám mây.![](data:image/png;base64...)

**Sikharin Kongpaiboon:** Kiến trúc sư giải pháp tại AWS, hỗ trợ khách hàng hiểu và áp dụng tốt nhất các giải pháp đám mây, tối ưu triển khai. Ông phối hợp chặt chẽ với khách hàng để thiết kế kiến trúc đám mây có khả năng mở rộng, linh hoạt, và chịu lỗi cao, giúp giải quyết các thách thức kinh doanh và tăng tính nhanh nhẹn, hiệu quả, và an toàn.

# **Các tài nguyên:**

[AWS in the Public Sector](https://aws.amazon.com/government-education?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=publicsector-resources)

[AWS for Government](https://aws.amazon.com/government-education/government/)

[AWS for Education](https://aws.amazon.com/education/)

[AWS for Nonprofits](https://aws.amazon.com/government-education/nonprofits/)

[AWS for Public Sector Health](https://aws.amazon.com/government-education/public-sector-healthcare/)

[AWS for Aerospace and Satellite Solutions](https://aws.amazon.com/government-education/aerospace-and-satellite/)

[Case Studies](https://aws.amazon.com/solutions/case-studies?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=publicsector-resources)

[Fix This Podcast](https://aws.amazon.com/government-education/fix-this/)

[Additional Resources](https://aws.amazon.com/government-education/resources?sc_ichannel=ha&sc_icampaign=acq_awsblogsb&sc_icontent=publicsector-resources)

[Contact Us](https://aws.amazon.com/government-education/contact/?trkCampaign=ps&trk=ps_blog_resources)