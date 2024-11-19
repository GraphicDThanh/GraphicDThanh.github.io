---
title: "Các bài viết ngắn - phần 8"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/09/Short-posts-11.png)
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
    

## Bạn chia sẻ file qua internet như thế nào?
    
Có thể bạn gửi qua email(với giới hạn 25MB), trực tiếp qua slack(cả workspace có dung lượng tói đa 5GB), messenger(giới hạn 25MB), hoặc tải lên drive rồi gửi link chia sẻ, …

Giới thiệu thêm hot trend vô cùng mạnh mẽ, Wormhole (wormhole.app)

Vậy tại [Wormhole](https://wormhole.app/) có gì đặc biệt?

– Đơn giản và nhanh chóng Bạn sẽ không cần đăng ký tài khoản hay đăng nhập, không yêu cầu địa chỉ email của bạn. Chỉ cần mở web/app lên, chọn file tải lên và thế là xong, trong chưa đầy 2 phút! Bạn có ngay một đường dẫn để chia sẻ trực tiếp hoặc qua email, mã QR code.

– Tùy chọn để xóa tập tin Bạn có thể tùy chọn sau một thời gian hay số lượt tải nhất định tập tin sẽ bị xóa.

– Thời gian xóa là từ 60 phút đến tối đa là 24 giờ. Số lượt tải từ 1 đến tối đa là 100. Điều này giúp bạn kiểm soát được dữ liệu của mình, tránh tình trạng lạc trôi trên internet.

– Tập tin được mã hóa đầu cuối. Tập tin của bạn sẽ thực sự được mã hóa đầu cuối(end-to-end encryption) giúp cho dữ liệu của bạn được bảo mật (đọc thêm ở [đây](https://wormhole.app/about)).

– Phát trực tiếp các tệp tức thì, không yêu cần phải tải hết lên xong rồi mới phát đi

– Không có quảng cáo

Hi vọng công cụ này sẽ giúp bạn chia sẻ file một cách nhanh chóng và bảo mật hơn nhé.
    
## Điều gì xảy ra khi một chương trình JavaScript được thực thi?

Mọi thứ trong JavaScript diễn ra bên trong một ngữ cảnh thực thi, hay **“Execution Context”**. Có hai giai đoạn trong **“Execution Context**” là **“Memory Creation”** và **”Code Execution"**

Khi chương trình JS khởi chạy, một execution context ở global sẽ được tạo. Ở giai đoạn **“Memory Creation Phase”**, bộ nhớ được cấp cho tất cả các biến và các hàm.

Ở giai đoạn **“Code Execution”**, code sẽ được thực thi từng dòng một theo thứ tự trên xuống dưới.

Nếu có một hàm được gọi, một **Execution Context** dành riêng cho hàm đó sẽ được tạo và thực hiện tương tự với hai giai đoạn trong **Execution Context** mới này. Khi một hàm kết thúc thực thi, thì **Execution Context** này sẽ được xóa đi.

Và cứ thế, chạy cho đến hết chương trình.

Quá trình ở trên thường được gọi là **call stack**

Mỗi execution context được tạo sẽ được bỏ vào(**push**) vào ngăn xếp(**stack**)

Mỗi execution context bị xóa sẽ được lấy ra khỏi(**pop**) ngăn xếp(**stack**)

Đây chính là cách JS Engine thực thi code.

Mời bạn đọc chi tiết về quá trình này kèm ví dụ và hình ảnh minh họa ở [blog post này](https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/) nhé.


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

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/09/mvc.png)

[Read more here](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)

## Hoisting trong JavaScript

Điều khiến JavaScript khó hiểu với những người mới hay chuyển từ ngôn ngữ khác qua chính là JavaScript cho phép sử dụng biến và hàm ngay cả trước cả khi bạn khai báo chúng.

Vậy điều gì đã khiến mình có thể truy cập vào các biến và hàm ngay cả khi chúng chưa được khai báo? Đó chính là cơ chế Hoisting trong JavaScript.

Bạn có nhớ hai giai đoạn của một “Execution Context” là Memory Creation và Code Execution(đọc thêm ở [bài viết này](https://beautyoncode.com/dieu-gi-xay-ra-khi-chay-mot-chuong-trinh-javascript/)).

Hoisting trong JavaScript chính là sau giai đoạn Memory Creation, các biến và hàm sẽ được cấp bộ nhớ trước khi code được thực thi, biến được cấp bộ nhớ với giá trị undefined , còn hàm thì sẽ được cấp bộ nhớ cho toàn bộ nội dung bên trong hàm f nameFunction(). Vì thế, bước vào giai đoạn thực thi Code Execution, thì các giá trị này đã có sẵn để sử dụng.

Hoisting trong JS sẽ dễ gây hiểu nhầm nếu bạn không hiểu về JavaScript Engine nên bạn cần tìm hiểu cơ chế này để dễ debug chương trình của mình nhé.

Mời bạn đọc thêm chi tiết ở [bài blog này](https://beautyoncode.com/hoisting-trong-javascript/).
