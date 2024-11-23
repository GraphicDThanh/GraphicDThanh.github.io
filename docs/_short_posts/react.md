---
title: "Các bài viết ngắn về React"
---

Các bài viết ngắn về "React"
- Những điều thú vị về React
- Hook Pattern
- Giới thiệu về XState
- 7 repo giúp bạn code React xịn hơn

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
