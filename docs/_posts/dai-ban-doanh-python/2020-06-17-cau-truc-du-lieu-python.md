---
layout: post
title:  "Cấu trúc dữ liệu​ trong Python"
date:   2020-06-17 10:00:00 +0700
categories: python, dai-ban-doanh-python
---
![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-cover.webp)

Chào mừng mọi người đến với bài post tiếp theo của phần [“The Python Tutorial”](https://docs.python.org/3/tutorial/) của series [Khám phá Đại Bản Doanh Python](https://graphicdthanh.github.io/python/dai-ban-doanh-python/2020/07/dai-ban-doanh-python-series-overview.html). The Python Tutorial mang đến những khái niệm và các tính năng cơ bản nhất của Python và cú pháp của nó.

Mình đã biết qua về những công cụ điều khiển luồng dữ liệu và hàm ở [bài trước](https://graphicdthanh.github.io/python/dai-ban-doanh-python/2020/03/dieu-khien-luong-du-lieu-python.html). Trong bài này, mình học tiếp về các cách mà Python có thể giúp mình lưu trữ những dạng dữ liệu khác nhau nhé.

(Những nội dung trong bài series này từ chủ yếu mình lấy từ python.org rồi viết lại hoặc dịch lại theo ngôn ngữ của mình)

## Cấu trúc dữ liệu

Cấu trúc dữ liệu là cách Python giúp tụi mình thể hiện, sắp xếp dữ liệu như thế nào.

Python có nhiều dạng cấu trúc khác nhau như: list, tuples, set, dictionary. Mỗi loại này sẽ thích hợp để thể hiện những dạng dữ liệu khác nhau tuỳ vào đặc điểm của loại dữ liệu đó.

Note: Trong PI(Python Interpreter), để kiểm tra những thuộc tính của như phương thức của một giá trị ta dùng dir() hoặc help() để xem tài liệu liên quan đến nó.

### Lists(danh sách)

List là kiểu dữ diệu danh sách, kiểm tra nhanh cách phương thức được hỗ trợ bởi list bằng lệnh **dir()** ta thấy có **.append(), .clear(), .copy(), .extend(), .index(), .insert(), .pop(), .remove(), .reverse(), .sort()** là các phương thức chính.

Lưu ý nho nhỏ ở đây mình không nói đến những phương thức đặt biệt trong Python, những phương thức bắt đầu và kết thúc bằng __ như "__add__()", "__str__()". Mời bạn đọc thêm về các phương thức đặt biệt này tại [Special Method Names.](https://docs.python.org/3/reference/datamodel.html#special-method-names)

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-1-list.webp)

Để biết rõ hơn các phương thức trên hoạt động ra sao, mình dùng **help()** để xem tài liệu về chúng.

Bạn có thấy đối số đặt biệt **/** bên dưới chứ, hi vọng bạn biết chúng dùng để làm gì ^^(nếu chưa rõ mời bạn ghé đọc phần Function trong [bài này](https://graphicdthanh.github.io/python/dai-ban-doanh-python/2020/03/dieu-khien-luong-du-lieu-python.html) nhé)

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-2-list-2.webp)

Một vài cách tiếp cận tương đương:

> **list.append(x)** tương đương với a[len(a):] = [x] hoặc a.insert(len(a), x)
>
> **list.extend(iterable)** tương đương a[len(a):] = iterable
>
> **list.clear()** tương đương với del a[:]
>
> **list.copy()** tương đương với a[:]
>
> **list.pop(x)** sẽ xoá một giá trị có index là x ra khỏi list và trả về giá trị đó
>
>còn **del(a[x])** sẽ đi xoá giá trị có index là x của list a, hoặc có thể xoá cả list a với **del(a)**.

Những phương thức gọi có thể gây lỗi như **list.remove(x)**, **list.index(x)** raise **ValueError** nếu x không tồn tại.

Những phương thức như **insert(), remove(), sort()** trả về **None**(vì làm thay đổi các dữ liệu gốc)

Với list, ta có thể sử dụng nó như là một **ngăn xếp(stack)**, thêm giá trị vào ngăn xếp với **append()**, lấy giá trị mới nhất được thêm vào ra ngoài ngăn xếp bằng **pop()**.

Với list, cũng có thể dùng như một **hàng đợi(queue)**, thêm giá trị vào hàng đợi với **append()**, lấy bạn đợi lâu nhất ra trước với **popleft()**.

Ngoài ra, **list comprehension** là cách tạo list đơn ngắn gọn, ví dụ: nu**mbers = [x for x in range(10)]** sẽ tương đương với

>
> numbers = []
>
> for x in range(10):
>
>      number.append(x)

### Tuples

Tuple cũng là một kiểu dữ kiệu chuỗi và các giá trị được bọc bên trong hai dấu ngoặc đơn ngăn cách bằng dấu phẩy, ví dụ: a = (‘hi’, ‘there’)

Tuple tương tự như list, chỉ khác là tuple là kiểu dữ liệu **immutable**(không thay đổi được), còn list thì **mutable**(có thể thay đối).

Là kiểu dữ liệu immutable nhưng tuple có thể chứa các dữ liệu mutable được, ví dụ: b = ([1,2], [3,4])

Tuple có khả năng **packing**(tự nối lại được), như sau: *a = ‘hi’, ‘there‘* hay *c = ‘hi’*

(chú ý dấu phẩy ở cuối trong trường hợp tuple chỉ chứa một phần tử con)

Và ngược lại, nó cũng có khả năng unpacking(tự tách ra được):** x, y = a** thì x sẽ có giá trị là ‘hi’ và y là ‘there’.

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-3-tuple.webp)

tuple là kiểu dữ liệu không thay đổi được nên nó chỉ có phương thức **count()** và **index()**

### Sets

Set là bộ sưu tập không theo thứ tự các phần tử không trùng nhau, được bọc bởi hai dấu ngoặc nhọn **{}** hoặc khởi tạo bằng **set()**.

Set có hỗ trợ các phương thức của tổ hợp như là phép toán giao, phép toán hợp, phép đối xứng, phép loại trừ.

Set có hỗ trợ set comprehensions.

*Lưu ý không khởi tạo set rỗng bằng {} được, phải dùng set(), vì {} thể hiện cho kiểu dữ liệu dict*

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-4-set-1.webp)

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-5-set-2.webp)

### Dictionary(từ điển)

Nếu như list, tuple, set là các kiểu dữ liệu có thứ tự là các chữ số thì dict là kiểu dữ liệu có thứ tự là các từ khoá, và từ khoá là kiểu dữ liệu immutable như strings, numbers, tuples(không chứa giá trị mutable).

Có thể hiểu đơn giản dictionary là một bộ sưu tập của các giá trị **key: value**, với điều kiện key là không trùng nhau.

Dict khai báo với **dict()** hoặc **{}**, ví dụ: **dict(name=’Thanh’)** hay **{‘name’: ‘Thanh’}**

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-6-dict-1.webp)

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-7-dict-2.webp)

### Kỹ thuật lặp qua các loại dữ liệu có trình tự

Ta thường làm việc với các loại dữ liệu có trình tự bằng cách duyệt qua tất cả các phần tử của nó với **for** và kết hợp:

→ dùng **.items()** để lặp qua key, value của một dictionary

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-8-loop-1.webp)

→ dùng **enumerate**([‘a’, ‘b’, ‘c’]) để lặp qua chỉ số index và giá trị của chỉ số đó trong một list
![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-9-loop-2.webp)

→ dùng **zip()** có thể lặp qua nhiều loại dữ liệu trình tự, ví dụ: zip([1, 2, 3], [‘a’, ‘b’, ‘c’])

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-10-loop-3.webp)

→ dùng **reversed()** có thể lặp theo thứ tự ngược lại

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-11-loop-4.webp)

→ dùng **sorted()** có thể tạo list mới theo thứ tự mà không làm thay đổi mảng ban đầu.

![](/assets/images/2020/06/2020-06-cau-truc-du-lieu-python-image-12-loop-5.webp)

### Các dạng so sánh

Trong các câu lệnh điều kiện, thường đi cùng với các dạng so sánh:

→ bằng/lớn hơn/nhỏ hơn với “**==**“,  “**>**“, “**<**“

→ giá trị thuộc một kiểu dữ liệu có trình tự với “**in**“, “**not in**“

→ so sánh hai đối tượng với “**is**” hoặc “**is not**“

Kết hợp nhiều dang so sánh với nhau bằng “**and**“, “**or**“. Phủ định bằng “**not**“.



Bài học cơ bản về các kiểu dữ liệu trong Python đến đây là hết rồi.

Ở bài viết sau, mình sẽ đi học tiếp về “mô-đun, các dữ liệu vào/ra kết hợp quản lý lỗi và các ngoại lệ” trong Python.

“The Python Tutorial” thuộc sê ri “Khám phá Đại Bản Doanh Python” học mãi vẫn chưa hết, cố lên nào!