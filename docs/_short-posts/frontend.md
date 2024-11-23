---
title: "Các bài viết ngắn về Frontend"
---

Các bài viết ngắn về "Frontend"
- Web Fundamentals
  - Trang web hoạt động ra sao
  - Defensive CSS
  - Vì sao nên gán min-width cho button?
  - UI / UX nền tảng
  - Mẹo sử dụng khoảng trắng
  - Sự phát triển của CSS
- JavaScript
  - JS debug tools
  - Chơi cùng JavaScript
  - Điều gì xảy ra khi chạy một chương trình JavaScript?
  - Stack overflow trong JS
  - Form 2022 có gì mới?
  - CSS-in-JS là gì?
  - Mảng trong JavaScript
  - Hoisting trong JavaScript
  - Một số tips viết code JavaScript sạch
  - Lexical environment trong JavaScript
  - Scope trong JavaScript
  - Giới thiệu chuỗi bài về JavaScript
- TypeScript
  - Hơn 30 bài blog giúp bạn học Typescript
- React
  - Những điều thú vị về React
  - Hook Pattern
  - Giới thiệu về XState
  - 7 repo giúp bạn code React xịn hơn


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

Thật thú vị đúng không! Bạn ghé đọc thêm ở [bài này](https://frontendmastery.com/posts/the-evolution-of-scalable-css/) nhé ^^

## JS debug tools
Các bạn Frontend Developer hay sử dụng gì để debug trong code JavaScript nhỉ?

Để hiển thị các thông tin lên trình duyệt thì có thể sử dụng:

– `alert()`: hiện popup kèm nội dung

– `console.log()`: hiển thị nội dung ở “Console” của trình duyệt

– `debugger;` chỗ đặt bạn này sẽ là một breakpoint, khi code thực thi sẽ dừng lại để bắt đầu chế độ debug trên trình duyệt

– `console.trace()`: hiện ra các dấu vết của nơi mình đặt bạn ấy vào và giúp mình kiểm tra đã đi qua những đâu, ở dòng bao nhiêu. Cái này gọi là trace ấy.


Ngoài ra thì nên tìm hiểu về Chrome DevTools , một công cụ vô cùng mạnh mẽ. Nếu làm app React thì có React DevTools. Visual Studio Code cũng cung cấp công cụ debug theo từng loại ngôn ngữ lập trình.

Bạn ghé đọc thêm về Debug JavaScript Tools ở [bài viết này](https://raygun.com/learn/javascript-debugging-tools).

## Chơi cùng JavaScript

Khi học JavaScript bạn thử nghiệm các đoạn code nhỏ bằng các cách nào ?
Thử xem bạn đã dùng cách nào trong các cách sau nhé!

### Cách 1: Chạy chương trình với browser

Tạo file index.html để chứa code của trang web. Sau đó viết nội dung trang web trong file index.html và viết code JS trong thẻ <script></script> hoặc tải vào thẻ script này với thuộc tính src.
Bạn có thể mở trực tiếp file index.html hoặc “Go Live” với extension “Live Server” trên VSCode.

Cách này thì khá cồng kềnh khi muốn thử nghiệm nhanh một đoạn logic nhỏ. Tuy nhiên sẽ cần thiết nếu bạn thực hành liên quan đến DOM.
Cách này không chia sẻ code online được.

### Cách 2: Chạy chương trình với nodejs

Cài nodejs trên máy (thường sẽ có sẵn vì dev thường sử dụng npm)
Chạy lệnh `“node <filename>.js”` ở command line để thực thi
Một tip là có thể sử dụng gói nodemon để tự động load lại khi mình có chỉnh sửa trên file.
Chạy câu lệnh: “npx nodemon example.js” để vừa cài gói nodemon vừa thực thi code.

Cách này sẽ tiện hơn nếu muốn chạy một chương trình JS nhỏ không liên quan đến DOM.
Cách này cũng không chia sẻ code online được.

### Cách 3: Sử dụng tab “Console” trên trình duyệt Chrome
Sử dụng browser Chrome, mở Console tab và thử nghiệm trực tiếp trên đó.

Cách này sẽ rất tiện khi mình muốn kiểm tra nhanh hay demo nhanh các đoạn code hay cú pháp của JS, vì trình duyệt có tích hợp sẵn để dùng.
Đặc biệt bạn có thể chơi với Web APIs như DOM, …

### Cách 4: Sử dụng javascript.makeup
[javascript.markup](https://javascript.makeup/file/default) cũng là một cách để có thể chơi với JS và kết quả cũng khá dễ nhìn.

### Cách 5: Sử dụng các công cụ online giúp viết và chia sẻ chương trình như: [Playcode.io](https://playcode.io/), JSBin, JSFiddle, Replit
Các công cụ này thường yêu cầu tài khoản để lưu và chia sẻ chương trình.

Trên đây là một số cách mình biết. Còn bạn thì sao, bạn hay thử nghiệm JS như thế nào?

Cùng chia sẻ với mình bên dưới comment nhé!

Bạn có thể xem hình ảnh minh họa ở [bài blog mình viết chi tiết][choi-cung-js] này.

## Điều gì xảy ra khi chạy một chương trình JavaScript?
Mọi thứ trong JavaScript diễn ra bên trong một ngữ cảnh thực thi, hay “Execution Context”. Có hai giai đoạn trong “Execution Context” là “Memory Creation” và ”Code Execution

Khi chương trình JS khởi chạy, một execution context ở global sẽ được tạo.
Ở giai đoạn **“Memory Creation Phase”**, bộ nhớ được cấp cho tất cả các biến và các hàm.

Ở giai đoạn **“Code Execution"**, code sẽ được thực thi từng dòng một theo thứ tự trên xuống dưới.

Nếu có một hàm được gọi, một Execution Context giành riêng cho hàm đó sẽ được tạo và thực hiện tương tự với hai giai đoạn trong Execution Context mới này. Khi một hàm kết thúc thực thi, thì Execution Context này sẽ được xóa đi.

Và cứ thế, chạy cho đến hết chương trình.

Quá trình ở trên thường được gọi là **call stack**

Mỗi execution context được tạo sẽ được bỏ vào(push) vào ngăn xếp(stack)

Mỗi execution context bị xóa sẽ được lấy ra khỏi(pop) ngăn xếp(stack)

Đây chính là cách JS Engine thực thi code.

Mời bạn đọc chi tiết về quá trình này kèm ví dụ và hình ảnh minh họa ở [blog post này][dieu-gi-xay-ra-khi-chay-chuong-trinh-js] nhé

## Stack overflow trong JS
Như đã nói ở bài [“Điều gì xảy ra khi chạy một chương trình JavaScript ?”](https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/), mỗi khi một chương trình JS chạy sẽ có một global execution context được khởi tạo, mỗi hàm được thực thi sẽ có một execution context của hàm đó được khởi tạo.

Execution context chứa toàn bộ các biến, hàm và các đối số truyền vào ở global hoặc ở hàm được thực thi.

Callstack chứa toàn bộ các execution contexts này theo thứ tự chúng được khởi tạo, và hoạt động theo nguyên lý LIFO (last-in-first-out).

Vì thế, JavaScript hoạt động synchronous.

`Stack Overflow` là hiện tượng tràn callstack khi một hàm được gọi đệ quy vô tận.
Trình duyệt có số lượng callstack nhất định do đó nếu gọi vô tận sẽ dẫn đến tràn stack, gây lỗi `“Maximum call stack size exceeded”`

Ví dụ chương trình này sẽ gây lỗi stack overflow:

```js
function callMySelf() {
  callMySelf()
}
callMySelf()
```

## Form 2022 có gì mới?

Một số công cụ làm việc với form mới có thể bạn chưa biết.

`.requestSubmit()` là lựa chọn tốt hơn giúp thay thế `.submit()` khi bạn muốn event `'submit'` được trigger đồng thời muốn form được validate. Ví dụ mỗi khi submit như các field có `required` sẽ là bắt buộc.

Thuộc tính`sumitter` của event, hay `event.submitter` cho phép xác định đâu là DOM thực hiện submit form khi form có nhiều nút có `type="submit"`

`formdata` event là một sự kiện khá mới được **trigger** khi một FormData được khởi tạo với new hoặc mặc định khi form được submit. `e.formData` là một FormData instance với các thuộc tính và phương thức cho phép truy cập vào các fields data ở dạng key / value. (đọc thêm về [APIs FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) và ví dụ mình có thử ở [đây](https://replit.com/@graphicdthanh/FormData#script.js)). 
Vậy là bạn có thể truy cập tất cả data của form khi submit đồng thời có thể chỉnh sửa trước khi gọi trực tiếp API nếu cần.

`showPicker()` của thẻ input cho phép hiển thị UI của các lựa chọn của thẻ input, đó có thể là màu sắc, ngày tháng, …

Thuộc tính `inert` cho phép hiển thị form như ở trạng thái không focus, không click được, và thuộc tính này cũng không áp dụng các style mặc định vào các thành phần. `inert` tương tự như `aria-hidden="true"` 

Bạn có thể xem các ví dụ minh họa ở [bài viết](https://css-tricks.com/whats-new-with-forms-in-2022/)

## CSS-in-JS là gì?
CSS-in-JS là một thuật ngữ mô tả việc viết code style CSS trong code JS, tức viết vào file .js , .jsx thay vì viết code CSS vào file .css như thông thường.

CSS-in-JS ra đời khi mà trang web ngày càng phức tạp và việc maintain tất cả các CSS của toàn bộ trang web trong một scope global document (hay global scope selectors) duy nhất của của file css gây nhiều xung đột khi trùng tên class, id hay việc ghi đè CSS trở nên khó khăn hơn.

Thêm vào đó xu hướng component-based development (hay component driven development) ngày càng phát triển với React khiến việc style từng component càng trở nên cấp thiết.

CSS-in-JS đã giúp giải quyết vấn đề này như thế nào?

CSS-in-JS sẽ trích xuất CSS theo từng component thay vì theo document như CSS.

Những ưu và nhược điểm khi sử dụng CSS-in-JS

**Ưu điểm**

– Code ngắn gọn hơn

– Giảm xung đột CSS

– CSS dynamic với props

– Kế thừa style

– Cú pháp SASS giúp style dễ dàng với pseudo element và pseudo class

– Tự động tạo prefix cho class CSS, không sợ bị trùng nhau

– Có thể viết unit test cho CSS

– Dễ dàng đổi theme với ThemeContext

**Nhược điểm**

– Không phù hợp với người chưa biết JS

– Tốn thời gian làm quen với thư viện, code base gây khó khăn cho người mới

– Sẽ khó khăn khi muốn debug bằng tên class

– Hiệu suất không tốt bằng CSS bình thường do tăng code base

Bạn tìm hiểu thêm ở [link](https://beautyoncode.com/css-trong-js-la-gi/)

## Mảng trong JavaScript
Có hai cách để tạo mảng trong JavaScript là tạo đối tượng của lớp Array: `let arr = new Array(1, 2)`  hay sử dụng cú pháp mảng []: `let arr1 = [3, 4]`

Khi làm việc với một danh sách, sẽ có các thao tác cơ bản như: (các phương thức của mảng sẽ bắt đầu với dấu `.`)

– thêm một phần tử vào danh sách `.push()`, `.unshift()`, `.splice()`

– xóa một phần tử ra khỏi danh sách `.pop()`, `.shift()`, `.splice()`

– thay thế phần tử trong mảng với `.splice()`

– lặp qua từng phần tử của mảng để lấy dữ liệu hay xử lý logic `for`, `.forEach()`, `.map()` (lưu ý map trả về mảng mới)

– kiểm tra index của một giá trị trong mảng với `.indexOf()`

– kiểm tra giá trị nào với vị trí index đã biết `.at()`

– nối hai mảng với nhau với `.concat()`

– nối các phần tử trong mảng với một ký tự liên kết với `.join()`

– chuyển đổi mảng về chuỗi với `.toString()` (lưu ý phương thức này của object, và array cũng là object)

– tìm kiếm phần tử đầu tiên thỏa điều kiện với `.find()`

– tìm kiếm tất cả phần tử thỏa điều kiện với `.filter()`

– lấy ra một mảng con từ mảng ban đầu

– sắp xếp mảng theo một thứ tự nào đó với `.sort()`, đảo ngược mảng với `.reverse()`

– kiểm tra tất cả các phần tử trong mảng thỏa điều kiện với `.every()`, kiểm tra một vài phần tử trong mảng thỏa điều kiện với `.some()`


Khi sử dụng các phương thức này bạn cần chú ý một số điều sau:
– Hiểu rõ phương thức sử dụng làm gì
– Nắm rõ cú pháp
– Kiểm tra giá trị trả về
– Kiểm tra xem phương thức có làm thay đổi mảng ban đầu hay không

Bạn có thể đọc thêm ví dụ ở [bài viết sau](https://dev.to/codewithtee/15-array-methods-in-javascript-1p1m).

## Hoisting trong JavaScript

Điều khiến JavaScript khó hiểu với những người mới hay chuyển từ ngôn ngữ khác qua chính là JavaScript cho phép sử dụng biến và hàm ngay cả trước cả khi bạn khai báo chúng.

Vậy điều gì đã khiến mình có thể truy cập vào các biến và hàm ngay cả khi chúng chưa được khai báo? Đó chính là cơ chế Hoisting trong JavaScript.

Bạn có nhớ hai giai đoạn của một “Execution Context” là Memory Creation và Code Execution(đọc thêm ở [bài viết này][dieu-gi-xay-ra-khi-chay-chuong-trinh-js]).

Hoisting trong JavaScript chính là sau giai đoạn Memory Creation, các biến và hàm sẽ được cấp bộ nhớ trước khi code được thực thi, biến được cấp bộ nhớ với giá trị undefined , còn hàm thì sẽ được cấp bộ nhớ cho toàn bộ nội dung bên trong hàm f nameFunction(). Vì thế, bước vào giai đoạn thực thi Code Execution, thì các giá trị này đã có sẵn để sử dụng.

Hoisting trong JS sẽ dễ gây hiểu nhầm nếu bạn không hiểu về JavaScript Engine nên bạn cần tìm hiểu cơ chế này để dễ debug chương trình của mình nhé.

Mời bạn đọc thêm chi tiết ở [bài blog này][hoisting-trong-javascript].

## Một số tips viết code JavaScript sạch
Viết code JS sạch cần đảm bảo các tiêu chí sau: **dễ đọc, dễ debug, hiệu quả và hiệu suất cao**

Một số tips bạn nên nắm rõ để viết code JS clean:

1. Sử dụng `try/catch` cho tất cả các request đến API và các phương thức liên quan JSON
2. Sử dụng linter (ESLint) để giúp scan code và chỉ ra các lỗi cần sửa dựa trên các quy tắc chuẩn hay tự config cho code dự án thống nhất.
3. Theo dõi các issue trên editor với extension như Stepsize([vscode](https://www.stepsize.com/r/vscode?utm_source=referral&utm_medium=dev.to&utm_campaign=10+must-know+tips+for+writing+clean+code+with+Javascript)) giúp quản lý tech debt
4. Sử dụng template string sẽ dễ đọc hơn. 
Thay vì `'Hello' + username` thì nên viết ``Hello ${username}``
5. Sử dụng optional chaining để nối các điều kiện kiểm tra lại
Thay vì `if (data && data.payload && data.payload.name == 'Anna')` 
thì nên viết `if (data?playload?name == 'Anna')`
6. Hạn chế code quá nhiều lớp lồng nhau, nên giới hạn là 2 - 5 lớp lồng là tối đa để giảm phức tạp cho source code.
7. Comment code cho những nội dung cần thiết, tránh comment để giải thích source code.

([Read more](https://dev.to/alexomeyer/8-must-know-tips-for-writing-clean-code-with-javascript-i4))

## Lexical environment trong JavaScript

Sau khi đã nắm rõ về execution context cùng hai giai đoạn của nó (memory creation và code execution) và call stack (các execution context được push / pop trong stack), mình sẽ cùng tìm hiểu về một khái niệm nền tảng nữa của JavaScrip, đó là lexical environment.

Hiểu về lexical environment sẽ giúp bạn dễ hiểu các khái niệm như scope, scope chain hay closures.

Vậy lexical environment là gì ?

“Lexical Environment” của hàm bao gồm local memory của hàm đó cộng với “Lexical Environment” của cha nó.

Lexical environment được tạo ra khi nào ?

Ngay khi một “Execution Context” khởi tạo, một “Lexical Environment” cũng đồng thời được khởi tạo.

Còn scope chain liên quan đến lexical environment như thế nào?

Scope Chain chính là chuỗi nối của các Lexical Environment.

Mời bạn ghé đọc [bài viết này][lexical-environment] với các hình ảnh minh hoạ các khái niệm nền tảng này nhé!

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

Ở `ES6`, JavaScript giới thiệu thêm hai cách khai báo biến với let, const (đọc thêm về var, let, const mình [ở đây][khai-bao-bien-voi-var-let-const] đi kèm đó là một loại scope mới – `block scope`.

Khi bạn khai báo một biến với `let`, `const` trong một `block`, được hiểu là bọc trong một cặp `{}` , thì biến này nằm trong `block scope` đó.

Bạn ghé xem thêm ví dụ ở [bài viết này][scope-trong-js]


## Giới thiệu chuỗi bài về JavaScript
Chuỗi bài viết này sẽ đi theo hướng trả lời các câu hỏi kiểu như cách JS hoạt động như thế nào (JS Engine), các concepts chính như stack, callstack, scope, hoisting, closures, … cách JS được tải và thực thi trên trang web, debug chương trình và các tools cũng như các tài liệu khác liên quan.

BeautyOnCode hân hạnh giới thiệu đến bạn:

Bài viết ["Điều gì xảy ra khi chạy một chương trình JavaScript"][[dieu-gi-xay-ra-khi-chay-chuong-trinh-js]] trả lời câu hỏi của tiêu đề, giới thiệu đến bạn cách JS Engine hoạt động thông qua Execution Context và tạo ra callstack.

Bài viết ["Hoisting trong JavaScript"][[hoisting-trong-javascript]] tìm hiểu về khái niệm hoisting trong JavaScript dựa vào cách JS Engine hoạt động.

Bài viết ["Khai báo biến với var, let, const"][khai-bao-bien-voi-var-let-const] giới thiệu các cách khai báo biến trong và sự khác nhau của chúng.

Bài viết ["Chiến lược tải và thực thi JS"][chien-luoc-tai-thuc-thi-code-javascript] giới thiệu các các thêm code JS vào trang web và chiến lược tải JS sao chi hiệu quả nhất

Bài viết ["Chơi cùng JavaScript"][choi-cung-js] giới thiệu các cách giúp bạn học và thử nghiệm nhanh một chương trình JS đơn giản.


[hoisting-trong-javascript]: {{ "" | relative_url }}{% post_url js/2022-09-07-hoisting-trong-javascript %}
[dieu-gi-xay-ra-khi-chay-chuong-trinh-js]: {{ "" | relative_url }}{% post_url js/2022-08-30-dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript %}
[khai-bao-bien-voi-var-let-const]: {{ "" | relative_url }}{% post_url js/2022-10-12-khai-bao-bien-voi-var-let-va-const-trong-javascript %}
[chien-luoc-tai-thuc-thi-code-javascript]: {{ "" | relative_url }}{% post_url js/2022-04-17-chien-luoc-tai-thuc-thi-code-javascript %}
[choi-cung-js]: {{ "" | relative_url }}{% post_url js/2022-10-18-choi-cung-javascript %}
[lexical-environment]: {{ "" | relative_url }}{% post_url js/2022-11-03-lexical-environment-trong-javascript %}
[scope-trong-js]: {{ "" | relative_url }}{% post_url js/2022-11-11-scope-trong-javascript %}

## Hơn 30 bài blog giúp bạn học Typescript
Bài viết chia làm 4 nhóm articles bao gồm:
Cơ bản, Nâng cao, Các thử thách của type, Các Design Patterns
Các hình ảnh động minh họa giúp dễ hiểu hơn các khái niệm khó nhằn,

Cơ bản:

- Các loại types
- Phân biệt K, T, V trong TypeScript Generics
- Phân biệt type và interface
- Cách sử dụng keyof, typeof
- Mục đích của các từ khóa khởi tạo

Nâng cao:

- Sử dụng Mapped Types, Conditional Types
- Sử dụng infer, template literal types, intersection types
- Sử dụng union types
- TypeScript Classes

Thử thách:

- Thực hành built-in Pick, Omit,
- Thực hành RequiredByKeys, PartialByKeys
- Thực hành OmitByType, PickByType, IsAny

Các Design Patterns:

- Strategy, Chain of Responsibility, Template Method, Observer, Adapter Patterns
- Simple Factory, Factory Method, Abstract Factory Patterns
- Builder, Flyweight Pattens

Mình cũng mới bắt đầu tự học TypeScript, vì ngôn ngữ này bây giờ là a must rồi ^^

Bạn có thể dùng tính năng Save trên medium để lưu lại [nguồn tài liệu này](https://medium.com/frontend-canteen/with-these-articles-you-will-not-be-confused-when-learning-typescript-d96a5c99e229).



## Những điều thú vị về React

ReactJS vẫn đang làm mưa làm gió trên cộng đồng lập trình web với mức lương khủng và nhu cầu thị trường rất nhiều.
Một số điều thú vị về React:

Thuật toán áp dụng khi xử lý DOM ảo là diff algorithm, nó sẽ so sánh các phiên trước và sau khi state hoặc props thay đổi.

DOM ảo là một bản copy của DOM thật theo tỉ lệ 1-1, DOM ảo là một object với các thuộc tính như loại element, các node con.

DOM ảo hoạt động và đồng bộ với DOM thật qua thư viện ReactDOM, quá trình này gọi là Reconciliation

DOM ảo cũng là một object, object được lưu trữ trong stack, heap, và các bạn này được lưu ở trên ram

DOM ảo có thực sự nhanh hơn DOM thật? Vấn đề này vẫn đang được tranh cãi

Có phải ReactJS là cha đẻ của DOM ảo? Không nha, ReactJS sử dụng DOM ảo nhưng không tạo ra khái niệm này, nó đã có từ trước. Vuejs hay Elm cũng có sử dụng DOM ảo, mỗi thư viện có cách áp dụng khác nhau.

Tại sao lại chia ra hai thư viện react và reactDOM?

Vì có sự xuất hiện React Native, lập trình app cho di động, nên react sẽ là phần lõi dùng chung của cả hai bên: web và di động, còn reactDOM thì chỉ sử dụng cho web app.

Bạn có thể đọc thêm ở [bài viết này](https://viblo.asia/p/su-that-thu-vi-ve-react-co-the-ban-chua-biet-L4x5xAawKBM)

## Hook Pattern

Hook pattern giúp sử dụng function để tái sử dụng các trạng thái(state) xuyên suốt nhiều components trong app.

React 16.8 giới thiệu Hooks, một cách mới vẫn có thể sử dụng state và lifecycle methods mà không cần dùng cú pháp class của ES2015.

**Vì sao lại thay thế class component?**

Để hiểu vì sao thì cần phải hiểu về class component. Trước đây, có hai cách để tạo một component là sử dụng function (stateless component) và class (stateful component). Class sẽ sử dụng nếu component cần làm việc với các trạng thái (state).

Việc này dẫn tới một vấn đề về code sẽ thay đổi nhiều lên rất nhiều khi một function component muốn chuyển sang class component vì syntax khác nhau. Class component cần có constructor để khởi tạo state, hàm render, các hàm khác, …

Thêm vào đó, việc chia sẻ state qua nhiều component có thể sử dụng HOC hay Render Props pattern, và khi có nhiều component lồng vào nhau sẽ sinh ra vấn đề component wrapper hell (có thể hiểu tương tự callback hell)

Ngoài ra, việc kiểm soát một component ở lifecycle methods như componentDidMount, … sẽ càng làm cho code base của một component gia tăng, và lặp lại ở nhiều component.

**Hooks ra đời giúp giải quyết các vấn đề trên như thế nào?**

– Hooks cho phép quản lý state trong một function component, nên không cần đổi code base nhiều khi sử dụng state nữa.

– Hooks cho phép quản lý component lifecycles mà không cần viết các hàm như componentDidMount, … như trước

– Hook cho phép tái sử dụng state xuyên suốt app

Mời bạn đọc thêm ở [bài này](https://www.patterns.dev/posts/hooks-pattern/) nhé, thú vị lắm ấy!

## Giới thiệu về XState
Hôm nay công ty có bài giới thiệu về XState cực thú vị, nên mình muốn giới thiệu đến bạn qua bài viết nhỏ này.

XState giúp phát triển web, app theo hướng State Machine, tức là lấy state của máy làm trung tâm và phát triển ứng dụng dựa trên sơ đồ các trạng thái và sự chuyển đổi trạng thái thông qua các sự kiện.

Hai điều thú vị mà mình ấn tượng nhất là:

Đầu tiên, sơ đồ trạng thái của ứng dụng được mô tả một cách trực quan, các luồng chạy của ứng dụng có thể được hiểu rõ qua sơ đồ (khi thiết kế trạng thái tương tự diagram) hay có thể chia sẻ luồng dữ liệu ứng dụng mà không cần đọc code.

Điều này sẽ giúp người lập trình suy nghĩ về logic ứng dụng trước khi code, sắp xếp các sự kiện hợp lý, theo đó UX cũng sẽ hợp lý theo vì các trạng thái sẽ chuyển đổi theo tác vụ của người dùng.

Thứ hai, là việc tái sử dụng mô hình state machine này vào các loại ứng dụng khác nhau mà XState hỗ trợ.

Điều này sẽ giúp ứng dụng web (xây dựng với React) và hydrid mobile (xây dựng với React Native) có thể sử dụng chung source code của ứng dụng với XState này. Do đó sẽ làm giảm thời gian lập trình và nhiều nên tảng ứng dụng sẽ có cùng định hướng, cùng sơ đồ trạng thái – single source of true.

Bạn có thể ghé [trang chủ của XState](https://xstate.js.org/) để tìm hiểu thêm.

## 7 repo giúp bạn code React xịn hơn

React - một UI framework, đứng sau bởi Facebook, với hơn 50 triệu dự án mỗi tháng, 9 năm tuổi, được sử dụng rộng khắp từ startup đến Fortune 500 companies.

Giới thiệu đến bạn 7 repo giúp nâng cao kỹ năng với framework này:

30 days of React

- thử thách học React trong 30 ngày kèm với các hướng dẫn chi tiết.
- để học khóa này bạn chỉ cần kiến thức HTML, CSS, JS. Bạn có thể tham khảo thêm repo 30DaysOfJavascript

Awesome React

- các nguồn tài liệu, công cụ trong hệ sinh thái React
- React, React Native, Redux, GraphQL, Relay, các videos, ...

React typescript cheatsheet

- một bảng giúp developer làm quen với TS và React

Learn React App

- Hướng dẫn bạn làm quen với React concepts kèm các bài tập hands-on

React Patterns

- nội dung về các patterns trong React, các mẹo khi sử dụng

Bạn có thể xem qua [các repo này](https://github.com/stars/GraphicDThanh/lists/react/) ở list và star hay fork về tài khoản github của mình để lưu lại nhé.
