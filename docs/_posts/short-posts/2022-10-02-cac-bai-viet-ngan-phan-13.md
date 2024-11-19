---
title: "Các bài viết ngắn - phần 8"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/10/Short-posts-13.png)

## Trực quan hóa dữ liệu JSON
Khi làm việc với dữ liệu (data), bạn có thể làm việc với một file JSON lớn tới vài trăm dòng là chuyện bình thường. Tệ hơn nữa là dữ liệu JSON của bạn ở dạng thu gọn (minify) thì thường sẽ cần chuyển sang định dạng đẹp hơn (beautify json) để dễ đọc.

Giới thiệu đến bạn một công cụ vô cùng tiện dụng, bạn có thể paste data JSON vào (thậm chí data ở dạng thu gọn) và [JSON Crack](https://jsoncrack.com/) sẽ trực quan hóa dữ liệu JSON của bạn thành đồ thị (graph).

Các điểm mạnh của [JSON Crack](https://jsoncrack.com/):

– Dễ dùng: sử dụng ngay trên website, không cần đăng ký hay đăng nhập. Và có thể paste data, import file data vào

– Hỗ trợ tìm kiếm theo node, và di chuyển qua các node tìm được

– Cho phép tải đồ thị về, có thể sử dụng trên blogs, websites, …

– Dễ dàng chỉnh sửa data trực tiếp trên đồ thị

Bạn có thể lưu lại để khi nào cần thì sử dụng nhé. So cool ^^!

## Form 2022 có gì mới ?
Một số công cụ làm việc với form mới có thể bạn chưa biết.

`.requestSubmit()` là lựa chọn tốt hơn giúp thay thế `.submit()` khi bạn muốn event `'submit'` được trigger đồng thời muốn form được validate. Ví dụ mỗi khi submit như các field có required sẽ là bắt buộc.

Thuộc tính `sumitter` của `event`, hay `event.submitter` cho phép xác định đâu là `DOM` thực hiện submit form khi form có nhiều nút có `type="submit"`

`formdata event` là một sự kiện khá mới được `trigger` khi một `FormData` được khởi tạo với new hoặc mặc định khi form được submit. 
`e.formData` là một FormData instance với các thuộc tính và phương thức cho phép truy cập vào các fields data ở dạng `key / value`. 
(đọc thêm về APIs FormData và ví dụ mình có thử ở đây). 
Vậy là bạn có thể truy cập tất cả data của form khi submit đồng thời có thể chỉnh sửa trước khi gọi trực tiếp API nếu cần.

`showPicker()` của thẻ input cho phép hiển thị UI của các lựa chọn của thẻ input, đó có thể là màu sắc, ngày tháng, …

Thuộc tính `inert` cho phép hiển thị form như ở trạng thái không focus, không click được, và thuộc tính này cũng không áp dụng các style mặc định vào các thành phần. inert tương tự như `aria-hidden="true"`

Bạn có thể xem các ví dụ minh họa ở bài viết [này](https://css-tricks.com/whats-new-with-forms-in-2022/)

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

## Lỗi thường gặp junior developer
Bài viết của một cựu lập trình viên từng làm việc tại Amazon trong 6 năm, bắt đầu từ vị trí thực tập và phát triển lên làm lead nhiều dự án. Anh chia sẻ những lỗi mình từng mắc phải khi làm junior developer:

### Là một junior developer, bạn có quyền
Đừng ngần ngại, thiếu chủ động và tự đánh giá thấp bản thân mình. Những việc này dẫn đến thiếu trách nhiệm và thiếu nghiêm túc trong công việc. Nếu bạn viết code, hãy viết những dòng code tốt nhất của bạn dù quy mô dự án có lớn hay nhỏ.

### Là một junior developer, bạn có từng cạnh tranh với đồng đội
Đừng chỉ tìm những lỗi sai của đồng đội và chỉ ra cho bằng hết trong các buổi review! Đó là cách tệ nhất mà bạn có thể làm cho những mối quan hệ lâu dài.

Thay vào đó, hãy tìm hiểu xem đồng đội đã làm được gì, tế nhị trong việc đưa ra các góp ý, chúc mừng khi họ hoàn thành công việc và giúp đỡ khi cần. Vì sau cùng, chúng ta là đồng đội của nhau.

### Là một junior developer, bạn đã e ngại khi nói chuyện tăng lương
Bạn từng nghĩ việc yêu cầu tăng lương / thăng chức là ích kỷ, nếu làm tốt thì cuối cùng cũng sẽ được và bạn đã không hỏi. Bạn đã bắt đầu minh bạch hơn về mục tiêu và nguyện vọng nghề nghiệp của mình, bắt đầu những cuộc nói chuyện về vấn đề tế nhị này với người quản lý, vì bạn hiểu những cuộc nói chuyện như vậy vừa giúp hiểu về nghề và có tính xây dựng.

### Là một junior developer, bạn đã thiếu sự hiểu biết về dự án
Trong các cuộc họp, hầu như bạn đã không lắng nghe xem đồng đội của mình làm gì, nhưng bạn đã hối tiếc khi gặp các vấn đề khi làm việc chung sau đó hay không hiểu bức tranh chung của dự án. Bạn đã khắc phục bằng cách chủ động lắng nghe và đặt thêm nhiều câu hỏi. Điều này giúp bạn nắm bức tranh chung của dự án và dễ dàng hơn khi làm những phần khác nhau của dự án.

### Là một junior developer, bạn đã nhanh chóng tìm cách đổ lỗi cho người khác
Nếu có gì đó xảy ra với dự án như bug trên production chẳng hạn, bạn đã tìm cách đổ lỗi cho người khác hay từ chối nếu đó không phải mã của mình. Điều này từng làm khó bạn khi làm việc nhóm. Bạn đã khắc phục bằng cách tích cực hơn khi review code của đồng đội để giảm lỗi, và tạo nên một team hoạt động hiệu quả hơn.

Hi vọng bạn đọc những dòng tâm sự này sẽ nhận ra và nhanh chóng vượt qua các lỗi này nhé. 

Thực sự là mình đã từng trải qua tất cả các lỗi trên và cũng có nhiều lỗi đang khắc phục dần ^^ 

[Link ref](https://curtiseinsmann.hashnode.dev/from-an-ex-amazon-team-lead-5-mistakes-i-made-as-a-junior-software-engineer)

## Typescript 4.8
TypeScript 4.8 vừa mới được ra mắt

Nếu bạn chưa quen thuộc với TypeScript, thì đây là ngôn ngữ được xây dựng dựa trên JavaScript kết hợp với các cú pháp về phân loại dữ liệu(types). Các loại types sẽ giúp bạn kiểm soát các loại dữ liệu truyền vào cho từng loại tham số, và sẽ được kiểm tra khi chạy type-checker. Điều này giúp giảm đáng kể các lỗi về chính tả, các tham số chưa được khai báo, khác kiểu dữ liệu mong đợi, …

Vậy TypeScript 4.8 có gì mới?

Phiên bản này đem đến thêm nhiều nguyên tắc kiểm tra cho cờ –strictNullChecks cải thiện các types kết hợp (intersection reduction, union compatibility, narrowing)

– unknown nay được cho phép khi truyền vào biến có kiểu type là {} | null | undefined

– NonNullable nay được hiểu là T & {}

– một giá trị không phải là `null` hay `undefined`, có thể dùng `{}`

Cho phép extends với infer type

Một số cải thiện về hiệu suất với `–build`, `–watch` và `–incremental`

So sánh giá trị với mảng không cho phép, ví dụ `arr === []`

Không cho phép import / export types trong file JavaScript nữa

Chi tiết mời bạn đọc thêm ở [link](https://devblogs.microsoft.com/typescript/announcing-typescript-4-8/)
