---
title: "Các bài viết ngắn - phần 28"
categories:
  - Short Posts
tags:
  - short-post
---
![](assets/images/2023/02/2023-02-21-cac-bai-viet-ngan-phan-28-1.webp)

## 20 câu hỏi phổ biến nhất về React
Nếu bạn là React developer, thử trả lời 20 câu hỏi phổ biến nhất về React sau:

1. React là gì và lợi ích của React ?
2. DOM ảo là gì và cách hoạt động ?
3. React xử lý cập nhật và render như thế nào ?
4. Giải thích khái niệm Components trong React
5. JSX là gì và vì sao được sử dụng trong React ?
6. Sự khác nhau giữa state và props trong React ?
7. Sự khác nhau giữa controlled components và uncontrolled component trong React ?
8. Redux là gì và hoạt động cùng React để làm gì ?
9. Giải thích khái niệm HOC trong React
10. Sự khác nhau giữa SSR và CSR trong React
11. React Hook là gì và hoạt động như thế nào ?
12. React xử lý việc quản lý các trạng thái như thế nào ?
13. useEffect hook được dùng như thế nào ?
14. Giải thích khái niệm SSR trong React
15. React xử lý sự kiện như thế nào và các cách phổ biến để xử lý sự kiện là gì ?
16. Giải thích khái niệm React context
17. React xử lý điều hướng trang (routing) như thế nào, và các thư viện phổ biến hỗ trợ routing là gì ?
18. Best practice giúp nâng cao hiệu xuất render trong React, cho ví dụ.
19. Kiểm thử trong React app như thế nào ? Các thư viện hỗ trợ phổ biến ?
20. Làm thế nào xử lý load data bất đồng bộ trong React ?

Đáp án thì bạn vào [đây](https://www.joshwcomeau.com/career/clever-code-considered-harmful/) đọc nha "Top 20 React.JS interview questions. - DEV Community 👩‍💻👨‍💻"
Note: Câu 19 trả lời chưa chính xác, kéo xuống comment đọc về React Testing library nhé.

## Code cao siêu quá lại lợi bất cập hại
Việc code hàng ngày của một lập trình viên khác hoàn toàn việc giải một bài toán khó chỉ chạy trên chiếc máy đời 2004 như dự án Project Euler (yêu cầu những đoạn code ngắn nhất, ít tốn bộ nhớ nhất, chạy nhanh nhất).

Bài giải của một dự án như Euler là những dòng code tối ưu nhất để giải được bài toán này, và thường bạn chỉ viết nó một lần rồi không bao giờ đụng đến nữa.

Code dự án lại khác, liệu một lập trình viên mới vào nghề có hiểu được những dòng code này không?
Đây gọi là "intern test".

Trong ngữ cảnh của việc mã code sẽ được chia sẻ, thì code tốt là code đơn giản và dễ hiểu.
Code đơn giản là code sử dụng các kiến thức cơ bản, chứa ít sự trừu tượng nhất, không có các loại biến bị thay đổi ẩn, ...

Code dài hay ngắn không quan trọng bằng code phức tạp hay đơn giản.

Khi tạo một lớp trừu tượng, bạn cần cân nhắc bởi nó sẽ tạo thêm một lớp nữa khi đọc hiểu và debug code.

Nếu lớp trừu tượng này thay thế cho một trăm đối tượng sắp khởi tạo thì trừu tượng này là xứng đáng. Nếu chỉ dùng ở một nơi và tăng độ phức tạp của code lên thì nên ưu tiên cho sự đơn giản.

Vì thế, việc viết code dễ hiểu đôi khi còn quan trọng hơn cả code clean.
Bạn ghé đọc thêm ở [bài này](https://www.joshwcomeau.com/blog/how-to-learn-stuff-quickly/) nhé!

## Làm sao để học nhanh?
Tất cả các kiến thức của nhân loại đều ở trên Google. Tuy nhiên, việc tiếp cận thông tin mới chỉ là một nửa của câu chuyện, bạn cũng cần có chuyển đổi các thông tin này trở nên hữu dụng cho công việc của mình.

Với hầu hết chúng ta, khoảng cách giữa hai điều này thường là các bài hướng dẫn, và bạn học hết bài này đến bài khác, nhưng không hề cảm thấy mình tiến bộ. Đó gọi là tutorial hell.

Học cách học một cách hiệu quả thì quan trọng, đặc biệt với lập trình viên. Nếu bạn có khả năng nắm bắt nhanh các công nghệ mới, ngôn ngữ, thư viện mới thì bạn có thể vượt lên mức trung bình. Nó như một siêu năng lực vậy.

Một số gợi ý giúp học hiệu quả:
- Kết hợp giữa học cùng hướng dẫn và học không cần hướng dẫn
- Trau dồi tư duy
- Xây dựng mục tiêu và động lực
- Xây dựng thói quen
- Học bằng cách chia sẻ

(Mình thích nhất gợi ý đầu tiên nên mình sẽ lược dịch nội dung đoạn này nhé)

Kết hợp giữa học cùng hướng dẫn và học không cần hướng dẫn

Có hai cách học:
- học theo hướng dẫn: như đọc tài liệu, khoá học, xem video, ...
- học không theo hướng dẫn: tạo dự án từ đầu, mở rộng khoá học, tìm kiếm và xem tài liệu, ...

Nếu bạn chỉ học theo hướng dẫn, bạn sẽ rơi vào tutorial hell. Bạn chưa rèn luyện được kỹ năng cần thiết như xây dựng (develop) và giải quyết vấn đề (problem-solving) để trở thành lập trình viên giỏi. Và không biết bắt đầu từ đâu khi xây dựng một dự án mới.

Ngược lại, nếu tập trung tất cả vào học không theo hướng dẫn, thì quá trình này kéo dài mãi. Không có những kinh nghiệm từ người đi trước, bạn phải giải các bài toán đã cũ, xây dựng tất cả từ đầu, và rất khó để theo đến cùng.

Một số cách giúp kết hợp cả hai:

Cố ý phạm lỗi
Thay vì chỉ làm theo nội dung khoá học, bạn hãy thử làm lại hay thay đổi các câu lệnh. Lỗi chắc chắn sẽ xuất hiện và bạn tiếp tục tìm hiểu về chúng.

Mở rộng các bài hướng dẫn
Thay vì chỉ làm đúng những gì bài hướng dẫn làm, bạn hãy thử mở rộng bài toán như thay đổi luật chơi, mở rộng bài toán, thêm các hiệu ứng, ...

Xây dựng các dự án liên quan đến chủ đề đã học
Học một thứ và xâu dựng một thứ tương tự khác, là cách tuyệt vời để học.

Bạn đọc thêm bài viết của tác giả ở [đây](https://www.joshwcomeau.com/blog/how-to-learn-stuff-quickly/).


## React data binding

Dữ liệu trong React controlled component được ràng buộc hai chiều như thế nào?

Uncontrolled component và controlled component

Khi một input như <input /> được tạo, giá trị của nó sẽ được DOM xử lý mặc định, do đó React không quản lý các giá trị này nên gọi là uncontrolled component.

Khi bạn muốn React quản lý component như input ở trên, bạn sẽ cần sử dụng thêm các biến để quản lý, <input value="Hello"/>.

Đây được gọi là controlled component bởi giá trị của input được React quản lý bởi value truyền vào.

Data binding

Về cơ bản thì React có nguyên lý chung trong việc liên kết dữ liệu như thế này, thường gọi là data binding.

Dữ liệu của input trên được ràng buộc bởi giá trị của “value” trong code.

Dữ liệu ràng buộc một chiều (“one-way” data binding):

value “Hello” ---> input có giá trị “Hello”

Và thường một input component như trên không có giá trị chỉ một chiều như thế.
Để hoàn thiện chiều thứ hai, cần sử dụng thêm một state rồi cho phép giá trị state thay đổi theo điều kiện bên ngoài như việc người dùng nhập giá trị.

Ví dụ:
```js
function App() {
  const [state, setState] = React.useState(‘Hello World’);

  return (
    <input
      value={state}
      onChange={(event) => { setState(event.target.value); }}
    />
    <p> Current value {state} </p>
  )
}
```

Dữ liệu ràng buộc hai chiều (“two-way” data binding):
- giá trị state ---> gán giá trị state vào input
- sự kiện onChange ---> cập nhật giá trị state

Ví dụ trên cũng có thể mở rộng cho các loại component phổ biến khác như checkbox, redio button, selects, ...

Mời bạn đọc thêm ở [bài viết này](https://www.joshwcomeau.com/react/data-binding/).

## Các định dạng màu trong CSS
CSS có nhiều loại định dạng màu sắc khác nhau như: `hex codes`, `rgb()`, `hsl()`, `lch()`

CSS có sẵn 140 màu được đặt tên mà bạn có thể dùng như red, hotpink, tomato, ...
Các màu có sẵn này sẽ tiện dụng khi bạn cần một màu nào đó có thể dùng tạm. Tuy nhiên các màu này lại ít được sử dụng trong các sản phẩm được thiết kế bởi 140 màu là không đủ.

Các định dạng được sử dụng phổ biến nhất là RGB, hex codes, và HSL.

Một số điều thú vị:
- Trong các màu có tên có sẵn, màu "darkgray" lại nhạt hơn màu "gray"
- Có thể viết opacity kèm sau mã màu rgb với dấu /, ví dụ `rgb(255 0 0 / 0.5)`
- Mã màu hex có thể có 8 ký tự sau dấu `#` với 2 ký tự cuối đại diện cho opacity, ví dụ: `#FFFF0080`
- sRGB là "standard RGB color space" bao gồm rgb(), hsl(), hex codes
- một số mã màu khác: display P3, LCH.

Vậy nên chọn mã màu nào để sử dụng?

Định dạng hex codes được dùng phổ biến hơn nhưng định dạng HSL lại có ý nghĩa đọc hiểu hơn. HSL đại diện cho Hue (màu), Saturation (độ bão hòa) và Lightness (độ sáng).

Ví dụ đọc mã màu #FF0000 có thể không rõ là màu gì phải đi xem hiển thị ra sao thì hsl(0deg, 100%, 50%) có thể giúp bạn liên tưởng đến:
- vòng tròn màu sắc, tại 0 độ
- độ bão hòa (saturation) 100%
- độ sáng (Lightness) là 50%.

![](assets/images/2023/02/2023-02-21-cac-bai-viet-ngan-phan-28-2.webp)

Bạn ghé đọc thêm ở [bài viết sau](https://www.joshwcomeau.com/css/color-formats/) để có thêm thông tin nhé.

