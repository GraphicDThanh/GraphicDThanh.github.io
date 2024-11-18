---
title: "Hàm trong Python là first-class object"
categories:
  - Python
tags:
  - python
  - function
---
![](/images/2022/10/2022-10-ham-trong-python-la-first-class-object-cover.webp)

## Vậy first-class object là gì?

> **first-class object** là một thực thể (entity) được gán vào biến, lưu trữ trong các loại dữ liệu, hay sử dụng như một đối số truyền vào hàm khác, và thậm chí là trả về chúng từ hàm khác.

Việc hiểu hàm là một first-class object sẽ giúp bạn dễ tiếp thu hơn các khái niệm khác như lambda hay decorators.

Cùng xem các ví dụ về hàm là first-class object bên dưới nhé!

Ví dụ mình có hàm:

```python
def say(text):
    return f"{text} !"
```

## Hàm là đối tượng

Có thể gán biến `greet` với giá trị là hàm `say`

```python
greet = say
greet("hello")
```

## Hàm có thể sử dụng trong cấu trúc dữ liệu

Có thể lưu các hàm vào một mảng:

```python
funcs = [say, greet]
for f in funcs:
    f("hello")
```

## Hàm có thể được truyền vào hàm khác như tham số

Hay được gọi là **high-order function**

```python
def call(say):
    call = say("are you there ?")
    print(call())

call(say)  # are your there?
```

## Hàm có thể lồng nhau

Cho phép định nghĩa hàm trong hàm, hay gọi là `inner function` hay `nested function`.

```python
def greet():
    def say_hi():
        print("Hi")

    return say_hi()

greet()  # Hi
```

Hàm `say_hi` không thể được gọi từ bên ngoài.

Nếu muốn gọi từ bên ngoài thì có thể trả về hàm để gọi:

```python
def greet(context, name):
    def say_hi(name):
        print(f"Hi, {name}")

    def say_morning(name):
        print(f"Good morning, {name}")

    if context == "hi":
        return say_hi
    if context == "morning":
        return say_morning


say_hi = greet("hi", "BeautyOnCode")
say_hi()  # Hi, BeautyOnCode
say_morning = greet("morning", "BeautyOnCode")
say_morning()  # Good morning, BeautyOnCode
```

## Hàm có thể truy cập các biến cục bộ
(hay gọi là lexical closures hoặc closures)

Tức biến name của `say_hi` , `say_morning` có thể sử dụng từ bên ngoài hàm `greet` .

Ví dụ trên có thể viết ngắn gọn lại như sau:

```python
def greet(context, name):
    def say_hi():
        print(f"Hi, {name}")

    def say_morning():
        print(f"Good morning, {name}")

    if context == "hi":
        return say_hi
    if context == "morning":
        return say_morning


say_hi = greet("hi", "BeautyOnCode")
say_hi()  # Hi, BeautyOnCode
say_morning = greet("morning", "BeautyOnCode")
say_morning()  # Good morning, BeautyOnCode
```

## Đối tượng có thể có hành vi giống hàm

Object không phải là `function` trong Python, nhưng chúng vẫn có thể được gọi như `function`.

```python
class SumWith:
    def __init__(self, a):
        self.a = a

    def __call__(self, b):
        return print(self.a + b)

# Gọi tính tổng 3 và 4
sum_with_three = SumWith(3)
sum_with_three(4)  # 7
```

Khi gọi `SumWith(3)`, hàm `__call__` sẽ được gọi.

Để kiểm tra một đối tượng có gọi được không, có thể sử dụng hàm built-in `callable`

```python
callable(sum_with_three)  # True
callable(True)  # False
```

Trên đây là một số tóm tắt từ bài viết hữu ích từ [Dan Bader](https://dbader.org/blog/python-first-class-functions).

