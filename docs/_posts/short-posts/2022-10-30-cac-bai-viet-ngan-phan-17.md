---
title: "Các bài viết ngắn - phần 17"
categories:
  - Short Posts
tags:
  - short-post
---
![](assets/images/2022/10/2022-10-30-cac-bai-viet-ngan-phan-17-1.webp)

## Thuật toán là gì?
Thuật toán hay giải thuật là một khái niệm quan trọng trong toán học và khoa học máy tính.

Thuật toán là gì?

Đầu tiên, để giải bài toán thì cần hiểu vấn đề của bài toán một cách rõ ràng. Vấn đề bạn cần giải quyết là gì, có đầu vào và đầu ra sau khi giải quyết bằng thuật toán là như thế nào?

Thuật toán sẽ là tập hợp các bước hữu hạn được đưa ra với một thứ tự cụ thể.

Mỗi bước của thuật toán cần riêng biệt. Tức là mỗi bước sẽ không được chứa các bước con hay lặp lại của bước khác.

Thuật toán cần đưa ra được kết quả.

Thuật toán cần kết thúc sau một khoảng thời gian nhất định.

Thế nào là một thuật toán tốt?

Có 2 tiêu chí để đo một thuật toán đủ tốt là:

Tính đúng đắn (correctness): với mỗi đầu vào, thuật toán xử lý và cho ra một đầu ra đúng như mong đợi của đề bài.

Tính hiệu quả (efficiency): thuật toán có giải quyết vấn đề một cách tốt hơn và nhanh hơn.
Có hai thước đo tính hiệu quả là “thời gian” (time complexity) và “không gian” (space complexity).
– Time complexity có thể hiểu là cần bao lâu để hoàn thành việc chạy thuật toán
– Space complexity có thể hiểu là cần bao nhiêu không gian(bộ nhớ) để hoàn thành việc chạy thuật toán

Big O là một mô tả về mặt lý thuyết thể hiện độ phức tạp của một thuật toán dựa trên kích thước của hàm.

Bắt đầu học về thuật toán và cấu trúc dữ liệu với [video](https://www.youtube.com/watch?v=8hly31xKli0) hơn 2 triệu lượt xem này nhé!

## Điều gì xảy ra khi chạy chương trình JavaScript?
Mọi thứ trong JavaScript diễn ra bên trong một ngữ cảnh thực thi, hay `“Execution Context”`.

Có hai giai đoạn trong “Execution Context” là “Memory Creation” và “Code Execution

Khi chương trình JS khởi chạy, một execution context ở global sẽ được tạo.

Ở giai đoạn “Memory Creation Phase”, bộ nhớ được cấp cho tất cả các biến và các hàm.

Ở giai đoạn “Code Execution”, code sẽ được thực thi từng dòng một theo thứ tự trên xuống dưới.

Nếu có một hàm được gọi, một Execution Context giành riêng cho hàm đó sẽ được tạo và thực hiện tương tự với hai giai đoạn trong Execution Context mới này. Khi một hàm kết thúc thực thi, thì Execution Context này sẽ được xóa đi.

Và cứ thế, chạy cho đến hết chương trình.

Quá trình ở trên thường được gọi là call stack

Mỗi execution context được tạo sẽ được bỏ vào(push) vào ngăn xếp(stack)

Mỗi execution context bị xóa sẽ được lấy ra khỏi(pop) ngăn xếp(stack)

Đây chính là cách JS Engine thực thi code.

Mời bạn đọc chi tiết về quá trình này kèm ví dụ và hình ảnh minh họa ở [blog post này](https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/) nhé

## Nguồn tài liệu video khoa học máy tính
Bạn là sinh viên ngành CNTT hay đã là lập trình viên nhưng các kiến thức nền tảng về khoa học máy tính còn lủng nhiều chỗ như mình?

Bạn có thể viết React App dễ dàng nhưng không hiểu về những gì đằng sau nó, các thuật toán nào được sử dụng, vì sao dùng kiểu dữ liệu này mà không dùng kiểu dữ liệu kia, …

Bạn muốn cải thiện tư duy logic, thuật toán hay cấu trúc dữ liệu nhưng các khoá học đắt đỏ hay nguồn tài liệu tràn lan thiếu chọn lọc, hay các cuốn sách đầy chữ khô khan.

Giới thiệu đến bạn một repo github với hơn 40 ngàn stars chứa tài nguyên là các “videos” về CS Foundation – Computer Science Foundation hay các kiến thức nền tảng về khoa học máy tính.

Các chủ đề bạn có thể tìm hiểu như:

* Introduction to Computer Science
* Data Structures and Algorithms
* Systems Programming
* Database Systems
* Software Engineering
* Artificial Intelligence
* Machine Learning
* Web Programming and Internet Technologies
* Computer Networks
* Math for Computer Scientist
* Theoretical CS and Programming Languages
* Embedded Systems
* Real time system evaluation
* Computer Organization and Architecture
* Security
* Computer Graphics
* Image Processing and Computer Vision
* Computational Biology
* Quantum Computing
* Robotics
* Computational Finance
* Blockchain Development
* Misc

Mình được bạn bè giới thiệu [nguồn này](https://github.com/Developer-Y/cs-video-courses) gần đây, cùng bắt đầu tìm hiểu về thế giới CS thú vị này nhé!

Tới lúc phải làm lập trình viên chân chính rồi, không thể là thợ code mãi được ^^

## Clean Code - cách tiếp cận theo hướng thực hành
Clean Code – một số cách tiếp cận theo hướng thực hành

Clean Code là gì ? Vì sao bạn nên quan tâm ?

Clean Code là quan trọng, bởi:
– clean code dễ đọc
– clean code dễ chỉnh sửa
– clean code được viết bởi những người thực sự quan tâm đến nó
– clean code luôn được mong đợi, không lừa bạn, không có những bất ngờ trớ trêu

Tại sao nên viết code clean?
– Vì đó là bước đầu tiên giúp đạt đến: giảm thiểu nguồn lực cần thiết để tạo và duy trì hệ thống
– Vì khi bạn code, bạn dành nhiều thời gian để đọc code hơn và viết code
– Vì chúng ta, những developer, code là để cho những developer khác có thể đọc

Một số nguyên tắc cơ bản:

Cách đặt tên
– sử dụng tên có ý nghĩa
– sử dụng tên có thể đọc được
– sử dụng tên có thể tìm kiếm được
– tránh sử dụng các tiền tố, hậu tố hay các từ viết tắt (prefix, suffix, hay abbreviations)

Hàm
– Hàm nên chỉ làm một việc
– Hàm nên nhỏ (hạn chế số lớp lồng như 2, 3 lớp)
– Hàm nên có càng ít tham số càng tốt

Comments (ghi chú)
– Tránh comment để giải thích code

Refactoring (tái cấu trúc code)
Là quá trình tái cấu trúc code mà không làm thay đổi logic, hành vi (behavior) của phần code được sửa.

Vậy nên và không nên refactoring code nào?
Không nên:
– thay đổi thuật toán
– thay đổi vòng lặp này bằng vòng lặp khác
– cải thiện hiệu suất của một đoạn code
Nên:
– tách nhỏ một đoạn logic ra hàm riêng
– thay đổi tên
– tách một vài hàm ra lớp
– tạo hằng số để chứa các giá trị cố định

Và nên thực hiện safe refactoring, bằng cách:
– đảm bảo đủ test case cho các tính năng
– sử dụng các tools ở các IDEs để thay đổi một cách tự động và tăng tính chính xác

Thế khi nào cần refactoring?
– Khi viết code
– Khi viết test
– Khi refactor

Chúc bạn viết code ít bug và nhiều niềm vui nhé!

Đọc thêm ở [bài viết sau](https://medium.com/clarityai-engineering/clean-code-a-practical-approach-896546435235)

## Function Python là first-class object

Vậy first-class object là gì ?

**first-class object là một thực thể được gán vào biến, lưu trữ trong các loại dữ liệu như bỏ vào list, hay sử dụng như một đối số truyền vào hàm khác, và thậm chí là trả về chúng từ hàm khác.**

Việc hiểu hàm là một first-class object sẽ giúp bạn dễ tiếp thu hơn các khái niệm khác như lambda hay decorators.

Hàm là một first-class object nên sẽ có các đặc điểm cụ thể sau:
– Hàm là đối tượng
– Hàm có thể sử dụng trong cấu trúc dữ liệu
– Hàm có thể được truyền vào hàm khác như tham số
– Hàm có thể lồng nhau
– Hàm có thể truy cập các biến cục bộ (hay gọi là lexical closures hoặc closures)
– Đối tượng có thể có hành vi giống hàm

Bạn ghé đọc thêm các ví dụ cho từng đặc điểm ở [bài viết sau](https://beautyoncode.com/ham-trong-python-la-first-class-object/) nhé
