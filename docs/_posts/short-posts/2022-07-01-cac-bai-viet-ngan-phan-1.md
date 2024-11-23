---
title: "Các bài viết ngắn - phần 1"
categories:
  - Short Posts
tags:
  - short-posts
  - git
  - database
  - website
  - career
  - life
---

![](/assets/images/2022/07/2022-07-01-cac-bai-viet-ngan-phan-1.webp)

## .gitkeep
File .gitkeep thường được biết đến như là cách để có thể commit một thư mục trống lên trong quá trình thiết kế cấu trúc thư mục cho dự án của bạn.

Ví dụ cấu trúc một website đơn giản:
```
src/
|-- assets/
  |-- images/
|-- styles/
  |-- main.css
index.html
README.md
```

Nếu không có `.gitkeep` trong thư mục `“images”` thì mình không thể commit cả hai thư mục `“assets”` và `“images”` lên repo được, kết quả là không giữ được cấu trúc thư mục như trên(hình 1)

![](/assets/images/2022/06/2022-06-02-gitkeep-1.webp)

Và đây là kết quả khi đặt .gitkeep trong thư mục `“images”`, cấu trúc thư mục sẽ được đảm bảo(hình 2)

![](/assets/images/2022/06/2022-06-02-gitkeep-3.webp)

**Câu hỏi đặt ra là**: tại sao lại là `.gitkeep`? Có thể dùng file khác thay thế được không?

**Trả lời**: CÓ thể dùng file khác thay thế! Ví dụ: text.txt hay thậm chí là `.gitignore`

Tuy nhiên vì mục đích của file này là giữ cho một thư mục có thể trống, theo nghĩa đen của nó, nên theo cách làm tiêu chuẩn sẽ là một file có đủ ý nghĩa trên:

– `.gitkeep` là file ẩn

– `.gitkeep` mang ý nghĩa đúng với vai trò của nó

Hi vọng bạn sẽ nhớ đến `.gitkeep` khi cần commit thư mục trống và hiểu thêm vì sao lại dùng bạn ấy nhé! Cơ mà nói chứ bạn sẽ ít xài lắm, vì thư mục có khi nào trống đâu haha.

## Redis cơ bản cho người mới bắt đầu
Redis là một cơ sở dữ liệu trong bộ nhớ(in memory database) 📀, dữ liệu được lưu trữ theo dạng key-value 🔑 🔤 tức là từ khóa và giá trị của nó.

👩‍🍳 Redis thường sử dụng như là một cơ sở dữ liệu caching 📜, có tốc độ truy cập rất nhanh 💨

💻 Để làm quen với Redis, cài đặt nhanh trên Mac với `brew install redis`, sau đó chạy server với `redis-server`.

Sau khi server được khởi chạy, bạn có thể bắt đầu làm quen với các câu lệnh cơ bản trong Redis bằng cách sử dụng CLI, mở một cửa sổ mới và gõ lệnh “redis-cli”

🧐 Câu lệnh `SET`, `GET`, `EXISTS`, `KEYS`

Vì lưu trữ dạng key-value nên câu lệnh cơ bản nhất sẽ là:

– gán trị vào từ khóa(set value to key): `SET <key> <value>`

– lấy giá trị ra từ từ khóa(get value from key): `GET <key>`

– kiểm tra xem từ khóa có trong bộ nhớ không: `EXIST <key>`

– tìm kiếm từ khóa theo pattern: `KEYS <pattern>`

Một bộ `key-value` cũng có thể được set thời gian nó tồn tại với từ khóa `EXPIRE <key> <time>`

Ngoài ra, Redis cũng có nhiều kiểu dữ liệu khác được lưu cho value như: `list`, `sets`, `hashes` và các từ khóa tương ứng sử dụng cho từng kiểu dữ liệu trên.

Mời bạn ghé đọc [bài viết này][basic-knowledge-about-redis] để tìm hiểu thêm và có video hướng dẫn để bạn có thể thực hành nữa ấy.

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

## Tài khoản tiết kiệm sự nghiệp
Bạn sẽ làm gì khi **“bị sa thải bất ngờ”** 😭, có thể vì mâu thuẫn với sếp, đồng nghiệp 😕, hay bế tắc trên con đường phát triển 🥺, hay thậm chí là ở một nơi an toàn quá lâu 🥲 và khi khủng hoảng ập đến làm bạn mất đi công việc đã gắng bó và cống hiến bao lâu nay 😅? 

“Nhảy việc hay thay đổi chính mình” 👍 – một cuốn sách của Jon Acuff, với tựa đề thật là “thách thức” 💪, đã đề cập đến một “Tài khoản tiết kiệm sự nghiệp” 🔑 – một vũ khí bí mật giành cho sự nghiệp của bạn khi có những sự cố bất ngờ như thế ập đến. 

Vậy “Tài khoản tiết kiệm sự nghiệp” là gì? ✨ ✨ ✨ 

```
Tài khoản tiết kiệm sự nghiệp 

= (Mối Quan Hệ + Kỹ Năng + Phẩm Chất) * Nhiệt Huyết 
```

Các định nghĩa 🧐: 

😀 **Mối quan hệ** = những người mà bạn quen biết, nhóm người mà bạn có mối quan hệ mật thiết trong quá trình làm việc 

⚒ **Kỹ năng** = những điều bạn có thể làm được, cầu nối giữa kẻ nghiệp dư và chuyên gia 

😊 **Phẩm chất** = con người bạn, chất keo gắn kết toàn bộ các yếu tố lại với nhau 

🥰 **Nhiệt huyết** = cách làm việc của bạn, nhiên liệu thúc đẩy bạn làm những việc mà người khác không làm, và vì thế bạn có thể tận hưởng những thành quả đạt được trong khi người khác thì không 

Và [link sách](https://ti.ki/M39Oj1kb/CAREER-UP) nếu bạn thích tậu bản giấy về nghiên cứu nè.

## Những quy luật của đời người
Những quy luật của **“đời người”**:

🫶 Bạn sẽ có một cái thân. Bạn có thể thích nó hay ghét nó, nhưng nó sẽ là của bạn trong suốt cả quãng đời này.

🫶 Bạn sẽ phải học các bài học. Bạn học trọn thời gian trong một ngôi trường không chính thức được gọi là cuộc đời. Mỗi ngày trong ngôi trường này bạn sẽ có cơ hội để học bài. Bạn có thể thích các bài học ấy hay nghĩ rằng chúng chẳng liên quan gì hay thậm chí còn rất ngu ngốc nữa.

🫶  Ở đó không có sai lầm, chỉ có các bài học. Trưởng thành là một quá trình thử nghiệm để phát hiện chỗ sai rồi sửa, một quá trình thử nghiệm. Những thử nghiệm thất bại cũng là một phần quan trọng trong quá trình ấy, không khác gì những thử nghiệm thành công. Về lâu dài, chúng ta sẽ nhận những gì mình xứng đáng được nhận.

🫶 Một bài học sẽ lặp đi lặp lại nhiều lần cho đến khi chúng ta học xong bài học ấy. Một bài học sẽ thể hiện ra dưới nhiều hình thức khác nhau cho đến khi bạn đã học xong. Học xong rồi, bạn mới có thể chuyển sang bài học kế tiếp. 

🫶 Quá trình học hỏi không bao giờ chấm dứt. Không có phần nào trong cuộc sống của chúng ta mà không chứa đựng những bài học ấy cả. Chừng nào bạn còn sống, chừng đó vẫn còn có những bài học cần phải học.

🫶 “Ở chỗ kia” không có gì tốt hơn “ở chỗ này”. Khi “chỗ kia” đó biến thành “chỗ này”, bạn sẽ lại thấy một “chỗ kia” khác tốt hơn “chỗ này” nữa.

🫶 Mọi người chỉ là một tấm gương để bạn tự soi lại chính mình. Khi bạn yêu hay ghét điều gì đó của người khác, nghĩa là bạn cũng đang yêu hay ghét chính những điều đó trong bản thân mình.

🫶 Bạn muốn tạo nên cuộc đời mình như thế nào là tùy thuộc vào chính bạn. Bạn có tất cả mọi công cụ và mọi nguồn lực mình cần. Sử dụng chúng như thế nào là tuỳ thuộc vào bạn. Sự lựa chọn là của bạn.

🫶 Các câu trả lời nằm bên trong bạn. Câu trả lời cho các câu hỏi của cuộc đời bạn ở bên trong bạn. Tất cả những gì bạn cần làm chỉ là quan sát, lắng nghe và tin tưởng.

🫶 Rồi bạn sẽ quên tất cả những điều này.

Đối với tôi, nó giống như một bản hướng dẫn cho những người chuẩn bị được sinh ra làm người. Chúng ta hãy cùng xem lại những lời hướng dẫn này một cách kỹ lưỡng hơn nhé.

Trích dẫn từ cuốn “Cuộc đời là một trường học”

[basic-knowledge-about-redis]: {{ "" | relative_url }}{% post_url database/2022-05-28-basic-knowledges-about-redis %}
[chien-luoc-tai-thuc-thi-code-javascript]: {{ "" | relative_url }}{% post_url js/2022-04-17-chien-luoc-tai-thuc-thi-code-javascript %}