---
title: "Các bài viết ngắn - phần 6"
categories:
  - Short Posts
tags:
  - git
---

## Public APIs
Bạn muốn làm một dự án chỉ với kiến thức frontend, và đang tìm những API được public để có sử dụng cho dự án của mình? Đó có thể là một trang web hiển thị các bạn mèo, cốc cà phê yêu thích hay một trang về anime, games, …

Đây, mình tìm được một [repo](https://github.com/public-apis/public-apis) với 51 thể loại, hơn 1400 apis, bạn có thể fork về repo của mình để dễ dàng tìm trong tương lai nhé.

Tuy nhiên, lưu ý nhỏ là khi sử dụng public apis, bạn hãy kiểm tra cẩn thận xem còn public không, kiểm tra những gì bạn có thể sử dụng(các endpoints, các method, resources). Các apis này sử dụng để thực hành các kiến thức lập trình hay làm pet projects thì hợp lý hơn là làm một dự án commercial nha(nhỡ đâu người ta không public nữa hay có vấn đề gì sẽ rất rủi ro)

Bạn nào làm được dự án nhỏ nào có thể chia sẻ dưới comment này nhé!

## Liệu JS có bị cho về hưu ?
Trong cuộc phỏng vấn gần đây với Evron, Douglas Crocklock, một trong những người tham gia khởi tạo ngôn ngữ JavaScript.

Ông cũng là tác giả của “How does JavaSript work?”, cũng là người khám phá ra JSON – định dạng dữ liệu được yêu thích nhất trên thế giới.

Douglas đã trả lời Evrone rằng “Điều tốt nhất ngày nay chúng ta nên làm cho JavaScrip là cho nó nghỉ ngơi (gỡ bỏ nó). Phải chăng đây cũng là lý do ông đã không còn viết nhiều về JavaScript nữa?

Evrone: In your opinion, what expected changes in JavaScript are going to be the most important?

Douglas: The best thing we can do today to JavaScript is to retire it.

Evron cũng đề cập đến cuộc chiến giữa XML và JSON, Douglas đã cho biết thời kỳ bán rã của XML từng là trong khoảng 3 năm.

Thật khó để nói về tương lai sẽ ra sao, liệu Typescript hay ngôn ngữ nào có thể thay thế cho chú khủng long JavaScript không?

Đọc thêm cuộc trò chuyện thú vị này ở [đây](https://evrone.com/douglas-crockford-interview).

## Tìm kiếm nhị phân (binary search)
Tìm [kiếm nhị phân](https://vi.wikipedia.org/wiki/T%C3%ACm_ki%E1%BA%BFm_nh%E1%BB%8B_ph%C3%A2n) (binary search) là một thuật toán tìm kiếm xác định vị trí của một giá trị cần tìm trong một mảng đã được sắp xếp.

Thuật toán sẽ tiến hành so sánh giá trị cần tìm với phần tử đứng giữa của mảng. Nếu hai giá trị không bằng nhau, thì một nửa mảng không chứa giá trị cần tìm sẽ được bỏ qua, và tiếp tục tìm kiếm trên nửa còn lại. Một lần nữa, lấy phần tử ở giữa so sánh với giá trị cần tìm, cứ thế lặp lại cho đến khi tìm thấy giá trị đó. Nếu phép tìm kiếm kết thúc mà vẫn chưa có giá trị cần tìm tức là nó không có trong mảng.

Binary search chạy theo giời gian logarit trong trường hợp tệ nhất, thực hiện O(logn) bước so sánh, với n là số phần tử của mảng. Thuật toán này sẽ nhanh hơn thuật toán tìm kiếm tuyến tính thông thường (lặp qua toàn mảng) với O(n)

Một số vấn đề thường gặp khi giải bài toán binary search:

– Khi nào thì sẽ thoát ra khỏi vòng lặp?

– Làm sao để khởi tạo và cập nhật biên bên trái (left), biên bên phải (right)?

[Bài viết sau](https://beautyoncode.com/tim-kiem-nhi-phanbinary-search/) giới thiệu một bản mẫu tổng quát về cách giải binary search sẽ giúp bạn hình dung về cách giải bài toán này dễ dàng hơn.

## Useful extensions for FE Developer
Là một Frontend Developer, một trong những bộ công cụ hữu dụng chính là những extensions(phần mở rộng) được cài đặt trên trình duyệt Chrome.

Giới thiệu đến bạn 4 extensions sẽ mang đến cho bạn thêm năng lực làm một FE developer xịn xò:

1. **WhatFont** – giúp bạn xem trang web đang sử dụng loại font nào, kích thước ra sao

2. **Measure It** – Một cây thước trên trình duyệt giúp đo đạc sẽ là công cụ hữu dụng

3. **Perfect Pixel** – Kiểm tra trang web của bạn với bản thiết kế bằng cách kéo thả bản thiết kế vào và thực hiện so sánh trực tiếp trên trang web với chế độ chỉnh opacity và drap/drop

4. **Live Editor CSS** – Sửa style của trang web ngay trên màn hình và có thể sử dụng những đoạn mã này nhanh chóng

Ghé [blog này](https://beautyoncode.com/chrome-extensions-huu-ich-danh-cho-frontend-developer/) để đọc thêm chi tiết với hình minh hoạ và link để cài đặt những extensions này nhé.
## Tự động push code giải leetcode bằng Leethub extensions
Bạn đã bắt đầu giải [leetcode.com](http://leetcode.com/) hàng ngày để rèn luyện tư duy logic cũng như học thêm về cấu trúc dữ liệu và thuật toán chưa?

Bạn có đang copy code đã giải trên leetcode rồi commit lên repo cá nhân của mình để lưu lại những bài tập mình đã làm không? Hay để làm đẹp tài khoản github bằng những contributions thường xuyên thể hiện bạn code mỗi ngày (cool mà ^^)

Nếu bạn đang làm như thế thì .. đây, minh muốn giới thiệu một tuyệt chiêu mình mới tậu gần đây, một extension giúp bạn không làm gì cả nhưng cứ Submit leetcode là sẽ có commit tự động lên repo cá nhân của bạn. Đó là LeetHub.

Đây là [link](https://chrome.google.com/webstore/detail/leethub/aciombdipochlnkbpcbgdpjffcfdbggi?hl=en) tải extension LeetHub 

Sau khi cài đặt và kết nối đến github với repo có sẵn hay repo mới sẽ được tạo, là bạn có thể bắt đầu thử nghiệm rồi.

Đây là [repo](https://github.com/GraphicDThanh/leetcode) mình thử nghiệm submit leetcode gần đây.

Giao diện LeetHub hiển thị:
![](assets/images/2022/08/2022-08-04-cac-bai-viet-ngan-phan-6-1.webp)
