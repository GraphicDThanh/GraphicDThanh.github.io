---
title: "GraphQL là gì ? Sự khác nhau giữa GraphQL và REST"
categories:
  - APIs
tags:
  - api
  - api-design
---

![](assets/images/2022/11/2022-11-graphql-la-gi-su-khac-nhau-giua-graphql-va-rest.webp)

## GraphQL là gì ?
GraphQL là query language dành cho API được phát triển bởi Meta.

GraphQL cung cấp schema của data trong API và cho phép client quyền truy vấn chính xác những thứ họ cần.

Ví dụ có đoạn data sau:
```json
{
  "book": {
    "title": "GraphQL book",
    "author": "Meta",
    "year": 2022
  }
}
```
thì ngôn ngữ GraphQL diễn tả:

```json
{
  book {
    title,
    author,
    year
  }
}
```
GraphQL đứng giữa client và backend

```
GraphQL Client → GraphQL 
Graph          → Backend Services (Auth APIs, Core APIs, Redis)
```

GraphQL có thể truy vấn đến nhiều resources chỉ trong một query.

GraphQL cũng hỗ trợ mutation (addNote) và subscription (newNode)

## Sự khác nhau giữa GraphQL và REST API
Vậy GraphQL và REST API giống và khác nhau như thế nào ?

### Giống nhau
- đều gửi HTTP request bằng một URL
- đều nhận HTTP response (JSON)

### Khác nhau
- GraphQL cho phép truy vấn chính xác resources và fields mà client cần
- REST API thì data trả về quyết định bởi phía backend

Ví dụ muốn lấy data như sau từ database:
```json
{
  "title": "GraphQL and REST API book",
  "authors": [{
    "name": "Meta"
  }, {
    "name": "Anna"
  }, ...]
}
```
(lưu ý là author được implement khác nơi với book)

Thì cách làm tương ứng mỗi loại như sau:

#### REST API
– trung tâm là resources, được xác định trên url như GET /api/v1/users

– gọi url lấy một book GET /api/v1/books/1, gọi url lấy một author GET /authors/1 – nhiều request qua nhiều resources

#### GraphQL
– trung tâm là GraphQL Schema

– định nghĩa các type (schema)

```json
type Book {
  id: ID,
  title: string,
  authors: [Author]
}
type Author {
  id: ID,
  name: string,
  books: [Book]
}
```
– để truy vấn data, định nghĩa type Query

```json
type Query {
  book(id: ID): Book
}
```
– gửi request với resource và fields cần lấy data 

`GET /graphql?query={ book(id: “123”), { title, authors { name } } }`

Tóm lại, GraphQL sử dụng Schema định nghĩa các type, cho phép truy vấn theo nhu cầu của client (resources, fields) và giải quyết được các vấn đề của REST API như thừa data trả về, nhiều request cùng lúc khi muốn lấy data từ nhiều resources.

### Lợi thế của REST:
– không cần một lib khác để dùng giữa request và server

– request có thể gửi đi từ curl hay web browser

– GET request dễ cache (CDNs, Proxies, Web Servers)

### Một số hạn chế của GraphQL:
– Cần công cụ khác hỗ trợ cả ở client và server (Apollo, schema.graphql, codegen.yml, operation.graphql) → tốn tiền hơn → không phù hợp với CRUD APIs

– Khó cache hơn vì mặc định sử dụng POST request

– Data quyết định bởi client có thể gây các vấn đề về dữ liệu

Do đó, việc lựa chọn sử dụng GraphQL hay REST API sẽ tùy thuộc vào từng loại dự án khác nhau.

([Ref video](https://youtu.be/yWzKJPw_VzM))