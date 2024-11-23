---
title: "Lexical environment trong JavaScript"
excerpt_separator: <!--more-->
categories:
  - js
tags:
  - js
  - lexical-environment
---

Trước khi tìm hiểu về `scope`, `scope chain`, hay cả `closures`, bạn cần hiểu về `Lexical Environment`.

Đây là một khái niệm nền tảng trong JavaScript.

## Execution Context và Callstack
Nhắc lại từ bài [“Điều gì xảy ra khi chạy một chương trình JavaScript ?”](https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/), mỗi khi chương trình JavaScript thực thi, sẽ khởi tạo ra các **“Execution Context”**

Và có hai giai đoạn của execution context là **“Memory Creation”** và **“Code Execution”**.

Ví dụ có đoạn code sau:

```js
function x () {
  var b = 10;
  y();

  function y () {
    var c = 5;
  }
}

x();
```

thì sơ đồ mô tả các execution context và callback được tạo với chương trình trên như sau:

![](/assets/images/2022/11/2022-11-03-lexical-environment-trong-javascript-1.webp)

## Lexical Environment & Scope Chain

Mình đã chọn hình cover cho bài viết này là hình ảnh trái đất nhìn từ ngoài vũ trụ, là điểm tương đồng khi nói về lexical environment. Cùng tìm hiểu nhé!

### Lexical là gì?

“Lexical” tiếng anh có nghĩa là sự kết nối từ bên ngoài theo một thứ tự nào đó.

### Lexical Enviroment là gì?

> “Lexical Environment” của hàm bao gồm local memory của hàm đó cộng với “Lexical Environment” của cha nó.

Ví dụ có hàm `y` ở trên nằm lồng trong hàm `x` (`y` con của `x`), và hàm `x` nằm bên trong `global scope` (`x` con của `global`). 

Hay còn gọi `y is lexically inside the x function. x is lexically inside global`. 

Ngay khi một **“Execution Context”** khởi tạo, một **“Lexical Environment”** cũng đồng thời được khởi tạo.

Cùng xem parent’s lexical environment tương ứng ở ví dụ trên:

![](/assets/images/2022/11/2022-11-03-lexical-environment-trong-javascript-2.webp)

Và `Lexical Environment` sẽ gồm `local memory` và `parent lexical environment` được biểu diễn với vòng tròn màu tím bên dưới.

![](/assets/images/2022/11/2022-11-03-lexical-environment-trong-javascript-3.webp)

## Scope Chain

**Nhìn vào hình trên bạn có thấy được cách chương trình tìm kiếm các giá trị của biến không ?**

Thứ tự tìm sẽ từ vòng tím của `y` sang vòng tím của `x` rồi sang vòng tím của `global` và vẫn tìm không thấy thì sẽ gặp `null` và kết thúc quá trình tìm kiếm này.

Giả sử tại vòng tím `x` không tồn tại `c` như trên, thì chương trình sẽ tiếp tục tìm kiếm xem ở các vòng tím `y`, rồi đến `global`.

Nếu vẫn không tìm thấy sẽ báo lỗi. Nếu có tìm thấy tại đâu trước thì sẽ ưu tiên dùng giá trị tại chỗ đó.

Đây chính là các mà JS Engine tìm kiếm từ trong ra ngoài, gọi là **Scope Chain**.

Hay nói đơn giản hơn **Scope Chain chính là chuỗi nối của các Lexical Environment.**

Nếu biến không được tìm thấy ở `local memory` của `execution context` thì nó sẽ tiến hành tìm kiểm ở các `lexical environment` cho đến hết chuỗi thì thôi.

## Tổng kết

– `Lexical Environment` được tạo cùng `Execution Context`

– `Lexical Environment = local memory + parent’s Lexical Environment`

– Chain of Lexical Environment gọi là `Scope Chain`

 ---

Vậy còn **scope** thì sao ? **Scope** có liên quan đến lexical environment này không ? 

Mời các bạn đón đọc bài tiếp theo về **scope** nhé!
