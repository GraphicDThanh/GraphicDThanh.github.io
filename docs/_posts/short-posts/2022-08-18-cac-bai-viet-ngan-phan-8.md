---
title: "Các bài viết ngắn - phần 8"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/08/Short-posts-08.png)

## Làm tròn số thực trong Python
Làm tròn số thực trong Python là chuyện thường ngày, và tụi mình sẽ sử dụng rất nhiều trong khi học Python cùng toán cũng như trong hiển thị các số thực với một số lượng các chữ số thập phân bất kỳ.

Có một số cách để làm tròn số thập phân:

– Dùng hàm `round()` Cách này sẽ làm tròn số `3.333333` thành `3.33` và số `3.5` sẽ giữ nguyên là `3.5`. 
`round(3.33333)` kết quả 3.33 `round(3.5)` kết quả 3.5 
Nếu bạn muốn bắt buộc có hai chữ số thập phân thì cách này chưa triệt để, kết quả cần là `3.50`

– Chuyển về định dạng chuỗi và cắt số ký tự đứng sau dấu `.` rồi chuyển về lại dạng số với ép kiểu qua float

`“{:.2f}”.format(3.5)` kết quả `“3.50”`

Lưu ý đây là chuỗi, muốn chuyển qua số bạn cần thực hiện ép kiểu từ string về số với `float()`

Nội dung này được tóm tắt từ bài viết chia sẻ tips trên blog cá nhân của mình.

## 8 ngôn ngữ lập trình không lo thất nghiệp năm 2022
Có tới hơn 200 ngôn ngữ lập trình, nhưng chỉ một ít trong số đó được sử dụng phổ biến trong những dự án thực thế.
Vì thế nếu bạn tính học ngôn ngữ lập trình nào đó, hãy chọn những ngôn ngữ đang được săn lùng nhiều nhất, có nhiều cơ hội công việc và mức lương hấp dẫn nhất để học nhé.

DevJobsScanner gửi đến các lập trình viên kết quả khảo sát trong 8 tháng (từ 10/21 đến 6/22), dự trên hơn 7 triệu công việc của lập trình viên, và đưa ra 8 ngôn ngữ lập trình có nhiều công việc để làm nhất:

1. JavaScript/TypeScript với 469K jobs

2. Python với 290K jobs

3. Java với 240K jobs

4. C# với 170K jobs

5. PHP với 190K jobs

6. C/C++ với 95K jobs

7. Ruby với 70K jobs

8. Go với 30K jobs

JavaScript/TypeScript thực sự thống trị thị trường và chiếm hơn 1/3 lượng jobs, tiếp sau đó là Python, Java và C#. Go cũng là một ngôn ngữ tiềm năng có thể thay đổi thị trường trong tương lai với số lượng jobs đang tăng dần.

Mời bạn đọc thêm chi tiết ở bài viết sau

## JS debug tools
Các bạn Frontend Developer hay sử dụng gì để debug trong code JavaScript nhỉ?

Để hiển thị các thông tin lên trình duyệt thì có thể sử dụng:

– `alert()`: hiện popup kèm nội dung

– `console.log()`: hiển thị nội dung ở “Console” của trình duyệt

– `debugger;` chỗ đặt bạn này sẽ là một breakpoint, khi code thực thi sẽ dừng lại để bắt đầu chế độ debug trên trình duyệt

– `console.trace()`: hiện ra các dấu vết của nơi mình đặt bạn ấy vào và giúp mình kiểm tra đã đi qua những đâu, ở dòng bao nhiêu. Cái này gọi là trace ấy.


Ngoài ra thì nên tìm hiểu về Chrome DevTools , một công cụ vô cùng mạnh mẽ. Nếu làm app React thì có React DevTools. Visual Studio Code cũng cung cấp công cụ debug theo từng loại ngôn ngữ lập trình.

Bạn ghé đọc thêm về Debug JavaScript Tools ở bài viết này.

## Frontend developer news
Chọn làm dev, là bạn đã chọn một công việc với nguồn thông tin bất tận và sự thay đổi chóng mặt của công nghệ diễn ra hàng ngày. Do đó, việc cập nhật các thay đổi đã và đang diễn ra sẽ giúp bạn không bị tụt hậu và có thêm nhiều kinh nghiệm, góc nhìn cho những quyết định hàng ngày trong công việc.

Bạn có thể cập nhật bằng cách tham gia các cộng đồng dev ở lĩnh vực mình làm việc, hay theo dõi những tay to trong ngành trên facebook, twitter, đọc blog, …

Một kênh cập nhật thông tin mình thấy khá là tiện và chủ động, là các newsletters. Các thư này sẽ được tổng hợp và gửi đến bạn qua email mà bạn đăng ký, các email này có thể là hàng ngày hoặc hàng tuần.

Để quản lý hòm thư trên gmail, bạn có thể tạo một label “Newsletters” và setup một bộ lọc để các email gửi từ những địa chỉ này này không nằm trong mục inbox mà tự động được gắn nhãn là “Newletters”. Làm như thế bạn sẽ dễ dàng quản lý, mỗi ngày hoặc mỗi tuần chỉ cần đọc các bản tin này ở một nơi là được.

Giới thiệu đến bạn một số newletters giành cho frontend developer ở bài viết này.

## Quá bận để thành công
Bận rộn có phải là niềm tự hào của bạn? 

Bạn có thường ngẩng cao đầu và nói với mọi người xung quanh rằng bạn làm việc đến tối tăm mặt mày, ngày làm công sở, tối làm thêm, … Tuy nhiên, bận rộn chính là con dao 2 lưỡi.

Khi mới ra trường và bắt đầu đi làm, bạn thuộc trường phái nào trong 3 nhóm sau:  Nhóm 1: đi làm hành chính, tối về nghỉ ngơi và hưởng thụ – chiếm 70%  Nhóm 2: đi làm hành chính và nhận thêm việc về làm OT – chiếm gần 30%.  Nhóm 3: đi làm hành chính, đồng thời còn học lên & làm ngoài – chưa đến 1%.

Nhìn qua hẳn bạn đều thấy nhóm 2,3 sẽ phát triển trong sự nghiệp hơn nhóm 1. Nhưng giữa 2 và 3 thì nhóm nào tốt hơn?

Điều mà tác giả chứng kiến là nhóm 2 sẽ thăng tiến nhanh trong 5 năm đầu tiên nhưng sau đó chững lại và trong 10 năm sẽ đạt đến đỉnh cao sự nghiệp rồi dừng ở đó. Trong khi đó nhóm 3 lại chậm chạp trong 5 năm đầu tiên, mười năm sau sẽ sắp kịp nhóm 2 và con đường sự nghiệp nhóm 3 mở ra nhiều cơ hội hơn.

Bạn sẽ chọn mình trong nhóm nào?

Mời bạn đọc thêm góc nhìn của tác giả đã chọn nhóm 3 ở [bài viết này](https://www.linkedin.com/posts/nguyenlonghaisharing_qu%C3%A1-b%E1%BA%ADn-%C4%91%E1%BB%83-kh%C3%B4ng-th%E1%BB%83-th%C3%A0nh-c%C3%B4ng-b%E1%BA%ADn-r%E1%BB%99n-activity-6956878997511168000-csHp)
