---
layout: post
title:  "Scope trong JavaScript"
date:   2022-11-23 10:00:00 +0700
categories: js
---

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/11/agriculture-gfa5e56941_1920.jpeg)

Scope liên quan trực tiếp bởi Lexical Environment bởi scope liên quan đến phạm vi truy cập của biến.

Mời bạn ghé đọc [bài viết Lexical Environment](https://beautyoncode.com/lexical-environment-trong-javascript/) trước nếu bạn chưa có dịp đọc nha.

Bài viết này sẽ tìm hiểu thêm về scope và các loại scope trong JavaScript.

## Scope là gì?
Scope (tiếng Việt là “phạm vi”) là phạm vi được xác định nơi mà bạn có thể truy cập vào biến.

> Scope determines the variables accessibility (visibility)

## Các loại scope trong JavaScript
Có 3 loại scope trong JavaScript:

– Block Scope (có từ ES6)

– Function Scope hay Local Scope

– Global Scope

---


Ở ES5, chỉ có hai scope là Function Scope và Global Scope

– Scope của function gọi là Function Scope

– Scope bên ngoài function gọi là Global Scope, tương ứng với khai báo biến với var

Tức là:

– trong function → biến thuộc Function Scope

– bên ngoài function → biến thuộc Global Scope

Ví dụ:

```js
// a in global scope
var a = 5;

function x () {
  // b in function x scope
  var b = 10;
  console.log(b);
}

console.log(a); // 5
x() // 10
```

Hình bên dưới minh họa hai loại scope này:

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/11/scope-es5.png)

Chiếc khung màu đen thể hiện phạm vi của từng loại scope.

– Khung bọc màu tím là phạm vi của hàm x, hay function x scope.

– Khung bọc màu xanh là phạm vi của global, hay global scope.

---

Ở ES6, JavaScript giới thiệu thêm hai cách khai báo biến với let, const ([đọc thêm về var, let, const mình ở đây](https://beautyoncode.com/khai-bao-bien-voi-var-let-va-const-trong-javascript/)) đi kèm đó là một loại scope mới – block scope.

Khi bạn khai báo một biến với let, const trong một block, được hiểu là bọc trong một cặp {} , thì biến này nằm trong block scope đó.

Ví dụ:

```js
var a = 5;
let b = 10;

function x() {
  let c = 15;

  if (c > 5) {
    let d = 0;
    console.log('hello from d');
  }
}

x();
```

Thử đặt một breakpoint và quan sát trên debugger:

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/11/check-scope.png)

Ở Global có a là 5, Local có c là 15, Block có d là 0 tương ứng với 3 scopes mình đã đề cập.

Vậy b đang ở đâu? Bạn có thấy b đang thuộc một nơi gọi là Script ?

Thực ra thì b vẫn đang thuộc global scope. Chỉ là vì nó được khai báo với let và được nằm trong một vùng nhớ riêng gọi là [Temporary Dead Zone (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz) nên được mô tả khác trên debugger ở một tab gọi là Script. (đọc thêm ở [blog này](https://beautyoncode.com/hoisting-trong-javascript/))

Bạn có thể chứng minh được b vẫn thuộc global scope vì tại dòng được debug, vẫn có thể truy cập vào b được. Tuy nhiên bạn không thể truy cập vào b từ window , ví dụ window.b


Hình bên dưới minh họa ba loại scope ở ví dụ trên:

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/11/scope-js-now.png)
