---
title: "Các bài viết ngắn về Software Principles"
---

Các bài viết ngắn về "Software Principles"
- CRUD
- DRY
- Orthogonality
- MVC
- SOLID

## CRUD là gì?
Thuật ngữ CRUD, hay CRUD Operation được sử dụng khá phổ biến, đó không phải là một từ mà là viết tắt của Create – Read – Update – Delete, đại diện cho 4 hoạt động chính của một ứng dụng

Ví dụ bạn tạo một app các công việc cần làm (todo list), thì sẽ cần người dùng nhập các công việc cần làm (create), xem được danh sách các công việc (read), thay đổi nội dung công việc (update) hoặc xoá công việc khi không cần làm nữa (delete).

Một ứng dụng CRUD sẽ bao gồm 3 phần chính: server (API) : truyền dữ liệu database : lưu dữ liệu client app (UI) : hiển thị dữ liệu, nơi người dùng nhập dữ liệu

CRUD cũng tương ứng với các phương thức HTTP cụ thể: Create tương ứng với POST Read tương ứng với GET Update tương ứng với PUT/PATCH. PUT là update toàn phần, PATCH là update một phần Delete tương ứng với DELETE

Bạn có thể đọc thêm về các ví dụ ở [link sau](https://www.freecodecamp.org/news/crud-operations-explained/).


## "Don't Repeat Yourself" hay DRY

Nói cho dễ hiểu hơn, thì khi bạn bắt gặp mình lặp lại một thao tác giống nhau, như việc copy / paste một đoạn code thì đã đến lúc bạn nên tạo cho nó một hàm để sử dụng lại.

Lợi ích dễ thấy của nguyên tắc này là giúp tái sử dụng code, hay “code resuse”.

Nhưng copy / paste code thì code thì có gì sai cơ chứ ?

Thực ra copy / paste code thì cũng không có gì sai trái, nhưng DRY bên cạnh giúp code reuse ra thì còn giúp lập trình viên ẩn đi những đoạn logic quá chi tiết cho từng phần công việc nhỏ giúp giảm tải khối lượng logic lại, nếu cần truy cập thì sẽ tìm đến nơi viết đọc sau.

Vì thế DRY không chỉ là giảm code lặp. Mà bạn đang chia nhỏ một quá trình phức tạp ra thành từng đoạn công việc nhỏ có tên và nhiệm vụ riêng. Từ đó, việc định nghĩa tên hàm, các biến, giá trị trả về, viết document cho hàm cũng trở nên quan trọng, giúp bạn self-document code base của mình.

[read more](
https://benwilhelm.com/articles/beyond-dry.html)


## Don't repeat yourself hay DRY (2)
Bạn có nghĩ giai đoạn bảo trì (maintenance) là sau khi chương trình được phát hành (release)? Và trong giai đoạn này là các công việc như fix bugs, hay cải thiện các tính năng?

Mình cũng từng nghĩ vậy, nhưng nghĩ vậy là chưa đúng.

Lập trình viên luôn ở trong giai đoạn bảo trì. Bởi sự hiểu của chúng ta thay đổi mỗi ngày, yêu cầu dự án, môi trường, … cũng thường xuyên cập nhật trong khi bạn đang thiết kế, đang code.
Vì thế vấn đề về lặp code cũng dễ dàng xảy ra, và đó là vấn đề lớn nhất thường gặp gây khó khăn cho việc bảo trì.
Cách tốt nhất để giúp chương trình dễ hiểu và dễ bảo trì, là tuân theo nguyên tắc DRY – Don’t Repeat YourSelf.

Khi đó bạn thay đổi một chỗ, sẽ không cần nhớ phải đổi 2,3 chỗ tương tự. Hay tệ hơn nữa là đổi một chỗ mà những chỗ khác bị sai đi. Và chắc chắn là sẽ có lúc bạn không thể nhớ hết được tất cả các nơi, vậy nên ngay từ đầu hãy viết code theo nguyên tắc DRY.
Nhưng vì sao code ngày càng bị lặp?

**Có 4 lý do chính:**

### Lặp vì không thể tránh khỏi
Đôi khi có yêu cầu viết code rõ ràng, lặp nhau vì những mục tiêu cụ thể của dự án (ví dụ như nhiều nền tảng) hay những ngôn ngữ yêu cầu như vậy.
Khi đó có một số cách để giúp bạn cải thiện như sử dụng chung các loại tài liệu chung (database chema, pseudo code), comment code, viết document, …

### Lặp vì không biết nó bị lặp
Điều này thường xảy ra. Ban đầu, bạn thiết kế chương trình theo yêu cầu A, sau đó chương trình thay đổi yêu cầu sang B và code bạn thiết kế không phù hợp nữa dẫn đến bị lặp.
Các quy tắc chuẩn hoá cơ sở dữ liệu, các nguyên tắc trong lập trình hướng đối tượng như SOLID là những cách giúp bạn cải thiện việc thiết kế chương trình.

### Lặp vì không cẩn thận, vội vàng
Mọi dự án đều có áp lực về thời gian, và dễ dàng thúc đẩy bạn đi đường nào ngắn nhất để “xong”.
Tuy nhiên, sự vội vàng này sẽ mang hậu quả lâu dài. Bạn có thể tiết kiệm thêm 5 phút bây giờ nhưng mất vài tiếng hay thậm chí vài ngày để sửa một con bug (vì không nhớ mình duplicate ra bao nhiêu nơi), hay thậm chí có thể gây dự án thất bại.

### Lặp vì có nhiều thành viên và mỗi người code một phần trùng nhau
Làm việc chung nhiều dev dễ dẫn đến trùng lặp. Ví dụ như việc kiểm tra id truyền vào có phải là số hay không, mỗi người làm ở những nơi khác nhau lại thực hiện kiểm tra này khác nhau.
Để giảm thiểu tình trạng này, việc review code lẫn nhau trở nên quan trọng trong việc duy trì tính thống nhất của dự án. Các thiết kế chung, các buổi thảo luận sẽ giúp cập nhật, một nơi chung cho những utils dùng lại sẽ có ích.

Vì thế, hãy viết code dễ dàng tái sử dụng.
—
Lược dịch từ sách “Dragmatic Programmer”

## Orthogonality (trực giao)
Orthogonality (trực giao) là khái niệm từ hình học chỉ hai đường thẳng vuông góc. Tức là khi một giá trị chạy dọc theo đường này thì giá trị của đường kia không thay đổi.

Ví dụ như hai trục x, y là trực giao với nhau tại 0. Tức giá trị nào trên x cũng có y là 0 và ngược lại.

Trong máy tính, khái niệm này đại diện cho hai thành phần hay đối tượng độc lập nhau. Tức là nếu thay đổi thành phần này sẽ không làm thay đổi thành phần kia.
Orthogonality giúp xây dựng dự án dễ thiết kế, chạy, kiểm thử và mở rộng.
Ví dụ việc thay đổi interface như DBMS (database management system) sẽ không ảnh hưởng đến database.

Orthogonality trong thiết kế phần mềm còn là sự kết hợp của hai nguyên tắc: strong cohesion (gắn kết chặt chẽ) và loose coupling (khớp nối lỏng lẻo).
Strong cohesion ý chỉ bên trong mỗi thành phần nên được kết nối chặt chẽ. Nếu một thành phần mà có nhiều bộ phận rời rạc thì cũng nên được tách ra thành các thành phần riêng lẻ.
Loose coupling ý chỉ giữa các thành phần nên có ít khớp nối. Nếu hai thành phần có kết nối chặt chẽ thì chúng nên gộp lại làm một hoặc nên tách chia theo cách khác để có nhiều thành phần độc lập hơn.

**Lợi ích của thiết kế theo hướng trực giao:**

**Tăng hiệu suất**

– thay đổi diễn ra độc lập giữa các thành phần nên chỉ cần thay đổi và kiểm thử cụ thể trên thành phần đó, giảm thời gian lập trình.

– các thành phần độc lập nên dễ tái sử dụng

– kết hợp các thành phần độc lập cũng dễ dàng hơn

**Giảm rủi ro**

– giảm code liên quan giữa các thành phần

– nếu một thành phần bị lỗi thì sẽ không ảnh hưởng nhiều đến cả hệ thống, dễ debug

– dễ kiểm thử từng thành phần

– hạn chế bị phụ thuộc

**Áp dụng tính trực giao trong lập trình:**
– Giữ mã code tách rời nhau
– Tránh dữ liệu toàn cục
– Tránh các hàm tương tự nhau

Tập thói quen quan sát và cân nhắc code của bạn, tìm cách để cải thiện cấu trúc và tăng tính trực giao.

Đọc thêm về cặp đôi hủy diệt code xấu DRY và Orthogonality ở [bài viết sau][cap-doi-huy-diet-code-xau]


## MVC là gì?

Lập trình web ngày càng phát triển, từ ban đầu là các trang web tĩnh chỉ với HTML / CSS rồi phát triển lên trang web động và các hệ thống web ngày càng trở nên đồ sộ với sự làm việc chung của cả ngàn lập trình viên.

Để làm việc với hệ thống ngày càng phức tạp, có nhiều mô hình kiến trúc khác nhau để phân chia code sao cho đỡ phức tạp hơn và dễ dàng làm việc với nhiều người.

Mô hình được sử dụng phổ biến nhất là MVC (Model – View – Controller).

MVC giúp phân chia một ứng dụng lớn thành từng nhóm cụ thể khác nhau với mục đích và nhiệm vụ khác nhau.

Các thành phần:

– Model: Là trung tâm của MVC, model là cấu trúc dữ liệu của ứng dụng, đứng độc lập với giao diện người dùng, chịu trách nhiệm quản lý dữ liệu, xử lý logic.

– View: Là giao diện của ứng dụng

– Controller: Là bộ điều khiển, nhận đầu vào là các yêu cầu và xử lý bằng cách gọi đến View, Model.

Trong mô hình này, Model và View sẽ không tương tác với nhau, chỉ có Controller là nói chuyện với cả Model và View.

![](/assets/images/2022/09/2022-09-08-cac-bai-viet-ngan-phan-11-1.webp)

([Read more here](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller))


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


[cap-doi-huy-diet-code-xau]: {{ "" | relative_url }}{% post_url principles/2023-01-01-cap-doi-huy-diet-code-xau-dry-va-orthogonality %}
[gioi-thieu-ve-linux]: {{ "" | relative_url }}{% post_url linux/2022-01-30-gioi-thieu-ve-linux %}