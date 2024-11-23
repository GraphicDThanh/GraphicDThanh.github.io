---
title: "Các bài viết ngắn về Python"
---

Các bài viết ngắn về "Python"
- Game Hang Man với Python
- Gỡ lỗi chương trình
- Inner function trong Python
- Làm tròn số thực trong Python
- Function Python là first-class object

## Game Hang Man với Python
Khi học một ngôn ngữ mới 🐍, việc làm ra một sản phẩm có thể dùng được, chơi được sẽ có động lực vô cùng lớn với bản thân 💪 🥳 😇

Hôm nay mình sẽ giới thiệu đến mọi người một phiên bản của trò chơi học từ vựng tiếng anh 🏴󠁧󠁢󠁥󠁮󠁧󠁿 bằng cách đoán từ 🤔, phiên bản Hangman(người treo cổ), cùng với các kiến thức Python 🐍🐍🐍 cơ bản nhé.

Trước tiên mời bạn chơi thử trò chơi ở đây 👉: https://replit.com/@diemthanhthanh/Hangman-Demo#main.py

Bạn cũng có thể đăng ký tài khoản [repl.it](http://repl.it) rồi chọn “Fork Repl” để tải ⬇️ bản game về tài khoản của bạn. Tại đây, bạn có thể thay đổi nội dung 🔤 trong file [words.py](http://words.py) để chứa các từ 🍎 🍊 🥦 🍇 bạn muốn học hay thực hành.

Để có thể làm được một trò chơi như vậy, sẽ đi qua các bước sau:

1. Tìm hiểu về trò chơi và luật chơi
2. Chơi thử game demo xem các chương trình sẽ hoạt động ra sao
3. Phân tích trò chơi và vẽ sơ đồ của trò chơi để mô tả logic
4. Làm phiên bản đơn giản
5. Nâng cấp trò chơi, thêm các yếu tố khác để trò chơi hấp dẫn với người dùng hơn

Và tất nhiên là không thể thiếu một ít kiến thức về Python cơ bản như biến, câu lệnh điều kiện(if/else), vòng lặp while/for, …

Còn chần chừ gì nữa, hãy ghé bài [blog này][lam-game-hangman-voi-python] để làm một trò chơi riêng của mình rồi khoe với bạn bè người thân nha

[lam-game-hangman-voi-python]: {{ "" | relative_url }}{% post_url python/2021-10-06-lam-game-hangman-voi-python %}

## Gỡ lỗi chương trình
Hôm nay mình muốn nói về “Gỡ lỗi”(Debugging)🐞, một qui trình sửa lỗi trong chương trình phần mềm. Điều quan trọng đầu tiên cần nhớ là:

Đừng cảm thấy thất vọng khi bạn tạo ra một con bug.

Khi viết một chương trình thì việc gặp bug 🐞 là việc đương nhiên 🥲. Mình sẽ giới thiệu một số mẹo và kỹ thuật để nhận dạng bug và sửa nó hiệu quả:

✍️ Mô tả vấn đề(Describe the problem)

Để fix bug, đầu tiên bạn cần mô tả được vấn đề mà mình gặp phải.

🐞  Tái tạo lại lỗi(reproduce the bug)

Rất nhiều khi bug chỉ thỉnh thoảng xuất hiện. Để fix được những bug như vậy lập trình viên cần biết cách tái tạo lại con bug đó và tìm hiểu chính xác vấn đề mà trường hợp đó gặp phải là gì thì mới có thể sửa lỗi được.

💻 Thử thực hiện chương trình như máy tính(Play computer)

Với một chương trình phức tạp như có logic với nhiều điều kiện rẽ nhánh, hay gọi nhiều hàm khác nhau, thì việc sửa lỗi sẽ càng khoai hơn. Lúc này bạn cần tưởng tượng mình là máy tính, và với đầu vào cụ thể nào đó, bạn tự kiểm tra từng dòng một của chương trình như cách máy tính chạy để tìm manh mối cho lỗi của mình.

🏹 Sửa lỗi(fix the errors)

Viết chương trình mà editor báo lỗi hay chạy chương trình mà bị lỗi là lỗi có thể thấy và sửa ngay được. Còn nếu chương trình chạy không đúng thì cần kiểm tra lại từng đoạn code, từng dòng code, hiểu rõ từng thứ mình viết ra thì mới mong sẽ tìm ra manh mối 🧐

🛠 Dùng các công cụ hỗ trợ kiểm tra lỗi(print, log, debugger)

In ra các dòng để hiển thị kết quả của biến, hay đơn giản là code có chạy vào đó không cũng là một cách debug. Thêm nữa hãy học cách dùng debugger là như hổ mọc thêm cánh luôn nhé 😎

Mời bạn ghé đọc thêm chi tiết ở [bài blog này][go-loi-chuong-trinh] của mình nhé.

[go-loi-chuong-trinh]: {{ "" | relative_url }}{% post_url debug/2020-06-20-go-loi-chuong-trinh %}

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

## Làm tròn số thực trong Python
Làm tròn số thực trong Python là chuyện thường ngày, và tụi mình sẽ sử dụng rất nhiều trong khi học Python cùng toán cũng như trong hiển thị các số thực với một số lượng các chữ số thập phân bất kỳ.

Có một số cách để làm tròn số thập phân:

– Dùng hàm `round()` Cách này sẽ làm tròn số `3.333333` thành `3.33` và số `3.5` sẽ giữ nguyên là `3.5`. 
`round(3.33333)` kết quả 3.33 `round(3.5)` kết quả 3.5 
Nếu bạn muốn bắt buộc có hai chữ số thập phân thì cách này chưa triệt để, kết quả cần là `3.50`

– Chuyển về định dạng chuỗi và cắt số ký tự đứng sau dấu `.` rồi chuyển về lại dạng số với ép kiểu qua float

`“{:.2f}”.format(3.5)` kết quả `“3.50”`

Lưu ý đây là chuỗi, muốn chuyển qua số bạn cần thực hiện ép kiểu từ string về số với `float()`

Nội dung này được tóm tắt từ [bài viết chia sẻ tips]
[lam-tron-dung-hai-chu-so-thap-phan-trong-python].

[lam-tron-dung-hai-chu-so-thap-phan-trong-python]: {{ "" | relative_url }}{% post_url python/2021-09-19-lam-tron-dung-hai-chu-so-thap-phan-trong-python %}

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

Bạn ghé đọc thêm các ví dụ cho từng đặc điểm ở [bài viết sau][ham-trong-python-la-first-class-object] nhé

[ham-trong-python-la-first-class-object]: {{ "" | relative_url }}{% post_url python/2022-10-10-ham-trong-python-la-first-class-object %}