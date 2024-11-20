---
title: "Các bài viết ngắn - phần 31"
categories:
  - Short Posts
tags:
  - short-post
---

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2023/04/short-posts-31.png)

## Blog từ tiết kiệm đến miễn phí
Chia sẻ kinh nghiệm viết blog từ tiết kiệm đến miễn phí

Khi bắt đầu tập viết blog cá nhân, bạn sẽ cần có nơi host trang web và domain riêng của trang, hoặc bạn sẽ được giới thiệu, hướng dẫn nên làm như thế ^^

Blog beautyoncode.com hiện tại đang sử dụng wordpress, host trên stablehost và domain godaddy. Mỗi năm tốn khoảng hơn 1 triệu để duy trì (thuê domain hàng năm và thuê host 3 năm).

Khi mới bắt đầu, mình chọn wordpress xây dựng sẵn vì nó dễ sử dụng nhất, mình dùng wordpress plugin elementor để xây dựng trang web từ các khối kéo thả và viết nội dung là công việc chính.

Sau một thời gian sử dụng, có một số bất tiện với dev như mình:
– bài viết lập trình thường có nhiều code ví dụ, nên chuyển đổi code sang html thì mới nhúng vào trang web được. Mình dùng tool online tohtml.com để chuyển.
– khi chuyển nội dung blog qua viblo hay kipalog, mình cần copy và chuyển qua markdown rồi đăng.
– trang blog khá chậm

Gần đây, mình tập viết blog tiếng anh, nên muốn chuyển nội dung của blog tiếng Việt beautyoncode.com sang domain mới là beautyoncode.online, luôn tiện cải thiện các bất tiện trên.

Github Page với jekyll giúp mình một số điểm:
– github page giúp tiết kiệm khoản tiền bảo trì website (domain + host). Nếu bạn muốn có domain khác ngoài account.githubio.com thì có thể cài đặt là “Pages” và thêm DNS ở nhà cung cấp domain như godaddy hay route53 để có thể chuyển sang.
– thân thiện với dev: mình có thể viết blog với markdown và quản lý source code, hay chạy web ở local.

Tuy nhiên, github page sẽ chưa phù hợp nếu bạn:
– hoàn toàn không biết gì về lập trình
– muốn xây dựng trang blog sử dụng nhiều tính năng như bên wordpress (admin, category, plugin, comment)
– không muốn public source của mình

Nếu bạn đã có dự định viết gì đó lại hoàn toàn miễn phí thì lựa chọn này rất đáng cân nhắc nha.
Ghé thăm trang thử nghiệm mình mới làm ở đây
https://beautyoncode.online/

## Xuất file docx trong Django
Việc xuất các loại file là một tính năng thường được sử dụng cho phép người dùng lấy lại dữ liệu của mình.

Trong series này, mình sẽ giới thiệu các phương pháp khác nhau để xuất tập tin trong ứng dụng Django. Các định dạng tệp được xuất có thể bao gồm docx, csv, zip hoặc pdf.

Trong bài viết đầu tiên, mình sẽ giới thiệu quá trình xuất tập tin docx, bằng cách sử dụng một thư viện gọi là python-docx.

python-docx là một thư viện Python cho phép tạo và cập nhật các tập tin Microsoft Word (.docx).

Về cơ bản, python-docx là tạo một đối tượng document và bạn có thể thêm nội dung như đoạn văn bản, tiêu đề, ngắt trang, bảng, hình ảnh và các tùy chọn định dạng như đậm hoặc nghiêng.

Bên cạnh việc xây dựng một docx file cơ bản, bài viết giới thiệu đến bạn cách xử lý nội dung HTML để giữ định dạng mong muốn bằng cách viết class custom HTMLParser để xử lý.

Cuối cùng, việc viết unit test cho code là quan trọng để đảm bảo chất lượng code đúng, mình giới thiệu unit test gồm hai phần: test view response và test nội dung document.

Bạn ghé đọc nội dung bài viết này ở blog nha, có code ví dụ và các hình ảnh minh hoạt rất chi tiết.

https://beautyoncode.com/export-docx-file-with-python-docx-in-django-app/

## Tìm hiểu về DNS
Người dùng sử dụng web thông qua các tên miền (domain) của trang web như beautyoncode.com. Các trình duyệt web thì lại tương tác bằng địa chỉ IP.

DNS (Domain Name System) là hệ thống đứng trung gian để dịch từ tên miền ở ngôn ngữ tự nhiên như google.com thành địa chỉ IP như 172.168.23.14

DNS là xương sống của internet. DNS sử dụng cấu trúc phân cấp theo tên

Các thuật ngữ về DNS: Domain registrar, DNS records, Zone file, Name server, Top level domain (TLD), Second level domain (SLD)

Bản ghi DNS (DNS record)

Mỗi bản ghi bao gồm: tên Domain hoặc sub domain, loại bản ghi, giá trị (value), chính sách định tuyến (routing policy)

Record type A, CNAME và alias record

– Record type A gắn với địa chỉ IPv4 cụ thể.

Ví dụ: khi bạn muốn domain của mình gắn đến địa chỉ IP của github page là 172.168.76.89 thì sẽ cần tạo một record loại A

– Record type CNAME giúp gắn domain của bạn với đến domain khác, và domain này cần phải có địa chỉ IP hay record A gắn vào nó.

  Không thể tạo CNAME cho SLD domain (apex domain) như beautyoncode.com. Nhưng có thể tạo CNAME record cho sub domain như www.beautyoncode.com

Ví dụ: sau khi đã gắn IP của github vào record A ở trên, bạn tạo thêm một record loại CNAME để chuyển truy cập từ www.beautyoncode.com sang beautyoncode.com.

Khi đó, trang web của bạn đã chuyển từ account.github.io sang domain.com thành công (lưu ý TTL để kiểm tra lại, có thể là 24h)

– Alias giúp gắn domain của bạn đến các nguồn tài nguyên khác như AWS ALB, và có thể sử dụng với apex domain. Loại record thường sử dụng cho alias là A và không gán TTL.

DNS hoạt động như thế nào? (mời bạn xem sơ đồ minh hoạ trong bài viết ở blog nhé)

https://beautyoncode.com/tim-hieu-ve-dns/

## Learning by doing với exercism.org
Exercism hỗ trợ học với hơn 67 ngôn ngữ lập trình thông qua các bài học coding thực hành.

Nền tảng này phù hợp với những người học lập trình với nhiều trình độ khác nhau (junior, mid-level, senior).

Thử tưởng tượng bạn sẽ giải các bài tập coding, rồi xem các cách giải khác từ những người khác, và có cả mentor hướng dẫn bạn các điểm giúp code tốt hơn.

Mỗi ngôn ngữ sẽ có một track gồm các bài tập theo chủ để cơ bản của ngôn ngữ (các concepts). Ví dụ Python có 15 concepts và 137 exercies.

Để giải bài tập, bạn có thể download tools về máy tính riêng hay giải trực tiếp trên nền tảng.

Bạn cũng có thể thử với vai trò mentor cho những người khác để giúp cộng đồng ngày càng lớn mạnh.

Nền tảng này có giao diện cực đẹp nha, enjoy your learning!

https://exercism.org/

## Liệu ngày tàn frontend đã đến?
Chủ đề về chat GPT được mọi người bàn luận sôi nổi trên tất cả các kênh. Mình đã chọn im lặng và mua thêm vào con bot để xài (ChatGPT, Copilot) rồi học dần về AI ^^

Hôm nay đọc bài viết của tác giả mình yêu thích bàn chủ đề này nên chia sẻ cùng cả nhà một vài gạch đầu dòng của bài viết:

Chuyện đe doạ developer mất việc đã xảy ra trước đây, khi mà các website được xây dựng no-code (WordPress, Webflow, tools) được ưa chuộng chỉ với vài đô mỗi tháng thay vì thuê lập trình viên làm từ đầu.
Thế nhưng lập trình viên vẫn tồn tại, và còn phát triển hơn nữa.

Gần đây, OpenAI ra mắt Chat-GPT4 với demo khá ấn tượng khi với bản viết tay vài dòng ChatGPT có thể dựng một trang web.
Tuy nhiên, lập trình viên ngày nay làm các trang web phức tạp hơn vậy nhiều.

Thêm nữa, các kết quả của ChatGPT thực tế có độ chính xác tầm 80%. Tương lai độ chính xác sẽ ngày càng cao, nhưng ai là người xác định kết quả đầu ra có chính xác hay không? Đó chính là lập trình viên.

Cứ cho là AI có thể giúp xây dựng một trang web lớn với vài chục nghìn dòng code, nhưng khi có lỗi xảy ra ai sẽ là người sửa và đảm bảo nó vẫn hoạt động. Các developer sẽ là người hiểu code của dự án và đảm bảo kết quả cuối cùng đến tay người dùng.

AI là công cụ hỗ trợ, không phải thay thế
Một câu nói mà boss mình mới nhắn gần đây:
“AI will not replace humans but humans with AI will replace humans without AI.”
AI sẽ giúp nâng hiệu suất công việc lên, và sẽ càng có nhiều công việc hơn để làm.

Chat-GPT giúp bạn học và làm nhanh hơn. Nhưng lưu ý cần kiểm tra đầu ra cẩn thận, hỏi thêm câu hỏi đến giải thích các phần liên quan, không copy code mù quáng, chắc chắn bạn hiểu rồi mới sử dụng và kiểm tra kết quả đầu ra.

Đọc thêm ở: https://www.joshwcomeau.com/blog/the-end-of-frontend-development/