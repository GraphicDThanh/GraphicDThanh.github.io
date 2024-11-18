---
title: "Cặp đôi hủy diệt code xấu: DRY và Orthogonality"
excerpt_separator: <!--more-->
categories:
  - Principle
tags:
  - clean-code
  - principle
---

![](/images/2023/01/2023-01-cap-doi-huy-diet-code-xau-dry-va-orthogonality-cover.webp)

Bạn có nghĩ giai đoạn bảo trì (maintenance) là sau khi chương trình được phát hành (release)? Và trong giai đoạn này là các công việc như fix bugs, hay cải thiện các tính năng?

Mình cũng từng nghĩ vậy, nhưng nghĩ vậy là chưa đúng.

Lập trình viên luôn ở trong giai đoạn bảo trì. Bởi sự hiểu của chúng ta thay đổi mỗi ngày, yêu cầu dự án, môi trường, … cũng thường xuyên cập nhật trong khi bạn đang thiết kế, đang code.

Có hai vấn đề thường gặp nhất là code bị lặp lại và code bị phụ thuộc lẫn nhau gây bảo trì khó khăn. 

Trong bài viết này mình sẽ giới thiệu đến bạn hai nguyên tắc giúp giải quyết hai vấn đề này. 

**Nguyên tắc 1:** **DRY** (Don’t repeat your self) – Không lặp code

**Nguyên tắc 2:** **Orthogonal** – Trực giao

## DRY hay không viết code lặp
Định nghĩa từ [wiki](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself):

> **“Don’t repeat yourself”** (DRY) là một nguyên tắc phát triển phần mềm nhằm giảm sự lặp lại các thành phần trong chương trình, thay vào đó sử dụng các khái niệm trừu tượng hoặc sử dụng chuẩn hóa data để giảm thiểu sự dư thừa.

Khi viết code theo nguyên tắc DRY, khi bạn thay đổi một chỗ, sẽ không cần nhớ phải đổi 2,3 chỗ tương tự. Hay tệ hơn nữa là đổi một chỗ mà những chỗ khác bị sai đi. Và chắc chắn là sẽ có lúc bạn không thể nhớ hết được tất cả các nơi, vậy nên ngay từ đầu hãy viết code theo nguyên tắc này.

### Một số lý do code bị lặp

Nhưng vì sao code ngày càng bị lặp? 

Có 4 lý do chính và các gợi ý giúp cải thiện:

**Lặp vì không thể tránh khỏi**

Đôi khi có yêu cầu viết code rõ ràng, lặp nhau vì những mục tiêu cụ thể của dự án (ví dụ như nhiều nền tảng) hay những ngôn ngữ yêu cầu như vậy.

Khi đó có một số cách để giúp bạn cải thiện như sử dụng chung các loại tài liệu chung (database chema, pseudo code), comment code, viết document, …

**Lặp vì không biết nó bị lặp**

Điều này thường xảy ra. Ban đầu, bạn thiết kế chương trình theo yêu cầu A, sau đó chương trình thay đổi yêu cầu sang B và code bạn thiết kế không phù hợp nữa dẫn đến bị lặp.

Các quy tắc chuẩn hoá cơ sở dữ liệu, các nguyên tắc trong lập trình hướng đối tượng như SOLID là những cách giúp bạn cải thiện việc thiết kế chương trình.

**Lặp vì không cẩn thận, vội vàng**

Mọi dự án đều có áp lực về thời gian, và dễ dàng thúc đẩy bạn đi đường nào ngắn nhất để “xong”.

Tuy nhiên, sự vội vàng này sẽ mang hậu quả lâu dài. Bạn có thể tiết kiệm thêm 5 phút bây giờ nhưng mất vài tiếng hay thậm chí vài ngày để sửa một con bug (vì không nhớ mình duplicate ra bao nhiêu nơi), hay thậm chí có thể gây dự án thất bại.

**Lặp vì có nhiều thành viên và mỗi người code một phần trùng logic nhau**

Làm việc chung nhiều dev dễ dẫn đến trùng lặp. Ví dụ như việc kiểm tra id truyền vào có phải là số hay không, mỗi người làm ở những nơi khác nhau lại thực hiện kiểm tra này khác nhau.

Để giảm thiểu tình trạng này, việc review code lẫn nhau trở nên quan trọng trong việc duy trì tính thống nhất của dự án. Các thiết kế chung, các buổi thảo luận sẽ giúp cập nhật, một nơi chung cho những utils dùng lại sẽ có ích.

## Orthogonality hay tính trực giao

Định nghĩa từ [wiki](https://en.wikipedia.org/wiki/Orthogonality):

> Trong toán học, **tính trực giao** là khái niệm hình học chỉ hai đường thẳng vuông góc. Mở rộng hơn, trực giao cũng sử dụng để nói sự tách biệt các tính năng của một hệ thống. 

**Orthogonality** (trực giao) là khái niệm từ hình học chỉ hai đường thẳng vuông góc. Tức là khi một giá trị chạy dọc theo đường này thì giá trị của đường kia không thay đổi. 

Ví dụ như hai trục x, y là trực giao với nhau tại 0. Tức giá trị nào trên x cũng có y là 0 và ngược lại.

Trong máy tính, khái niệm này đại diện cho hai thành phần hay đối tượng độc lập nhau. Tức là nếu thay đổi thành phần này sẽ không làm thay đổi thành phần kia.

Orthogonality giúp xây dựng dự án dễ thiết kế, chạy, kiểm thử và mở rộng.

Ví dụ việc thay đổi interface như DBMS (database management system) sẽ không ảnh hưởng đến database.

### Lợi ích của thiết kế theo hướng trực giao

**Tăng hiệu suất**

– thay đổi diễn ra độc lập giữa các thành phần nên chỉ cần thay đổi và kiểm thử cụ thể trên thành phần đó, giảm thời gian lập trình.

– các thành phần độc lập nên dễ tái sử dụng

– kết hợp các thành phần độc lập cũng dễ dàng hơn

**Giảm rủi ro**

– giảm code liên quan giữa các thành phần

– nếu một thành phần bị lỗi thì sẽ không ảnh hưởng nhiều đến cả hệ thống, dễ debug

– dễ kiểm thử từng thành phần

– hạn chế bị phụ thuộc

### Áp dụng Orthogonality trong thực tế

**Team dự án**

Một team hoạt động hiệu quả khi mọi thành viên đều biết mình cần phải làm gì và đóng góp tích cực. Nếu một team luôn cãi nhau, công việc người này phụ thuộc vào người khác, một sự thay đổi nhỏ cũng cần sự có mặt của rất nhiều người bởi ai cũng có thể bị ảnh hường … 

Thì đó thường là vấn đề của tính trực giao (Orthogonality).

Cách giải quyết tùy thuộc vào từng dự án và số người trong dự án. Có thể là phân chia các thành phần khác nhau riêng biệt như FrontEnd, BackEnd, DevOps hay phân tách từng loại feature một thành viên chịu trách nhiệm.

Nếu bạn muốn kiểm tra team mình có bị vấn đề này không, cứ để ý vào số người tham gia các cuộc họp sẽ rõ. Càng ít người thì team càng có tính trực giao tốt.

**Thiết kế**

Hầu hết các lập trình viên đều quen thuộc với các khái niệm mà nằm bên dưới là tính trực giao được áp dụng như module, component-based, layer, … 

Hệ thống nên được cấu thành bởi các các thành phần (module) tách biệt nhau, hoặc được tổ chức thành các lớp (layer).

Khi thiết kế chương trình, hãy tự hỏi xem một thành phần thay đổi sẽ ảnh hưởng đến bao nhiêu loại khác? Nếu một hệ thống thiết kế trực giao thì câu trả lời là “một”. Thực tế thì hãy làm con số trả lời này thấp nhất có thể.

Các loại mô hình như MVC (Model-View-Controller) sẽ giúp thiết kế chương trình trực giao hơn.

**Bộ công cụ và thư viện**

Hãy cẩn thận khi sử dụng các thư viện bên thứ ba. Và mỗi lần cần sử dụng, hãy lưu ý tình huống xấu nhất có thể xảy ra là gì và cố gắng hạn chế tối đa sự phụ thuộc vào các thư viện này.


**Lập trình**

Một số cách gợi ý dành cho code:

– Giữ mã code tách rời nhau

– Tránh dữ liệu toàn cục

– Tránh các hàm tương tự nhau

Tập thói quen quan sát và cân nhắc code của bạn, tìm cách để cải thiện cấu trúc và tăng tính trực giao.

**Kiểm thử**

Việc xây dưng một hệ thống trực giao sẽ giúp dễ dàng cho việc kiểm thử từng thành phần riêng biệt. Mỗi mô-đun sẽ có unit test riêng đảm bảo chúng hoạt động.

Khi fix bug, là cơ hội để bạn kiểm tra về tính trực giao của chương trình, bao nhiêu nơi ảnh hưởng, bao nhiêu thành phần cần chỉnh sửa, …

**Tài liệu**

Trực giao cũng áp dụng trong việc viết tài liệu, các trục là nội dung và cách trình bày. Các công cụ như sheet hay macro, hay map giúp thể hiện nội dung độc lập hơn.

---

Orthogonality và DRY là bộ đôi không thể thiếu đi cùng nhau. Với DRY, bạn viết code ít hơn, và với Orthogonality thì bạn viết code ít phụ thuộc lẫn nhau hơn.

Áp dụng cả hai sẽ giúp hệ thống của bạn linh hoạt, dễ hiểu, dễ debug, test và dễ bảo trì.
