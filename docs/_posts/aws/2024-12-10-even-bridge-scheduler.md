---
title: "Một Vài Lưu Ý Khi Lập Lịch Hàng Tháng với EventBridge"
excerpt_separator: <!--more-->
categories:
  - AWS
tags:
  - aws
  - eventbridge
---

![](/assets/images/2024/12/2024-12-10-even-bridge-scheduler-cover.jpg)

Trong bài viết hôm nay, mình sẽ chia sẻ về một chủ đề đơn giản nhưng thú vị: lập lịch công việc định kỳ (scheduling). Hãy tưởng tượng bạn cần tự động tặng thêm $10 hàng tháng cho khách hàng đã đăng ký gói Premium của dịch vụ bạn cung cấp.

Với AWS, có hai giải pháp phổ biến để giải quyết bài toán này: **SQS Queue** và **EventBridge**. Trong bài viết này, mình sẽ tập trung vào giải pháp sử dụng **Amazon EventBridge Scheduler**.

Để bạn dễ hình dung bài toán, dưới đây là [**Subscription-Based Payment Flow with AWS EventBridge and Stripe**](https://drive.google.com/file/d/1zsuc1sh_sLDmxJxjsJRunB42yioDdwdm/view?usp=drive_link):
![](/assets/images/2024/12/2024-12-10-even-bridge-scheduler-flow-1.png)

- (1) Người dùng muốn mua gói **subscription Premium** theo hình thức thanh toán **hàng năm**
- (2) Ứng dụng Frontend gọi đến Backend để lấy thông tin phiên checkout của Stripe
- (3) Ứng dụng FE nhận được URL phiên checkout và chuyển hướng người dùng đến giao diện Stripe để bắt đầu thanh toán
- (4) Người dùng điền thông tin và thanh toán thành công
- (5) Stripe kích hoạt một Webhook event thông báo thanh toán thành công, một gói đăng ký mới được kích hoạt
- (6) Ứng dụng BE lắng nghe sự kiện và tạo một Event Bridge Scheduler sẽ chạy **hàng tháng**, bắt đầu từ thời gian hiện tại
- (7) Event Bridge Scheduler kích hoạt sự kiện theo lịch (hàng tháng), hàm Lambda được cài đặt làm mục tiêu sẽ chạy
- (8) Lambda xử lý logic công việc và cập nhật cơ sở dữ liệu (nếu có)

Bài viết này sẽ tập trung và phân tích cách lập lịch hàng tháng với EventBridge Scheduler thuộc flow 6, 7
**Schedule Monthly Task with Event Bridge**

## Amazon EventBridge là gì?

[Amazon EventBridge](https://aws.amazon.com/eventbridge/) là một dịch vụ serverless của AWS, giúp bạn dễ dàng kết nối các ứng dụng thông qua các sự kiện (event-driven). EventBridge hỗ trợ lập lịch công việc và chuyển tiếp sự kiện từ nhiều nguồn khác nhau (AWS services, SaaS apps, custom applications) đến các mục tiêu như Lambda, SQS, Step Functions...

Bạn có thể xem thêm video giới thiệu ngắn gọn này:
<iframe width="640" height="360" src="https://www.youtube.com/embed/5K6qpMOVS0E?si=XaQ5r_pPQI-1yD7y" frameborder="0" allowfullscreen></iframe>


## Phân Loại Lịch trong EventBridge Scheduler

EventBridge Scheduler hỗ trợ 3 loại schedule:

### **Rate-based** schedule (định kỳ theo chu kỳ):
- Dùng để trigger event theo khoảng thời gian cố định.
- Cú pháp: `rate(value unit)` với value là số dương và unit là minutes, hours, hoặc days.
- Ví dụ: `rate(5 minutes)` sẽ trigger event mỗi 5 phút.

![](/assets/images/2024/12/2024-12-10-even-bridge-scheduler-rate.png)

### **Cron-based** schedule (định kỳ theo lịch cụ thể):
- Dùng để trigger event vào thời gian cụ thể trong ngày, tuần, tháng hoặc năm.
- Cú pháp: `cron(minutes hours day-of-month month day-of-week year)`
 - Ví dụ: `cron(0 0 1 * ? *)` sẽ trigger vào 0h ngày 1 mỗi tháng.

![](/assets/images/2024/12/2024-12-10-even-bridge-scheduler-cron-1.png)

### **One-time** schedule (chỉ định một lần):
- Trigger sự kiện duy nhất vào một thời điểm cụ thể.

![](/assets/images/2024/12/2024-12-10-even-bridge-scheduler-one-time-schedule.png)

(Đọc thêm tại [official document](https://docs.aws.amazon.com/scheduler/latest/UserGuide/schedule-types.html))

## Phân Tích Bài Toán Lập Lịch Hàng Tháng

Giả sử bạn cần tự động thực hiện tác vụ trên (tặng $10 vào tài khoản) hàng tháng vào đúng ngày mua "Premium subscription" của khách hàng, mình sẽ phân tích hai phương pháp phổ biến:

### Rate-based Schedule
- **Rate expression**: `rate(30 days)`
- **Hạn chế**: Tháng có thể dài hơn hoặc ngắn hơn 30 ngày (ví dụ tháng 2 có 28 ngày). Do đó, việc sử dụng rate(30 days) sẽ gây ra sự chênh lệch, khiến người dùng nhận thông báo hoặc hành động không đúng ngày mong muốn.

### Cron-based Schedule
- **Cron expression**: `cron(0 0 x * ? *)`
  - trigger event mỗi tháng vào ngày `x` là ngày mua Premium subcription.
- **Hạn chế**:
  - Nếu người dùng mua gói vào ngày **31**, cron sẽ *không thể* trigger trong các tháng không có ngày 31 (tháng 2, 4, 6, 9, 11).
  - Tương tự cho các ngày 29, 30 thì tháng 2 sẽ bị thiếu trigger.

![](/images/2024/12/2024-12-10-even-bridge-scheduler-cron.png)

## Giải Pháp Xử Lý Cron-based Schedule
### 1: Sử Dụng Ngày Đầu Tháng Tiếp Theo
- Đặt cron chuyển các ngày lớn hơn 28 thành ngày 1 của tháng tiếp theo.
- Cách này đơn giản, đảm bảo mỗi tháng đều có event trigger, nhưng có thể gây trễ 1-2 ngày với người dùng.
- Ví dụ:
  - Ngày ≤ 28: `cron(0 0 x * ? *)`
  - Ngày > 28: `cron(0 0 1 * ? *)`

### 2: Sử Dụng One-time Schedule
- Với mỗi lần trigger, Lambda function sẽ tạo ra lịch trigger tiếp theo dựa trên logic tính toán ngày cuối cùng của tháng.
- Ví dụ: nếu user mua gói Premium vào ngày 31/12/2024, các lần trigger tiếp theo sẽ là 31/01/2025, 28/02/2025, 31/03/2025. Viết logic code để chọn đúng ngày tiếp theo và tạo one-time schedule tương ứng.

## Kết Luận
Khi lập lịch công việc định kỳ với AWS EventBridge, bạn cần cân nhắc kỹ các trường hợp đặc biệt như:

- Các tháng không có đủ số ngày trong cron expression.
- Sự khác biệt về số ngày giữa các tháng.

Hy vọng bài viết này giúp bạn hiểu rõ hơn cách dùng EventBridge Scheduler và cách chọn shedule type phù hợp với bài toán của mình.