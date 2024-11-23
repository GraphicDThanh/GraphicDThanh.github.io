---
title: "Các bài viết ngắn về Devops và Cloud Computing"
---

Các bài viết ngắn về "Devops"
- Phân biệt IaaS, PaaS và SaaS
- Học AWS theo career path
- AWS Certified Developer Associate
- IAM - Identity and Access Management
- Microservice là gì?
- Vì sao NGINX là reverse proxy?
- CDN và cách hoạt động

## Phân biệt IaaS, PaaS và SaaS
Cloud Fundamentals – Phân biệt IaaS, PaaS và SaaS

Cloud computing (điện toán đám mây) cung cấp cho developers khả năng tập trung vào việc quan trọng nhất là xây dựng sản phẩm thay vì phải đau đầu với các loại kiến trúc tốn kém hay việc vận hành và bảo trì hệ thống.

Cùng với sự phát triển của cloud computing, các loại dịch vụ khác nhau ra đời phục vụ cho các đối tượng người dùng khác nhau. Hiểu sự khác nhau của IaaS, PaaS, SaaS sẽ giúp bạn chọn đúng loại dịch vụ cần dùng.

IaaS
“Infrastructure as a Service” hay “Cơ sở hạ tầng dưới dạng dịch vụ”
IaaS hứa các khối hạ tầng cơ bản cho hệ thống (phần cứng, hệ điều hành) và các quyền truy cập, như các máy tính ảo hay không gian lưu dữ liệu.
IaaS có mức linh hoạt cao nhất và khả năng quản lý tài nguyên tối ưu nhất.

PaaS
“Platform as a Service” hay “Nền tảng dưới dạng dịch vụ”
PaaS loại bỏ việc quản lý cơ sở hạ tầng, cho phép bạn tập trung vào việc quản lý ứng dụng của mình.

SaaS
“Software as a Service” hay “Phần mềm dưới dạng dịch vụ”
SaaS cung cấp một dịch vụ hoàn chỉnh do nhà cung cấp dịch vụ vận hành và quản lý.
Đây là loại dịch vụ dành cho người dùng cuối, ví dụ như Gmail.

Bạn có thể xem thêm các video về Cloud Fundamentals của IBM ở list này nhé
![](https://www.youtube.com/playlist?list=PLOspHqNVtKAC-_ZAGresP-i0okHe5FjcJ)
s
## Học AWS theo career path
Gõ AWS lên google mình tìm thấy vô số nguồn tài liệu, các khoá học, … và không biết đầu từ đâu.

May mắn mình tìm được một video giới thiệu cách học AWS cho từng đối tượng cụ thể “by career path”.

Video giới thiệu các services chung, các services dành cho frontend, backend, devops, data engineer.

Services common:
– Regions and Availability Zones
– Identity and Access Management (IAM)
– Cloudwatch Logs
– Cloud Development Kit (CDK) / CloudFormation
– Virtual Private Cloud (VPC)

Frontend
– Amplify
– CloudFront
– API Gateway
– Cognito
– Simple Storage Service (S3)

Backend
– EC2 (Elastic Cloud Computing)
– Lambda
– ECS / EKS
– Load Balancers
– Certificate Managers
– Simple Notification Service (SNS)
– Simple Queue Service (SQS)
– Step Functions
– DynamoDB
– Relational Database Service (RDS)
– ElastiCache

Devops
– Commit
– CodeBuild
– CodePipeline
– Cloudwatch Alarms
– Cloudwatch Monitoring
– Cloudwatch Dashboards

Data Engineer
– Glue
– Batch
– Redshift
– Athena
– Lake Infomation

Bạn có thể xem tác giả giới thiệu cụ thể hơn trong [video](https://youtu.be/N8lcedBPmE8) nhé


## AWS Certified Developer Associate
Hiện nay, dịch vụ AWS được sử dụng rộng khắp toàn cầu. Việc lấy chứng chỉ “AWS Certified Developer Associate” được nhiều lập trình viên ưu tiên vì là bằng chứng dễ thấy nhất để khẳng định khả năng có thể làm việc với các dịch vụ điện toán đám mây của AWS (Cloud Computing and AWS services)

Kỳ thi này kéo dài 130 phút, với 65 câu hỏi (câu hỏi nhiều lựa chọn và câu hỏi tình huống)
Nếu bạn đạt từ 720 điểm (thang điểm 100) sẽ có chứng chỉ.
Chi phí $150, kết quả có ngay sau khi thi, chứng chỉ có hạn trong 3 năm.

Kỳ thi này bao gồm 4 lĩnh vực chính:
– Deployment chiếm 22% điểm
– Security chiếm 26% điểm
– Development with AWS Services chiếm 30% điểm
– Refactoring 10%
– Monitoring and Troubleshooting 12%

Bạn đọc thêm chi tiết ở [tài liệu chính thức này](https://aws.amazon.com/certification/certified-developer-associate/) nhé

## IAM - Identity and Access Management

IAM - Identity and Access Management
IAM giúp quản lý người dùng và các cấp độ truy cập của họ trên bảng điều khiển AWS (AWS Console).

IAM là dịch vụ AWS cơ bản nhất mà bạn sẽ làm việc cùng ngay sau khi tạo tài khoản AWS, hiểu rõ về IAM sẽ giúp bạn hoàn thành tốt các kỳ thi lấy tín chỉ AWS cũng như vô cùng quan trọng trong thực tế, khi mà bạn cần quản lý quyền truy cập vào các tài nguyên AWS trong dự án, công ty.

Một số khái niệm cơ bản:

- Users: người dùng cuối (mọi người)
- Groups: một nhóm các người dùng với các quyền riêng cho họ
- Roles: các vai trò được tạo và gán vào người dùng, ứng dụng hay dịch vụ để có thể truy cập vào các tài nguyên AWS
- IAM Policy (Policy Document) là tài liệu ở dạng JSON xác định một hay nhiều quyền.

```json
{
	“Version”: “2022-10-17",
	“Statement”: [
		{
			“Effect”: “Allow”,
			“Action”: “*”,
			“Resource”: “*”
		}
	]
}
```

- Access keys: một người dùng mới sẽ có bộ access key ID và secret access key sử dụng để truy cập AWS qua APIs hay command line.
Các keys này không thay thế cho mật khẩu và không thể sử dụng để đăng nhập vào bảng điều khiển (AWS Management Console)
Các keys này chỉ được cấp (và thấy) một lần, sau đó nếu bạn bị mất sẽ cần tạo lại.
Lưu ý tải / copy và giữ các keys này cẩn thận

Một số lưu ý:
- IAM là global (toàn cầu) không theo region (vùng)
- Root account là tài khoản bạn tạo khi đăng ký aws, và tài khoản này có đầy đủ quyền của admin
- Một user mới được tạo thì chưa có quyền nào, admin cần gán quyền cho user đó

Bạn có thể sử dụng IAM Policy Simulator để kiểm tra quyền của các tài khoản.

## Microservice là gì?

Kiến trúc Microservices cho phép xây dựng các ứng dụng có thể mở rộng.

Microservices là gì?

Kiến trúc Microservices bao gồm nhiều service tách rời nhau.
Mỗi service có nhiệm vụ riêng tách biệt nhau trong một hệ thống lớn thường xuyên được mở rộng.

Ví dụ:
Shopping cart -> shopping domain
Billing -> billing domain
User Profile -> user domain
Push Notification -> push domain

Tất cả các nhóm nhiệm vụ riêng ở trên đều có thể là một service tách rời nhau, thường gọi là domain.

Microservices giao tiếp với nhau ra sao?

Microservices giao tiếp với nhau qua giao diện (interface) ở khoảng cách gần (surface area nhỏ) giúp giảm tỉ lệ bị lỗi. Điều này làm mỗi service có thể trở thành một phần của toàn bộ hệ thống.

Microservices nói chuyện với nhau thông qua sự kết hợp của RPC (remote produce calls), Event Streaming, Message Brokers.

Các điểm mạnh của Microservices:

- Microservices mang đến sự linh hoạt cho việc mở rộng từng service độc lập nhau.
- Microservices có thể được triển khai (deploy) độc lập với nhau vì mỗi service thì nhỏ, tách biệt, và có thể deploy thường xuyên.
- Kiến trúc Microservices tốt giúp ẩn đi nhiều thông tin vì mỗi loại thông tin sẽ nằm ở các service khác nhau.
Ví dụ như một “Monolithic Database” sẽ được chia thành các thành phần khác như Shopping Card DB, Billing DB, User DB, Notification DB.

Các điểm yếu của Microservices:

- Kiến trúc Microservices phá vỡ cơ sở dữ liệu, tức sẽ không có các loại quan hệ.
- Xây dựng và vận hành Microservices sẽ tốn nhiều tiền

Vậy thì khi nào nên sử dụng Microservices?
- Xây dựng và vận hành Microservices sẽ tốn nhiều tiền, do đó nó chỉ phù hợp cho các dự án lớn (nhiều team lớn).
  Khi đó, các team vận hành độc lập, mỗi domain có thể được vận hành và bảo trì độc lập bởi từng team.
  Mỗi team có thể tự phát triển domain của mình nhanh chóng, tự thiết kế, phát triển, triển khai, mở rộng.

- Microservices sẽ không phù hợp với các dự án nhỏ startup vì chi phí cao.
  Tuy nhiên, để phát triển theo hướng microservice trong tương lai, với startup, khuyến khích nên thiết kế mỗi tính năng trong ứng dụng tách biệt nhau càng nhiều càng tốt để dễ dàng chuyển đổi khi cần.

Bạn xem minh họa mô hình ở video này nhé.

<iframe width="640" height="360" src="https://youtu.be/lTAcCNbJ7KE" frameborder="0" allowfullscreen></iframe>

## Vì sao NGINX là reverse proxy?
Vì sao NGINX gọi là reverse proxy? proxy là gì?

Proxy là một server trung gian đứng giữa máy tính của bạn và thế giới internet ngoài kia.

Có 2 loại proxy phổ biến là Forward Proxy và Reverse Proxy.

Forward Proxy đứng giữa một nhóm người và internet, như trung gian chặn các request và nói chuyện với các máy chủ khác đại diện cho các request đó.

Vì sao lại sử dụng forward proxy?

Một số lý do:
– bảo vệ thông tin của người dùng trong hệ thống, máy chủ sẽ không biết được địa chỉ IP của người dùng
– sử dụng để bỏ qua các hạn chế khi duyệt web (các công ty, trường học, …)
– sử dụng để chặn một số nguồn nhất định

Reverse Proxy (như NGINX) đứng giữa web server và internet, như trung gian chặn các request từ client và nói chuyện với web server đại diện client đó.

Vì sao website sử dụng reverse proxy?

Một số lý do:
– bảo vệ máy chủ web, client không biết được địa chỉ IP của máy chủ vì địa chỉ này được reverse proxy ẩn đi, hạn chế các tấn công đồng loạt như DDoS
– reverse proxy sử dụng cho load balancing, vì nếu một trang web có lưu lượng truy cập lớn sẽ cần có nhiều server thì reverse proxy đóng vai trò chuyển đổi các request đến nhiều máy chủ khác, giúp giảm quá tải server. Dịch vụ như Cloudflare có máy chủ reverse proxy trên toàn cầu, gần với người dùng nhất có thể.
– reverse proxy cache các nội dung tĩnh (static content) giúp các truy cập nhanh hơn.
– reverse proxy có thể xử lý các kết nối mã hoá SSL, giảm tải cho server

Reverse Proxy được sử dụng khắp mọi nơi (Google, Meta, Amazon, Apple, …) và có nhiều lớp reverse proxy.
– Lớp đầu tiên có thể là một dịch vụ Edge Server như Cloudflare
– Lớp thứ hai có thể là API gateway hay load balancer của hosting

[Mời bạn xem video thú vị này ở đây](https://youtu.be/4NB0NDtOwIQ)

## CDN và cách hoạt động
CDN (Content Delivery Network) là hệ thống các máy chủ trên khắp thế giới.

Ban đầu hệ thống này giúp phân phối nội dung tĩnh của website (HTML) cho người dùng. Qua nhiều thập kỷ, CDN ngày càng phát triển và trở thành công cụ nên được sử dụng bất cứ khi nào có HTTP request.

Vậy CDN giúp gì cho bạn?

Thông qua hệ thống máy chủ PoP (Points of Presence) hay Edge Server trên toàn thế giới, CDN đưa nội dung đến gần với người dùng hơn, từ đó nâng cao trải nghiệm của người dùng.

Các CDN khác nhau (Amazon Cloudfront, Cloudflare, Akamai, Microsoft Azure CDN) sử dụng các loại công nghệ khác nhau để mang HTTP request từ user đến các PoP ở gần họ.
Có 2 loại công nghệ phổ biến là DNS-based routing và Anycast

– Với DNS-based routing, mỗi PoP có địa chỉ IP riêng. Khi người dùng gọi đến CDN, DNS trả về địa chỉ IP của PoP gần với người dùng nhất.
– Với Anycast, tất cả các PoP chia sẻ cùng địa chỉ IP

Mỗi edge server hoạt động như một reverse proxy với nội dung cache khổng lồ. Nội dung được cache thường chỉ các các file tĩnh như HTML cho nên nếu nội dung nào cần yêu cầu thêm thì PoP sẽ gửi yêu cầu đến máy chủ để tải về.

Điều này giúp giảm tải nội dung cần yêu cầu trực tiếp đến máy chủ.

CDN còn giúp nén nội dung lại (minify hay thay đổi format png sang webp, …) và giúp giảm thời gian khi request bằng giao thức TLS (https)

Ngoài ra CDN còn giúp tăng tính bảo mật(tránh được DDoS) và tăng tính khả dụng (một PoP chết thì request sẽ chuyển đến PoP khác)

[Mời bạn xem video nội dung ở đây](https://www.youtube.com/watch?v=RI9np1LWzqw)

