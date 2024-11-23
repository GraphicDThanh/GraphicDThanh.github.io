---
title: "Các bài viết ngắn - phần 12"
categories:
  - Short Posts
tags:
  - short-posts
  - javascript
  - blog
  - debug
  - css
---
![](/assets/images/2022/09/2022-09-25-cac-bai-viet-ngan-phan-12-1.webp)

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

## BeautyOnCode - các bài viết được xem nhiều nhất
Hôm kiểm tra blog giật mình nhận ra BeautyOnCode đã xuất bản 86 bài viết. Vậy là cái ngày đạt con số 100 đầu tiên đang tiến tới rất gần 🥰

(Chuyện tâm linh là cứ viết 100 bài là bạn tự dưng nổi tiếng luôn 😅)

Sau khi lướt qua lượt xem nhìn nhận ra có nhiều bài viết đạt số người xem khá ấn tượng, nên mình đã thêm một chuyên mục “Xem Nhiều Nhất” với số lượt xem từ 500 trở lên (có bài hơn 2k views), có 36 bài viết hiện đang ở đây.

Điều là mình vui nhất là các bài viết được xem nhiều nhất lại về kỹ thuật, các chủ đề tech được giới thiệu theo phong cách tự do lại được bạn đọc đón nhận ngày càng nhiều.

Top 5 bài viết trên một ngàn lượt xem về tech:

[“Giới thiệu về Linux”][gioi-thieu-ve-linux] đạt 2252 lượt xem

[“Khám phá đại bản doanh Python series overview”][kham-pha-dai-ban-doanh-python-series-overview] đạt 1517 lượt xem

[“Lớp trong Python”][lop-trong-python] với 1405 lượt xem

[“Iterable, iterator và generator trong Python”][iterable-iterator-va-generator-trong-python] với 1369 lượt xem

[“Làm quen câu lệnh và hệ thống tập tin trong Linux”][lam-quen-cau-lenh-va-he-thong-tap-tin-trong-linux] với 1304 lượt xem

Bật mí nhỏ là đây chỉ mới là lượt xem trực tiếp trên blog cá nhân, bên cạnh đó còn hơn 30 ngàn lượt xem trên viblo, kipalog nữa.

## Kỹ năng debug
Khi gặp bug, hẳn bạn sẽ chăm chăm vào con bug và tìm cách sửa chúng. Tuy nhiên việc fix được một con bug chưa quan trọng bằng việc tìm hiểu nguyên nhân vì sao chúng lại xảy ra và làm sao tránh sinh thêm bug tương tự trong tương lai.

Julia Evans giới thiệu đến bạn một số cách để quy trình debug hiệu quả hơn (từ paper “Learning to Troubleshooting”), bằng cách chú trọng vào nguyên nhân, nâng cao kiến thức để có thêm nhiều manh mối khi debug:

### Học code base

Đầu tiên bạn cần hiểu về code base của dự án, hiểu về cách dự án đang hoạt động.

### Học về hệ thống

Hiểu về ngôn ngữ, thư viện, hệ thống bạn đang sử dụng. Ví dụ như HTTP caching hoạt động ra sao, CORs diễn ra như thế nào, …

### Học về các công cụ

Biết và có thể sử dụng các công cụ debug như debugger, devtools, profilers, trace, dumps …

### Học các chiến lược

Tìm hiểu về các chiến lược có thể debug hiệu quả như viết unit test hay viết một chương trình nhỏ để tái tạo lại bug, in và tracking log, nghỉ ngơi, nói chuyện với người có kinh nghiệm hơn, …

### Học từ trải nghiệm

Không ngại sai và học hỏi nghiêm túc từ các trải nghiệm, giúp đỡ người khác fix bugs cũng là một cách tăng trải nghiệm của bản thân. Cảng nhiều kinh nghiệm thì việc debug sẽ càng dễ dàng hơn.

[Ref link](https://jvns.ca/blog/2022/08/30/a-way-to-categorize-debugging-skills/)

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

Bạn tìm hiểu thêm ở [link][css-trong-js-la-gi]

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


[gioi-thieu-ve-linux]: {{ "" | relative_url }}{% post_url linux/2022-01-30-gioi-thieu-ve-linux %}
[lam-quen-cau-lenh-va-he-thong-tap-tin-trong-linux]: {{ "" | relative_url }}{% post_url linux/2022-06-14-gioi-thieu-ve-cli-va-mot-so-cau-lenh-lam-viec-voi-file-trong-linux %}
[kham-pha-dai-ban-doanh-python-series-overview]: {{ "" | relative_url }}{% post_url python/2020-07-01-dbd-dai-ban-doanh-python-series-overview %}
[lop-trong-python]: {{ "" | relative_url }}{% post_url python/2021-06-30-dbd-lop-trong-python %}
[iterable-iterator-va-generator-trong-python]: {{ "" | relative_url }}{% post_url python/2020-09-09-dbd-iterator-va-generator-trong-python %}
[css-trong-js-la-gi]: {{ "" | relative_url }}{% post_url js/2022-09-14-css-trong-js-la-gi %}
