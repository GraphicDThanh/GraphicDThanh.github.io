---
title: "Các bài viết ngắn về CS Foundation"
---

Các bài viết ngắn về CS Foundation (Algorithms and Problem-Solving Skills)
- Array
- Tìm kiếm nhị phân (binary search)
- Giải bài toán đồ thị (graph problem) với python
- CS50

## Array

**Mảng (array) là kiểu dữ liệu phổ biến nhất**, câu hỏi về mảng thường là quan trọng trong các cuộc phỏng vấn về kỹ thuật dành cho lập trình viên.

Mảng (array) cho phép lưu nhiều phần tử vào một biến duy nhất và truy cập các phần tử trong mảng với index (chỉ mục).

Tuy nhiên, việc thay đổi các phần tử trong mảng diễn ra chậm hơn linked list khi thay đổi các phần tử giữa mảng vì các phần tử còn lại sẽ phải di chuyển để phù hợp với vị trí mới sau khi đã thêm / xóa. 

Bên cạnh đó, một số ngôn ngữ yêu cầu kích thước mảng cần khai báo trước và không thể thay đổi sau khi đã khởi tạo. Nếu phần tử được thêm vào vượt quá kích thước mảng thì việc sao chép lại mảng cũ và thêm mảng mới làm tốn thời gian là O(n).

Mời các bạn tìm hiểu thêm về mảng qua các nguồn tài liệu, các kỹ thuật giải toán với kiểu dữ liệu này và các bài toán luyện tập ở [bài blog này][array].


## Tìm kiếm nhị phân (binary search)

Tìm [kiếm nhị phân](https://vi.wikipedia.org/wiki/T%C3%ACm_ki%E1%BA%BFm_nh%E1%BB%8B_ph%C3%A2n) (binary search) là một thuật toán tìm kiếm xác định vị trí của một giá trị cần tìm trong một mảng đã được sắp xếp.

Thuật toán sẽ tiến hành so sánh giá trị cần tìm với phần tử đứng giữa của mảng. Nếu hai giá trị không bằng nhau, thì một nửa mảng không chứa giá trị cần tìm sẽ được bỏ qua, và tiếp tục tìm kiếm trên nửa còn lại. Một lần nữa, lấy phần tử ở giữa so sánh với giá trị cần tìm, cứ thế lặp lại cho đến khi tìm thấy giá trị đó. Nếu phép tìm kiếm kết thúc mà vẫn chưa có giá trị cần tìm tức là nó không có trong mảng.

Binary search chạy theo giời gian logarit trong trường hợp tệ nhất, thực hiện O(logn) bước so sánh, với n là số phần tử của mảng. Thuật toán này sẽ nhanh hơn thuật toán tìm kiếm tuyến tính thông thường (lặp qua toàn mảng) với O(n)

Một số vấn đề thường gặp khi giải bài toán binary search:

– Khi nào thì sẽ thoát ra khỏi vòng lặp?

– Làm sao để khởi tạo và cập nhật biên bên trái (left), biên bên phải (right)?

[Bài viết sau][tim-kiem-nhi-phan] giới thiệu một bản mẫu tổng quát về cách giải binary search sẽ giúp bạn hình dung về cách giải bài toán này dễ dàng hơn.


## Giải bài toán đồ thị (graph problem) với python

### Graph là gì?

Graph là một cấu trúc dữ liệu gồm các nút (nodes) hay N và các nhánh (edges) hay E. Loại cấu trúc dữ liệu này thường sử dụng để mô tả khoảng cách giữa các địa điểm hay trong những loại liên kết phức tạp khác.

Node là điểm, thường thể hiện bằng hình tròn, có giá trị (hoặc không). Edge là nhánh, thường thể hiện bằng đường nối giữa hai điểm với nhau, có giá trị (hoặc không)

### Giải quyết vấn đề graph

– Duyệt qua graph với Breadth First Search (BFS) hay thuật toán tìm kiếm theo chiều rộng

– Duyệt qua graph với Depth First Search (DFS) hay thuật toán tìm kiếm theo chiều sâu

– Tạo graph với một Adjacency List

– Directed Graph (có một chiều nhất định giữa hai node) và Undirected Graph (giữa hai nút có hai chiều)

Ngoài ra còn có các bài tập cụ thể và được giải với python ở [link](https://www.giulianopertile.com/blog/the-definitive-guide-to-graph-problems/).


## CS50

Bạn có từng nghe về khoá CS50, một khoá học nền tảng dành cho bất cứ ai muốn bắt đầu với lĩnh vực khoa học máy tính ?

Các chủ đề bao gồm các khái niệm trừu tượng (abstraction), thuật toán (algorithms), cấu trúc dữ liệu (data structures), đóng gói (encapsulation), quản lý mã nguồn (resource management), bảo mật (security), kỹ thuật phần mềm (software engineering), và lập trình web (web programming).
Các ngôn ngữ bao gồm C, Python, và SQL, thêm vào đó là HTML, CSS, và JavaScript.

Nội dung theo từng bài học như sau:
* Lecture 0 - Scratch
* Lecture 1 - C
* Lecture 2 - Arrays
* Lecture 3 - Algorithms
* Lecture 4 - Memory
* Lecture 5 - Data Structures
* Lecture 6 - Python
* Lecture 7 - SQL
* Lecture 8 - HTML, CSS, JavaScript
* Lecture 9 - Flask
* Lecture 10 - Emoji
* Cybersecurity

Khoá học 25 giờ này hoàn toàn miễn phí được giảng dạy bởi David J. Malan.
Cám ơn freecodecamp cho tài liệu tuyệt vời này!

Lưu ngay vào danh sách todo của bạn để có một bước nền tảng vào ngành khoa học máy tính nha !

<iframe width="640" height="360" src="https://www.youtube.com/watch?v=8mAITcNt710" frameborder="0" allowfullscreen></iframe>


[tim-kiem-nhi-phan]: {{ "" | relative_url }}{% post_url fundamentals/2022-08-02-tim-kiem-nhi-phan-binary-search %}
