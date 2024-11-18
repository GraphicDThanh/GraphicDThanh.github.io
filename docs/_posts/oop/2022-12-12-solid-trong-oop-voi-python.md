---
title: "Nguyên tắc SOLID trong lập trình hướng đối tượng (OOP) - thực hành cùng ngôn ngữ Python"
categories:
  - OOP
tags:
  - oop
  - solid
  - python
---
![](/images/2022/12/2022-12-solid-trong-oop-voi-python-cover.webp)

## SOLID là gì?

SOLID là 5 nguyên tắc nền tảng trong lập trình hướng đối tượng OOP (Object Oriented Programming)

SOLID giúp thiết kế chương trình hướng đối tượng linh động, dễ hiểu và dễ duy trì.

SOLID là viết tắt của 5 chữ cái đầu của mỗi nguyên tắc sau:

- S: Single Responsibility Principle (SRP)

- O: Open-Closed principle (OCP)

- L: Liskov Substitution Principle (LSP)

- I: Interface Segregation Principle (ISP)

- D: Dependency Inversion Principle (DIP)

## SOLID theo hướng thực hành cùng Python
Trong bài viết này, sẽ bắt đầu với chương trình Python và lần lượt đi qua từng loại nguyên tắc trên.

Cụ thể là lý do vì sao lại vi phạm nguyên tắc đó và cách thiết kế lại code để chương trình không vi phạm nữa.

Qua đó, giúp cải thiện kỹ năng lập trình hướng đối tượng của bạn.

---

Giới thiệu chương trình:

Trong một ứng dụng mua hàng, có lớp Order (đơn hàng) chứa:

Các thuộc tính:

– items (hàng hóa)

– quantities (số lượng)

– prices (giá cả)

– status (trạng thái)

Các phương thức:

– add_item: thêm một sản phẩm gồm name, quantity, price vào đơn hàng

– pay: tiến hành thanh toán với phương thức thanh toán và mã bảo mật

```python
class Order:
    items = []
    quantities = []
    prices = []
    status = "open"

    def add_item(self, name, quantity, price):
        self.items.append(name)
        self.quantities.append(quantity)
        self.prices.append(price)

    def total_price(self):
        total = 0
        for i in range(len(self.prices)):
            total += self.quantities[i] * self.prices[i]

        return total

    def pay(self, payment_type, security_code):
        if payment_type == "debit":
            print("Processing debit payment type")
            print(f"Verifying security code: {security_code}")
            self.status = "paid"
        elif payment_type == "credit":
            print("Processing credit payment type")
            print(f"Verifying security code: {security_code}")
            self.status = "paid"
        else:
            raise Exception(f"Unknown payment type: {payment_type}")


order = Order()
order.add_item("Macbook Pro", 1, 600)
order.add_item("Keyboard", 1, 100)
order.add_item("iphone X", 1, 400)

print(order.total_price())
order.pay("debit", "13454356")
```

Chương trình trên cũng:

– tạo một đối tượng order và thêm 3 sản phẩm với tên, số lượng và giá cả của từng sản phẩm.

– in ra tổng số tiền của đơn hàng

– tiến hành thanh toán với phương thức thanh toán debit

Kết quả in ra:

```
1100
Processing debit payment type
Verifying security code: 13454356
```

## Nguyên tắc S: Single responsibility principle
### Nội dung nguyên tắc
Trước tiên, cùng tìm hiểu nội dung của nguyên tắc bắt đầu bằng chữ S, hay Single responsibility principle (SRP) từ Wikipedia:

> The Single-responsibility principle:
>
> “There should never be more than one reason for a class to change.” In other words, every class should have only one responsibility.

Tạm dịch: Mỗi lớp đối tượng chỉ nên có một lý do để thay đổi. Đồng nghĩa với, mỗi lớp đối tưởng chỉ nên có một trách nhiệm duy nhất.

Nguyên tắc này chỉ ra mỗi lớp hay phương thức chỉ nên có một trách nhiệm duy nhất.

Nhờ đó, khi thay đổi chúng cũng được thay đổi với một mục đích nhất định, và có thể dễ dàng sử dụng lại ở nhiều nơi.

### Thực hành
#### Giải thích lý do vi phạm
Quan sát ví dụ trên, class Order chứa phương thức add_item, tính total_price là hợp lý vì cả hai đều liên quan đến đơn hàng.

Nhưng pay thì nên tách ra riêng biệt vì phụ thuộc vào các yếu tố không thuộc về order như các loại phương thức thanh toán payment_type.

Nên đoạn code này vi phạm nguyên tắc SRP.

#### Cải thiện
Để cải thiện, tách riêng payment ra một lớp riêng biệt gọi là PaymentProcesser.

Lớp này có các phương thức thanh toán là từng phương thức riêng biệt.

Đồng thời xóa phương thức pay ở Order.

Code sẽ thay đổi như sau:

```python
# ...

class PaymentProcessor:
    def pay_credit(self, order, security_code):
        print("Processing debit payment type")
        print(f"Verifying security code: {security_code}")
        order.status = "paid"

    def pay_debit(self, order, security_code):
        print("Processing credit payment type")
        print(f"Verifying security code: {security_code}")
        order.status = "paid"

# ...
print(order.total_price())
processor = PaymentProcessor()
processor.pay_debit(order, "13454356")
```

Và thay vì gọi order.pay(…) như cũ thì sẽ tạo một đối tượng cho phương thức thanh toán và gọi đến phương thức thanh toán pay_debit.

Kết quả vẫn vậy, nhưng code đã không còn vi phạm nguyên tắc S nữa.

## Nguyên tắc O - Open-closed principle

Nguyên tắc bắt đầu bằng chữ O, hay Open-closed principle (OCP) từ Wikipedia:

### Nội dung nguyên tắc

> The Open–closed principle:
> Software entities … should be open for extension, but closed for modification.

Tạm dịch: Các thực thể phần mềm chỉ nên mở rộng để kế thừa và không nên chỉnh sửa.

Nguyên tắc này chỉ ra các thực thể phần mềm như lớp đối tượng khuyến khích mở rộng ra bằng cách kế thừa chứ không nên chỉnh sửa code đã có sẵn.

### Thực hành
#### Giải thích lý do vi phạm
Cũng với ví dụ trên, nếu một phương thức thanh toán mới được thêm vào, ví dụ như paypal, thì cần phải thêm một phương thức mới vào lớp PaymentProcessor.

Điều này sẽ vi phạm nguyên tắc OCP này vì đã chỉnh sửa lớp PaymentProcessor.

#### Cải thiện
Để xử lý mà không vi phạm nguyên tắc OCP, có thể tạo thêm lớp trừu tượng PaymentProccessor với phương thức pay là một abstractmethod.

Và sử dụng lớp này để mở rộng ra tạo các lớp cụ thể hơn cho từng loại phương thức thanh toán như DebitPaymentProcessor và viết phương thức pay riêng của mình.

```python
from abc import ABC, abstractmethod

# ...
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order, security_code):
        pass

class DebitPaymentProcessor(PaymentProcessor):
    def pay(self, order, security_code):
        print("Processing debit payment type")
        print(f"Verifying security code: {security_code}")
        order.status = "paid"

class CreditPaymentProcessor(PaymentProcessor):
    def pay(self, order, security_code):
        print("Processing credit payment type")
        print(f"Verifying security code: {security_code}")
        order.status = "paid"

# ...

print(order.total_price())
processor = DebitPaymentProcessor()
processor.pay(order, "13454356")
```

Thiết kế như vậy thì khi sử dụng sẽ thay đổi thành tạo DebitPaymentProcessor() và gọi phương thức pay của nó.

Đồng thời với phương thức thanh toán mới, paypal, có thể mở rộng từ PaymentProcessor với tên PaypalPaymentProcessor. Đồng thời viết phương thức pay riêng cho paypal mà không thay đổi code có sẵn.

Như vậy sẽ không phạm vào nguyên tắc OCP nữa.

```python
class PaypalPaymentProcessor(PaymentProcessor):
    def pay(self, order, security_code):
        print("Processing credit payment type")
        print(f"Verifying security code: {security_code}")
        order.status = "paid"
```

## Nguyên tắc L - Liskov substitution principle
### Nội dung nguyên tắc
Nguyên tắc bắt đầu bằng chữ L, hay Liskov principle (LSP) từ Wikipedia:

> The Liskov substitution principle:
>
> Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

Tạm dịch: Các đối tượng hay phương thức của lớp con (lớp dẫn xuất) có thể sử dụng thay thế đối tượng hay phương thức của lớp cha mà không có lỗi.

Nguyên tắc này chỉ ra một lớp con nên sử dụng thay thế lớp cha mà không làm trái ý nghĩa của lớp cha hay thậm chí gây lỗi.

### Thực hành
#### Giải thích lý do vi phạm
Giả sử với phương thức thanh toán Paypal, cách xử lý thanh toán có khác với các loại thẻ, thay vì security_code lại cần dùng email.

Khi đó, giá trị email sẽ được truyền vào vào giá trị của biến security_code như thế này:

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order, security_code):
        pass

class PaypalPaymentProcessor(PaymentProcessor):
    def pay(self, order, security_code):
        print("Processing credit payment type")
        print(f"Verifying email address: {security_code}")
        order.status = "paid"


order = Order()
order.add_item("Macbook Pro", 1, 600)
order.add_item("Keyboard", 1, 100)
order.add_item("iphone X", 1, 400)

print(order.total_price())
processor = DebitPaymentProcessor()
processor.pay(order, "user@domain.com")
```

Tuy nhiên với cách này thì security_code của paypal sẽ không có ý nghĩa mà lớp cha PaymentProcessor mong đợi.

Điều này sẽ làm vi phạm nguyên tắc LSP vì lớp con PaypalPaymentProcessor sử dụng biến security_code như là email không có cùng ý nghĩa với lớp cha là mã bảo mật.

#### Cải thiện
Để xử lý không vi phạm nguyên tắc LSP, tại đây cần xóa security_code ra khỏi lớp cha PaymentProcessor. Đồng thời, chuyển đổi bạn ấy vào biến khởi tạo cho từng lớp con cần bạn là CreditPaymentProcessor và DebitPaymentProcessor.

Còn lớp PaypalPaymentProcessor, khởi tạo với biến email_address dành riêng cho phương thức thanh toán này.

Code sẽ thay đổi như bên dưới:

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order):
        pass

class DebitPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def pay(self, order):
        print("Processing debit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class CreditPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def pay(self, order):
        print("Processing credit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class PaypalPaymentProcessor(PaymentProcessor):
    def __init__(self, email_address):
        self.email_address = email_address

    def pay(self, order):
        print("Processing credit payment type")
        print(f"Verifying email address: {self.email_address}")
        order.status = "paid"


order = Order()
order.add_item("Macbook Pro", 1, 600)
order.add_item("Keyboard", 1, 100)
order.add_item("iphone X", 1, 400)

print(order.total_price())
processor = PaypalPaymentProcessor("user@domain.com")
processor.pay(order)
```

Sau khi xử lý như vậy, có thể thấy lớp con không làm thay đổi ngữ nghĩa của lớp cha nữa. Do đó không còn phạm nguyên tắc LSP.

## Nguyên tắc I - Interface segregation principle
### Nội dung nguyên tắc
> The Interface segregation principle:
>
> Clients should not be forced to depend upon interfaces that they do not use.

Tạm dịch: Một lớp con (lớp trích xuất) không nên bắt buộc kế thừa những phương thức interface mà nó không sử dụng. Nên tách nhỏ ra nhiều interface để kế thừa đúng cái cần mà thôi.

Nguyên tắc này chỉ ra rằng nếu một lớp con được trích xuất từ lớp cha nhưng không sử dụng hết các phương thức của lớp cha. Hay các phương thức này lớp con bắt buộc phải kế thừa nhưng bị thừa.

Thì đây, chính là lúc bạn cần tách ra nhiều interface với mục đích cụ thể khác nhau để lớp con chỉ kế thừa những cái bạn cần, thay vì một interface chung lớn.

### Thực hành

Giả sử có thêm phương thức xác minh qua tin nhắn, auth_sms trong lớp PaymentProcessor chịu trách nhiệm nhân vào mã code và tiến hành xác minh danh tính.

Nếu đã xác minh, verified = True thì cho phép tiến hành thanh toán. Và ngược lại, sẽ báo lỗi chưa được xác minh.

Tuy nhiên, xác minh SMS lại không áp dụng cho phương thức thanh toán credit card. Do đó, sẽ báo lỗi là không hỗ trợ xác minh SMS với credit card payment.

Đoạn code cho tình huống này như sau:

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order):
        pass

    @abstractmethod
    def auth_sms(self, code):
        pass



class DebitPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def auth_sms(self, code):
        print(f"Verifying SMS code {code}")
        self.verified = True

    def pay(self, order):
        if not self.verified:
            raise Exception("Not authorized")
        print("Processing debit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class CreditPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def auth_sms(self, code):
        raise Exception("Credit card payments don't support SMS code authorization.")

    def pay(self, order):
        print("Processing credit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"
```

Lớp PaypalPaymentProcessor tương tự với DebitPaymentProcessor nên mình sẽ tạm không ghi lại.

Trong tình huống này, thì lớp CreditPaymentProcessor đã không cần sử dụng auth_sms, cái được kế thừa từ lớp cha PaymentProcessor.

Do đó, đoạn code trên vi phạm nguyên tắc ISP.

#### Cải thiện

Khi lớp con không dùng đến phương thức của lớp cha nữa, thì chính là lúc nên tách lớp cha ra nhiều interface khác nhau.

Tạo một lớp mới trích xuất từ PaymentProcessor với tên PaymentProcessor_SMS và chuyển phương thức auth_sms vào đây.

Lớp DebitPaymentProcessor và lớp PaypalPaymentProcessor sẽ được kế thừa từ PaymentProcessor_SMS vì cần sử dụng auth_sms.

Còn CreditPaymentProcessor sẽ không cần xử lý auth_sms vì nó không còn ở lớp PaymentProcessor nữa.

Code sẽ thay đổi thành:

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order):
        pass

class PaymentProcessor_SMS(PaymentProcessor):
    @abstractmethod
    def auth_sms(self, code):
        pass

class DebitPaymentProcessor(PaymentProcessor_SMS):
    def __init__(self, security_code):
        self.security_code = security_code
        self.verified = False

    def auth_sms(self, code):
        print(f"Verifying SMS code {code}")
        self.verified = True

    def pay(self, order):
        if not self.verified:
            raise Exception("Not authorized")
        print("Processing debit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class CreditPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def pay(self, order):
        print("Processing credit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class PaypalPaymentProcessor(PaymentProcessor_SMS):
    def __init__(self, email_address):
        self.email_address = email_address
        self.verified = False

    def auth_sms(self, code):
        print(f"Verifying SMS code {code}")
        self.verified = True

    def pay(self, order):
        if not self.verified:
            raise Exception("Not authorized")
        print("Processing credit payment type")
        print(f"Verifying email address: {self.email_address}")
        order.status = "paid"
```

Code trên đã sạch hơn, tuy nhiên việc xác minh SMS vẫn đang thuộc quá trình payment. Có thể áp dụng composition để tách quá trình này ra thêm một interface riêng chỉ dùng để xác thực, đặt tên class mới là Auth_SMS thực hiện quá trình xác thực này riêng biệt.

Sau đó từng lớp payment cụ thể sẽ được truyền vào một authorizer tương ứng giúp xác thực.

```python
class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, order):
        pass

class SMS_Auth:
    authorized = False

    def verify_code(self, code):
        print(f"Verifying code {code}")
        self.authorized = True

    def is_authorized(self) -> bool:
        return self.authorized


class DebitPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code, authorizer: SMS_Auth):
        self.security_code = security_code
        self.authorizer = authorizer

    def pay(self, order):
        if not self.authorizer.is_authorized():
            raise Exception("Not authorized")
        print("Processing debit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"

class CreditPaymentProcessor(PaymentProcessor):
    def __init__(self, security_code):
        self.security_code = security_code

    def pay(self, order):
        print("Processing credit payment type")
        print(f"Verifying security code: {self.security_code}")
        order.status = "paid"


class PaypalPaymentProcessor(PaymentProcessor):
    def __init__(self, email_address, authorizer):
        self.email_address = email_address
        self.authorizer = authorizer

    def pay(self, order):
        if not self.authorizer.is_authorized():
            raise Exception("Not authorized")
        print("Processing credit payment type")
        print(f"Verifying email address: {self.email_address}")
        order.status = "paid"


order = Order()
order.add_item("Macbook Pro", 1, 600)
order.add_item("Keyboard", 1, 100)
order.add_item("iphone X", 1, 400)

print(order.total_price())
authorizer = SMS_Auth()
processor = PaypalPaymentProcessor("user@domain.com", authorizer)
processor.pay(order)
```

Cách xử lý này sẽ tách ra nhiều interface với các mục đích riêng và tái sử dụng ở lớp con. Do đó, không còn vi phạm nguyên tắc ISP nữa.

## Nguyên tắc D - Dependency inversion principle
### Nội dung nguyên tắc
> The Dependency inversion principle:
>
> Depend upon abstractions, [not] concretions.

Tạm dịch: Các mô-đun cấp cao không nên phụ thuộc vào module cấp thấp. Nếu có sự phụ thuộc thì cả hai nên phụ thuộc vào abstraction hay interface.

Nguyên tắc này chỉ ra các lớp không nên phụ thuộc lẫn nhau, mà nên xây dựng interface để phụ thuộc.

### Thực hành
#### Giải thích lý do vi phạm
Giả sử có thêm một phương thức authorizer nữa là xác minh không phải là robot đang sử dụng (có thể bằng capcha hoặc chọn hình ảnh liên quan). Thì sẽ cần phải thay đổi authorizer không sử dụng SMS_Auth nữa.

Đoạn code ở trên, bạn có thể thấy lớp PaypalPaymentProcessor đang phụ thuộc vào lớp SMS_Auth.

Do đó sẽ vi phạm nguyên tắc DIP.

#### Cải thiện
Xây dựng một lớp abstract đại diện cho Authorizer với phương thức is_authorized.

Thì với cách xác minh không phải là robot, sẽ tạo một lớp mở rộng từ Authorizer, đặt tên NotARobot_Auth và xác minh theo cách riêng biệt với phương thức not_a_robot.

Đồng thời, authorizer sẽ có loại là Authorizer thay vì SMS_Auth. Thì có thể thích nghi với cả SMS_Auth hay NotARobot_Auth.

Code sẽ thay đổi thành:

```python
class Authorizer(ABC):
    @abstractmethod
    def is_authorized(self, order):
        pass

class SMS_Auth(Authorizer):
    authorized = False

    def verify_code(self, code):
        print(f"Verifying code {code}")
        self.authorized = True

    def is_authorized(self) -> bool:
        return self.authorized

class NotARobot_Auth(Authorizer):
    authorized = False

    def not_a_robot(self):
        print(f"Are you a robot? Naaaa ...")
        self.authorized = True

    def is_authorized(self) -> bool:
        return self.authorized


class PaypalPaymentProcessor(PaymentProcessor):
    def __init__(self, email_address, authorizer: Authorizer):
        self.email_address = email_address
        self.authorizer = authorizer

    def pay(self, order):
        if not self.authorizer.is_authorized():
            raise Exception("Not authorized")
        print("Processing credit payment type")
        print(f"Verifying email address: {self.email_address}")
        order.status = "paid"

# ...

print(order.total_price())
authorizer = NotARobot_Auth()
processor = PaypalPaymentProcessor("user@domain.com", authorizer)
authorizer.not_a_robot()
processor.pay(order)
```

Code trên đã không còn vi phạm nguyên tắc DIP nữa vì cả lớp con như PaypalPaymentProcessor hay lớp SMS_Auth đều không phụ thuộc vào nhau nhưng phụ thuộc vào interface Authorizer.

---

Nếu bạn đọc đến đây thì là bạn thực sự muốn tìm hiểu về SOLID, cảm ơn bạn ^^

5 nguyên tắc của SOLID cùng các ví dụ thực hành bên trên sẽ giúp bạn lập trình hướng đối tượng hiệu quả hơn, code sạch và dễ mở rộng và bảo trì.

Khi nắm rõ các nguyên tắc này, hãy bắt tay vào cải thiện từng phần một để nâng cao kỹ năng code nhé.

Các ví dụ trong bài viết này mình sử dụng từ video “[Uncle Bob’s SOLID principles made easy 🍀 – in Python!](https://www.youtube.com/watch?v=pTB30aXS77U)”, bạn có thể ghé xem kênh này có nhiều video về Python rất hay.