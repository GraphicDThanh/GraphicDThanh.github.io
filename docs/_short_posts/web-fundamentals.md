---
title: "Các bài viết ngắn về Web Fundamentals"
---

Các bài viết ngắn về "Web Fundamentals":
- Trang web hoạt động ra sao
- Defensive CSS
- Vì sao nên gán min-width cho button?
- UI / UX nền tảng
- Mẹo sử dụng khoảng trắng
- Sự phát triển của CSS

## Trang web hoạt động ra sao
Ba thành phần chính cấu tạo 🏗 nên một trang web là HTML 🪜, CSS 🌈 và JavaScript ✨.

👉 🪜 `HTML` là ngôn ngữ đánh dấu giúp cấu trúc cho nội dung trang.

👉 🌈 `CSS` là ngôn ngữ về các kiểu áp dụng vào nội dung HTML để làm đẹp cho trang

👉 ✨ `JavaScript(JS)` là ngôn ngữ kịch bản cho phép tạo một trang web với nội dung cập nhật, hình ảnh động, …


🧐 **Vậy trang web được dựng lên như thế nào?**

Khi bạn gõ đường dẫn vào trình duyệt và nhấn enter 👩‍💻🧑🏻‍💻, một yêu cầu ➡️ được gửi đến máy chủ và file HTML được tải về ⬇️

Sau đó, trình duyệt sẽ phân tích 🧐 HTML đầu tiên, theo thứ tự từ trên xuống dưới ⏬. Trong file này chứa <link> để tải tiếp CSS 🌈 và <script> để tải tiếp tệp JavaScript ✨

Trong khi phân tích HTML, trình duyệt tạo cây DOM, tạo cấu trúc CSSOM với nội dung CSS đồng thời cũng biên dịch và thực thi JavaScript 🏗

Quá trình này diễn ra đồng thời 🤖, trang web được vẽ lên màn hình 🖼 và bạn thấy trang web được hiển thị 🧑🏻‍💻

Thật thú vị phải không 🤩 Ngoài ra thì cũng có nhiều cách để tải và thực thi code JavaScript sao cho trang web hiển thị lên nhanh nhất, mời bạn ghé đọc thêm ở [bài viết trên blog này][chien-luoc-tai-thuc-thi-code-javascript].

[chien-luoc-tai-thuc-thi-code-javascript]: {{ "" | relative_url }}{% post_url js/2022-04-17-chien-luoc-tai-thuc-thi-code-javascript %}

## Defensive CSS
Khi viết code HTML/CSS cho một trang web, sẽ có những tình huống không mong đợi xảy ra, ví dụ như: đoạn chữ dài quá kích thước của khung làm chữ tràn ra ngoài, hay kích thước ảnh thay đổi ngẫu nhiên, hay hình nền bị lặp lại khi kích thước hình ảnh nhỏ

Những tình huống như trên đôi khi bản thiết kế không có sẵn, thường sẽ dựa trên kinh nghiệm của Front Developer xử lý, hoặc cho đến khi gặp lỗi(bug) thì phải sửa.

Để chủ động trong những tình huống này, giới thiệu đến bạn một trang chuyên viết về Defensive CSS.

Vậy vì sao Defensive CSS? Hay vì sao viết HTML/CSS cần phải chuẩn bị trước(phòng thủ) có những tình huống như trên có thể xảy ra?

Vì:

– Nội dung trong bản thiết kế có thể thay đổi, tức là nội dung có thể tràn(break) layout

– Hình ảnh có thể có các tỉ lệ khác nhau

– Sử dụng các CSS như flex, grid một cách hiệu quả có thể giảm bug/break layout

– Bản thiết kể chỉ mang tính chất định hướng thiết kế, dữ liệu thật có thể thay đổi, cần học cách viết layout sao cho có thể dễ bảo trì(maintain) và extend(mở rộng)

– Trong đây có nhiều tips như là Flexbox Wrapping, Image Distortion, Long Content, …

Mời bạn vào đọc và xem ví dụ ở [đây](https://defensivecss.dev/tips).

## Vì sao nên gán min-width cho button?
Một vấn đề phổ biến khi tạo một nút bấm (button) là để chiều rộng của nút tùy vào nội dung của nút (text content) cộng với khoảng cách hai bên (padding).

Một vài lý do cho vấn đề này:

– Nút bấm có nội dung hiển thị thay đổi trên UI tuỳ loại ngôn ngữ là rất phổ biến. Ví dụ nút Done trong tiếng Anh hiển thị qua tiếng Việt có thể là Đã Xong, và trong tiếng Arabic thì là تمthì khi đó button Done trong tiếng Anh có độ rộng là 72px thì sẽ có độ rộng 95px trong tiếng Việt và 43px trong tiếng Ả Rập.

– Việc hai nút bấm đứng cạnh nhau có cùng chiều rộng như Done và Cancel cũng thường xảy ra

– Hoặc nội dung nút bấm ở phiên bản đầu là Done nhưng qua phiên bản sau đổi thành Finished cũng làm cho kích thước của nút bấm thay đổi theo

Vì thế, việc gán cho nút thuộc tính `min-width` sẽ giúp hạn chế những vấn đề ở trên. Nút `Done`

sẽ được gán `min-width` là 95px và sẽ hiển thị tốt cho cả ngôn ngữ là tiếng Việt hay tiếng Ả Rập.

```css
.button {
  min-width: 95px;
}
```
[Link ref](https://defensivecss.dev/tip/button-min-width/)

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

## UI / UX nền tảng

Nếu bạn nghĩ làm web developer chỉ cần biết code, ai đưa gì làm nấy thì đó mà mindset chưa đúng.

Việc dev học về thiết kế UI/UX như là một nền tảng cơ bản để làm web developer. giúp bạn: 

- hiểu về người dùng hơn, sản phẩm hơn
- hỗ trợ bộ phần thiết kế, nghiên cứu hành vi người dùng
- lựa chọn các kỹ thuật phù hợp hơn
- hoàn thành công việc tốt hơn
- dễ dàng hơn trong việc tự thiết kế sản phẩm riêng của mình

Vì thế, mình muốn giới thiệu đến bạn một khóa học về UI/UX với các nội dung:

- UI/UX là gì ?
- Tìm hiểu về “Stages of development" để hiểu về quy trình phát triển phần mềm
- Tìm hiểu về UI - “Graphic Design”, bao gồm:
    - Tìm hiểu về màu sắc
        - Tâm lý học màu sắc
        - Lý thuyết về màu sắc
        - Bánh xe màu và bảng màu
        - Màu nóng, màu lạnh
    - Tìm hiểu về fonts
    - Tìm hiểu về Icons
- Tìm hiểu về UX - trải nghiệm của người dùng, bao gồm:
    - Nguyên tắc lấy người dùng làm trung tâm
    - Hành trình của khách hàng
    - Mô hình phễu bán hàng

Bạn có thể tìm hiểu các nội dung trên qua video sau

<iframe width="640" height="360" src="https://www.youtube.com/watch?v=uL2ZB7XXIgg" frameborder="0" allowfullscreen></iframe>

## Mẹo sử dụng khoảng trắng

Một số mẹo sử dụng khoảng trắng hợp lý cho các tiêu đề và chữ trên trang web

– Giảm khoảng trắng bên dưới tiêu đề và tăng khoảng trắng bên trên tiêu đề Điều này sẽ giúp tiêu đề to hơn và nổi bật hơn, đồng thời giúp người đọc dễ đọc nội dung bên dưới hơn vì nó gần hơn

– Thêm khoảng trắng giữa các đề mục và các đường link nên rõ ràng thể hiện có thể click được

– Kiểm tra font tải có đúng không và chính tả của nội dung

– Giảm lineheight giữa các dòng ngắn

– Hạn chế sử dụng xuống dòng vì sẽ gây khó đọc

– Sử dụng font custom sẽ làm trang web có dấu ấn riêng, nhưng lưu ý kiểm tra font có load được không nhé.

Bạn có thể ghé [link](https://pimpmytype.com/hugo-md/) để xem kết quả trước và sau những thay đổi này nhé ^^

[choi-cung-js]: {{ "" | relative_url }}{% post_url js/2022-10-18-choi-cung-javascript %}
[dieu-gi-xay-ra-khi-chay-chuong-trinh-js]: {{ "" | relative_url }}{% post_url js/2022-08-30-dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript %}

## Sự phát triển của CSS
Sự phát triển của CSS theo hướng có thể mở rộng trong dự án

CSS là một trong ba trụ cột của website (HTML, CSS, JS). Khi nhắc đến CSS hẳn bạn sẽ nghĩ bạn này quá đơn giản đúng không ^^ Tuy nhiên, viết CSS trong dự án lớn để có thể dễ dàng mở rộng và hiệu quả là điều không hề dễ dàng.

Bài viết sau giới thiệu đến bạn về CSS và quá trình phát triển của bạn ấy:

Trước khi CSS ra đời, style được viết luôn vào code HTML. Khi CSS ra đời, tách code CSS ra riêng. Và nổi tiếng với trang CSS Garden, nơi chỉ với cùng cấu trúc html nhưng xây dựng được các thiết kế khác nhau

CSS có global namespaces, theo cascade rules và selector specificity – tức code CSS được truy cập trong toàn bộ trang web, với luật tính điểm để quyết định có ghi đè nhau không (cascade) và chọn các phần tử với selector.

Bên cạnh đó, việc đặt tên class, ghi đè với `!important`, code thừa trong dự án lớn (vì không dám xoá sợ ảnh hưởng các tính năng đang hoạt động) ngày càng phổ biến. CSS lại không có lỗi (silent error).

Tất cả những đều này làm CSS rất dễ để bắt đầu nhưng là nhanh chóng lộn xộn và khó kiểm soát.

Việc quản lý CSS ra đời với các khái niệm về “CSS Architectures” như SMASS, BEM, ITCSS, Cube CSS, SASS, LESS, …

Tiếp đó, việc phát triển của các trang web SPAs và component-driven development dẫn đến nhiều hướng tiếp cận mới với CSS như là inline styles, CSS in JS
Làm sóng đầu tiên của CSS in JS với styled-component, Emotion
Làn sóng thứ hai của CSS in JS với việc complie CSS giúp giảm thời gian chạy trên trình duyệt của người dùng. CSS biên dịch qua Atomic CSS, các thư việc như Vanilla extract, Linaria, Compiled.

Cùng lúc đó, song song với sự phát triển của CSS in JS, một hướng mới quản lý CSS với Atomic CSS ra đời với việc style các cấp thấp hơn cả blockers, objects, tập trung vào single-purpose atoms với các thư viện như ACSS, Tachyons, WindiCSS, và nổi nhất hiện nay là Tailwind.

Thật thú vị đúng không! Bạn ghé đọc thêm ở [bài này](https://frontendmastery.com/posts/the-evolution-of-scalable-css/) nhé ^

