---
title: "Các bài viết ngắn về Backend"
tag: 
  - backend
  - database
  - api
  - python
  - sql
  - redis
  - GraphQL
  - REST
---

Các bài viết ngắn về "Backend"
- Databases intro course
- Tài liệu học SQL
- Redis for beginner
- GraphQL là gì ? Sự khác nhau giữa GraphQL và REST

## Databases intro course
Dành hơn tiếng đồng hồ để học cơ bản về Database lấy certificate làm đẹp profile 😎 là rất đáng phải không ?

Giới thiệu đến bạn khóa học **“Programming Foundations: Databases**”, được miễn phí trên Linkedin Learning

Bạn sẽ được làm quen với:

– Database là gì, Relational Database là gì?

– Database giúp bạn quản lý dữ liệu thực tế như thế nào?

– Cách thiết kế một database dựa trên những dữ liệu thực tế

– Các kiến thức cơ bản về bảng(table), cột dữ liệu(columns/fields), hàng dữ liệu(rows/records), khóa chính(primary key), khóa phụ(foreign keys)

– Các loại data types

– Các mối quan hệ(relationships) giữa các bảng gồm có các kiểu one-to-many, many-to-many, one-to-one

– Cách tối ưu hóa trong thiết kế database

– Các truy xuất dữ liệu(tìm kiếm, lọc, tổng hợp, chỉnh sửa …) trong database với SQL queries

[Link khóa học](https://linkedin.com/learning/programming-foundations-databases-2).

Nếu khóa này trở lại trả phí thì bạn có thể học ở series [này](https://www.youtube.com/playlist?list=PLLGlmW7jT-nTr1ory9o2MgsOmmx2w8FB3) về database nhé.

## Tài liệu học SQL

Bạn có biết gần 53% lập trình viên chuyên nghiệp xem SQL là ngôn ngữ phổ biến nhất 🙀, chỉ đứng sau HTML, CSS. (theo kết quả nghiên cứu trên 700,000 lập trình viên của StackOverflow 2022)

Vậy SQL là gì? 🤔

✅ SQL – viết tắt của Structured Query Language, là ngôn ngữ truy vấn dữ liệu có cấu trúc. Nó gồm các câu lệnh dùng để tương tác với cơ sở dữ liệu quan hệ.

✅ Tất cả các hệ thống quản lý cơ sở dữ liệu quan hệ(RDMS) như MySQL, Oracle, Postgres, MS Access, SQL Server đều sử dụng SQL làm ngôn ngữ dữ liệu chuẩn.

✅ SQL sẽ giúp quản lý hiệu quả và truy vấn thông tin nhanh hơn, giúp bảo trì, bảo mật thông tin dễ dàng hơn.

Nếu bạn làm việc trong lĩnh vực công nghệ, hẳn sẽ có lúc bạn cần đến SQL, vì nó cần thiết cho:

👉 Software Developer

👉 Business Analyst

👉 Database Administrator

  👉 QA Tester

👉 Project/Product Manager

Vì vậy, có kỹ năng SQL sẽ giúp bạn làm tốt hơn công việc hiện tại của mình, cũng như dễ xin việc vào các vị trí yêu cầu kỹ năng này 💪

Hẳn là bạn cũng nóng lòng muốn học SQL rồi phải không ?

🤩 Mình sẽ giới thiệu đến mọi người Top Resources for SQL Bootcamp, bao gồm các series, khóa học, bài thực hành, … và các đánh giá của bạn Omer(là chủ notion [page này](https://www.notion.so/Top-Resources-for-SQL-Bootcamp-38a39207d09a4dc19492ca8e8c64e0ae))

Chúc các bạn mau sở hữu kỹ năng này bỏ vào túi kỹ năng của mình dể nâng cao giá trị bản thân nhé 🥰

## Redis for beginner

🤩 Redis basic ☕️

Redis là một cơ sở dữ liệu trong bộ nhớ (in memory database) 💿, dữ liệu được lưu trữ theo dạng key-value 🔑 🪟 tức là từ khóa và giá trị của nó.

👩‍🍳 Redis thường sử dụng như là một cơ sở dữ liệu caching📜, có tốc độ truy cập rất nhanh 💨.

💻 Để làm quen với Redis, cài đặt nhanh trên Mac với “brew install redis”, sau đó chạy server với  “redis-server”.

Sau khi server được khởi chạy, bạn có thể bắt đầu làm quen với các câu lệnh cơ bản trong Redis bằng cách sử dụng CLI, mở một cửa sổ mới và gõ lệnh “redis-cli”

🧐 Câu lệnh SET, GET, EXISTS, KEYS

Vì lưu trữ dạng key-value nên câu lệnh cơ bản nhất sẽ là:

- gán trị vào từ khóa (set value to key): SET <key> <value>
- lấy giá trị ra từ từ khóa (get value from key): GET <key>
- kiểm tra xem từ khóa có trong bộ nhớ không: EXIST <key>
- tìm kiếm từ khóa theo pattern: KEYS <pattern>

Một bộ key-value cũng có thể được set thời gian nó tồn tại với từ khóa EXPIRE <key> <time>

Ngoài ra, Redis cũng có nhiều kiểu dữ liệu khác được lưu cho value như: list, sets, hashes và các từ khóa tương ứng sử dụng cho từng kiểu dữ liệu trên.

Mời bạn ghé đọc [bài viết này][basic-knowledges-about-redis] để tìm hiểu thêm và có video hướng dẫn để bạn có thể thực hành nữa ấy.

[basic-knowledges-about-redis]: {{ "" | relative_url }}{% post_url database/2022-05-28-basic-knowledges-about-redis %}

## GraphQL là gì ? Sự khác nhau giữa GraphQL và REST

GraphQL là query language dành cho API được phát triển bởi Meta. GraphQL cung cấp schema của data trong API và cho phép client quyền truy vấn chính xác những thứ họ cần.

GraphQL đứng giữa client và backend

**GraphQL Client → GraphQL → Backend Services (Auth APIs, Core APIs, Redis)**

GraphQL có thể truy vấn đến nhiều resources chỉ trong một query.
GraphQL cũng hỗ trợ mutation (addNote) và subscription (newNode)

**Vậy GraphQL và REST API giống và khác nhau như thế nào ?**

Giống:

- đều gửi HTTP request bằng một URL
- đều nhận HTTP response (JSON)

Khác:

- GraphQL cho phép truy vấn chính xác resources và fields mà client cần
- REST API thì data trả về quyết định bởi phía backend
    
    REST API
    
    - trung tâm là resources, được xác định trên url như GET /api/v1/users
    - gọi url lấy một book GET /api/v1/books/1, gọi url lấy một author GET /authors/1 - nhiều request qua nhiều resources
    
    GraphQL
    
    - trung tâm là GraphQL Schema
    - định nghĩa các type (schema)
    - gửi request với resource và fields cần lấy data

Tóm lại, GraphQL sử dụng Schema định nghĩa các type, cho phép truy vấn theo nhu cầu của client (resources, fields) và giải quyết được các vấn đề của REST API như thừa data trả về, nhiều request cùng lúc khi muốn lấy data từ nhiều resources.

Một số hạn chế của GraphQL:

- Không có các lợi thế của REST.
Lợi thế của REST như:
- không cần một lib khác để dùng giữa request và server
- request có thể gửi đi từ curl hay web browser
- GET request dễ cache (CDNs, Proxies, Web Servers)
- Cần công cụ khác hỗ trợ cả ở client và server (Apollo, schema.graphql, codegen.yml, operation.graphql) → tốn tiền hơn → không phù hợp với CRUD APIs
- Khó cache hơn vì mặc định sử dụng POST request
- Data quyết định bởi client có thể gây các vấn đề về dữ liệu

Do đó, việc lựa chọn sử dụng GraphQL hay REST API sẽ tùy thuộc vào từng loại dự án khác nhau.

Mời bạn xem thêm ở [blog này][graphql-la-gi-su-khac-nhau-giua-graphql-va-rest] nhé!

[graphql-la-gi-su-khac-nhau-giua-graphql-va-rest]: {{ "" | relative_url }}{% post_url apis/2022-11-11-graphql-la-gi-su-khac-nhau-giua-graphql-va-rest %}