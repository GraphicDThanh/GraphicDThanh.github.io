---
title: "Các bài viết ngắn - phần 30"
categories:
  - Short Posts
tags:
  - short-post
---
![](/assets/images/2022/03/2022-03-26-cac-bai-viet-ngan-phan-30-1.webp)

## 9 lỗi người mới học React thường mắc phải
### Lỗi 1: Phép so sánh với 0

Dòng code dưới sẽ hiển thị trên UI số 0 bởi 0 là giá trị valid trong JSX
```js
<div>{items.length && <ShoppingList items=items>}</div>
<div>{items.length && <ShoppingList items=items>}</div>
```

Sửa lỗi:
– Cách 1: `items.length > 0`

– Cách 2: `items.length ? <ShoppingList items=items> : null`

### Lỗi 2: Thay đổi giá trị của state

Đoạn code sau không chạy đúng bởi giá trị state không được tự thay đổi:
```js
items.push(value);
setItems(items);
```
Sửa lỗi:
```js
const nextItems = [...items, value]
setItems(nextItems)
```

### Lỗi 3: Không tạo key khi render phần tử trong danh sách

Sửa lỗi: thêm key có giá trị duy nhất như UUID

### Lỗi 4: Thiếu khoảng trắng (hoặc hiểu nhầm cách dòng trong code là khoảng trắng)

Sửa lỗi: thêm khoảng trắng với {‘ ‘}

### Lỗi 5: Truy cập vào giá trị state sau khi thay đổi chúng

Đoạn code sau hiện ra console là items list chưa thay đổi:

```js
setItems([…items, value]);
console.log(items);
```

Sửa lỗi:
```js
const nextItems = [...items, value]
setItems(nextItems)
console.log(nextItems)
```
### Lỗi 6: Trả về nhiều thành phần trong component

Sửa lỗi: sử dụng React.Fragment hay <></>

### Lỗi 7: Chuyển component từ uncontrolled sang controlled

Đoạn code sau sẽ báo lỗi khi thay đổi email:
```js
const [email, setEmail] = React.useState();
<input
value={email}
onChange={e => setEmail(e.target.value)}
/>
111
Sửa lỗi: đảm bảo giá trị ban đầu là empty string thay vì undefined để tránh React hiểu component là uncontrolled.

```js
const [email, setEmail] = React.useState(‘’);
```
### Lỗi 8: Thiếu dấu {} cho code style

Code đúng:
```
<button style={{ color: "red", fontSize: "1em" }}></button>
```
### Lỗi 9: Async effect function

useEffect hook không thể xử lý nếu hàm bên trong trả về promise nên cần viết hàm async riêng biệt và gọi bên trong nó.

Code đúng:
```js
React.useEffect(() => {
  async function runEffect() {
    const res = await fetch(“/api/v1/items”);
    const json = await res.json();
    setItems(json);
  }
  runEffect();
});
```
Bài viết tóm tắt từ blog bên dưới bạn ghé đọc ủng hộ tác giả nha

Bản tóm tắt tiếng Việt với code minh họa dễ nhìn mình note lại ở blog dưới nha

https://beautyoncode.com/9-loi-nguoi-moi-hoc-react-thuong-gap/

## Câu chuyện nữ nhân sự trong ngành CNTT
Nhân ngày 8/3, Viblo đã chia sẻ đến bạn đọc một số câu chuyện về “Women-in-tech”.
“Women-in-tech” là một cụm từ phổ biến chỉ nữ giới đang làm việc trong lĩnh vực Công Nghệ.

Khách mời gồm có 3 chị:

– Đặng Trung Anh (Employer Branding & Sourcing Specialist tại CMC Global)

– Đặng Thị Duyên (Trường phòng Ươm mầm tài năng trẻ tại công ty Suns Asterisk VN)

– Nguyễn Diễm Thanh (Web Developer tại AgilityIO, tác giả blog beautyoncode.com) (là mình đó ^^)


Bài viết gửi đến một số thông tin:
– Được đào tạo bài bản sẽ là nền tảng để làm trong ngành
– Các con số mô tả tỉ lệ nữ làm việc trong ngành, và nhiều chị em cũng giữ những vị trí khó nhằn như PM, Tech Lead
– Một số phụ nữ nổi tiếng trong ngành như GS Nguyễn Thục Quyên, He Yi, Margaret Heafield Hamilton, Huyền Chip
– Bất bình đẳng – chỉ là ba từ ghép lại mà thôi. Mình đã chia sẻ:
“Để vượt qua rào cản, cách đơn giản và tốt nhất là không để rào cản ảnh hướng đến mình. Các rào cản này giống như lực ma sát vậy, bạn cần làm những điều mà có thể chiến thắng những lực ma sát này. Nếu bạn có thể xem tất cả đều không phải là rào cản, thì là bạn không có lực ma sát nào cả.”
– Là phụ nữ, hãy bảo vệ chính mình
– Học tập là kim chỉ nam để thành công
– Bạn không bao giờ đi một mình (cô đơn thì ghé blog mình chơi nha ^^)
– Hãy xây dựng cái gì đó cho mình, ví dụ như là tham gia “Careerly_ITSharathon” đi này

Lời cuối mình gửi tặng mọi người:
—
Bốn điểm quan trọng với mình:
1. yêu thích công việc
2. sống một cuộc sống đơn giản sẽ đỡ áp lực
3. làm những công việc nho nhỏ hàng ngày
4. chăm sóc bản thân và người xung quanh.
—
Chúc chị em 8/3 vui vẻ!

Bài viết của Viblo “Women-in-tech: Inspiring Success Stories | Những câu chuyện truyền cảm hứng thành công“

## Python iterators và iterables
Trước khi tìm hiểu về nội dung này, bạn nên có kiến thức cơ bản về Python, hiểu rõ các khái niệm như loop, iteration, for, while, OOP, kế thừa, các hàm đặt biệt như __iter__, và lập trình bất đồng bộ asynchronous.

Bài viết sau giới thiệu đến bạn:
* Tạo iterators sử dụng iterator protocol trong Python
* Hiểu sự khác nhau giữa iterators và iterables
* Làm việc với iterators và iterables trong code Python
* Sử dụng hàm generator và yield để tạo generator iterators
* Xây dựng iterables của riêng bạn sử dụng các kỹ thuật khác nhau, như iterable protocol
* Sử dụng mô-đun asyncio và các từ khoá await, async để tạo asynchronous iterators.

Một số kiến thức cơ bản:

### Iteration là gì?
Iteration là sự lặp đi lặp lại, có 2 loại iteration thường gặp:
– indefinite iteration: lặp với số lần không xác định (while)
– definite iteration: lặp với số lần nhất định (for)

### Iterator là gì?
Iterator là một object cho phép bạn lặp qua nó, trả ra giá trị cho mỗi lần đó, được thiết kế sử dụng iterator pattern.

Một iterator sẽ có 2 hành động chính:
1. Trả về phần tử cho mỗi lần yêu cầu
2. Theo dõi phần hiện tại và những phần tử đã từng đi qua

Một object là một iterator khi nó có 2 phương thức đặc biệt __iter__() và __next__(), gọi là iterator protocol

### Khi nào sử dụng iterator?
Khi bạn muốn cho phép lặp qua một lượng dữ liệu hay một cấu trúc của các loại dữ liệu.
Iterator sẽ cực hữu ích với các loại data lớn và không biết số lần sẽ lặp qua.

Các loại iterator đã được python hỗ trợ như comprehension, iterable unpacking.

Các kiến thức của những phần nâng cao hơn bạn ghé đọc ở bài viết này nhé.
https://realpython.com/python-iterators-iterables/

## Giới thiệu hơn 50 dịch vụ AWS cung cấp
AWS được ra mắt vào năm 2006 với 3 dịch vụ chính: Storage, Compute, Messaging. Hiện nay AWS cung cấp hơn 250 dịch vụ, khiến việc chọn dịch vụ AWS để sử dụng như là đi mua sắm vậy.

Các dịch vụ AWS mà bạn có thể chưa từng nghe qua
1. ROBOTMAKER: giúp mô phỏng và kiểm tra khi bạn tạo robot
2. IOT CORE: giúp thu thập data khi robot được sử dụng, cập nhật phần mềm và quản lý từ xa
3. GROUND STATION: kết nối dữ liệu từ vệ tinh ngoài trái đất
4. BRACKET: giúp tương tác với máy tính lượng tử

Các dịch vụ giúp giải quyết các vấn đề thực tế hơn:

COMPUTE (Máy chủ)
5. ELASTIC COMPUTE CLOUD (EC2): giúp tạo máy chủ ảo trên cloud (chọn OS, memory, computing power)
6. LOAD BALANCING (ELB): giúp tự động phân phối truy cập đến nhiều máy chủ
7. CLOUD WATCH: giúp theo dõi các số liệu, log của các loại dịch vụ
8. AUTO SCALING: giúp tự động tăng, giảm số lượng máy chủ một cách tự động theo các cài đặt như lượng traffic, CPU, … Các số liệu có thể lấy từ cloud watch.
9. ELASTIC BEANSTALK: là một PaaS, cung cấp các cài đặt có sẵn (Node.js, Ruby on Rails), … cho EC2 kèm tự động scale.
10. LIGHTSAIL: giúp deploy một ứng dụng nhanh chóng (WordPress, LAMP, Node.js, Django, …). Bạn sẽ không cần quan tâm đến hạ tầng bên dưới, và ít quản lý cấu hình. Bạn sẽ trả tiền theo giây máy chủ sử dụng (lưu ý là máy chủ ở đây sẽ luôn được chạy).
11. LAMBDA: là FaaS hay serverless computing, giúp bạn tải code lên và chọn các sự kiện để run code đó. Cách này giúp bạn tiết kiệm hơn bởi chỉ trả tiền cho các yêu cầu thực hiện chương trình và thời gian tính toán được sử dụng.
12. SERVERLESS REPO: giúp để tìm các hàm dựng sẵn giúp bạn nhanh chóng dựng chương trình.
13. OUTPOSTS: nếu bạn là công ty có sẵn hạ tầng máy chủ, thì OutPosts giúp bạn chạy aws api trên hạ tầng có sẵn này
14. SNOW: giúp bạn tương tác với AWS từ xa (như bạn là nhà khoa học làm việc ở Bắc cực chẳng hạn)

Docker container trở nên vô cùng phổ biến cho phép ứng dụng có thể nhanh chóng chạy trên nhiều clouds khác nhau (AWS, GCP, Azure)

15. CONTAINER REGISTRY: cho phép bạn tải lên docker image
16. CONTAINER SERVICE: lấy image từ container registry và chạy các container lên. ECS là api giúp start, stop và phân phối các máy EC2 cho các container. Đồng thời cho phép kết nối với những dịch vụ khác như Load Balancer
17. KUBENETES: giúp chạy công cụ Kubenetes để có nhiều quyền kiểm soát hơn trong việc app được scale như thế nào
18. FARGATE: giúp tự động hóa container, làm nó giống serverless function, có thể tự động phân bổ tài nguyên của EC2
19. APP RUNNER: giúp deploy các container được dựng sẵn lên AWS (đã bao gồm tự động scale)

Chạy một ứng dụng chỉ là một nửa của câu chuyện, nửa còn lại là lưu trữ dữ liệu lên cloud.

FILE STORAGE (Lưu trữ file)

20. SIMPLE STORAGE SERVICE (S3): giúp lưu trữ các loại file hay object (image, video, document, …).
21. GLACIER: (tương tự S3) khi không truy cập dữ liệu thường xuyên, giúp giảm chi phí (thời gian trả file về lâu hơn)
22. BLOCK STORAGE: (tương tự S3) khi muốn truy cập dữ liệu với tốc độ cực nhanh và có thể xử lý nhiều lưu lượng (tự cấu hình bởi lập trình viên)
23. ELASTIC FILE SYSTEM: hiệu suất cao, được quản lý đầy đủ (giá cao hơn)

DATABASE (Lưu trữ dữ liệu có cấu trúc)

24. SIMPLEDB: database đơn giản no sql phục vụ mục đích chung chung
25. DYNAMO DB: (document database) dễ dàng scale theo chiều rộng (scales, fast, cheap), không cho phép dữ liệu quan hệ, giới hạn số queries
26. DOCUMENT DB: (document database) nếu bạn quen với MongoDB thì db này tương tự thế
27. ELASTIC SEARCH: giúp bạn xây dựng full-text search engine
28. RDS: (relational database) hỗ trợ nhiều loại database sql như PostgresSQL, MySQL, MariaDB, ORACLE, Microsoft SQL Server, đồng thời hỗ trợ sao lưu (backup), chắp vá (patching) và mở rộng (scale)
29. AURORA: (relational database) độc quyền của aws, tích hợp với các loại PostgresSQL, MySQL và có thể hoạt động tối ưu hơn (5x MySQL) với giá cả tốt hơn. Aurora còn cung cấp lựa chọn serverless giúp dễ dàng scale hơn và bạn chỉ trả phí khi db được sử dụng.
30. NEPTUNE: (graph database) giúp tối ưu hóa các data kết nối như social graph, recommendation engine
31. ELASTIC SCALE: giúp quản lý cache đầy đủ của redis, và in-memory database (tốc độ đọc cực nhanh)
32. TIMESTREAM: (time series database) (ví dụ như giá cổ phiếu) với các hàm dựng sẵn cho time-based queries và các tính năng mở rộng để phân tích
33. QUANTUM LEDGER: cho phép xây dựng các tệp data không thay đổi của các giao dịch crypto (tương tự công nghệ block chain)

ANALYTICS (Phân tích dữ liệu)

34. REDSHIFT: (data warehouse) giúp lưu trữ dữ liệu cần phân tích. Dữ liệu ở warehouse có cấu trúc nên có thể query được.
35. LAKE FORMATION: nơi giúp lưu trữ lượng lớn các dữ liệu phi cấu trúc (dump raw data & file)
36. KINESIS: phân tích data realtime. Kinesis giúp lấy dữ liệu realtime từ hạ tầng của bạn sau đó dựng lên các công cụ business khác.
37. MAP REDUCE: giúp bạn chạy Apache Spark (streaming processing framework). Là một dịch vụ cho phép hoạt động trên tập dữ liệu lớn hiệu quả với thuật toán phân phối đồng thời (parallel distributed algorithm)(Kafka, Flume, HDFS/S3, Kinesis, Twitter) —> Spark Streaming -> (HDFS, Databases, Dashboards)
38. MSK: giúp bắt đầu sử dụng Apache kafka (là open source có thể sử dụng thay thế kinesis cho việc streaming data)
39. GLUE: serverless, giúp dễ dàng trích xuất, chuyển đổi và load dữ liệu một cách tự động. Có thể kết nối với aurora, Lambda, redshift, s3. Glue studio giúp bạn tạo các jobs mà không cần viết source code.

MACHINE LEARNING (Máy học)
40. DATA EXCHANGE: giúp mua data từ bên thứ ba
41. SAGEMARKER: kết nối data và bắt đầu xây dựng machine learning model với Tensorflow hay Pitorch, giúp chạy trên nhiều lớp giúp machine learning dễ dàng hơn, và cung cấp jupiter notebook để quản lý và kết nối với GPU instance để train machine learning model rồi deploy lên đâu đó để dùng
42. REKOGNITION: model giúp phân tích hình ảnh, đối tượng
43. LEX: model giúp trong hội thoại
44. DEEP RACER: bạn có thể chơi và học machine learning với một con robot (xe) và deep racer dùng để viết code cho machine learning

DEVELOPER ESSENTIALS (Các dịch vụ dev cần biết)
45. IAM: Identity & Access Management – bảo mật, giúp tạo các role, quản lý quyền truy cập trên tài khoản ăn
46. Cognito: dịch vụ giúp người dùng log in vào ứng dụng với nhiều phương thức xác thực và quản lý các phiên truy cập của người dùng
47. SIMPLE NOTIFICATION SERVICE: SNS là công cụ giúp gửi thông báo đến người dùng
48. SIMPLE EMAIL SERVICE: SES là công cụ giúp gửi mail
49. CLOUD FORMATION: giúp tạo các templates dựa trên hạ tầng của bạn bằng yml, json cho phép bạn kích hoạt nhiều dịch vụ một cách đơn giản
50. AMPLIFY: cung cấp SDK cho phép kết nối và tương tác với các dịch vụ từ app frontend (web, iOS, android)
51. BUDGETS: tất cả các dịch vụ đều tốn phí, nên hãy sử dụng budgets để đảm bảo bạn không trả quá mức cho phép.

Ref: ![](https://youtu.be/JIbIYCM48to)


## Giới thiệu dịch vụ EC2 của AWS
EC2 là viết tắt của Elastic Compute Cloud, là một dịch vụ AWS thuộc loại Infrastructure as a Service (IaaS)

Hiện nay, EC2 cung cấp 4 nhóm dịch vụ chính bao gồm:
1. Cho thuê (tạo) máy chủ ảo (EC2 instance)
2. Lưu trữ dữ liệu trên máy chủ ảo (EBS – Elastic Block Store, EFS – Elastic File System)
3. Phân phối tải trên nhiều máy chủ ảo (ELB – Elastic Load Balancing)
4. Tự động tăng hay giảm (scale) số lượng máy chủ ảo (ASG – Auto Scaling Group)

Khi thuê một máy chủ ảo, bạn có thể tạo máy với cấu hình mong muốn:
– OS (operating system): hệ điều hành như Linux, MacOS, Window
– CPU (central processing unit): bộ xử lý trung tâm hay bộ vi xử lý (các loại chip như core i7, m1)
– RAM (random access memory): bộ nhớ tạm giúp CPU truy xuất lấy thông tin nhanh
– Các loại bộ nhớ kèm theo như:
– bộ nhớ bên ngoài được gắn vào như EBS, EFS (các network drive)
– bộ nhớ bên trong như EC2 instance store
– Card mạng
– Tường lửa (security group)
– Bootstrap script (EC2 user data) giúp boot máy tính khi lần đầu tạo

### Lưu trữ dữ liệu trên máy chủ ảo
EC2 Instance store là bộ nhớ bên trong máy EC2
- EBS – Elastic Block Store là một network drive được gắn vào máy EC2 instance của bạn khi chạy
- EFS – Elastic File System có thể gắn vào nhiều máy chủ EC2 ở nhiều AZ khác nhau.

### Phân phối tải trên nhiều máy chủ ảo
AWS cung cấp 3 loại Load Balancers là: Clasic Load Balancer (đã cũ), Application Load Balancer, Network Load Balancer, Gateway Load Balancer
Lợi ích khi sử dụng load balancer:
– giúp phân phối tải (traffic) đến nhiều máy chủ
– ứng dụng chỉ có một địa chỉ DNS
– Xử lý lỗi và thực hiện kiểm tra sức khỏa (health check) các máy chủ
– Cung cấp dịch vụ SSL (HTTPS)
– Có thể gắn người dùng với cookie
– Tăng tính khả dụng (high availability) qua nhiều AZ
– Tách các loại traffic khác nhau để xử lý

### Tự động scale số lượng máy chủ
Thực tế là không thể biết trước số tải (traffic) sẽ truy cập đến ứng dụng của bạn. ASG – Auto Scaling Group giúp bạn:
– tự động tăng số lượng máy chủ khi tải tăng
– tự động giảm số lượng máy chủ khi tải giảm
– đảm bảo số máy chủ tối đa và tối thiểu nhất định
– tự động tạo máy chủ mới với cấu hình định sẵn (launch template)
– tự động tạo lại nếu máy chủ bị tắt khi unhealthy

Có thể kích hoạt ASG từ thông số của thông báo từ CloudWatch về chỉ số như Average CPU, hay tự tạo chỉ số.

Bạn ghé bài viết sau trên blog để đọc thêm nhé.

https://beautyoncode.com/gioi-thieu-dich-vu-ec2-cua-aws/