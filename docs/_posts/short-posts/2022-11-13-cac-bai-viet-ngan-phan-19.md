---
title: "Các bài viết ngắn - phần 8"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/12/Short-posts-19.png)

## Giới thiệu về XState
Hôm nay công ty có bài giới thiệu về XState cực thú vị, nên mình muốn giới thiệu đến bạn qua bài viết nhỏ này.

XState giúp phát triển web, app theo hướng State Machine, tức là lấy state của máy làm trung tâm và phát triển ứng dụng dựa trên sơ đồ các trạng thái và sự chuyển đổi trạng thái thông qua các sự kiện.

Hai điều thú vị mà mình ấn tượng nhất là:

Đầu tiên, sơ đồ trạng thái của ứng dụng được mô tả một cách trực quan, các luồng chạy của ứng dụng có thể được hiểu rõ qua sơ đồ (khi thiết kế trạng thái tương tự diagram) hay có thể chia sẻ luồng dữ liệu ứng dụng mà không cần đọc code.

Điều này sẽ giúp người lập trình suy nghĩ về logic ứng dụng trước khi code, sắp xếp các sự kiện hợp lý, theo đó UX cũng sẽ hợp lý theo vì các trạng thái sẽ chuyển đổi theo tác vụ của người dùng.

Thứ hai, là việc tái sử dụng mô hình state machine này vào các loại ứng dụng khác nhau mà XState hỗ trợ.

Điều này sẽ giúp ứng dụng web (xây dựng với React) và hydrid mobile (xây dựng với React Native) có thể sử dụng chung source code của ứng dụng với XState này. Do đó sẽ làm giảm thời gian lập trình và nhiều nên tảng ứng dụng sẽ có cùng định hướng, cùng sơ đồ trạng thái – single source of true.

Bạn có thể ghé [trang chủ của XState](https://xstate.js.org/) để tìm hiểu thêm.

## Một số tips viết clean code JS

Viết clean code JS cần đảm bảo các tiêu chí sau: dễ đọc, dễ debug, hiệu quả và hiệu suất cao

Một số tips bạn nên nắm rõ để viết code JS clean:

1. Sử dụng try/catch cho tất cả các request đến API và các phương thức liên quan JSON

2. Sử dụng linter (ESLint) để giúp scan code và chỉ ra các lỗi cần sửa dựa trên các quy tắc chuẩn hay tự config cho code dự án thống nhất.

3. Theo dõi các việc cần làm ngay trên editor với extension như Stepsize, hay TODO highlight

4. Sử dụng template string sẽ dễ đọc hơn.

Thay vì `‘Hello’ + username` thì nên viết `Hello ${username}`

5. Sử dụng optional chaining để nối các điều kiện kiểm tra lại
Thay vì if (data && data.payload && data.payload.name == ‘Anna’)
thì nên viết if (data?playload?name == ‘Anna’)

6. Hạn chế code quá nhiều lớp lồng nhau, nên giới hạn là 2 – 5 lớp lồng là tối đa để giảm phức tạp cho source code.

7. Comment code cho những nội dung cần thiết, tránh comment để giải thích source code.

https://dev.to/alexomeyer/8-must-know-tips-for-writing-clean-code-with-javascript-i4

## Lexical Environment trong JS
Sau khi đã nắm rõ về execution context cùng hai giai đoạn của nó (memory creation và code execution) và call stack (các execution context được push / pop trong stack), mình sẽ cùng tìm hiểu về một khái niệm nền tảng nữa của JavaScrip, đó là lexical environment. 

Hiểu về lexical environment sẽ giúp bạn dễ hiểu các khái niệm như scope, scope chain hay closures. 

Vậy lexical environment là gì ? 

“Lexical Environment” của hàm bao gồm local memory của hàm đó cộng với “Lexical Environment” của cha nó. 

Lexical environment được tạo ra khi nào ? 

Ngay khi một “Execution Context” khởi tạo, một “Lexical Environment” cũng đồng thời được khởi tạo. 

Còn scope chain liên quan đến lexical environment như thế nào? 

Scope Chain chính là chuỗi nối của các Lexical Environment. 

Mời bạn ghé đọc [bài viết này](https://beautyoncode.com/lexical-environment-trong-javascript/) với các hình ảnh minh hoạ các khái niệm nền tảng này nhé! 


## Take note for view với Obsidian

https://obsidian.md/ là một công cụ miễn phí giúp bạn take notes một các thông minh và giúp điều hướng các note với nhau.

Nếu http://Notion.so là công cụ note cho database thì Obsidian MD là công cụ note cho view.

Các notes sẽ lưu dưới máy tính local của bạn, hoặc có thể lưu online với gói $8/month hoặc bạn sử dụng folder của google drive của mình để lưu
– Obsidian take note với ngôn ngữ document markdown
– Sử dụng help của Obsidian để làm quen với cách take note này
– Có thể edit và preview cùng một lúc
– Kết nối các note khác nhau với internal links
– Có thể nhanh chóng tạo note mới từ internal link chỉ với một phím tắt
– Có view graph kết nối các note với nhau
– Sử dụng template để dùng lại
– Sử dụng plugin như flashcard để ôn tập nội dung

Bạn có thể xem qua [video này](https://www.youtube.com/watch?v=jAPn6yqrDxQ) để xem độ cool của bạn này nhé!

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
