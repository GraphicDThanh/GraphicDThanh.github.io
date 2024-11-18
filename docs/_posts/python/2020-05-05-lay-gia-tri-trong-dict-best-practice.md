---
title: "Lấy giá trị trong dict sao cho xịn(Python best practices)"
header:
  teaser: /assets/images/2020/05/2020-05-lay-gia-tri-trong-dict-best-practice-cover.webp
  og_image: /assets/images/2020/05/2020-05-lay-gia-tri-trong-dict-best-practice-cover.webp
excerpt_separator: <!--more-->
categories:
  - Python
tags:
  - python
last_modified_at: 2020-04-29T15:12:19-04:00
---

## Mở bài
Khi làm việc với dictionary trong Python, có nhiều cách để tìm kiếm giá trị của "key" trong dictionary cũng như gán giá trị mặc định nếu "key" này chưa tồn tại.

Ví dụ mình có một dict là **person = {"name": "BeautyOnCode", "age": 28}**

Đây là các cách mình đã dùng để lấy giá trị của một key đã tồn tại:
```
person["name"]
```
Với một key chưa tồn tại, nếu dùng dict[key] sẽ gặp lỗi `KeyError: 'class'`
Khi đó, mình có thể dùng những cách sau để gán giá trị cho key chưa tồn tại như sau:

```python
if "class" in person:
        return person["class"]
else:
       person["class"] = 2
```

hoặc bắt cái lỗi như thế này:

```python
try:
       person["class"]
except KeyError:
       persone["class"] = 2
```
Nếu bạn giống mình, từng làm như trên, thì đây là bài post giành cho bạn.Vì cách còn nhiều cách hay ho hơn, ngắn gọn hơn mấy bạn ở trên, có thể bạn chưa biết nên cùng đọc tiếp nhé ^^
<hr>

Có hai phương thức liên quan đến việc gán giá trị mặc định với key chưa tồn tại là **dict.get(key[, value])** và **dict.setdefault(key, value)**.

Hai bạn ni khá là cool ngầu và được xem là best practice trong vụ lấy giá trị và gán giá trị mặc định cho dict.

Mình sẽ lần lượt giới thiệu kỹ cú pháp, cách dùng rồi so sánh hai bạn với nhau nữa.
## Thân bài
### dict.get(key[, value])
> **Hàm get() trả về giá trị của "key" nếu từ khoá này có trong dict.**
> Cú pháp: **dict.get(key[, value])**

Hàm này nhận tối đa hai biến truyền vào:

- **key** là từ khoá cần tìm trong dict

- **value(**optional - trường này không bắt buộc): là giá trị trả về nếu "key" không tìm thấy trong dict. Nếu không được gán, mặc định trả về **None**

Ví dụ:
![alt](https://beautyoncode.com/wp-content/uploads/2020/07/dict-get-function-1536x344.png)

Trong ví dụ trên:
```
>>> person.get("name")
```
Key "name" tồn tại trong dict person nên kết quả là giá trị của nó "BeautyOnCode"
```
>>> person.get("class")
```
Key "class" không tồn tại trong dict, và không có giá trị mặc định được gán nên trả ra None, nên person.get("class") is None là True
```
>>> person.get("class", 12)
```
Key "class" không tồn tại trong dict, và mình gán giá trị mặc định là 12 nên nó trả ra giá trị mặc định là 12

**Best practice**: Sử dụng **dict.get(key, default)** khi lấy giá trị trong dict và trả ra giá trị mặc định hoặc trả ra None có thể tránh viết code dài xử lý KeyErrror hay phải kiểm tra key tồn tại trong dict hay không như ví dụ ở đầu bài.

### dict.setdefault(key, value)

>**Hàm setdefault() trả về giá trị của "key" nếu từ khoá này có trong dict.** Nếu từ khoá "key" chưa có trong dict, dict sẽ được thêm từ khoá này với giá trị "value" truyền vào.
>Cú pháp: **dict.setdefaut(key[, value])**

Hàm này nhận tối đa hai biến truyền vào:

- **key** là từ khoá cần tìm trong dict

- **value**(optional - trường này không bắt buộc): "key" với giá trị "value" sẽ được gán vào dict nếu không tìm thấy "key" trong dict. Nếu không có "value", mặc định giá trị là None.

**Lưu ý**: Nếu giá trị của key đã có, thì giá trị mặc định sẽ không được gán nữa

Ví dụ:
![](https://beautyoncode.com/wp-content/uploads/2020/07/Screen-Shot-2020-07-03-at-6.44.13-PM.png)

Trong ví dụ trên:
```
>>> person.setdefault("class")
```
Key "class" chưa tồn tại nên gán giá trị mặc định cho bạn ấy là None, vì không có giá trị mặc định được truyền vào
```
>>> person.setdefault("class", 12)
```
Key "class" đã tồn tại với giá trị là "None" cho nên lúc này không nhận setdefault nữa.

Do đó hàm này chỉ hoạt động lúc key chưa tồn tại thôi.

**Best practice**: Sử dụng dict.setdefault(key, value) khi khởi tạo dict có thể tránh việc set giá trị mặc định bằng if ... else.

 Ví dụ:

Thay vì viết:

```
if "subjects" not in person:
      subjects = []
else:
   subjects.append("math")
```
Nay mình viết
```
person.setdefault("subjects", []).append("math")
```
Bạn có thấy nó ngầu hơn hẳn không :D

Bạn đã thấy hai hàm ni khác nhau ở đâu chưa? Mình nghĩ bạn đã đoán được, cùng kiểm tra lại nhé!

### So sánh

#### Điểm tương đồng
Khi làm việc với key chưa tồn tại trong dictionary, hai hàm này đều trả về giá trị mặc định mình mong muốn return.

Ví dụ bên dưới cho thấy cả hai cách đều giúp trả ra giá trị b là 'Thanh'
![](https://beautyoncode.com/wp-content/uploads/2020/07/Screen-Shot-2020-07-03-at-10.59.43-PM.png)

#### Điểm khác biệt
Tuy nhiên, sự khác biệt ở đây là:

Hàm **.setdefault()** sẽ thêm giá trị default kèm từ khoá vào dict, và chỉ được gán lần đầu tiên(khi key không tồn tại)

Do đó, hàm .setdefault() sẽ tương ứng với đoạn code này:
```
if 'key' not in dict:
   dict['key'] = value
return dict['key']
```
Hàm **.get(key, value)** sẽ không thêm giá trị cho key đó vào dict, chỉ trả ra kết quả default mong đợi thôi.

Còn hàm .get(key, value) sẽ tương ứng với đoạn code này:
```
if 'key' not in dict:
   return value
else:
   return dict['key']
```
Đây là kết quả dict a của ví dụ trên:
![](https://beautyoncode.com/wp-content/uploads/2020/07/Screen-Shot-2020-07-03-at-11.07.29-PM.png)

## Kết bài
Bài post đến đây tạm hết rồi, học làm Pythonista cũng đâu khó lắm đâu mọi người nhỉ, chỉ cần mình để ý xíu là có thể cải thiện từ những đoạn code nho nhỏ như thế này rồi.
