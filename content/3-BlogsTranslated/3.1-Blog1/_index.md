---
title: "Blog 1"
date: "2025-10-15"
weight: 3
chapter: false
pre: " <b> 3.1 </b> "
---
# **Tăng cường deployment guardrails với tính năng rolling update cho inference component trên Amazon SageMaker AI inference**

Bài viết này có đồng tác giả là : Melanie Li, Andrew Smith, Dustin Liu, Vivek Gangasani, Shikhar Mishra, và June Won

Ngày: 25 tháng 3, 2025 | in [Amazon SageMaker](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/), [Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-ai/), [Intermediate (200)](https://aws.amazon.com/blogs/machine-learning/category/learning-levels/intermediate-200/) [Permalink](https://aws.amazon.com/blogs/machine-learning/enhance-deployment-guardrails-with-inference-component-rolling-updates-for-amazon-sagemaker-ai-inference/) | [Comments](https://aws.amazon.com/blogs/machine-learning/enhance-deployment-guardrails-with-inference-component-rolling-updates-for-amazon-sagemaker-ai-inference/#Comments) |  [Share](https://aws.amazon.com/vi/blogs/machine-learning/enhance-deployment-guardrails-with-inference-component-rolling-updates-for-amazon-sagemaker-ai-inference/)

Triển khai các mô hình một cách hiệu quả, tin cậy và tiết kiệm chi phí là một thách thức quan trọng đối với các tổ chức ở mọi quy mô. Khi ngày càng nhiều tổ chức triển khai các foundation model (FM) và các mô hình machine learning (ML) khác vào môi trường production, họ phải đối mặt với những thách thức liên quan đến việc tận dụng tài nguyên, hiệu quả chi phí và duy trì tính khả dụng cao trong quá trình cập nhật. [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai) đã giới thiệu chức năng [inference component](https://aws.amazon.com/blogs/machine-learning/reduce-model-deployment-costs-by-50-on-average-using-sagemakers-latest-features/) có thể giúp các tổ chức giảm chi phí triển khai mô hình bằng cách tối ưu hóa việc sử dụng tài nguyên thông qua khả năng đóng gói và mở rộng mô hình thông minh. Inference component trừu tượng hóa các mô hình ML và cho phép phân bổ tài nguyên chuyên dụng cũng như các chính sách mở rộng cụ thể cho từng mô hình.

Tuy nhiên, việc cập nhật các mô hình này—đặc biệt trong môi trường production với các SLA về độ trễ nghiêm ngặt—về mặt lịch sử có nguy cơ gây downtime hoặc tắc nghẽn tài nguyên. Các triển khai blue/green truyền thống thường gặp khó khăn với những hạn chế về năng lực, khiến việc cập nhật trở nên khó dự đoán đối với các mô hình sử dụng GPU nặng. Để giải quyết vấn đề này, chúng tôi rất vui mừng công bố một cải tiến mạnh mẽ khác cho RageMaker AI:[tính năng rolling update cho inference component endpoint](https://aws.amazon.com/about-aws/whats-new/2025/03/amazon-sagemaker-inference-rolling-update-component-endpoints/), một tính năng được thiết kế để đơn giản hóa việc cập nhật cho các mô hình có kích thước khác nhau đồng thời giảm thiểu chi phí vận hành.

Trong bài viết này, chúng tôi thảo luận về những thách thức mà các tổ chức phải đối mặt khi cập nhật mô hình trong production. Sau đó, chúng tôi đi sâu vào tính năng rolling update mới cho inference component và cung cấp các ví dụ thực tế sử dụng các mô hình DeepSeek distilled để minh họa tính năng này. Cuối cùng, chúng tôi khám phá cách thiết lập rolling update trong các tình huống khác nhau.

# **Những thách thức với triển khai blue/green**

Theo truyền thống, RageMaker AI inference đã hỗ trợ mô hình triển khai blue/green để cập nhật inference component trong production. Mặc dù có hiệu quả trong nhiều tình huống, cách tiếp cận này đi kèm với những thách thức cụ thể:

* **Kém hiệu quả về tài nguyên** – Triển khai blue/green yêu cầu cung cấp tài nguyên cho cả môi trường hiện tại (blue) và môi trường mới (green) đồng thời. Đối với các inference component chạy trên các GPU instance đắt tiền như P4d hoặc G5, điều này có nghĩa là có khả năng tăng gấp đôi yêu cầu tài nguyên trong quá trình triển khai. Hãy xem xét một ví dụ trong đó khách hàng có 10 bản sao của một inference component phân bố trên 5 instance ml.p4d.24xlarge, tất cả đều hoạt động với công suất đầy đủ. Với triển khai blue/green, SageMaker AI sẽ cần cung cấp thêm năm instance ml.p4d.24xlarge để lưu trữ phiên bản mới của inference component trước khi chuyển đổi lưu lượng và ngừng sử dụng các instance cũ.
* **Tài nguyên tính toán hạn chế** – Đối với khách hàng sử dụng các GPU instance mạnh mẽ như dòng P hoặc G, năng lực cần thiết có thể không có sẵn trong một Availability Zone hoặc Region nhất định. Điều này thường dẫn đến các ngoại lệ về năng lực instance trong quá trình triển khai, gây ra lỗi cập nhật và rollback.
* **Chuyển đổi theo kiểu tất cả hoặc không có gì** – Các triển khai blue/green truyền thống chuyển toàn bộ lưu lượng cùng một lúc hoặc dựa trên lịch trình được cấu hình. Điều này để lại không gian hạn chế cho việc xác thực dần dần và tăng phạm vi ảnh hưởng nếu có vấn đề phát sinh với triển khai mới.

Mặc dù triển khai blue/green đã là một chiến lược đáng tin cậy cho các bản cập nhật zero-downtime, những hạn chế của nó trở nên rõ ràng khi triển khai các large language model (LLM) quy mô lớn hoặc các mô hình thông lượng cao trên các GPU instance cao cấp. Những thách thức này đòi hỏi một cách tiếp cận tinh tế hơn—một cách tiếp cận xác thực các bản cập nhật từng bước trong khi tối ưu hóa việc sử dụng tài nguyên. Rolling update cho inference component được thiết kế để loại bỏ sự cứng nhắc của các triển khai blue/green. Bằng cách cập nhật các mô hình theo các batch được kiểm soát, mở rộng cơ sở hạ tầng một cách linh hoạt và tích hợp các kiểm tra an toàn theo thời gian thực, chiến lược này đảm bảo các triển khai vẫn tiết kiệm chi phí, đáng tin cậy và có khả năng thích ứng—ngay cả đối với các workload sử dụng GPU nặng.

# **Rolling deployment để cập nhật inference component**

Như đã đề cập trước đó, inference component được giới thiệu như một tính năng của RageMaker AI để tối ưu hóa chi phí; chúng cho phép bạn định nghĩa và triển khai các tài nguyên cụ thể cần thiết cho workload suy luận mô hình của bạn. Bằng cách điều chỉnh đúng kích thước tài nguyên tính toán để phù hợp với yêu cầu của mô hình, bạn có thể tiết kiệm chi phí trong quá trình cập nhật so với các phương pháp triển khai truyền thống.

Với rolling update, RageMaker AI triển khai các phiên bản mô hình mới theo các batch inference component có thể cấu hình trong khi mở rộng instance một cách linh hoạt. Điều này đặc biệt có tác động đối với các LLM:

* **Tính linh hoạt về kích thước batch** – Khi cập nhật các inference component trong một SageMaker AI endpoint, bạn có thể chỉ định kích thước batch cho mỗi bước rolling. Đối với mỗi bước, RageMaker AI cung cấp năng lực dựa trên kích thước batch được chỉ định trên endpoint fleet mới, định tuyến lưu lượng đến fleet đó và dừng năng lực trên endpoint fleet cũ. Các mô hình nhỏ hơn như DeepSeek Distilled Llama 8B có thể sử dụng các batch lớn hơn để cập nhật nhanh chóng, và các mô hình lớn hơn như DeepSeek Distilled Llama 70B sử dụng các batch nhỏ hơn để hạn chế tranh chấp GPU.
* **Bảo vệ an toàn tự động** – Các alarm [Amazon CloudWatch](http://aws.amazon.com/cloudwatch) tích hợp giám sát các metric trên một inference component. Bạn có thể cấu hình các alarm để kiểm tra xem phiên bản mới được triển khai của inference component có hoạt động đúng hay không. Nếu các alarm CloudWatch được kích hoạt, RageMaker AI sẽ bắt đầu một rollback tự động.

Chức năng mới được triển khai thông qua các phần mở rộng cho RageMaker AI API, chủ yếu với các tham số mới trong API Update Inference Component:

sagemaker\_client.update\_inference\_component(

InferenceComponentName=inference\_component\_name,

RuntimeConfig={ "CopyCount": number },

Specification={ ... },

DeploymentConfig={

"RollingUpdatePolicy": {

"MaximumBatchSize": { # Value must be between 5% to 50% of the IC's total copy count.

"Type": "COPY\_COUNT", # COPY\_COUNT | CAPACITY\_PERCENT

"Value": 1 # Minimum value of 1

},

"MaximumExecutionTimeoutInSeconds": 600, #Minimum value of 600. Maximum value of 28800.

"RollbackMaximumBatchSize": {

"Type": "COPY\_COUNT", # COPY\_COUNT | CAPACITY\_PERCENT

"Value":1

},

"WaitIntervalInSeconds": 120 # Minimum value of 0. Maximum value of 3600

}

},

AutoRollbackConfiguration={

"Alarms": [

{

"AlarmName": "string" #Optional

}

]

},

)

Đoạn code trên sử dụng các tham số sau:

* **MaximumBatchSize** – Đây là một tham số bắt buộc và định nghĩa kích thước batch cho mỗi bước rolling trong quy trình triển khai. Đối với mỗi bước, RageMaker AI cung cấp năng lực trên endpoint fleet mới, định tuyến lưu lượng đến fleet đó và dừng năng lực trên endpoint fleet cũ. Giá trị phải nằm trong khoảng từ 5–50% số lượng bản sao của inference component.
  + **Type** – Tham số này có thể chứa một giá trị như COPY\_COUNT | CAPACITY\_PERCENT, chỉ định loại năng lực endpoint.
  + **Value** – Định nghĩa kích thước năng lực, dưới dạng số lượng bản sao inference component hoặc phần trăm năng lực.
* **MaximumExecutionTimeoutSeconds** – Đây là thời gian tối đa mà rolling deployment sẽ dành cho việc thực thi tổng thể. Vượt quá giới hạn này sẽ gây ra timeout.
* **RollbackMaximumBatchSize** – Đây là kích thước batch cho một rollback về endpoint fleet cũ. Nếu trường này vắng mặt, giá trị được đặt thành mặc định, là 100% tổng năng lực. Khi sử dụng mặc định, RageMaker AI cung cấp toàn bộ năng lực của fleet cũ cùng một lúc trong quá trình rollback.
  + **Value** – Tham số Value của cấu trúc này sẽ chứa giá trị mà Type sẽ được thực thi. Đối với chiến lược rollback, nếu bạn không chỉ định các trường trong đối tượng này, hoặc nếu bạn đặt Value thành 100%, thì SageMaker AI sử dụng chiến lược rollback blue/green và roll lưu lượng trở lại fleet blue.
* **WithIntervalInSeconds** – Đây là giới hạn thời gian cho tổng triển khai. Vượt quá giới hạn này sẽ gây ra timeout.
* **AutoRollbackConfiguration** – Đây là cấu hình rollback tự động để xử lý lỗi triển khai endpoint và khôi phục.
  + **AlarmName** – Alarm CloudWatch này được cấu hình để giám sát các metric trên một InferenceComponent Bạn có thể cấu hình nó để kiểm tra xem phiên bản mới được triển khai của InferenceComponent có hoạt động đúng hay không.

Để biết thêm thông tin về SageMaker AI API, tham khảo [SageMaker AI API Reference](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_UpdateInferenceComponent.html).

# **Trải nghiệm khách hàng**

Hãy cùng khám phá cách rolling update hoạt động trong thực tế với một số tình huống phổ biến, sử dụng các LLM có kích thước khác nhau. Bạn có thể tìm thấy notebook ví dụ trong [GitHub repo](https://github.com/aws-samples/sagemaker-genai-hosting-examples/blob/main/deployment-guardrails/enhance-deployment-guardrails-with-inference-component-rolling-deployment.ipynb).

## **Tình huống 1: Nhiều cluster GPU đơn**

Trong tình huống này, giả sử bạn đang chạy một endpoint với ba instance ml.g5.2xlarge, mỗi instance có một GPU duy nhất. Endpoint lưu trữ một inference component yêu cầu một CPU accelerator, có nghĩa là mỗi instance chứa một bản sao. Khi bạn muốn cập nhật inference component để sử dụng phiên bản inference component mới, bạn có thể sử dụng rolling update để giảm thiểu sự gián đoạn.

Bạn có thể cấu hình một rolling update với kích thước batch là một, có nghĩa là RageMaker AI sẽ cập nhật từng bản sao một. Trong quá trình cập nhật, RageMaker AI trước tiên xác định năng lực có sẵn trong các instance hiện có. Vì không có instance hiện tại nào có không gian cho các workload tạm thời bổ sung, RageMaker AI sẽ khởi chạy các instance ml.g5.2xlarge mới từng cái một để triển khai một bản sao của phiên bản inference component mới lên một GPU instance. Sau khoảng thời gian chờ được chỉ định và container của inference component mới vượt qua kiểm tra healthy, RageMaker AI loại bỏ một bản sao của phiên bản cũ (vì mỗi bản sao được lưu trữ trên một instance, instance này sẽ được dỡ bỏ tương ứng), hoàn tất bản cập nhật cho batch đầu tiên.

Quy trình này lặp lại cho bản sao thứ hai của inference component, cung cấp một quá trình chuyển đổi suôn sẻ với zero downtime. Bản chất dần dần của bản cập nhật giảm thiểu rủi ro và cho phép bạn duy trì tính khả dụng nhất quán trong suốt quy trình triển khai. Sơ đồ sau đây cho thấy quy trình này.

![](data:image/png;base64...)

## **Tình huống 2: Cập nhật với rollback tự động**

Trong một tình huống khác, bạn có thể đang cập nhật inference component của mình từ Llama-3.1-8B-Instruct sang DeepSeek-R1-Distill-Llama-8B, nhưng phiên bản mô hình mới có các kỳ vọng API khác nhau. Trong trường hợp sử dụng này, bạn đã cấu hình một alarm CloudWatch để giám sát lỗi 4xx, điều này sẽ cho biết các vấn đề về tương thích API.

Bạn có thể bắt đầu một rolling update với kích thước batch là một bản sao. RageMaker AI triển khai bản sao đầu tiên của phiên bản mới trên một GPU instance mới. Khi instance mới sẵn sàng phục vụ lưu lượng, RageMaker AI sẽ chuyển tiếp một phần các yêu cầu invocation đến mô hình mới này. Tuy nhiên, trong ví dụ này, phiên bản mô hình mới, đang thiếu cấu hình biến môi trường "MESSAGES\_API\_ENABLED", sẽ bắt đầu trả về lỗi 4xx khi nhận các yêu cầu ở định dạng Messages API.

![](data:image/png;base64...)

Alarm CloudWatch được cấu hình phát hiện các lỗi này và chuyển sang trạng thái alarm. RageMaker AI tự động phát hiện trạng thái alarm này và bắt đầu quy trình rollback theo cấu hình rollback. Theo kích thước batch rollback được chỉ định, RageMaker AI loại bỏ phiên bản mô hình mới có vấn đề và duy trì phiên bản gốc đang hoạt động, ngăn chặn sự gián đoạn dịch vụ trên diện rộng. Endpoint trở về trạng thái ban đầu với lưu lượng được xử lý bởi phiên bản mô hình gốc hoạt động đúng.

Đoạn code sau đây cho thấy cách thiết lập một alarm CloudWatch để giám sát lỗi 4xx:

# Create alarm

cloudwatch.put\_metric\_alarm(

AlarmName=f'SageMaker-{endpoint\_name}-4xx-errors',

ComparisonOperator='GreaterThanThreshold',

EvaluationPeriods=1,

MetricName='Invocation4XXErrors',

Namespace='AWS/SageMaker',

Period=300,

Statistic='Sum',

Threshold=5.0,

ActionsEnabled=True,

AlarmDescription='Alarm when greather than 5 4xx errors',

Dimensions=[

{

'Name': 'InferenceComponentName',

'Value': inference\_component\_name

},

],

)

Sau đó bạn có thể sử dụng alarm CloudWatch này trong yêu cầu cập nhật:

DeploymentConfig={

"RollingUpdatePolicy": {

"MaximumBatchSize": {

"Type": "COPY\_COUNT",

"Value": 1

},

"WaitIntervalInSeconds": 120,

"RollbackMaximumBatchSize": {

"Type": "COPY\_COUNT",

"Value": 1

}

},

'AutoRollbackConfiguration': {

"Alarms": [

{"AlarmName": f'SageMaker-{endpoint\_name}-4xx-errors'}

]

}

}

## **Tình huống 3: Cập nhật với năng lực đầy đủ trong các instance hiện có**

Nếu một endpoint hiện có có nhiều GPU accelerator và không phải tất cả các accelerator đều được sử dụng, bản cập nhật có thể sử dụng các GPU accelerator hiện có mà không cần khởi chạy các instance mới cho endpoint. Xem xét nếu bạn có một endpoint được cấu hình với hai instance ml.g5.12xlarge ban đầu có bốn GPU accelerator trong mỗi instance. Endpoint lưu trữ hai inference component: IC-1 yêu cầu một accelerator và IC-2 cũng yêu cầu một accelerator. Trên một instance ml.g5.12xlarge, có bốn bản sao của IC-1 đã được tạo; trên instance khác, hai bản sao của IC-2 đã được tạo. Vẫn còn hai GPU accelerator có sẵn trên instance thứ hai.

Khi bạn bắt đầu một bản cập nhật cho IC-1 với kích thước batch là hai bản sao, RageMaker AI xác định rằng có đủ năng lực trong các instance hiện có để lưu trữ các phiên bản mới trong khi duy trì các phiên bản cũ. Nó sẽ tạo hai bản sao của phiên bản IC-1 mới trên instance thứ hai. Khi các container đã khởi động và chạy, SageMaker AI sẽ hướng lưu lượng đến các IC-1 mới và sau đó bắt đầu định tuyến lưu lượng đến các inference component mới. RageMaker AI cũng sẽ loại bỏ hai trong số các bản sao IC-1 cũ khỏi instance. Bạn không bị tính phí cho đến khi các inference component mới bắt đầu nhận các invocation và tạo ra các phản hồi.

Bây giờ có thêm hai GPU slot trống. RageMaker AI sẽ cập nhật batch thứ hai, và nó sẽ sử dụng các GPU accelerator trống vừa có sẵn. Sau khi các quy trình hoàn tất, endpoint có bốn IC-1 với phiên bản mới và hai bản sao của IC-2 không bị thay đổi.

![](data:image/png;base64...)

## **Tình huống 4: Cập nhật yêu cầu năng lực instance bổ sung**

Xem xét nếu bạn có một endpoint được cấu hình với ban đầu một instance ml.g5.12xlarge (tổng cộng 4 GPU) và được cấu hình [managed instance scaling](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_ProductionVariant.html#sagemaker-Type-ProductionVariant-ManagedInstanceScaling) (MIS) với số instance tối đa được đặt thành hai. Endpoint lưu trữ hai inference component: IC-1 yêu cầu 1 GPU với hai bản sao (Llama 8B), và IC-2 (mô hình DeepSeek Distilled Llama 14B) cũng yêu cầu 1 GPU với hai bản sao—sử dụng tất cả 4 GPU có sẵn.

Khi bạn bắt đầu một bản cập nhật cho IC-1 với kích thước batch là hai bản sao, RageMaker AI xác định rằng không có đủ năng lực trong các instance hiện có để lưu trữ các phiên bản mới trong khi duy trì các phiên bản cũ. Thay vì làm thất bại bản cập nhật, vì bạn đã cấu hình [MIS](https://docs.aws.amazon.com/sagemaker/latest/APIReference/API_ProductionVariant.html#sagemaker-Type-ProductionVariant-ManagedInstanceScaling), RageMaker AI sẽ tự động cung cấp một instance g5.12.xlarge thứ hai để lưu trữ các inference component mới.

Trong quá trình cập nhật, RageMaker AI triển khai hay bản sao của phiên bản IC-1 mới lên instance mới được cung cấp, như được hiển thị trong sơ đồ sau. Sau khi các inference component mới đã khởi động và chạy, RageMaker AI bắt đầu loại bỏ các bản sao IC-1 cũ khỏi các instance gốc. Đến cuối bản cập nhật, instance đầu tiên sẽ lưu trữ IC-2 sử dụng 2 GPU, và instance thứ hai mới được cung cấp sẽ lưu trữ IC-1 đã cập nhật với hai bản sao sử dụng 2 GPU. Sẽ có các không gian mới có sẵn trong hai instance, và bạn có thể triển khai thêm các bản sao inference component hoặc các mô hình mới vào cùng một endpoint bằng cách sử dụng các tài nguyên GPU có sẵn. Nếu bạn thiết lập managed instance auto scaling và đặt inference component auto scaling về không, bạn có thể scale down các bản sao inference component về không, điều này sẽ dẫn đến instance tương ứng được scale down. Khi inference component được scale up, SageMaker AI sẽ khởi chạy các inference component trong instance hiện có với các GPU accelerator có sẵn, như đã đề cập trong tình huống 3.

![](data:image/png;base64...)

## **Tình huống 5: Cập nhật đối mặt với năng lực không đủ**

Trong các tình huống không có đủ năng lực GPU, RageMaker AI cung cấp phản hồi rõ ràng về các ràng buộc năng lực. Xem xét nếu bạn có một endpoint chạy trên 30 instance ml.g6e.16xlarge, mỗi instance đã được sử dụng đầy đủ với các inference component. Bạn muốn cập nhật một inference component hiện có bằng cách sử dụng rolling deployment với kích thước batch là 4, nhưng sau khi bốn batch đầu tiên được cập nhật, không có đủ năng lực GPU có sẵn cho phần còn lại của bản cập nhật. Trong trường hợp này, RageMaker AI sẽ tự động rollback về thiết lập trước đó và dừng quy trình cập nhật.

Có thể có hai trường hợp cho trạng thái cuối cùng của rollback này. Trong trường hợp đầu tiên, rollback đã thành công vì có năng lực mới có sẵn để khởi chạy các instance cho phiên bản mô hình cũ. Tuy nhiên, có thể có một trường hợp khác trong đó vấn đề năng lực vẫn tồn tại trong quá trình rolling back, và endpoint sẽ hiển thị là UPDATE\_ROLLBACK\_FAILED. Các instance hiện có vẫn có thể phục vụ lưu lượng, nhưng để chuyển endpoint ra khỏi trạng thái failed, bạn cần liên hệ với nhóm AWS support của mình.

# **Các cân nhắc bổ sung**

Như đã đề cập trước đó, khi sử dụng triển khai blue/green để cập nhật các inference component trên một endpoint, bạn cần cung cấp tài nguyên cho cả môi trường hiện tại (blue) và môi trường mới (green) đồng thời. Khi bạn đang sử dụng rolling update cho các inference component trên endpoint, bạn có thể sử dụng phương trình sau để tính số lượng service quota tài khoản cho loại instance cần thiết. GPU instance cần thiết cho endpoint có X số GPU accelerator, và mỗi bản sao inference component yêu cầu Y số GPU accelerator. Kích thước batch tối đa được đặt thành Z và endpoint hiện tại có N instance. Do đó, service quota cấp tài khoản cần thiết cho loại instance này cho endpoint phải lớn hơn đầu ra của phương trình:

ROUNDUP(Z x Y / X) + N

Ví dụ, giả sử endpoint hiện tại có 8 (N) instance ml.g5.12xlarge, có 4 GPU accelerator của mỗi instance. Bạn đặt kích thước batch tối đa thành 2 (Z) bản sao, và mỗi bản sao cần 1 (Y) GPU accelerator. Giá trị service quota AWS tối thiểu cho ml.g5.12xlarge là ROUNDUP(2 x 1 / 4) + 8 = 9. Trong một tình huống khác, khi mỗi bản sao của inference component yêu cầu 4 GPU accelerator, thì service quota cấp tài khoản cần thiết cho cùng một instance phải là ROUNDUP(2 x 4 / 4) + 8 = 10.

# **Kết luận**

Các bản cập nhật cuốn chiếu (*rolling updates*) cho các thành phần suy luận đại diện cho một bước tiến quan trọng trong khả năng triển khai của SageMaker AI. Tính năng này trực tiếp giải quyết các thách thức trong việc cập nhật mô hình đang chạy trong môi trường sản xuất, đặc biệt là với những khối lượng công việc nặng về GPU. Nó giúp loại bỏ việc phải ước lượng dung lượng thủ công, đồng thời giảm thiểu rủi ro khi cần hoàn tác (rollback).

Bằng cách kết hợp quy trình cập nhật theo lô (*batch-based updates*) cùng với các biện pháp bảo vệ tự động, SageMaker AI đảm bảo rằng các quá trình triển khai luôn linh hoạt và ổn định.

Các lợi ích chính bao gồm:

* Giảm chi phí tài nguyên trong quá trình triển khai, không cần cấp phát thêm cụm máy chủ dự phòng.
* Cải thiện cơ chế bảo vệ trong quá trình triển khai nhờ cập nhật dần và khả năng tự động hoàn tác khi xảy ra lỗi.
* Duy trì khả năng hoạt động liên tục trong khi cập nhật, với kích thước lô có thể cấu hình.
* Đơn giản hóa việc triển khai các mô hình phức tạp cần nhiều bộ tăng tốc (*multi-accelerator models*).

Dù bạn đang triển khai mô hình nhỏ gọn hay các mô hình lớn sử dụng nhiều bộ tăng tốc, **rolling updates** mang lại một phương pháp hiệu quả hơn, tiết kiệm chi phí và an toàn hơn để giữ cho các mô hình máy học của bạn luôn được cập nhật trong môi trường sản xuất.

Chúng tôi khuyến khích bạn dùng thử khả năng mới này trên các endpointSageMaker AI của mình và khám phá cách nó có thể nâng cao hiệu quả hoạt động ML của bạn. Để biết thêm thông tin, vui lòng tham khảo [SageMaker AI documentation](https://docs.aws.amazon.com/) hoặc liên hệ với nhóm tài khoản AWS của bạn.

# **Về các tác giả**![](data:image/png;base64...)

**Melanie Li, Tiến sĩ**, là Chuyên gia Kiến trúc Giải pháp Generative AI Cấp cao tại AWS, trụ sở tại Sydney, Úc. Cô tập trung vào việc hỗ trợ khách hàng xây dựng các giải pháp ứng dụng các công cụ AI và máy học tiên tiến nhất. Cô đã tham gia vào nhiều sáng kiến Generative AI trên toàn khu vực APJ, tận dụng sức mạnh của Large Language Models (LLMs). Trước khi gia nhập AWS, Tiến sĩ Li từng đảm nhiệm vai trò nhà khoa học dữ liệu trong lĩnh vực tài chính và bán lẻ.![](data:image/png;base64...)

**Andrew Smith** là Kỹ sư Hỗ trợ Đám mây trong nhóm SageMaker, Vision & Other tại AWS, trụ sở Sydney, Úc. Anh hỗ trợ khách hàng sử dụng nhiều dịch vụ AI/ML của AWS, đặc biệt có chuyên môn sâu về Amazon SageMaker. Ngoài công việc, anh thích dành thời gian cho gia đình, bạn bè và tìm hiểu các công nghệ mới.

![](data:image/png;base64...)

**Dustin Liu** là Kiến trúc sư Giải pháp (Solutions Architect) tại AWS, tập trung hỗ trợ các công ty khởi nghiệp và doanh nghiệp SaaS trong lĩnh vực dịch vụ tài chính và bảo hiểm (FSI). Anh có nền tảng đa dạng trong kỹ thuật dữ liệu (data engineering), khoa học dữ liệu (data science) và máy học (machine learning), đồng thời đam mê ứng dụng AI/ML để thúc đẩy đổi mới và chuyển đổi doanh nghiệp.

![](data:image/png;base64...)

**Vivek Gangasani** là Chuyên gia Kiến trúc Giải pháp Generative AI Cấp cao tại AWS. Anh giúp các công ty khởi nghiệp về Generative AI xây dựng các giải pháp sáng tạo bằng cách sử dụng dịch vụ AWS và hạ tầng tính toán tăng tốc. Hiện tại, anh tập trung vào việc phát triển các chiến lược tinh chỉnh (fine-tuning) và **t**ối ưu hiệu năng suy luận (inference performance) cho các mô hình ngôn ngữ lớn (LLMs). Ngoài công việc, Vivek thích leo núi, xem phim và khám phá ẩm thực.![](data:image/png;base64...)

**Shikher Mishra** là Kỹ sư Phát triển Phần mềm (Software Development Engineer) thuộc nhóm SageMaker Inference, với hơn 9 năm kinh nghiệm trong ngành. Anh đam mê xây dựng các giải pháp mở rộng, hiệu quả, giúp khách hàng triển khai và quản lý ứng dụng máy học một cách dễ dàng. Thời gian rảnh, Shikher yêu thích thể thao ngoài trời, leo núi và du lịch.![](data:image/png;base64...)

**June Won** là Quản lý sản phẩm (Product Manager) của Amazon SageMaker JumpStart. Anh tập trung vào việc giúp khách hàng dễ dàng tìm kiếm và sử dụng các mô hình nền tảng (foundation models) để xây dựng ứng dụng Generative AI. Kinh nghiệm của anh tại Amazon còn bao gồm phát triển ứng dụng mua sắm di động và giải pháp giao hàng chặng cuối (last-mile delivery).