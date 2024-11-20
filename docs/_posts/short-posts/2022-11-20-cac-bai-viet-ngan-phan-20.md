---
title: "Các bài viết ngắn - phần 20"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/12/Short-posts-20.png)


## GraphQL là gì? Sự khác nhau giữa GraphQL và REST
GraphQL là query language dành cho API được phát triển bởi Meta. GraphQL cung cấp schema của data trong API và cho phép client quyền truy vấn chính xác những thứ họ cần.

GraphQL đứng giữa client và backend

```
GraphQL Client → GraphQL → Backend Services (Auth APIs, Core APIs, Redis)
```

GraphQL có thể truy vấn đến nhiều resources chỉ trong một query.

GraphQL cũng hỗ trợ mutation (addNote) và subscription (newNode)

**Vậy GraphQL và REST API giống và khác nhau như thế nào ?**

**Giống:**
– đều gửi HTTP request bằng một URL
– đều nhận HTTP response (JSON)

**Khác:**
– GraphQL cho phép truy vấn chính xác resources và fields mà client cần
– REST API thì data trả về quyết định bởi phía backend

**REST API**
– trung tâm là resources, được xác định trên url như GET /api/v1/users
– gọi url lấy một book GET /api/v1/books/1, gọi url lấy một author GET /authors/1 – nhiều request qua nhiều resources

**GraphQL**
– trung tâm là GraphQL Schema
– định nghĩa các type (schema)
– gửi request với resource và fields cần lấy data

Tóm lại, GraphQL sử dụng Schema định nghĩa các type, cho phép truy vấn theo nhu cầu của client (resources, fields) và giải quyết được các vấn đề của REST API như thừa data trả về, nhiều request cùng lúc khi muốn lấy data từ nhiều resources.

**Một số hạn chế của GraphQL:**
– Không có các lợi thế của REST.

Lợi thế của REST như:
– không cần một lib khác để dùng giữa request và server
– request có thể gửi đi từ curl hay web browser
– GET request dễ cache (CDNs, Proxies, Web Servers)
– Cần công cụ khác hỗ trợ cả ở client và server (Apollo, schema.graphql, codegen.yml, operation.graphql) → tốn tiền hơn → không phù hợp với CRUD APIs
– Khó cache hơn vì mặc định sử dụng POST request
– Data quyết định bởi client có thể gây các vấn đề về dữ liệu

Do đó, việc lựa chọn sử dụng GraphQL hay REST API sẽ tùy thuộc vào từng loại dự án khác nhau.

Mời bạn xem thêm ở [blog này](https://beautyoncode.com/graphql-la-gi-su-khac-nhau-giua-graphql-va-rest/ ) nhé!

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

## Sự phát triển của CSS
Sự phát triển của CSS theo hướng có thể mở rộng trong dự án

CSS là một trong ba trụ cột của website (HTML, CSS, JS). Khi nhắc đến CSS hẳn bạn sẽ nghĩ bạn này quá đơn giản đúng không ^^ Tuy nhiên, viết CSS trong dự án lớn để có thể dễ dàng mở rộng và hiệu quả là điều không hề dễ dàng.

Bài viết sau giới thiệu đến bạn về CSS và quá trình phát triển của bạn ấy:

Trước khi CSS ra đời, style được viết luôn vào code HTML. Khi CSS ra đời, tách code CSS ra riêng. Và nổi tiếng với trang CSS Garden, nơi chỉ với cùng cấu trúc html nhưng xây dựng được các thiết kế khác nhau

CSS có global namespaces, theo cascade rules và selector specificity – tức code CSS được truy cập trong toàn bộ trang web, với luật tính điểm để quyết định có ghi đè nhau không (cascade) và chọn các phần tử với selector.

Bên cạnh đó, việc đặt tên class, ghi đè với `!important`, code thừa trong dự án lớn (vì không dám xoá sợ ảnh hưởng các tính năng đang hoạt động) ngày càng phổ biến. CSS lại không có lỗi (silent error).

Tất cả những đều này làm CSS rất dễ để bắt đầu nhưng là nhanh chóng lộn xộn và khó kiểm soát.

Việc quản lý CSS ra đời với các khái niệm về “CSS Architectures” như SMASS, BEM, ITCSS, Cube CSS, SASS, LESS, …

Tiếp đó, việc phát triển của các trang web SPAs và component-driven development dẫn đến nhiều hướng tiếp cận mới với CSS như là inline styles, CSS in JS
Làm sóng đầu tiên của CSS in JS với styled-component, Emotion
Làn sóng thứ hai của CSS in JS với việc complie CSS giúp giảm thời gian chạy trên trình duyệt của người dùng. CSS biên dịch qua Atomic CSS, các thư việc như Vanilla extract, Linaria, Compiled.

Cùng lúc đó, song song với sự phát triển của CSS in JS, một hướng mới quản lý CSS với Atomic CSS ra đời với việc style các cấp thấp hơn cả blockers, objects, tập trung vào single-purpose atoms với các thư viện như ACSS, Tachyons, WindiCSS, và nổi nhất hiện nay là Tailwind.

Thật thú vị đúng không! Bạn ghé đọc thêm ở [bài này](https://frontendmastery.com/posts/the-evolution-of-scalable-css/) nhé ^^