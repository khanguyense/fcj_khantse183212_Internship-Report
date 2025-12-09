---
title: "Blog 2"
date: "2025-10-15"
weight: 3
chapter: false
pre: " <b> 3.1 </b> "
---
# **Thông báo kết thúc hỗ trợ và khả năng khám phá nâng cao cho Amazon EKS**

Ngày 05 tháng 03 năm 2025

**Tác giả:** Praseeda Sathaye (Principal Solutions Architect, Containers & OSS), AJ Davis (AWS Enterprise Support) và Arvind Viswanathan (Principal Solutions Architect)

# Giới thiệu

Trong thế giới ứng dụng container hóa đang phát triển nhanh chóng, việc duy trì khả năng phục hồi và khả năng quan sát trên các môi trường Kubernetes đã trở thành một thách thức quan trọng. Khi các tổ chức ngày càng áp dụng [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS) để quản lý khối lượng công việc container hóa của họ, nhu cầu về quản lý vòng đời phiên bản cluster và cơ chế khám phá trở nên cực kỳ quan trọng. Khi môi trường Amazon EKS trở nên phức tạp hơn và mở rộng trên nhiều [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) và tài khoản, người dùng thường gặp khó khăn trong việc theo dõi phiên bản cluster, vòng đời hỗ trợ và trạng thái triển khai tổng thể.

Giám sát chủ động vòng đời cluster EKS và kết thúc hỗ trợ là rất quan trọng để đảm bảo tính bảo mật, ổn định và tuân thủ của các triển khai Kubernetes. Hơn nữa, việc có được khả năng hiển thị các triển khai cluster EKS trên toàn bộ [AWS Organization](https://aws.amazon.com/organizations/) là điều cần thiết cho việc quản lý tài nguyên hiệu quả, lập kế hoạch chiến lược và duy trì bảng kiểm kê chính xác.

Trong bài viết này, để giải quyết những điểm yếu này, chúng tôi chia sẻ hai giải pháp mạnh mẽ cung cấp khả năng quan sát các cluster EKS:

* Thông báo kết thúc hỗ trợ
* Khám phá và báo cáo

Giải pháp đầu tiên sử dụng [AWS Health](https://docs.aws.amazon.com/health/latest/ug/what-is-aws-health.html), [Amazon EventBridge](https://aws.amazon.com/eventbridge/) và [Amazon Simple Notification Service (Amazon SNS)/](https://aws.amazon.com/sns/)[Amazon Simple Queue Service (Amazon SQS](https://aws.amazon.com/sqs/)) để giám sát các sự kiện cụ thể của Amazon EKS, đặc biệt đối với các cluster sắp kết thúc hỗ trợ (tiêu chuẩn và mở rộng). Việc cung cấp thông báo sớm khi một cluster EKS sắp kết thúc cửa sổ hỗ trợ cho phép giải pháp này trao quyền cho bạn chủ động lập kế hoạch và cập nhật phiên bản Kubernetes của cluster.

Bổ sung cho điều này, giải pháp thứ hai là một cơ chế khám phá và báo cáo tự động xác định và tổng hợp thông tin chi tiết về các cluster EKS trên tất cả các AWS Regions và tài khoản trong Organization của bạn. Khả năng hiển thị toàn diện này về các phiên bản cluster, tags liên quan và các chi tiết chính khác giúp kiểm tra tuân thủ, quản lý bảng kiểm kê tài nguyên chính xác và lập kế hoạch nâng cấp chiến lược.

Cùng nhau, hai giải pháp này cung cấp một framework mạnh mẽ để quản lý vòng đời cluster EKS hiệu quả, cho phép các tổ chức luôn đi trước các vấn đề tiềm ẩn, tối ưu hóa việc sử dụng tài nguyên và đưa ra các quyết định sáng suốt phù hợp với mục tiêu chiến lược dài hạn của họ.

# Điều kiện tiên quyết

Bạn cần những điều sau để hoàn thành hướng dẫn:

* Một [AWS account](https://aws.amazon.com/console/) với Organizations được bật
* Gói hỗ trợ Business, Enterprise On-Ramp hoặc Enterprise từ [AWS Support](https://aws.amazon.com/premiumsupport/) để sử dụng AWS Health API
* Kiến thức cơ bản về Amazon EKS, AWS Health, EventBridge,  [AWS Lambda](https://aws.amazon.com/lambda/), [AWS Identity and Access Management (IAM](https://aws.amazon.com/iam/)), [Amazon S3](https://aws.amazon.com/pm/serv-s3/), Amazon SNS, Amazon SQS và [AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/)
* Khả năng ủy quyền từ tài khoản quản lý đến tài khoản tooling được sử dụng để tập trung thông báo và thực hiện khám phá cluster EKS trên toàn bộ Organization
* Kiến thức về Python

# Thiết lập ban đầu

Các bước sau hướng dẫn bạn qua quá trình thiết lập ban đầu.

### Bật AWS Health Organizational View trong tài khoản quản lý

Bật [Organizational View in AWS Health](https://docs.aws.amazon.com/health/latest/ug/aggregate-events.html) để có được chế độ xem tập trung, tổng hợp các sự kiện AWS Health trên toàn bộ Organization của bạn. Bạn có thể xác minh rằng điều này được bật thông qua console hoặc bằng cách chạy lệnh sau bằng [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/):

aws health describe-health-service-status-for-organization. Bạn sẽ thấy kết quả sau:

{"healthServiceAccessStatusForOrganization": "ENABLED" }

Gói hỗ trợ Business, Enterprise On-Ramp hoặc Enterprise từ AWS Support là cần thiết để sử dụng AWS Health API và hoàn thành bước này.

### Ủy quyền quản trị từ tài khoản quản lý đến tài khoản tooling trung tâm

Thiết lập một tài khoản AWS trong Organization làm tài khoản tooling cho giải pháp này. Tài khoản này được sử dụng để tập trung thông báo và khám phá.

Từ tài khoản quản lý, ủy quyền quản trị [AWS CloudFormation](https://aws.amazon.com/cloudformation/) StackSets bằng cách làm theo các bước được mô tả trong bài viết này: [CloudFormation StackSets delegated administration](https://aws.amazon.com/blogs/mt/cloudformation-stacksets-delegated-administration/).

Kết quả tương tự cũng có thể đạt được bằng cách chạy lệnh sau từ tài khoản quản lý. Thay thế 012345678901 bằng AWS account ID của tài khoản tooling của bạn.

aws organizations register-delegated-administrator \

--serviceprincipal=member.org.stacksets.cloudformation.amazonaws.com \

--account-id="012345678901"

Đây là lần duy nhất chúng ta cần truy cập tài khoản quản lý. Các bước còn lại được hoàn thành từ trong tài khoản tooling.

### Bootstrap AWS CDK

Chọn một Region chính nơi tất cả báo cáo và sự kiện được hợp nhất trong tài khoản tooling trung tâm. Đặt biến AWS\_DEFAULT\_REGION thành Region chính này.

Đối với giải pháp khám phá và báo cáo, bạn phải bootstrap AWS CDK trong Region chính này trên toàn bộ Organization. Hơn nữa, AWS CDK cũng phải được bootstrap trong tất cả các AWS Regions nơi các cluster EKS được triển khai để nhận thông báo kết thúc hỗ trợ. Để đơn giản hóa hướng dẫn này, chúng tôi chỉ demo triển khai tài nguyên đến Region chính mà bạn đã chọn.

Các bước để bootstrap AWS CDK trên nhiều AWS Regions và tài khoản có sẵn trong bài viết này: [Bootstrapping multiple AWS accounts for AWS CDK using CloudFormation StackSets](https://aws.amazon.com/blogs/mt/bootstrapping-multiple-aws-accounts-for-aws-cdk-using-cloudformation-stacksets/).

### Tải xuống các AWS CDK stacks

Chúng tôi cung cấp các AWS CDK stacks để bạn nhanh chóng triển khai giải pháp trong môi trường của mình. Tải mã từ [our GitHub repository](https://github.com/aws-samples/container-resiliency/tree/main/patterns/observability/eks-event-centralization-discoverability) và thiết lập môi trường bằng cách chạy các lệnh sau trong thư mục cdk:

python3 -m venv .venv

source .venv/bin/activate

pip install -r requirements.txt

## Hướng dẫn chi tiết

Các bước sau sẽ hướng dẫn bạn qua các giải pháp này.

### Giải pháp 1: Thông báo kết thúc hỗ trợ cluster EKS

Giải pháp đầu tiên của chúng tôi giải quyết nhu cầu quan trọng về nhận thức kịp thời về các sự kiện vòng đời cluster EKS, đặc biệt là việc tiếp cận ngày kết thúc hỗ trợ tiêu chuẩn. Việc sử dụng AWS Health, EventBridge và Amazon SNS (và tùy chọn Amazon SQS) cho phép chúng tôi tạo một hệ thống tập trung:

* Giám sát các sự kiện AWS Health trên nhiều AWS Regions và tài khoản
* Tập trung vào các sự kiện cụ thể của Amazon EKS, đặc biệt là AWS\_EKS\_PLANNED\_LIFECYCLE\_EVENT
* Cung cấp thông báo sớm khi một cluster EKS còn 180 ngày nữa sẽ đạt đến cuối giai đoạn hỗ trợ tiêu chuẩn và hỗ trợ mở rộng

Cách tiếp cận tập trung này đảm bảo rằng người dùng Amazon EKS nhận được đủ thời gian để lập kế hoạch và thực hiện nâng cấp phiên bản, duy trì tính bảo mật và ổn định của môi trường Kubernetes của họ, như được hiển thị trong hình sau.

![](data:image/png;base64...)

*Hình 1: Tổng quan giải pháp – thông báo kết thúc hỗ trợ*

#### Bước 1: Triển khai AWS CDK stack eks-health-events

Triển khai AWS CDK stack eks-health-events vào tài khoản tooling trung tâm bằng lệnh sau:

cdk deploy eks-health-events --app "python3 tooling\_account.py" —require-approval never

Điều này triển khai AWS CDK app trong tooling\_account.py, cung cấp các tài nguyên sau trong tài khoản tooling trung tâm:

* Event bus
* SNS topic và SQS queue để giám sát các sự kiện
* EventBridge rule để chuyển tiếp các sự kiện vòng đời đã lên kế hoạch cho Amazon EKS đến Amazon SNS
* EventBridge rule để chuyển tiếp giám sát các sự kiện vòng đời đã lên kế hoạch cho Amazon EKS đến Amazon SQS
* Resource policies cho các event rules để publish đến Amazon SNS và Amazon SQS

#### Bước 2: Triển khai AWS CDK stack eks-health-events-stack-set

Triển khai AWS CDK stack eks-health-events-stack-set.

cdk deploy eks-health-events-stack-set --app "python stack\_sets.py" —require-approval never

Điều này sử dụng CloudFormation StackSets để triển khai các tài nguyên sau vào Region chính đã chọn trên tất cả các tài khoản trong Organization ngoại trừ tài khoản Management:

* Local event bus
* EventBridge rule để chuyển tiếp các sự kiện vòng đời đã lên kế hoạch cho Amazon EKS đến central event bus được cung cấp trong Bước 2
* Resource policies cho các event rules để publish đến central event bus

#### Bước 3: Cấu hình thông báo SNS

Duyệt đến dịch vụ Amazon SNS có tên eks-health-events-EKSHealthEvents-<primary region> và tạo một subscription cho topic mới được tạo (ví dụ: địa chỉ email nhóm).

#### Bước 4: Xác thực giải pháp

Bạn có thể kiểm tra và xác thực rằng các EventBridge rules, SQS queue và SNS topic đã được tạo bởi các CloudFormation stacks có tên eks-health-events và eks-health-events-stack-set. Từ thời điểm này trở đi, khi các cluster EKS của bạn còn 180 ngày nữa sẽ đạt đến cuối hỗ trợ (tiêu chuẩn và mở rộng), các EventBridge rules sẽ áp dụng và Amazon SNS và/hoặc Amazon SQS được kích hoạt, như được hiển thị trong các hình sau.

*![](data:image/png;base64...)*

*Hình 2: Xác thực triển khai EventBridge*

*![](data:image/png;base64...)*

*Hình 3: Xác thực triển khai SQS*

*![](data:image/png;base64...)*

*Hình 4: Xác thực triển khai SNS*

*![](data:image/png;base64...)*

*Hình 5: Mẫu thông báo kết thúc hỗ trợ*

## Giải pháp 2: Khám phá và báo cáo cluster EKS

Bổ sung cho giải pháp thông báo kết thúc hỗ trợ cluster EKS, giải pháp thứ hai của chúng tôi cung cấp cái nhìn toàn diện về các cluster EKS trên toàn bộ Organization. Giải pháp này:

* Xác định các cluster EKS trong tất cả các AWS Regions và tài khoản trong một Organization
* Thu thập thông tin chi tiết về từng cluster, chẳng hạn như chi tiết tài khoản, region, tên cluster, phiên bản và các tags liên quan
* Tổng hợp dữ liệu về các phiên bản cluster, cung cấp thông tin chi tiết về phân phối phiên bản
* Tạo cả báo cáo chi tiết và tóm tắt, được lưu trữ tập trung để truy cập trực tiếp

Việc cung cấp khả năng hiển thị trên toàn tổ chức này cho phép giải pháp giúp các nhóm duy trì bảng kiểm kê chính xác về tài nguyên Amazon EKS, tạo điều kiện thuận lợi cho việc kiểm tra tuân thủ và hỗ trợ lập kế hoạch nâng cấp chiến lược, như được hiển thị trong hình sau.

*![](data:image/png;base64...)*

*Hình 6: Tổng quan giải pháp – khám phá và báo cáo*

#### Bước 1: Triển khai AWS CDK stack eks-discovery

Triển khai AWS CDK stack eks-discovery-lambda vào tài khoản tooling trung tâm bằng lệnh sau:

cdk deploy eks-discovery-lambda —require-approval never

Điều này triển khai AWS CDK stack có tên eks-discovery-lambda trong tooling\_account.py, cung cấp các tài nguyên sau trong tài khoản tooling trung tâm:

* Lambda function để khám phá các cluster EKS trên tất cả các AWS Regions và tài khoản
* S3 bucket để lưu trữ kết quả
* SNS topic cho thông báo
* EventBridge scheduler để thực thi định kỳ
* Các IAM roles và policies cần thiết

Lambda function thu thập chi tiết cluster, tạo báo cáo và gửi thông báo.

#### Bước 2: Sửa đổi EventBridge scheduler theo nhu cầu

Nếu bạn muốn tùy chỉnh lịch khám phá cluster EKS, hãy điều hướng đến EventBridge và trong phần schedules tìm EKSDiscoveryWeeklySchedule mới được tạo. Đây là một scheduler dựa trên cron, như được hiển thị trong hình sau.

*![](data:image/png;base64...)*

*Hình 7: Tùy chỉnh lịch cho khám phá cluster*

Để nhận thông báo từ Amazon SNS, bạn phải tạo một subscription cho topic. Để làm điều này, hãy điều hướng đến dịch vụ Amazon SNS, tìm Topic mới được tạo có tên EKSDiscoverySNSTopic và cấu hình giao thức để đáp ứng yêu cầu của bạn (ví dụ: gửi email đến một nhóm).

#### Bước 3: Triển khai cross-account role mà Lambda function có thể assume để thực hiện khám phá

Lambda function bạn triển khai trong Bước 1 dựa vào một cross-account role trong mỗi tài khoản trong Organization để thực hiện khám phá cluster.

Triển khai AWS CDK stack eks-discovery-stack-set để triển khai cross-account role này.

cdk deploy eks-discovery-stack-set --app "python stack\_sets.py" --require-approval never

#### Bước 4: Xác thực giải pháp

Để xác thực giải pháp, hãy điều hướng đến Lambda function mới được tạo và test với một event mới và một đối tượng JSON rỗng. Khi Lambda hoàn thành, hãy xác minh rằng S3 bucket nhận được file zip và xác nhận rằng bạn đã nhận được thông báo SNS, như được hiển thị trong các hình sau.

*![](data:image/png;base64...)*

*Hình 8: Mẫu output khám phá cluster trong S3 bucket*

*![](data:image/png;base64...)*

*Hình 9: Mẫu nội dung của output file*

*![](data:image/png;base64...)*

*Hình 10: Mẫu danh sách clusters*

*![](data:image/png;base64...)*

*Hình 11: Mẫu số lượng clusters theo phiên bản*

#### Bước 5: (Tùy chọn) Giám sát giải pháp

Bạn có thể muốn giám sát giải pháp. Điều này có thể được thực hiện bằng cách thiết lập [Amazon CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) để giám sát việc thực thi của Lambda function và bất kỳ lỗi tiềm ẩn nào. Hơn nữa, hãy thường xuyên xem xét các báo cáo được tạo trong S3 bucket và định kỳ xem xét và cập nhật các quyền IAM nếu cần.

# Khắc phục sự cố

* Đảm bảo rằng tất cả các IAM roles và policies được thiết lập chính xác và có các quyền cần thiết.
* Kiểm tra CloudWatch Logs để tìm bất kỳ thông báo lỗi nào trong các Lambda functions hoặc EventBridge rules.

# Cân nhắc về bảo mật

* Xem xét và điều chỉnh các IAM roles và policies để tuân thủ nguyên tắc đặc quyền tối thiểu và môi trường của bạn.
* Thường xuyên kiểm toán quyền truy cập vào hệ thống quản lý sự kiện tập trung.

#

# Dọn dẹp

Chạy các lệnh sau để dọn dẹp các tài nguyên đã cung cấp:

cdk destroy --app "python stack\_sets.py" --all --force

cdk destroy --all --force

Lệnh đầu tiên xóa các CloudFormation StackSets đã được triển khai trên toàn bộ Organization bằng AWS CDK App có tên stack\_sets.py.

Lệnh thứ hai dọn dẹp các tài nguyên được cung cấp trong tài khoản tooling trung tâm bằng AWS CDK App có tên tooling\_account.py.

# Kết luận

Hướng dẫn này có thể giúp bạn thiết lập một hệ thống mạnh mẽ sử dụng các dịch vụ AWS để cung cấp thông báo chủ động về kết thúc hỗ trợ tiêu chuẩn. Điều này cho phép lập kế hoạch kịp thời cho các nâng cấp, giảm thiểu rủi ro từ các cluster lỗi thời trong khi duy trì tính bảo mật, ổn định và tuân thủ. Hơn nữa, giải pháp khám phá và báo cáo cluster Amazon EKS đánh dấu một bước tiến đáng kể trong việc quản lý các môi trường Kubernetes đa tài khoản phức tạp trên AWS. Giải pháp tăng cường khả năng hiển thị, hợp lý hóa nỗ lực tuân thủ, tạo điều kiện thuận lợi cho việc lập kế hoạch chiến lược và hỗ trợ ra quyết định sáng suốt cho việc nâng cấp cluster và phân bổ tài nguyên.

Khi các tổ chức tiếp tục mở rộng quy mô ứng dụng container hóa của họ, các giải pháp này trở thành tài sản vô giá. Chúng cho phép các nhóm duy trì cái nhìn tổng quan rõ ràng về cảnh quan Amazon EKS của họ, tối ưu hóa việc sử dụng tài nguyên và đảm bảo các thực hành quản lý nhất quán trên các triển khai đa dạng. Việc triển khai các giải pháp này cho phép bạn thực hiện một bước tiến đáng kể trong việc quản lý khả năng quan sát, khả năng phục hồi và quản trị của các môi trường Amazon EKS của bạn. Đến lượt nó, điều này đảm bảo thành công lâu dài và khả năng mở rộng của các sáng kiến Kubernetes của bạn trên AWS.

Chúng tôi khuyến nghị thử cả hai giải pháp để bắt đầu tăng cường khả năng quan sát cluster EKS của bạn ngay hôm nay!

**Nguồn gốc:** AWS Containers Blog
 **Ngày xuất bản:** 12 tháng 3, 2025
 **Danh mục:** Amazon EKS, AWS Health, Container Management, Kubernetes
