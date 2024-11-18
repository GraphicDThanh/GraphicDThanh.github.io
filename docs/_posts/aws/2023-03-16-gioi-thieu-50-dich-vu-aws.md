---
title: "Giới thiệu 50 dịch vụ AWS"
excerpt_separator: <!--more-->
categories:
  - AWS
tags:
  - aws
---

![](/assets/images/2023/03/2023-03-16-gioi-thieu-50-dich-vu-aws.webp)


AWS được ra mắt vào năm 2006 với 3 dịch vụ chính: Storage, Compute, Messaging

Hiện nay AWS cung cấp hơn 250 dịch vụ, khiến việc chọn dịch vụ AWS để sử dụng như là đi mua sắm trong siêu thị vậy.

## Các dịch vụ AWS có thể bạn chưa từng biết

1. [ROBOTMAKER](https://aws.amazon.com/robomaker/): giúp mô phỏng và kiểm tra khi làm robot

2. [IOT CORE](https://aws.amazon.com/iot-core/): giúp thu thập data khi robot được sử dụng, cập nhật phần mềm và quản lý từ xa

3. [GROUND STATION](https://aws.amazon.com/ground-station/): kết nối dữ liệu từ vệ tinh ngoài trái đất

4. [BRAKET](https://aws.amazon.com/braket/): giúp tương tác với máy tính lượng tử

## Các dịch vụ AWS giải quyết các vấn đề thực tế

### COMPUTE (Máy chủ)

5. [ELASTIC COMPUTE CLOUD (EC2)](https://aws.amazon.com/ec2/): giúp tạo máy chủ ảo trên cloud (chọn OS, memory, computing power)

6. [LOAD BALANCING (ELB)](https://aws.amazon.com/elasticloadbalancing): giúp tự động phân phối truy cập đến nhiều máy chủ

7. [CLOUD WATCH](https://aws.amazon.com/cloudwatch): giúp theo dõi các số liệu, log của các loại dịch vụ

8. [AUTO SCALING](https://aws.amazon.com/autoscaling/): giúp tự động tăng, giảm số lượng máy chủ một cách tự động theo các cài đặt như lượng traffic, CPU, … Các số liệu có thể lấy từ cloud watch.

9. [ELASTIC BEANSTALK](https://aws.amazon.com/elasticbeanstalk): là một PaaS, cung cấp các cài đặt có sẵn (Node.js, Ruby on Rails), … cho EC2 kèm tự động scale.

10. [LIGHTSAIL](https://aws.amazon.com/lightsail/): giúp deploy một ứng dụng nhanh chóng (WordPress, LAMP, Node.js, Django, …). Bạn sẽ không cần quan tâm đến hạ tầng bên dưới, và ít quản lý cấu hình. Bạn sẽ trả tiền theo giây máy chủ sử dụng (lưu ý là máy chủ ở đây sẽ luôn được chạy).

11. [LAMBDA](https://aws.amazon.com/lambda): là FaaS hay serverless computing, giúp bạn tải code lên và chọn các sự kiện để run code đó. Cách này giúp bạn tiết kiệm hơn bởi chỉ trả tiền cho các yêu cầu thực hiện chương trình và thời gian tính toán được sử dụng.

12. [SERVERLESS REPO](https://aws.amazon.com/serverless/serverlessrepo): giúp để tìm các hàm dựng sẵn giúp bạn nhanh chóng dựng chương trình.

13. [OUTPOSTS](https://aws.amazon.com/outposts): nếu bạn là công ty có sẵn hạ tầng máy chủ, thì OutPosts giúp bạn chạy aws api trên hạ tầng có sẵn này

14. [SNOW](https://aws.amazon.com/snowball/): giúp bạn tương tác với AWS từ xa (như bạn là nhà khoa học làm việc ở Bắc cực chẳng hạn)

Docker container trở nên vô cùng phổ biến cho phép ứng dụng có thể nhanh chóng chạy trên nhiều clouds khác nhau (AWS, GCP, Azure)

15. [CONTAINER REGISTRY](https://aws.amazon.com/ecr): cho phép bạn tải lên docker image

16. [CONTAINER SERVICE](https://aws.amazon.com/ecs): lấy image từ container registry và chạy các container lên. ECS là api giúp start, stop và phân phối các máy EC2 cho các container. Đồng thời cho phép kết nối với những dịch vụ khác như Load Balancer

17. [KUBERNETES](https://aws.amazon.com/eks/): giúp chạy công cụ Kubernetes để có nhiều quyền kiểm soát hơn trong việc app được scale như thế nào

18. [FARGATE](https://aws.amazon.com/fargate): giúp tự động hóa container, làm nó giống serverless function, có thể tự động phân bổ tài nguyên của EC2

19. [APP RUNNER](https://aws.amazon.com/apprunner): giúp deploy các container được dựng sẵn lên AWS (đã bao gồm tự động scale)

Chạy một ứng dụng chỉ là một nửa của câu chuyện, nửa còn lại là lưu trữ dữ liệu lên cloud.

### FILE STORAGE (Lưu trữ file)

20. [SIMPLE STORAGE SERVICE](https://aws.amazon.com/s3/) (S3): giúp lưu trữ các loại file hay object (image, video, document, …).

21. [GLACIER](https://aws.amazon.com/s3/storage-classes/glacier): (tương tự S3) khi không truy cập dữ liệu thường xuyên, giúp giảm chi phí (thời gian trả file về lâu hơn)

22. [BLOCK STORE](https://aws.amazon.com/ebs/): (tương tự S3) khi muốn truy cập dữ liệu với tốc độ cực nhanh và có thể xử lý nhiều lưu lượng (tự cấu hình bởi lập trình viên)

23. [ELASTIC FILE SYSTEM](https://aws.amazon.com/efs) (EFS): hiệu suất cao, được quản lý đầy đủ (giá cao hơn)

### DATABASE (Lưu trữ dữ liệu có cấu trúc)

Bên cạnh việc quản lý file, lập trình viên còn cần lưu trữ các loại data có cấu trúc của người dùng.

24. [SIMPLEDB](https://aws.amazon.com/simpledb/): database đơn giản no sql phục vụ mục đích chung chung

25. [DYNAMO DB](https://aws.amazon.com/dynamodb): (document database) dễ dàng scale theo chiều rộng (scales, fast, cheap), không cho phép dữ liệu quan hệ, giới hạn số queries

26. [DOCUMENT DB](https://aws.amazon.com/documentdb): (document database) nếu bạn quen với MongoDB thì db này tương tự thế

27. [ELASTIC SEARCH](https://aws.amazon.com/opensearch-service/): giúp bạn xây dựng full-text search engine

28. [RDS](https://aws.amazon.com/rds): (relational database) hỗ trợ nhiều loại database sql như PostgresSQL, MySQL, MariaDB, ORACLE, Microsoft SQL Server, đồng thời hỗ trợ sao lưu (backup), chắp vá (patching) và mở rộng (scale)

29. [AURORA](https://aws.amazon.com/rds/aurora): (relational database) độc quyền của aws, tích hợp với các loại PostgresSQL, MySQL và có thể hoạt động tối ưu hơn (5x MySQL) với giá cả tốt hơn. Aurora còn cung cấp lựa chọn serverless giúp dễ dàng scale hơn và bạn chỉ trả phí khi db được sử dụng.

30. [NEPTUNE](https://aws.amazon.com/neptune): (graph database) giúp tối ưu hóa các data kết nối như social graph, recommendation engine

31. [ELASTICACHE](https://docs.aws.amazon.com/elasticache/): giúp quản lý cache như redis, memcached  với tốc độ đọc cực nhanh

32. [TIMESTREAM](https://aws.amazon.com/timestream): (time series database) (ví dụ như giá cổ phiếu) với các hàm dựng sẵn cho time-based queries và các tính năng mở rộng để phân tích

33. [QUANTUM LEDGER](https://aws.amazon.com/qldb): cho phép xây dựng các tệp data không thay đổi của các giao dịch crypto (tương tự công nghệ block chain)

### ANALYTICS (Phân tích dữ liệu)

34. [REDSHIFT](https://aws.amazon.com/redshift): (data warehouse) giúp lưu trữ dữ liệu cần phân tích. Dữ liệu ở warehouse có cấu trúc nên có thể query được.

35. [LAKE FORMATION](https://aws.amazon.com/lake-formation/): nơi giúp lưu trữ lượng lớn các dữ liệu phi cấu trúc (dump raw data & file)

36. [KINESIS](https://aws.amazon.com/kinesis/): phân tích data realtime. Kinesis giúp lấy dữ liệu realtime từ hạ tầng của bạn sau đó dựng lên các công cụ business khác.

37. [MAP REDUCE](https://aws.amazon.com/emr): giúp bạn chạy Apache Spark (streaming processing framework). Là một dịch vụ cho phép hoạt động trên tập dữ liệu lớn hiệu quả với thuật toán phân phối đồng thời (parallel distributed algorithm)

      (Kafka, Flume, HDFS/S3, Kinesis, Twitter) -> Spark Streaming -> (HDFS, Databases, Dashboards)

38. [MSK](https://aws.amazon.com/msk/): giúp bắt đầu sử dụng Apache kafka (là open source có thể sử dụng thay thế kinesis cho việc streaming data)

39. [GLUE](https://aws.amazon.com/glue): serverless, giúp dễ dàng trích xuất, chuyển đổi và load dữ liệu một cách tự động. Có thể kết nối với aurora, Lambda, redshift, s3. Glue studio giúp bạn tạo các jobs mà không cần viết source code.

### MACHINE LEARNING (Máy học)

40. [DATA EXCHANGE](https://aws.amazon.com/data-exchange): giúp mua data từ bên thứ ba

41. [SAGEMARKER](https://aws.amazon.com/sagemaker/): kết nối data và bắt đầu xây dựng machine learning model với Tensorflow hay Pitorch, giúp chạy trên nhiều lớp giúp machine learning dễ dàng hơn, và cung cấp jupiter notebook để quản lý và kết nối với GPU instance để train machine learning model rồi deploy lên đâu đó để dùng

42. [REKOGNITION](https://aws.amazon.com/rekognition/): model giúp phân tích hình ảnh, đối tượng

43. [LEX](https://aws.amazon.com/lex/): giúp xây dụng trong hội thoại và text chatbots

44. [DEEP RACER](https://aws.amazon.com/deepracer): bạn có thể chơi và học machine learning với một con robot (xe) và deep racer dùng để viết code cho machine learning

### DEVELOPER ESSENTIALS (Các dịch vụ lập trình viên cần biết)

45. [IAM](https://aws.amazon.com/iam/): Identity & Access Management – bảo mật, giúp tạo các role, quản lý quyền truy cập trên tài khoản ăn

46. [Cognito](https://aws.amazon.com/cognito/): dịch vụ giúp người dùng log in vào ứng dụng với nhiều phương thức xác thực và quản lý các phiên truy cập của người dùng

47. [SIMPLE NOTIFICATION SERVICE](https://aws.amazon.com/sns/): SNS là công cụ giúp gửi thông báo đến người dùng

48. [SIMPLE EMAIL SERVICE](https://aws.amazon.com/ses/): SES là công cụ giúp gửi mail

49. [CLOUD FORMATION](https://aws.amazon.com/cloudformation/): giúp tạo các templates dựa trên hạ tầng của bạn bằng yml, json cho phép bạn kích hoạt nhiều dịch vụ một cách đơn giản

50. [AMPLIFY](https://aws.amazon.com/amplify/): cung cấp SDK cho phép kết nối và tương tác với các dịch vụ từ app frontend (web, iOS, android)

51. [BUDGETS](https://aws.amazon.com/aws-cost-management/aws-budgets/): tất cả các dịch vụ đều tốn phí, nên hãy sử dụng budgets để đảm bảo bạn không trả quá mức cho phép.
---
