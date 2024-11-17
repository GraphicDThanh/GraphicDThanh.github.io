---
title: "Chiếc máy tính PI(Python Interpreter)"
header:
  teaser: /assets/images/2020/05/2020-05-chiec-may-tinh-PI-cover.jpg
  og_image: /assets/images/2020/05/2020-05-chiec-may-tinh-PI-cover.jpg
excerpt_separator: <!--more-->
categories:
  - Đại Bản Doanh Python
tags:
  - python
last_modified_at: 2020-05-20T15:12:19-04:00
---

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-cover.jpg)
Chào mừng mọi người đến với phần [“The Python Tutorial”](https://graphicdthanh.github.io/python/2020/05/chiec-may-tinh-PI.html) của series “Khám phá Đại Bản Doanh Python”. The Python Tutorial mang đến những khái niệm và các tính năng cơ bản nhất của Python và cú pháp của nó.

Những nội dung trong bài series này từ chủ yếu mình lấy từ python.org rồi viết lại theo ngôn ngữ của mình.

## Khai vị với Python

→ Bạn đang cần cái gì đó có thể tự động giúp bạn hoàn thành một số công việc như là: tìm kiếm và thay thế một lượng lớn files hay đổi tên và sắp xếp lại một đống ảnh theo một cách nào đó.

→ Bạn là một là lập trình viên và đang làm việc với một số thư viện như C/C++/Java nhưng thấy chu trình ghi, biên dịch, kiểm tra rồi lại biên dịch riết rồi thấy chán vì nó chậm quá, rồi  bạn muốn tìm một bạn nào đó ngon lành và có thể mở rộng nó trên phần tiếp theo của dự án mình đang làm mà chạy nhanh hơn.

**Thứ bạn cần là Python đó, vì Python có thể giúp bạn:***

→ Viết tập script shell Unix hay batch files cho Windows để hoàn thành một công việc nào đó như là duyệt qua các files, thay đổi văn bản, …

→ Bạn có thể viết chương trình Python thành các mô-đun để dùng lại ở những nơi khác. Python cũng đi kèm với một bộ mô-đun tiêu chuẩn đã cung cấp sẵn để bạn sử dụng cho ứng dụng của mình hay đơn giản là dùng như những ví dụ thực thế khi học như là: file I/O, system call, sockets hay thậm chí là bộ mô-đun giành cho người dùng đồ họa như Tk.

→ Python sẽ giúp bạn tiết kiệm thời gian cho việc biên dịch hay kết nối, vì nó tự dịch rồi. Trình thông dịch còn là nơi mình hay dùng để kiểm tra những đoạn code nhỏ hay dùng để tính toán nhanh chóng.

**Chương trình Python thường ngắn và dễ đọc vì:**

→ không cần khai báo biến

→ nhóm lệnh được phân biệt bằng cách tab đầu dòng

**Chương trình Python có thể mở rộng với các bạn khác như C, C++**

Cuối cùng nhưng góp phần phá tang định kiến về Python(đối với mình) là tên bạn ấy được đặt theo một chương trình BBC có tên “Monty Python’s Flying Circus” chớ không có bất kỳ liên quan tới loài bò sát(con trăn – tiếng anh là python) đâu nghe!
Ơ cơ mà không phải cái logo nó hình hai con trăn hay sao (?!)

## Dùng luôn Python

### Gọi Python Interpreter(PI)

Có mấy cách giúp mình có thể gọi bạn này lên:

– Ở Windows: Gõ python ở Command Prompt

– Ở Linux: Gõ python3 ở cửa sổ Terminal

– Ở MacOS: Gõ python3 ở Terminal

Sau khi gọi được python interpreter lên, bạn sẽ thấy bạn đang ở primary prompt với ba dấu >>>, còn ba dấu … là thể hiện bạn đang ở secondary prompt, nơi những câu lệnh được tiếp tục viết.

Vì python phân biệt nhóm lệnh bằng tab đầu dòng nên với dấu … của nội dung trong nhóm lệnh nhớ tab vào nhé.

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-1-pi.webp)

### Xài Python như một chiếc máy tính nhỏ

#### Số(number)

Số trong Python:

→ cộng(+), trừ(-) , nhân(*) , chia(/), chia lấy nguyên(//), chia lấy dư(%), luỹ thừa(**)

→ nhóm phép toán với (), gán biến với =

→ _ : kết quả cuối cùng trả ra trong PI, dùng làm ký tự đại diện cho tính toán tiếp theo

Python hỗ trợ: số nguyên(int), số thực(float), số thập phân(decimal), phân số(fraction), số phức(complex), …

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-2-number.webp)

#### Chuỗi(string)

Trong Python, string được bọc bởi dấu ngáy đơn ‘ hoặc dấu nháy kép “. Khi chuỗi có nhiều dòng nó được bọc bởi cặp ba dấu nháy đơn hoặc cặp ba dấu nháy kép.

Ký tự đặt biệt có thể escape với dấu \, ví dụ \n trong string thể hiện sự xuống dòng.

Khi gọi print() với chuỗi, thì chuỗi sẽ được in kèm định dạng của nó, ví dụ print(‘a\nb’) sẽ in ra \n là xuống dòng. Muốn print không kèm định dạng, thêm r trước dấu nháy đầu tiên thể hiện print raw string .

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-3-string.webp)

→ Hai chuỗi có thể nối nhau bằng toán tử (+) hoặc hai chuỗi(literals – không chứa variable, phép toán) đứng gần nhau sẽ tự động nối vào nhau, ví dụ: ‘Py’ ‘thon’ sẽ nối thành ‘Python’

→ Chuỗi trong Python là sequence types(iterable, kiểu data có thể dùng for để loop qua từng phần tử của nó được), do đó nó có thể indexed(theo chỉ số index), index bắt đầu từ số 0, duyệt từ trái qua phải. Nếu nó là số âm, thì sẽ duyệt từ phải qua trái, ví dụ: a = ‘abcde’ thì a[0] là ‘a’, a[-1] là e.


Khi truy cập index lớn hơn giới hạn của chuỗi, sẽ raise error “IndexError“, nhưng khi slice chuỗi mới index trên thì vẫn bình thường, ví dụ: a[2:52] là ‘cde’.

Built-in function len() dùng cho chuỗi trả ra chiều dài của chuỗi đó.

→ Chuỗi trong Python là kiểu data immutable(bất biến, không thể thay đổi), do đó không thể gán giá trị cho chuỗi theo index, ví dụ: a = ‘abc’, không thể gán a[0] = ‘x’.

→ Chuỗi còn hỗ trợ slicing(cắt thành chuỗi con) với : , ví dụ: a = ‘abcde’ thì a[2:4] là ‘cd’, start là a[2] luôn luôn được lấy, end là a[4] luôn luôn bị loại. a[2] là ‘c’, a[4] là ‘e’.

Khi start không có [:2] thì nó lấy default là 0, khi end không có [2:] thì nó lấy end là chiều dài của chuỗi đang được sử dụng. Điều này đảm bảo a[:i] + a[i:] = a.

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-4-string-2.webp)

#### Danh sách(list)

Python biết có nhiều kiểu dữ liệu hỗn hợp(được sử dụng để nhóm những kiểu dữ liệu khác với nhau), trong đó sử dụng nhiều nhất là list, được bọc bởi hai dấu ngoặc vuông mở đóng và các giá trị cách nhau bởi dấu phấy, ví dụ: list_a = [1, 2, 3, 4].

List cũng là sequence types, nên list cũng có thể indexed and sliced như string được, len() trả ra chiều dài của list. Có thể shallow copy một list với list_a[:]

Nối hai list lại với nhau bằng toán tử + cũng được luôn

List là mutable type, cho nên có thể thay đổi nội dung của bạn ấy được:

– gán trí trị trực tiếp, ví dụ: list_a[2] = 8, thì list_a sẽ trở thành [1, 2, 8, 4]

– thêm một giá trị mới với append()

– gán với slice, ví dụ: list_a[1:3] = [8, 9] thì list_a là [1, 8, 9, 4], nếu gán list_a[1:3] = [] thì list_a sẽ thành [1, 4]

– clear list_a bằng cách gán list_a[:] = []

Ngoài ra, list có thể chứa nhiều list khác gọi là nested lists

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-4-list.webp)

### Lập trình cùng Python

Sau các phép toán đơn giản, là lúc bạn có thể tính toán phức tạp hơn, giải quyết nhiều bài toán khác nhau, và bước chân vào thế giới lập trình rồi đó.

Như mình có thể gán nhiều biến cùng lúc, ví dụ: a, b = 2, 3 thì a là 2 và b là 3

Rồi mình có thể dùng vòng lặp for, while để duyệt qua các sequences types(list, string, set, dict, …), nội dung trong vòng lặp sẽ quy định bằng khoảng cách là một tab.

Hoặc mình có thể viết những điều kiện với các dấu <, >, ==, <=, >=, !=

print function giúp mình in ra các giá trị để kiểm tra nữa

Từ những điều trên, bạn có thể viết một chương trình đơn giản rồi đấy.

![](/assets/images/2020/05/2020-05-chiec-may-tinh-PI-image-6-fibonanci.webp)

Hôm nay, tụi mình cùng tìm hiểu Python đến đây thôi.

Ở bài viết sau, mình sẽ qua bài thứ hai của phần “The Python Tutorial” thuộc sê ri vĩ đại “Khám phá Đại Bản Doanh Python”.