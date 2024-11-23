---
title: "Các bài viết ngắn về Dev Skills"
---

Các bài viết ngắn về "Dev Skills"
- Code review là một phần tất yếu của dự án
- Clean code - Câu chuyện câu chuyện code xấu giết chết một công ty
- Clean Code - một số cách tiếp cận theo hướng thực hành
- Kỹ năng debug
- Dev self-learning
- Viết lách dành cho lập trình viên


## Code review là một phần tất yếu của dự án
Code review nên là một phần tất yếu của dự án 😅

Với fresher developer hay developer mới tham gia dự án, việc một PR(pull request) hay MR(merge request) của mình nhận được nhiều comments từ những thành viên khác có thể là quá tải và bạn đôi khi sẽ không tin được rằng có mình lại có nhiều lỗi sai đến vậy 🥲 Tuy nhiên, nếu nhận được review chất lượng, có tính đóng góp cao thì bạn sẽ ngày càng có code chất lượng hơn, đồng nghĩ với you are a better as a programmer.

Dưới đây là các lợi ích của code review mà mình tóm tắt từ bài post này

1. Giúp bạn hiểu hơn về code của dự án

2. Bạn sẽ học được nhiều cách để tiếp cận vấn đề hơn

3. Bạn có thể gợi ý cho người khác những cách tiếp cận tốt hơn(theo bạn nghĩ)

4. Giảm thời gian QA và tăng hiệu suất làm việc của team, vì review kỹ thì sẽ giảm các vấn đề nảy sinh

5. Giảm các lỗi trên production khi các edge case(trường hợp ngách) được nhận ra trong quá trình review

6. Giúp nhận ra các bottlenecks(vấn đề nguy hiểm) hay leak memories(rò rỉ bộ nhớ) sớm hơn

7. Giúp giảm code bị lặp và tăng việc tái sử dụng

Các bạn có thể ghé đọc thêm chi tiết và ví dụ ở bài này nhé 👇 Chúc các bạn review code vui vẻ không quạu nha 😁

## Clean code - Câu chuyện câu chuyện code xấu giết chết một công ty
Một câu chuyện về một dự án với một team dev vô cùng tài năng và cứng tay nghề 💪, có giai đoạn đầu phát triển cực nhanh và làm việc cực kỳ năng suất 🚀.

Mọi chuyện rất êm đẹp ở những tháng đầu tiên, qua những tháng tiếp theo thì tốc độ phát triển bắt đầu chậm lại. Bước ngoặt là ở tháng thứ 7, khi mà một feature không được release đúng dự kiến, quản lý thất hứa với khách hàng quan trọng, họ hủy hợp đồng ❌. Đó chính là lúc khoảng cách của Scary Gap (chênh lệch giữa thời gian business plan và thời gian thực tế) tăng dần 🆘.

Họ quyết định thuê thêm dev 👨‍🏭 để tăng năng suất, nhưng năng suất tháng đầu lại giảm và sau ba tháng khi dev mới đã quen với luồng công việc thì năng suất chỉ tăng được tầm 1.2 lần 😕. Điều này đồng nghĩa với quỹ lương tăng gấp đôi, gấp ba những năng suất gần như là như cũ. Cứ như vậy, Scary Gap của dự án tăng dần 🆘. Cuối cùng đành đập sản phẩm để xây lại.

Bài toán khó lại đặt ra: “làm sao có thể bơ hết requirements từ dự án cũ qua dự án mới?” 🤔

Tài liệu của dự án thì rất ít mà còn bị outdate 😭, requirements thì thay đổi liên tục, ở khắp mọi (slack, cho tới cả nói miệng trong những buổi call hay discussion). Chỉ còn một nơi tin tưởng nhất, là code. Nhưng, đọc code vẫn không hiểu :))) vì … code xấu 🥲.

Cuộc chạy đua giữa thỏ(dự án mới) và rùa(dự án cũ) 🏎 diễn ra đến tận hai năm cuối cùng đã có thể release 🙏. Nhưng, vẫn sót requirement nào đó, bug vẫn xảy ra trên hệ thống mới 🐞, khách hàng vẫn phàn nàn liên tục 😞. Sau vài tháng, dự án mới cũng bắt đầu phình to ra, không thua gì dự án cũ, và vòng lặp lại bắt đầu ⭕️.

Kết cuộc chắc bạn cũng đoán được.

Vậy nguyên nhân chính ở đây là gì?

Đó là code xấu ❌**. Việc code xấu đã dẫn đến hệ thống quá cồng kềnh, phức tạp, không có độ tin cậy cao. Động chỗ này hỏng chỗ kia, không ai dám sửa.**

Và việc năng suất làm việc tăng cao khi bắt đầu một hệ thống mới khiến chúng ta có một ảo tưởng đó là “đập đi xây lại” sẽ giải quyết được mọi vấn đề.

Và giải pháp là?

Chạy trốn khỏi code bẩn không phải là cách làm đúng đắn. Có nợ thì phải trả, nợ kỹ thuật tương tự như nợ ngân hàng. Nợ ngân hàng nếu cứ chần chừ không trả, sớm muộn cũng bị lấy nhà. Nợ kỹ thuật không trả, sớm muộn cũng bị lấy mất công ty 😭

Và cuốn sách “Clean Code” nên là cuốn sách gối đầu giường của dev(hic, tui chưa đọc)

Mời bạn đọc thêm [bài viết ở blog hung.dev](https://hung.dev/clean-code-1)

## Clean Code - một số cách tiếp cận theo hướng thực hành

**Clean Code là gì ? Vì sao bạn nên quan tâm ?**

## Clean Code là quan trọng, bởi:

- clean code dễ đọc
- clean code dễ chỉnh sửa
- clean code được viết bởi những người thực sự quan tâm đến nó
- clean code luôn được mong đợi, không lừa bạn, không có những bất ngờ trớ trêu

## Tại sao nên viết code clean?

- Vì đó là bước đầu tiên giúp đạt đến: giảm thiểu nguồn lực cần thiết để tạo và duy trì hệ thống
- Vì khi bạn code, bạn dành nhiều thời gian để đọc code hơn và viết code
- Vì chúng ta, những developer, code là để cho những developer khác có thể đọc

## Một số nguyên tắc cơ bản:

### Cách đặt tên

- sử dụng tên có ý nghĩa
- sử dụng tên có thể đọc được
- sử dụng tên có thể tìm kiếm được
- tránh sử dụng các tiền tố, hậu tố hay các từ viết tắt (prefix, suffix, hay abbreviations)

### Hàm

- Hàm nên chỉ làm một việc
- Hàm nên nhỏ (hạn chế số lớp lồng như 2, 3 lớp)
- Hàm nên có càng ít tham số càng tốt

### Comments (ghi chú)

- Tránh comment để giải thích code

### Refactoring (tái cấu trúc code)

> Là quá trình tái cấu trúc code mà không làm thay đổi logic, hành vi (behavior) của phần code được sửa.
> 

**Vậy nên và không nên refactoring code nào?**

**Không nên:**

- thay đổi thuật toán
- thay đổi vòng lặp này bằng vòng lặp khác
- cải thiện hiệu suất của một đoạn code

**Nên:**

- tách nhỏ một đoạn logic ra hàm riêng
- thay đổi tên
- tách một vài hàm ra lớp
- tạo hằng số để chứa các giá trị cố định

**Và nên thực hiện safe refactoring, bằng cách:**

- đảm bảo đủ test case cho các tính năng
- sử dụng các tools ở các IDEs để thay đổi một cách tự động và tăng tính chính xác

**Thế khi nào cần refactoring?**

- Khi viết code
- Khi viết test
- Khi refactor

---

Từ nay có thể áp dụng các nội dung trên để viết code clean hơn rồi.

Chúc bạn viết code ít bug và nhiều niềm vui nhé!

Đọc thêm ở [bài viết sau](https://medium.com/clarityai-engineering/clean-code-a-practical-approach-896546435235)


## Kỹ năng debug
Khi gặp bug, hẳn bạn sẽ chăm chăm vào con bug và tìm cách sửa chúng. Tuy nhiên việc fix được một con bug chưa quan trọng bằng việc tìm hiểu nguyên nhân vì sao chúng lại xảy ra và làm sao tránh sinh thêm bug tương tự trong tương lai.

Julia Evans giới thiệu đến bạn một số cách để quy trình debug hiệu quả hơn (từ paper “Learning to Troubleshooting”), bằng cách chú trọng vào nguyên nhân, nâng cao kiến thức để có thêm nhiều manh mối khi debug:

### Học code base

Đầu tiên bạn cần hiểu về code base của dự án, hiểu về cách dự án đang hoạt động.

### Học về hệ thống

Hiểu về ngôn ngữ, thư viện, hệ thống bạn đang sử dụng. Ví dụ như HTTP caching hoạt động ra sao, CORs diễn ra như thế nào, …

### Học về các công cụ

Biết và có thể sử dụng các công cụ debug như debugger, devtools, profilers, trace, dumps …

### Học các chiến lược

Tìm hiểu về các chiến lược có thể debug hiệu quả như viết unit test hay viết một chương trình nhỏ để tái tạo lại bug, in và tracking log, nghỉ ngơi, nói chuyện với người có kinh nghiệm hơn, …

### Học từ trải nghiệm

Không ngại sai và học hỏi nghiêm túc từ các trải nghiệm, giúp đỡ người khác fix bugs cũng là một cách tăng trải nghiệm của bản thân. Cảng nhiều kinh nghiệm thì việc debug sẽ càng dễ dàng hơn.

[Ref link](https://jvns.ca/blog/2022/08/30/a-way-to-categorize-debugging-skills/)

## Dev self-learning

Tất cả lập trình viên đều cần có khả năng “tự học” ngay từ ngày đầu tiên bạn bước vào nghề này. Trong suốt quá quá trình làm việc, bạn sẽ cải thiện dần khả năng tự học của mình sao cho có hiệu quả nhất

Một vài kỹ thuật / mẹo giúp bạn tự học lập trình hiệu quả:

– Học mỗi ngày với kế hoạch được vạch ra sẵn. Bạn có thể sử dụng reminder của lịch để nhắc bản thân.

– Nghỉ ngơi hợp lý. Thường xuyên nghỉ giữa các khung giờ làm việc để nạp lại năng lượng, đó có thể là 15-20 phút sau khi làm việc 2-3 giờ, và nhất là khi bạn đang bí với một con bug, nghỉ ngơi là cách tốt nhất để não có thể tự tìm cách giúp bạn.

– Chuyển đổi giữa các chủ đề khác nhau. Vì học hoài 1 chủ đề kéo dài sẽ dẫn đến chán, chuyển đổi chủ đề giúp giảm sự nhàm chán này lại, nhưng đừng chuyển nhiều chủ đề quá.

– Kiên định với mục tiêu những không quá cứng nhắc. Bạn không nhất thiết phải học từ a-z một khoá học, mà có thể xem trước nội dung toàn khoá, rồi chọn những phần thích để học trước, … Tuy nhiên đừng nên học quá nhiều khoá một lúc.

– Tìm niềm vui. Học điều mới thì luôn không dễ dàng, bạn có thể bị bí bất cứ khi nào. Để giữ lửa vượt qua những lúc khó khăn như vậy, bạn hãy nghỉ ngơi thường xuyên, giải trí bằng một bản nhạc yêu thích, … rồi sau đó có thể tiếp tục.

– Ôn lại kiến thức đã học để có thể nhớ và hiểu sâu hơn. Dành ra vài chục phút để ôn tập hay hướng dẫn người khác cũng là một cách rất hay để có thể ôn lại kiến thức.

– Xem xét quá trình học của bản thân và điều chỉnh cho phù hợp.

– Ghi chép bằng tay những điều quan trọng có thể giúp bạn nhớ sâu hơn.

– Hiểu vấn đề, lý thuyết đằng sau thay vì nhớ ví dụ hay code sẽ giúp bạn dễ dàng tìm được những kiến thức chung được áp dụng cho nhiều loại ngôn ngữ như design patterns hay các concepts cơ bản.

(Mời bạn đọc thêm ở [đây](https://aviyel.com/post/3649/top-9-ways-to-become-a-successful-self-taught-developer))


## Viết lách dành cho lập trình viên
Hàng ngày, ngoài viết code, lập trình sẽ viết tài liệu dự án, viết nội dung ticket, viết mô tả cho pull request / merge request, viết mô tả yêu cầu của khách hàng, các loại báo cáo, …

Tất cả các công việc này đều liên quan đến kỹ năng viết.
Và đây cũng là kỹ năng thiết yếu khi làm ở các tổ chức lớn.

Viết lách thật là khó!
Đặc biệt còn khó hơn với người làm lập trình!
Vậy làm sao để cải thiện kỹ năng này?

Viết lách thường bao gồm ba giai đoạn: trước, trong và sau khi viết.

Giới thiệu đến bạn một số mẹo để viết tốt hơn dưới đây:

**Trước khi viết**
– Tìm kiếm ý tưởng hay viết gì ?
– Không nên nhầm giữa viết và học. Học là khi mình chưa biết thì tìm hiểu thêm, còn viết là khi bạn đã hiểu và mô tả vấn đề đến người khác
– Hiểu đối tượng bạn hướng đến
– Cần đủ không gian yên tĩnh
– Viết ngay khi có chủ đề phù hợp
– Nếu không có ý tưởng thì nên tìm kiếm bằng cách đọc, học, thảo luận thêm hay hỗ trợ đồng nghiệp cũng có thêm nhiều ý tưởng.

**Trong khi viết**
– Đừng bắt đầu với lời mở đầu quá chi tiết và lạc trôi luôn. Cái bạn cần làm một bản nháp về mục lục (outline)
– Khi bạn viết nội dung cho từng mục có thể điều chỉnh thứ tự cho phù hợp
– Hoàn thành nội dung toàn bài trước khi đi vào các chi tiết nhỏ hơn như chỉnh câu chữ, ngữ pháp, lỗi chính tả
– Làm cho nội dung của bạn có thể đọc lướt qua với các tiêu đề cho mức độ quan trọng
– Tóm tắt nội dung cuối bài

**Thực hành viết**
– Duy trì viết hàng ngày, hàng tuần, hàng tháng
– Thử nghiệm với các dạng bài ngắn, dài
– Khi có outline có thể đem đi hỏi thăm để nhận feedback
– Gửi bản draft đến đối tượng phù hợp đến nhận feedback

Mời bạn ghé đọc bài viết chi tiết ở [link sau](https://www.heinrichhartmann.com/posts/writing/?utm_source=CSS-Weekly&utm_campaign=Issue-527)
