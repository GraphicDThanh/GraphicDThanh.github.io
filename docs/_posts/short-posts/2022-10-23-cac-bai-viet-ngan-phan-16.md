---
title: "Các bài viết ngắn - phần 16"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/10/Short-posts-17.png)

## var, let, const

Ba cách giúp bạn khai báo biến trong `JavaScript` là sử dụng từ khóa `var`, `let`, `const`.

`var` và `let` đều dùng để khai báo một biến có thể thay đổi giá trị được.

Tuy nhiên với `let` bạn không truy cập được trước khi khai báo.

Và `scope` của biến của bạn sẽ khác nhau:
– `var` là global / local scoped
– `let` và `const` là block scoped hay lexical scoped.

`let` và `var` cho phép khai báo tên một biến mà không cần giá trị khởi tạo, còn `const` chỉ cho phép khai báo với một giá trị ban đầu. Và `const` không cho bạn thay đổi giá trị của biến.

**Cách sử dụng**

– `const`: sử dụng khai báo hằng số, các giá trị không thay đổi trong suốt chương trình, và cố gắng dùng nhiều nhất có thể vì nó chặt chẽ nhất

– `let`: ưu tiên tiếp theo sau const, cố gắng sử dụng bất cứ khi nào có thể vì `let` có `Temporal Dead Zone` giúp bạn không truy cập trước khi khai báo tránh các lỗi về undefined khi truy cập trước khai báo như khi dùng với `var`

– `var`: không nên dùng, hạn chế tối đa (hiểu để đọc code những chương trình viết với `ES5`)

[Mời bạn đọc thêm ở bài blog này](https://beautyoncode.com/khai-bao-bien-voi-var-let-va-const-trong-javascript/)

## Mảng (array)
Mảng (array) là kiểu dữ liệu phổ biến nhất, câu hỏi về mảng thường là quan trọng trong các cuộc phỏng vấn về kỹ thuật dành cho lập trình viên.

Mảng (array) cho phép lưu nhiều phần tử vào một biến duy nhất và truy cập các phần tử trong mảng với index (chỉ mục).

Tuy nhiên, việc thay đổi các phần tử trong mảng diễn ra chậm hơn linked list khi thay đổi các phần tử giữa mảng vì các phần tử còn lại sẽ phải di chuyển để phù hợp với vị trí mới sau khi đã thêm / xóa.

Bên cạnh đó, một số ngôn ngữ yêu cầu kích thước mảng cần khai báo trước và không thể thay đổi sau khi đã khởi tạo. Nếu phần tử được thêm vào vượt quá kích thước mảng thì việc sao chép lại mảng cũ và thêm mảng mới làm tốn thời gian là O(n).

Mời các bạn tìm hiểu thêm về mảng qua các nguồn tài liệu, các kỹ thuật giải toán với kiểu dữ liệu này và các bài toán luyện tập ở [bài blog dưới đây]( https://beautyoncode.com/array/).

## Chơi cùng JavaScript

Khi học JavaScript bạn thử nghiệm các đoạn code nhỏ bằng các cách nào ?
Thử xem bạn đã dùng cách nào trong các cách sau nhé!

### Cách 1: Chạy chương trình với browser

Tạo file index.html để chứa code của trang web. Sau đó viết nội dung trang web trong file index.html và viết code JS trong thẻ <script></script> hoặc tải vào thẻ script này với thuộc tính src.
Bạn có thể mở trực tiếp file index.html hoặc “Go Live” với extension “Live Server” trên VSCode.

Cách này thì khá cồng kềnh khi muốn thử nghiệm nhanh một đoạn logic nhỏ. Tuy nhiên sẽ cần thiết nếu bạn thực hành liên quan đến DOM.
Cách này không chia sẻ code online được.

### Cách 2: Chạy chương trình với nodejs

Cài nodejs trên máy (thường sẽ có sẵn vì dev thường sử dụng npm)
Chạy lệnh `“node <filename>.js”` ở command line để thực thi
Một tip là có thể sử dụng gói nodemon để tự động load lại khi mình có chỉnh sửa trên file.
Chạy câu lệnh: “npx nodemon example.js” để vừa cài gói nodemon vừa thực thi code.

Cách này sẽ tiện hơn nếu muốn chạy một chương trình JS nhỏ không liên quan đến DOM.
Cách này cũng không chia sẻ code online được.

### Cách 3: Sử dụng tab “Console” trên trình duyệt Chrome
Sử dụng browser Chrome, mở Console tab và thử nghiệm trực tiếp trên đó.

Cách này sẽ rất tiện khi mình muốn kiểm tra nhanh hay demo nhanh các đoạn code hay cú pháp của JS, vì trình duyệt có tích hợp sẵn để dùng.
Đặc biệt bạn có thể chơi với Web APIs như DOM, …

### Cách 4: Sử dụng javascript.makeup
[javascript.markup](https://javascript.makeup/file/default) cũng là một cách để có thể chơi với JS và kết quả cũng khá dễ nhìn.

### Cách 5: Sử dụng các công cụ online giúp viết và chia sẻ chương trình như: [Playcode.io](https://playcode.io/), JSBin, JSFiddle, Replit
Các công cụ này thường yêu cầu tài khoản để lưu và chia sẻ chương trình.

Trên đây là một số cách mình biết. Còn bạn thì sao, bạn hay thử nghiệm JS như thế nào?

Cùng chia sẻ với mình bên dưới comment nhé!

Bạn có thể xem hình ảnh minh họa ở [bài blog mình viết chi tiết](https://beautyoncode.com/choi-cung-javascript/) này.

## Inner function trong Python
> Inner function là hàm được định nghĩa bên trong một hàm khác.

Ví dụ:

```python
def outer_func(name):
    def inner_func():
        print(f'hello {name}')
    inner_func()
```

gọi `outer_func(“Anna”)` sẽ in ra `‘hello Anna’`

Inner function thường được được sử dụng:

– **Sử dụng đóng gói hàm (encapsulation)**

Ở ví dụ trên, `inner_func` chỉ được truy cập bên trong hàm `outer_func` , bên ngoài không thể truy cập được.
Đây gọi là **encapsulation**.

– Sử dụng để chia logic trong một hàm lớn thành các hàm logic nhỏ và có thể tái sử dụng

– Sử dụng viết các các hàm helper để sử dụng chỉ trong hàm nhất định. Có thể dùng prefix `_` để mô tả hàm này là private với hàm, module hay class.

– **Sử dụng để tạo closures**

Closures là hàm được tự động tạo bằng cách trả về một hàm khác.

   Tạo closures với 3 bước:
   1. Tạo một inner function
   2. Tham chiếu biến từ hàm bên ngoài để xử lý trong hàm inner function
   3. Trả về inner function

   Ví dụ: tạo closures `“generate_power”` để tạo ra các hàm tính luỹ thừa.

```python
def generate_power(exponent):
    def power(base):
        return base ** exponent
    return power
```

sử dụng tạo hàm luỹ thừa hai

```python
raise_two = generate_power(2)
```

và tính luỹ thừa hai với raise_two(5) là 25

– **Sử dụng để tạo decorators**

**Decorators** là một **HOC** hay **higher-order function** nhận đầu vào một hàm, class, object và trả về hàm khác.

Decorators thưởng được sử dụng trong debug, caching, logging, timing.

Ví dụ tạo một decorator thêm một số log trước và sau khi gọi hàm:

```py
def add_messages(func):
    def _add_messages():
        print("Start call function")
        func()
        print("Finish call function")
```
và được sử dụng với @

```python
@add_messages
def greet():
    print("Hi")
```

và khi gọi greet() sẽ in ra 3 dòng:

```
Start call function
Hi
Finish call function
```

Inner function là một công cụ vô cùng mạnh mẽ đúng không nào !

Bạn đọc thêm ở [bài viết này](https://realpython.com/inner-functions-what-are-they-good-for/) nhé

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