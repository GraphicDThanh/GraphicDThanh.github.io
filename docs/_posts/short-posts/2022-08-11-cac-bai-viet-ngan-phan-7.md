---
title: "Các bài viết ngắn - phần 7"
categories:
  - Short Posts
tags:
  - git
---

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/12/Short-posts-07.png)

## Trực quan hóa khi chạy mã chương trình
Giả sử bạn đang giả một bài toán nhưng gặp bug, thì bạn sẽ làm gì?

Giới thiệu đến bạn một công cụ Visualize Code Running có tên là [pythontutor.com](http://pythontutor.com/) giúp bạn xem được từng bước được mô tả một cách trực quan. Dù là pythontutor nhưng công cụ này hỗ trợ nhiều loại ngôn ngữ như Python, JavaScript, C, C++, and Java.

Bạn vào trang pythontutor.com sau đó chọn Start writing and visualizing code now và chọn ngôn ngữ muốn viết.

Sau khi đã nhập (paste) đoạn code cần debug vào, nhấn nút Visualize Executionđể bắt đầu xem code thực thi ra sao. Bấm Next để di chuyển đến bước tiếp theo.

Nửa màn hình bên trái chứa code, các nút bấm để di chuyển đến bước tiếp theo Next, bước trước đó Prev, bước cuối cùng Last và bước đầu tiên First

– Mũi tên xanh lá câu nhạt chỉ dòng vừa mới thực thi

– Mũi tên đỏ chỉ dòng sẽ thực thi tiếp theo

Mời bạn ghé đọc [bài viết này](https://beautyoncode.com/truc-quan-hoa-khi-chay-ma-chuong-trinh/) là một ví dụ cụ thể về cách bạn có thể sử dụng pythontutor để debug một đoạn logic của bài leetcode [**35. Search Insert Position**](https://leetcode.com/problems/search-insert-position/) và xem từng bước chạy như thế nào. 

Thay vì đi console.log mọi nơi thì cách này xịn xò hơn hẳn phải không?

## npkill
Nếu muốn hiện các dependences trong một một dự án quản lý bởi npm (Node Package Manager), câu lệnh “npm list” hoặc “npm ls”. Nếu muốn tìm kiếm có thể sử dụng “npm search [search term]”

Gần đây, npm v8.16.0 đã mắt thêm một câu lệnh “npm query” cho phép tìm kiếm theo Dependences Selector, có cú pháp tương tự như CSS Selectors, một ngôn ngữ mà hầu như lập trình viên nào cũng biết.

Ví dụ thay vì “npm list –all” thì nay có thể thay bằng npm query “*” Hoặc muốn tìm kiếm những phiên bản của react thì có thể kiếm bằng: npm query “#react” Tìm những phiên bản react mà không phải là peer dependences: npm query “#react:not(.peer)” Tìm tất cả dependences loại git: npm query “:type(git)” Tìm tất cả dependences có license là MIT: npm query “license=MIT”

Bạn ghé đọc [bài viết này](https://github.blog/changelog/2022-08-03-introducing-the-new-npm-dependency-selector-syntax/) để bỏ túi thêm vài típ sử dụng khác nha.

## CRUD là gì?
Thuật ngữ CRUD, hay CRUD Operation được sử dụng khá phổ biến, đó không phải là một từ mà là viết tắt của Create – Read – Update – Delete, đại diện cho 4 hoạt động chính của một ứng dụng

Ví dụ bạn tạo một app các công việc cần làm (todo list), thì sẽ cần người dùng nhập các công việc cần làm (create), xem được danh sách các công việc (read), thay đổi nội dung công việc (update) hoặc xoá công việc khi không cần làm nữa (delete).

Một ứng dụng CRUD sẽ bao gồm 3 phần chính: server (API) : truyền dữ liệu database : lưu dữ liệu client app (UI) : hiển thị dữ liệu, nơi người dùng nhập dữ liệu

CRUD cũng tương ứng với các phương thức HTTP cụ thể: Create tương ứng với POST Read tương ứng với GET Update tương ứng với PUT/PATCH. PUT là update toàn phần, PATCH là update một phần Delete tương ứng với DELETE

Bạn có thể đọc thêm về các ví dụ ở [link sau](https://www.freecodecamp.org/news/crud-operations-explained/).

## npm query
Nếu muốn hiện các dependences trong một một dự án quản lý bởi npm(Node Package Manager), câu lệnh “npm list” hoặc “npm ls”. Nếu muốn tìm kiếm có thể sử dụng “npm search [search term]”

Gần đây, npm v8.16.0 đã mắt thêm một câu lệnh “npm query” cho phép tìm kiếm theo Dependences Selector, có cú pháp tương tự như CSS Selectors, một ngôn ngữ mà hầu như lập trình viên nào cũng biết.

Ví dụ thay vì “npm list –all” thì nay có thể thay bằng npm query “*” Hoặc muốn tìm kiếm những phiên bản của react thì có thể kiếm bằng: npm query “#react” Tìm những phiên bản react mà không phải là peer dependences: npm query “#react:not(.peer)” Tìm tất cả dependences loại git: npm query “:type(git)” Tìm tất cả dependences có license là MIT: npm query “license=MIT”

Bạn ghé đọc [bài viết này](https://github.blog/changelog/2022-08-03-introducing-the-new-npm-dependency-selector-syntax/) để bỏ túi thêm vài típ sử dụng khác nha.

## Giới thiệu về mã 
Trong thế giới phần mềm, bạn sẽ hay gặp câu hỏi: “Phần mềm này là loại mã nguồn mở (open source) hay mã nguồn đóng (closed source)?”

Vậy thì mã nguồn là gì? mã nguồn mở hay mã nguồn đóng nghĩa là sao?

Mã nguồn (source code) là phần code của ứng dụng. Ví dụ đơn giản nhất là chương trình hello world, in ra một dòng “Hello Linux!”

```python
print("Hello Linux")
```
nội dung trên chính là mã nguồn của chương trình viết bằng Python.

Mã nguồn đóng(closed source) là những phần mềm độc quyền với mục đích bảo vệ mã nguồn để tránh cạnh tranh, sao chép, … (Windows, MacOS, …)

Mã nguồn mở(open source) là chương trình có mã nguồn được cung cấp sẵn (Linux, Firefox, Git, …). Open source có thể hiểu là khả năng truy cập vào mã nguồn.

Ngoài ra còn có free source, là những phần mềm được tự do copy hay có thể thay đổi của chương trình, chứ không liên quan đến giá cả.

Open source có rất nhiều lợi ích như được sự đóng góp của cộng đồng, source code tốt hơn và giảm thời gian phát triển phần mềm. Và cũng vì được mở nên sẽ tiếp cận được nhiều người hơn.

Linux thường hay được biết đến là hệ điều hành mã nguồn mở phổ biến. Tuy nhiên thực tế Linux chỉ là một phần mềm nhân (kernel). Mời bạn đọc thêm về các loại mã nguồn và giới thiệu về Linux ở [đây](https://beautyoncode.com/gioi-thieu-ve-linux/).
