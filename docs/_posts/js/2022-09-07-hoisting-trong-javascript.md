---
title: "Hoisting trong JavaScript"
excerpt_separator: <!--more-->
categories:
  - js
tags:
  - js, hoisting
---

![](assets/images/2022/09/2022-09-07-hoisting-trong-javascript-1.webp)

Điều khiến JavaScript khó hiểu với những người mới hay chuyển từ ngôn ngữ khác qua chính là JavaScript cho phép sử dụng biến và hàm ngay cả trước cả khi bạn khai báo chúng.

Ví dụ ở đoạn code này:

```js
1. console.log(a)
2. aFunction()
3. 
4. var a = 3;
5. function aFunction() {
6. 	console.log("Hello")
7. }
```

Chương trình khi chạy không báo lỗi gì và kết quả in ra ở Console là:

```js
undefined
Hello
```
Lưu ý ở đây mình dùng `var` , nếu sử dụng `let` hay `const` thì sẽ bị lỗi `Uncaught ReferenceError: x is not defined` vì với `let` hay `const` của ES6 thì chỉ sau khi bạn khai báo mới sử dụng được chúng.

Vậy điều gì đã khiến bạn có thể truy cập vào các biến và hàm ngay cả khi chúng chưa được khai báo? 

**Chính là cơ chế Hoisting trong JavaScript.**

Vậy cụ thể thì `hoisting` là như thế nào?

Bạn có nhớ hai giai đoạn của một `“Execution Context”` là `Memory Creation` và `Code Execution` đã được giới thiệu trong bài [Điều gì xảy ra khi chạy một chương trình JavaScript?][dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript] không? 

[dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript]: {{ "" | relative_url }}{% post_url js/2022-08-30-dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript %}

**Hoisting** trong JavaScript được thực hiện trong giai đoạn cấp phát bộ nhớ – **Memory Creation**. Các biến và hàm sẽ được cấp bộ nhớ trước khi code được thực thi, biến được cấp bộ nhớ với giá trị `undefined` , còn hàm thì sẽ được cấp bộ nhớ cho toàn bộ nội dung bên trong hàm `f aFunction()`. 

Vì thế, bước vào giai đoạn thực thi **Code Execution**, thì các giá trị này đã có sẵn để sử dụng, nên gọi các hàm và biến này đã được `hoist` lên trước khi code được thực thi.

---

Bạn có thể kiểm tra trực tiếp trên **devTools** bằng cách đặt một breakpoint ngay tại dòng số 4, ngay trước khi code của biến và hàm được khai báo.

Khi chương trình chạy, gặp **breakpoint** dừng lại, hãy kiểm tra tab **Global** và tìm `a` , `aFunction` , tại đây tìm thấy biến `a` và hàm `aFunction` đã được cấp phát bộ nhớ và sẵn sàng để sử dụng.

![](assets/images/2022/09/2022-09-07-hoisting-trong-javascript-2.webp)

Một lưu ý ở đây, nếu aFunction được khai báo ở dạng biểu thức dưới tên một biến

```js
var aFunction = function() {}
```

thì `aFunction` sẽ có giá trị ban đầu là `undefined` như với một biến bình thường, và chương trình này sẽ báo lỗi.

**Hoisting** trong JavaScript sẽ dễ gây hiểu nhầm nếu bạn không hiểu về JavaScript Engine nên bạn cần tìm hiểu cơ chế này để dễ debug chương trình của mình nhé.


Thêm nữa, ở phiên bản ES6, cung cấp let và const để yêu cầu bạn chỉ sử dụng biến sau khi đã khai báo chúng nên sẽ tránh được các sử dụng không mong đợi như trên. 

Vì thế, bạn nên ưu tiên sử dụng let và const thay thế cho var.

([Ref series Namaste JavaScript](https://www.youtube.com/watch?v=pN6jk0uUrD8&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP))
