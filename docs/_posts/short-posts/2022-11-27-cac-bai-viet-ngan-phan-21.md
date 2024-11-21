---
title: "Các bài viết ngắn - phần 21"
categories:
  - Short Posts
tags:
  - short-post
---
![](assets/images/2022/11/2022-11-27-cac-bai-viet-ngan-phan-21-1.webpg)

## BeautyOnCode sharing fun news
Chào bạn, mình muốn chia sẻ với bạn một số thông tin vui của mình tuần này:

1. BeautyOnCode đã viết được hơn 100 bài viết ngắn về tech trên Careerly, và cám ơn hơn 3,600 bạn đã theo dõi (https://lnkd.in/gE8hxhbY)

2. Chỉ còn 2 bài viết nữa thôi là số lượng bài viết trên blog BeautyOnCode (https://beautyoncode.com/) đạt đến con số 100.

3. Kênh YouTube BeautyOnCode (https://lnkd.in/gv4Ua6ra) đã được ra mắt với 30 bạn subscribers đầu tiên (Cám ơn nha! Subscribe channel giúp mình nhé!)

Và 3 videos đầu tiên đã ra mắt:

a. Giới thiệu về blog BeautyOnCode (https://lnkd.in/g3Zg4CS4)

b. Series UI/UX dành cho lập trình viên

  i. Tập 1: Giới thiệu nội dung (https://lnkd.in/g9-ZcKc7)

  ii. Tập 2: UI vs. UX và các giai đoạn phát triển phần mềm (https://lnkd.in/gRsbgGmB) Các video sắp ra mắt:

  iii. Tập 3: Graphic Design – Colors (https://www.youtube.com/watch?v=ivkJhpGpi9U) (sẽ ra mắt vào thứ 4 tuần sau).

  iv. Tập 4: Graphic Design – Fonts & Icons (coming soon).

  v. Tập 5: UX Design (coming soon).

Cám ơn các bạn đã luôn ủng hộ các sản phẩm của mình!

## SOLID là gì?

SOLID là nguyên tắc nền tảng trong lập trình hướng đối tượng OOP (Object Oriented Programming) giúp thiết kế hướng đối tượng linh động, dễ hiểu và dễ duy trì

SOLID là viết tắt của 5 chữ cái đầu của:
– S: single responsibility principle (SRP)
– O: open-closed principle (OCP)
– L: Liskov Substitution Principle (LSP)
– I: Interface Segregation Principle
– D: Dependency Inversion Principle

S: single responsibility principle (SRP) đại diện cho nguyên tắc: “mỗi đối tượng chỉ có một lý do để thay đổi”, điều này có nghĩa là mỗi lớp đối tượng chỉ đại diện cho một loại đối tượng và làm một việc

O: open-closed principle (OCP) đại diện cho nguyên tắc: “các loại thực thể như class, module, hàm, … khuyến khích mở rộng nhưng không khuyến khích chỉnh sửa code có sẵn.

L: Liskov Substitution Principle (LSP) là nguyên tắc chỉ ra lớp con được kế thừa từ lớp cha nên có chung hành vi với lớp cha

I: Interface Segregation Principle chỉ ra rằng nơi sử dụng interface không nên có những loại phương thức có sẵn (từ implement) mà nó không được sử dụng

D: Dependency Inversion Principle chỉ ra hai nguyên tắc chính là:
1. Các mô đun cấp cao không nên nạp bất cứ gì từ mô đun cấp thấp mà phụ thuộc nhau qua lớp trừu tượng như interface
2. Lớp trừu tượng nên độc lập với các loại thực thi

Đọc khó hiểu thế mà nhìn ví dụ là bạn hiểu hơn ấy, mời bạn đọc [bài này](https://www.freecodecamp.org/news/solid-principles-for-programming-and-software-design/) mà ngâm cứu thêm hí


## AWS Certified Developer Associate
Hiện nay, dịch vụ AWS được sử dụng rộng khắp toàn cầu. Việc lấy chứng chỉ “AWS Certified Developer Associate” được nhiều lập trình viên ưu tiên vì là bằng chứng dễ thấy nhất để khẳng định khả năng có thể làm việc với các dịch vụ điện toán đám mây của AWS (Cloud Computing and AWS services)

Kỳ thi này kéo dài 130 phút, với 65 câu hỏi (câu hỏi nhiều lựa chọn và câu hỏi tình huống)
Nếu bạn đạt từ 720 điểm (thang điểm 100) sẽ có chứng chỉ.
Chi phí $150, kết quả có ngay sau khi thi, chứng chỉ có hạn trong 3 năm.

Kỳ thi này bao gồm 4 lĩnh vực chính:
– Deployment chiếm 22% điểm
– Security chiếm 26% điểm
– Development with AWS Services chiếm 30% điểm
– Refactoring 10%
– Monitoring and Troubleshooting 12%

Bạn đọc thêm chi tiết ở [tài liệu chính thức này](https://aws.amazon.com/certification/certified-developer-associate/) nhé


## CSS range
Tính năng mới của CSS giúp viết media queries dễ dàng hơn

Ví dụ bạn có đoạn code sau:
```css
body {
    background: green;
}

@media (min-width: 300px) and (max-width: 640px) {
    body {
        background: red;
    }
}
```
Đoạn code này sẽ chuyển đổi màu nền từ xanh lá sang đỏ khi màn hình có chiều rộng từ 300px đến 640px

Cú pháp CSS mới sẽ giúp bạn viết đoạn media queries này dễ hiểu hơn với range selected
300px <= width <= 640px

```css
@media (300px <= width <= 640px) {
    body {
        background: red;
    }
}
```
hoặc có thể nhanh chóng thay đổi chỉ nhỏ hơn 640px “width <= 640px” hay chỉ lớn hơn 300px “300px <= width”

Ngoài ra bạn cũng có thể sử dụng “or” để nối các điều kiện của media queries.
Ví dụ: width nhỏ hơn 300px hoặc màn hình ở chiều ngang

`@media (width <= 300px) or (oriented: landscape) {}`

Bạn ghé đọc chi tiết ở [bài này](https://css-tricks.com/the-new-css-media-query-range-syntax/) nha

## Scope trong JavaScript

Scope liên quan trực tiếp bởi Lexical Environment bởi scope liên quan đến phạm vi truy cập của biến.

Mời bạn ghé đọc bài viết Lexical Environment (https://beautyoncode.com/lexical-environment-trong-javascript/) trước nếu bạn chưa có dịp đọc nha.

Scope (tiếng Việt là “phạm vi”) là phạm vi được xác định nơi mà bạn có thể truy cập vào biến.
Scope determines the variables accessibility (visibility)

Có 3 loại scope trong JavaScript:
– Block Scope (có từ ES6)
– Function Scope hay Local Scope
– Global

Ở ES5, chỉ có hai scope là Function Scope và Global Scope
– Scope của function gọi là Function Scope
– Scope bên ngoài function gọi là Global Scope, tương ứng với khai báo biến với var

Ở `ES6`, JavaScript giới thiệu thêm hai cách khai báo biến với let, const (đọc thêm về var, let, const mình ở đây https://beautyoncode.com/khai-bao-bien-voi-var-let-va-const-trong-javascript/) đi kèm đó là một loại scope mới – `block scope`.

Khi bạn khai báo một biến với `let`, `const` trong một `block`, được hiểu là bọc trong một cặp `{}` , thì biến này nằm trong `block scope` đó.

Bạn ghé xem thêm ví dụ ở [bài viết này](https://beautyoncode.com/scope-trong-javascript/)
