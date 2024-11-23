---
title: "Các bài viết ngắn - phần 23"
categories:
  - Short Posts
tags:
  - short-posts
  - devops
  - css
  - learning-resources
---
![](/assets/images/2022/12/2022-12-11-cac-bai-viet-ngan-phan-23-1.webp)

## Giới thiệu Microservices
Kiến trúc Microservices cho phép xây dựng các ứng dụng có thể mở rộng.

Microservices là gì?

Kiến trúc Microservices bao gồm nhiều service tách rời nhau.
Mỗi service có nhiệm vụ riêng tách biệt nhau trong một hệ thống lớn thường xuyên được mở rộng.

Ví dụ:
```
Shopping cart -> shopping domain
Billing -> billing domain
User Profile -> user domain
Push Notification -> push domain
```
Tất cả các nhóm nhiệm vụ riêng ở trên đều có thể là một service tách rời nhau, thường gọi là domain.

Microservices giao tiếp với nhau ra sao?

Microservices giao tiếp với nhau qua giao diện (interface) ở khoảng cách gần (surface area nhỏ) giúp giảm tỉ lệ bị lỗi. Điều này làm mỗi service có thể trở thành một phần của toàn bộ hệ thống.

Microservices nói chuyện với nhau thông qua sự kết hợp của RPC (remote produce calls), Event Streaming, Message Brokers.

Các điểm mạnh của Microservices:

– Microservices mang đến sự linh hoạt cho việc mở rộng từng service độc lập nhau.
– Microservices có thể được triển khai (deploy) độc lập với nhau vì mỗi service thì nhỏ, tách biệt, và có thể deploy thường xuyên.
– Kiến trúc Microservices tốt giúp ẩn đi nhiều thông tin vì mỗi loại thông tin sẽ nằm ở các service khác nhau.
Ví dụ như một “Monolithic Database” sẽ được chia thành các thành phần khác như Shopping Card DB, Billing DB, User DB, Notification DB.

Các điểm yếu của Microservices:

– Kiến trúc Microservices phá vỡ cơ sở dữ liệu, tức sẽ không có các loại quan hệ.
– Xây dựng và vận hành Microservices sẽ tốn nhiều tiền

Vậy thì khi nào nên sử dụng Microservices?
– Xây dựng và vận hành Microservices sẽ tốn nhiều tiền, do đó nó chỉ phù hợp cho các dự án lớn (nhiều team lớn).
Khi đó, các team vận hành độc lập, mỗi domain có thể được vận hành và bảo trì độc lập bởi từng team.
Mỗi team có thể tự phát triển domain của mình nhanh chóng, tự thiết kế, phát triển, triển khai, mở rộng.

– Microservices sẽ không phù hợp với các dự án nhỏ startup vì chi phí cao.
Tuy nhiên, để phát triển theo hướng microservice trong tương lai, với startup, khuyến khích nên thiết kế mỗi tính năng trong ứng dụng tách biệt nhau càng nhiều càng tốt để dễ dàng chuyển đổi khi cần.

[Bạn xem minh họa mô hình ở video này nhé.](https://youtu.be/lTAcCNbJ7KE)

## Học về Flexbox
Flexbox ra đời giúp cho việc thiết kế layout trên trang web trở nên dễ dàng và ngắn gọn hơn rất nhiều so với thời dùng float.

Flexbox và layout mode

CSS có nhiều loại layout khác nhau, được gọi là “layout mode”.
Layout mặc định là “flow layout”, có thể hiểu các phần tử sẽ xếp theo thứ tự lần lượt nhau.

Để chuyển layout mặc định qua flex, bạn sẽ dùng “display: flex;” gán vào phần tử cha. Khi đó, CSS hiểu phần tử cha này sẽ có “flex formatting context”, và sẽ áp dụng thuật toán của flex cho các phần tử con bên trong nó.

Mỗi thuật toán của layout được thiết kế giúp giải quyết một vấn đề cụ thể.
Như “flow layout” có nghĩa là tạo tài liệu online, nó thuật toán layout cơ bản của Microsoft Word. Tiêu đề và các đoạn văn như các khối được xếp theo chiều dọc, còn chữ, các link và hình ảnh sẽ nằm bên trong các khối .

Vậy còn flexbox sẽ giúp giải quyết vấn đề gì?

Flexbox giải quyết vấn đề sắp xếp một nhóm các thành phần theo hàng (row) hay cột (column).

Đúng như tên của nó, flexbox rất linh hoạt flexibility. Nó cho phép kiểm soát và phân phối các thành phần và khoảng cách giữa chúng.

Các khái niệm chính của flexbox bao gồm:
– Các trục (axis)
– Flex direction
– Alignment
– Content với items
– Kích thước giả thuyết (hypothetical size) và kích thước tối thiểu (min width)
– Giãn và co (grow and shrink)
– Gap

[Cùng mình tìm hiểu thêm ở bài viết này nha][hoc-ve-flexbox]

## Điều gì xảy ra khi bạn enter url?
Điều gì xảy ra khi bạn gõ một đường dẫn (URL) vào trình duyệt và bấm enter?

Đầu tiên, URL là gì?
URL là Universal Resource Locator.
Ví dụ:

http://example.com/product/electric/phone

1 2 3 4

URL có 4 phần:
1. “http://” là schemeGiao thức kết nối với server là HTTP, ngoài ra giao thức khác đang phổ biến là HTTPS
2. “example.com” là domainTên miền của trang
3. “product/electric” là pathCó thể hiểu là đường dẫn, hoặc thư mục
4. “phone” là resourceCó thể hiểu là các tài nguyên hay file path và resource gộp lại sẽ giúp xác định tài nguyên cần tải cho trang

Các bước trả lời cho câu hỏi mở đề.

Bước 1: gõ URL vào trình duyệt và nhấn enter

Bước 2: tìm kiếm địa chỉ IP của server

Trình duyệt sẽ cần xác định server example.com.

DNS sẽ giúp tìm và xác định địa chỉ IP của server dựa trên tên miền. DNS là Domain Name System

Trình duyệt đầu tiên sẽ tìm kiếm trong DNS’s cache (lưu trong máy tính) xem đã có IP server này chưa, nếu có rồi thì sẽ sử dụng luôn, còn chưa có sẽ gửi một yêu cầu đi đến DNS Resource.

Bước 3: thiết lập kết nối TCP với server
Nếu là giao thức HTTPS, thiết lập SSL/TLS cũng xảy ra ở bước này

Bước 4: trình duyệt gửi HTTP request đến server dựa trên kết nối TCP đã thiết lập ở bước 3

Bước 5: Server gửi trả về kết quả (response)

Bước 6: Trình duyệt nhận kết quả và render nội dung HTML

Nếu có thêm các nội dung khác cần được load như javascript, images, … trình duyệt sẽ thực hiện các bước tương tự từ 2.

[Bạn có thể xem thêm bản tiếng anh ở video này](https://youtu.be/AlkDbnbv7dk)

## Bộ sưu tập components
Xu hướng thiết kế web hiện nay là components driven development, lấy các thành phần (component) trong trang web làm cơ sở để phát triển.
Các thư viện như React giúp phân tách tất cả các thành phần trong trang web thành các component.
Do đó việc hiểu về các component phổ biến được sử dụng là vô cùng cần thiết với web developer.

Bạn có đang tìm một bộ sưu tập các components thông dụng của trang web?
Bạn không biết cách đặt tên các components như thế nào?

Mình muốn giới thiệu một bộ sưu tập các thành phần (components) không thể cool hơn của web.dev (Google team)
Mỗi component sẽ gồm:
– demo
– code HTML/CSS/JS
– bài blog hướng dẫn xây dựng component
– video hướng dẫn
– source code ở github

Các components như:
– Breadcumbs
– Buttons
– Carousel
– Dialog
– Loading Bar
– Multi-select
– Setting
– Sidenav
– Split buttons
– Switch
– Tabs
– Toast
– …

Quá tuyệt vời đúng không! Cám ơn team Google nhiều <3

Điều tuyệt vời hơn nữa là các components này cross browsers luôn ấy ơi!

Và bộ này đang được cập nhật thường xuyên nhé!
[Lưu ngay để dùng khi cần nha.](https://web.dev/patterns/components/)


[hoc-ve-flexbox]: {{ "" | relative_url }}{% post_url css/2022-12-09-hoc-ve-flexbox %}