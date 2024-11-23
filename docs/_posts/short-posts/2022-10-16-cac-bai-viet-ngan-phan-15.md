---
title: "Các bài viết ngắn - phần 15"
categories:
  - Short Posts
tags:
  - short-post
---
![](assets/images/2022/10/2022-10-16-cac-bai-viet-ngan-phan-15-1.webp)

## Authorization là gì ?

Authorization là quá trình kiểm tra xem người dùng có quyền truy cập vào những phần nhất định nào của ứng dụng hay được thực hiện các thao tác cụ thể nào trên ứng dụng.

Bạn cũng có thể nghe về nó với tên “access control” hay “privilege control”. Lưu ý authorization diễn ra sau quá trình authentication, và bao gồm cả cho phép (grant) và từ chối (deny) các quyền. Ví dụ như blog, người dùng sẽ được quyền comment, nhưng chỉ có người dùng đồng thời là tác giả mới có quyền đăng bài.

vậy kiểm tra bằng cách nào?

**“role-based access control”** – kiểm soát quyền truy cập dựa trên vai trò người dùng trong ứng dụng (viewer, editor, manager, admin, …)

Mỗi role này sẽ có các quyền truy cập nhất định được định nghĩa tuỳ theo cách những loại kỹ thuật bạn dùng.

Ví dụ như trong Django sẽ có sẵn các quyền read, write, edit, view cho từng loại model và bạn có thể kiểm soát quyền truy cập của từng role dựa vào từng loại quyền của model đó.

**“claims-based access control”** – kiểm soát quyền truy cập dựa trên việc kiểm tra các quyền mà người dùng có.

Ví dụ bạn có một trường owner cho phép xác định chủ sở hữu của đối tượng cụ thể nào đó. Hoặc bạn có một trường `account_type` cho phép xác định phân loại người dùng.

Bạn đọc thêm ở [bài viết này](https://www.freecodecamp.org/news/whats-the-difference-between-authentication-and-authorisation/) có thêm ví dụ và sơ đồ minh hoạ nhé.

## "Don't Repeat Yourself" hay DRY

Nói cho dễ hiểu hơn, thì khi bạn bắt gặp mình lặp lại một thao tác giống nhau, như việc copy / paste một đoạn code thì đã đến lúc bạn nên tạo cho nó một hàm để sử dụng lại.

Lợi ích dễ thấy của nguyên tắc này là giúp tái sử dụng code, hay “code resuse”.

Nhưng copy / paste code thì code thì có gì sai cơ chứ ?

Thực ra copy / paste code thì cũng không có gì sai trái, nhưng DRY bên cạnh giúp code reuse ra thì còn giúp lập trình viên ẩn đi những đoạn logic quá chi tiết cho từng phần công việc nhỏ giúp giảm tải khối lượng logic lại, nếu cần truy cập thì sẽ tìm đến nơi viết đọc sau.

Vì thế DRY không chỉ là giảm code lặp. Mà bạn đang chia nhỏ một quá trình phức tạp ra thành từng đoạn công việc nhỏ có tên và nhiệm vụ riêng. Từ đó, việc định nghĩa tên hàm, các biến, giá trị trả về, viết document cho hàm cũng trở nên quan trọng, giúp bạn self-document code base của mình.

https://benwilhelm.com/articles/beyond-dry.html

## Bộ sưu tập git alias
**git alias là gì ?**

`git alias` là các câu lệnh do người dùng tự định nghĩa, hay gọi là alias, các câu lệnh này sẽ đại diện cho một câu lệnh git cụ thể với các lựa chọn tương ứng.

Ví dụ: trong file `.gitconfig` bạn viết tất cả các câu lệnh alias nằm dưới mục [alias]

```
[alias]
	a = add .
```

thì bạn có thể có thể sử dụng `git a` thay cho `git add .`

Vì sao nên sử dụng git alias ?

- tăng hiệu suất làm việc (vì ngắn gọn hơn ^^)
- có thêm một tài liệu tự tạo về các câu lệnh git và có thể sử dụng và học thêm từ các câu lệnh phức tạp

Bạn có thể vào [bài viết sau](https://dev.to/imjoseangel/what-are-your-git-aliases-43om) để xem bộ sưu tập git alias của tác giả nhé.

Một lưu ý nhỏ là nếu bạn dùng `zsh (oh-my-zsh)` thì bạn đã có sẵn bộ git alias được cung cấp sẵn (bạn có thể tìm `“Oh my zsh git alias”` nhé.

## Terminal

Nếu mình ngại làm việc với terminal, thì là mình chưa hiểu về nó đủ.

Vì thế, mình đã tìm hiểu thêm về terminal, về các khái niệm shell, bash, console và bắt gặp một bài viết vô cùng xuất sắc của tác giả, lại là tiếng Việt nữa ^^

Bài viết giúp bạn tìm hiểu kỹ hơn về:

– Shell, các loại shell

Shell tiếng anh là vỏ ^^, là một trình thông dịch dòng lệnh phát triển trên các loại máy có nhân Unix, Linux. Shell cung cấp giao diện để bạn có thể nói chuyện với hệ điều hành.
Bạn có thể gõ trực tiếp lệnh lên terminal hoặc chạy với file .sh

Có nhiều loại shell như bash, zsh, ksh, tcsh, fish, ssh, …

Phổ biến nhất là bash, zsh và mạnh nhất hiện nay là zsh.

– zsh
Tìm hiểu về zsh, cách cài đặt và oh-my-zsh hỗ trợ quản lý plugins và theme của zsh

– phím tắt

Các phím tắt giúp sử dụng terminal hiệu năng hơn

Và một số phím tắt `Chrome` hay dùng

Bạn ghé đọc ở [đây](https://viblo.asia/p/cai-oh-my-zsh-powerlevel10k-toi-uu-va-su-dung-phim-tat-cho-terminal-ORNZqowM50n ) hay lưu lại để đọc dần nhé

## sli.dev
Lập trình viên tạo slide thuyết trình từ source code, bạn đã biết điều này chưa ^^

Sli.dev cung cấp một cách làm slide mới lạ bằng cách sử dụng các công cụ mà lập trình viên quen thuộc như `markdown`, `npm`, `vue`, `vite`, `CSS`, …

Một số tính năng cool ngầu từ `sli.dev`:

**Viết nội dung với markdown**

Nội dung sẽ được viết bằng markdown, một loại ngôn ngữ thân thuộc với lập trình viên khi viết các loại tài liệu.

Điều này sẽ giúp bạn tập trung vào phần nội dung và tách biệt nó với phần thiết kế.

**Dùng themes**

Cho phép sử dụng theme, và các theme này có thể được tải từ cộng đồng thông qua npm, và sử dụng chỉ với một dòng config.

**Thân thiện với lập trình viên**

Cung cấp các hỗ trợ đặc biệt giành cho các đoạn mã, highlight, live coding, …

**Nhanh**

Slide.dev chạy bằng Vite, Vue3 và WindyCSS giúp việc xây dựng slide diễn ra nhanh chóng và các thay đổi lập tức được cập nhật.

**Cho phép tương tác bằng Vue**

Nếu bạn quen thuộc với Vue bạn có thể viết các component bằng Vue và nhúng vào slide của mình

Có thể xuất slide ra dạng PNG, PDF hay host một SPA (Single-page Application)

Các bạn dev thử dùng xem bạn này cool như thế nào nhé. Chỉ việc viết markdown và xài npm có thể quản lý với git thôi là mình đã yêu bạn ý rồi ^^

https://sli.dev/
