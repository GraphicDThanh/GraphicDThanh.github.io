---
title: "Giới thiệu dịch vụ EC2 của AWS"
excerpt_separator: <!--more-->
categories:
  - AWS
tags:
  - aws
  - ec2
---

![](/images/2023/03/2023-03-gioi-thieu-dich-vu-ec2-cua-aws.webp)

[EC2](https://aws.amazon.com/ec2/) là viết tắt của Elastic Compute Cloud, là một dịch vụ AWS thuộc loại Infrastructure as a Service (IaaS)

Hiện nay, EC2 cung cấp 4 nhóm dịch vụ chính bao gồm:

1. Cho thuê (tạo) máy chủ ảo (EC2 instance)

2. Lưu trữ dữ liệu trên máy chủ ảo (EBS – Elastic Block Store, EFS – Elastic File System)

3. Phân phối tải trên nhiều máy chủ ảo (ELB – Elastic Load Balancing)

4. Tự động scale số lượng máy chủ ảo (ASG – Auto Scaling Group)

## Thuê máy chủ ảo (EC2 instance)

Khi thuê một máy chủ ảo, bạn có thể tạo máy với cấu hình mong muốn:

* OS (operating system): hệ điều hành như Linux, MacOS, Window
* CPU (central processing unit): bộ xử lý trung tâm hay bộ vi xử lý (các loại chip như core i7, m1)
* RAM (random access memory): bộ nhớ tạm giúp CPU truy xuất lấy thông tin nhanh
* Các loại bộ nhớ kèm theo như:
  * bộ nhớ bên ngoài được gắn vào như EBS, EFS (các network drive)
  * bộ nhớ bên trong như EC2 instance store
  * card mạng
  * tường lửa (security group)
  * bootstrap script (EC2 user data) giúp boot máy tính khi lần đầu tạo
      
## Lưu trữ dữ liệu trên máy chủ ảo

### EC2 Instance Store

EC2 Instance store là bộ nhớ bên trong máy EC2

### EBS - Elastic Block Store

EBS volume là một network drive được gắn vào máy EC2 instance của bạn khi chạy. Mỗi EBS volume chỉ được gắn vào một EC2 tại một thời điểm. EBS volume nằm cố định ở AZ cụ thể.

Vì EBS volume chỉ nằm ở một AZ cụ thể nên nếu muốn di chuyển bộ nhớ này qua vùng AZ khác sẽ cần tạo EBS snapshot rồi sử dụng để tạo EBS volume ở AZ cần chuyển qua.

Có nhiều loại EBS volume khác nhau như gp2, gp3, io1, io2, stl, scl. Mỗi loại sẽ có các thông số về Size, Throughput, IOPS tương ứng.

EBS multi-attach loại io1, io2 có thể gắn vào nhiều máy EC2

### EFS - Elastic File System

EFS có thể gắn vào nhiều máy chủ EC2 ở nhiều AZ khác nhau.

EFS chỉ hỗ trợ máy Linux, thưởng sử dụng trong chia sẻ nội dung như web server, WordPress.

## Phân phối tải trên nhiều máy chủ ảo

### Khả năng mở rộng

**Scalability** (khả năng mở rộng) có nghĩa là hệ thống có thể tự xử lý tải.

Có 2 loại:

* **Vertical Scalability**: chỉ việc tăng khả năng của máy chủ như CPU, RAM, bộ nhớ. Kiểu mở rộng này phổ biến với các hệ thống không phân tán, như cơ sở dữ liệu (RDS, ElastiCache).

* **Horizontal Scalability**: chỉ việc tăng số lượng máy chủ.Kiểu mở rộng này phổ biến với các hệ thống phân tán, như ứng dụng web.

### Lợi ích khi sử dụng load balancer

*  giúp phân phối tải (traffic) đến nhiều máy ch
*  ứng dụng chỉ có một địa chỉ DNS
*  xử lý lỗi và thực hiện kiểm tra sức khỏa (health check) các máy chủ
*  cung cấp dịch vụ SSL (HTTPS)
*  có thể gắn người dùng với cookie
*  tăng tính khả dụng (high availability) qua nhiều AZ
*  tách các loại traffic khác nhau để xử lý

### AWS Load Balancers
AWS cung cấp 3 loại Load Balancers là:

* Classic Load Balancer (CLB)
* Application Load Balancer (ALB)
* Network Load Balancer (NLB)
* Gateway Load Balancer (GWLB) 

Người dùng khi truy cập đến ứng dụng sẽ đi qua security group của load balancer, sau đó đi đến máy chủ. 

Bạn có thể truyền tải đến nhiều nhóm máy chủ được thiết lập theo target group. 
#### Classic Load Balancer (CLB)
**Classic Load Balancer (CLB)** (thế hệ cũ – không khuyến khích sử dụng) cho phép truyền tải với các giao thức HTTP, HTTPS, TCP, SSL (secure TCP). 

#### Application Load Balancer (ALB)
**Application Load Balancer (ALB)** cho phép truyền tải với giao thức **HTTP, HTTPS và WebSocket.**

Các truy cập có thể được phân loại dựa trên URL, hostname query string, headers, … để xác định đi đến target group nào. Các target group có thể là EC2 instances, ECS tasks, lambda function, private IP address

ALB phù hợp cho micro services và ứng dụng container-based.

ALB có hostname cố định, ví dụ xxx.region.elb.amazoneaws.com.

Health check hỗ trợ ở target group.

#### Network Load Balancer (NLB)
**Network Load Balancer (NLB)** cho phép truyền tải với giao thức** TCP, TLS (secure TCP) và UDP.**

NLB có static IP cho mỗi AZ.

Các target group có thể là EC2 instances, địa chỉ IP, ALB

Health check hỗ trợ theo TCP, HTTP và HTTPS.

#### Gateway Load Balancer (GWLB)
**Gateway Load Balancer (GWLB)** cho phép truyền tải với giao thức IP.

GWLB cung cấp Transparent Network Gateway (vào, ra một lần) và Load Balancer (phân phối tải)

Các target group có thể là EC2 instances, địa chỉ IP

*Ghi chú:* TCP (layer 4), HTTP & HTTPS (layer 7), IP (layer 3)

Ngoài ra, để giữ cookie của người dùng và cho phép truy cập đến đúng máy chủ đã phục vụ trước đó, có thể dùng **sticky session**.

Còn nếu muốn phân phối tải với tỉ lệ đồng đều giữa cái AZ thì sử dụng **cross-zone load balancing**.

SSL certificate cho phép data giữa máy client và load balancer được mã hóa (encrypt)
Nếu bạn có nhiều SSL certificate cho từng loại máy chủ khác nhau thì **SNI** (Server Name Indication) giúp bạn xác định loại cert.

## Tự động scale số lượng máy chủ

Thực tế là không thể biết trước số tải (traffic) sẽ truy cập đến ứng dụng của bạn.

ASG – Auto Scaling Group giúp bạn:

* tự động tăng số lượng máy chủ khi tải tăng
* tự động giảm số lượng máy chủ khi tải giảm
* đảm bảo số máy chủ tối đa và tối thiểu nhất định
* tự động tạo máy chủ mới với cấu hình định sẵn (launch template)
* tự động tạo lại nếu máy chủ bị tắt khi unhealthy

Có thể kích hoạt ASG từ thông số của thông báo từ CloudWatch về chỉ số như Average CPU, hay tự tạo chỉ số.

Có thể tạo policies để kích hoạt ASG theo nhiều loại như:

* Target tracking scaling: muốn CPU tầm 40%
* Simple / Step Scaling:
  * khi có cảnh báo từ CloudWatch với CPU > 70% -> thêm 2 máy chủ
  * khi có cảnh báo từ CloudWatch với CPU < 30% -> bỏ bớt 1 máy chủ
  * scheduled Actions: tăng hay giảm số máy chủ vào cuối tuần

---

Bài viết giới thiệu đến bạn một số kiến thức cơ bản về dịch vụ EC2 cung cấp bởi AWS.

Bạn ghé trang chủ EC2 nếu muốn tìm hiểu thêm nhé.
