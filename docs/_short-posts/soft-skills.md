---
title: "Các bài viết ngắn về Soft Skills"
category:
- Short Posts
- Soft Skills
tag:
- soft-skills
---

Các bài viết ngắn về "Soft Skills"
- Code review là một phần tất yếu của dự án
- Clean code - Câu chuyện câu chuyện code xấu giết chết một công ty
- Clean Code - một số cách tiếp cận theo hướng thực hành
- Kỹ năng debug
- Dev self-learning
- Viết lách dành cho lập trình viên
- Lộ trình lên đai của lập trình viên
- Tài khoản tiết kiệm sự nghiệp
- Những kỹ năng vô hình
- Đạo của Warren Buffet
- Từ fullstack đến devops
- Quá bận để thành công
- 10X developers
- Lỗi thường gặp junior developer
- Chuyện tiếng Anh
- Vì sao feedback rất quan trọng
- Hãy dành cho nó 5 phút


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


## Lộ trình lên đai của lập trình viên

Một định hướng phát triển nghề nghiệp rõ ràng sẽ giúp bạn định hướng mình đang ở đâu, đang đi theo hướng nào và sẽ là ai trong năm hay mười năm tới 🧐

Got It AI Blog giới thiệu về “Lộ trình lên đại của lập trình viên” vô cùng chi tiết và sinh động với các hình vẽ minh họa 

Giai đoạn đầu tiên mà bất cứ ai cũng phải đi qua gọi là “Starting Track”, với 3 cột mốc lần lượt là:

1. Junior Software Engineer hay Software Engineer Intern

2. Software Engineer

3. Senior Software Engineer with Tech Lead add-on

Sau giai đoạn đầu, bạn sẽ đứng ở ngã ba đường, nơi bạn có hai hướng để đi: “Individual Contributor Track” hoặc là “Managerial Track”

Với “Individual Contributor Track”, có 3 cột mốc lần lượt là:

1. “Staff Engineer”

2. “Senior Staff Engineer”

3. “Principal Engineer”

Với “Managerial Track”, có 3 cột mốc lần lượt là:

1. “Engineering Manager”

2. “Director of Manager”

3. “Vice President of Engineering”

Qua đây bạn có thể thấy nếu một lập trình viên không thích làm quản lý thì con đường “Individual Contributor” là hoàn toàn khả thi và có khi còn có mức lương khủng hơn manager nữa. Nếu quan tâm bạn hãy tìm hiểu kỹ để chọn con đường phù hợp với kỹ năng của mình nhé 😉

Bạn có thể ghé đọc bài viết chi tiết ở [GotIt AI Blog](https://vn.got-it.ai/blog/software-engineer-zero-to-hero)

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

## Những kỹ năng vô hình

KỸ NĂNG LÀ TẤT CẢ MỌI THỨ  🤯🤯🤯

Đúng vậy, tất cả những gì bạn làm trong công việc đều là kỹ năng: cách bạn nói chuyện với mọi người trong phòng nghỉ, ghi nhớ ngày sinh nhật của đồng nghiệp, … 

Tất cả những điều có vẻ rất nhỏ nhặt trên đều là kỹ năng, nó như là khoản lợi tức kép tiết kiệm dài hạn cho sự nghiệp của bạn.

3 kỹ năng vô hình quan trọng nhất:

👉 Đi làm

👉 Gia tăng giá trị của bạn

👉 Làm chủ thái độ của bạn. Thái độ là một quyết định.

Ngoài ra còn 9 kỹ năng vô hình khác, như là “vượt qua mong đợi”, “sự khéo léo”, “thể hiện lòng biết ơn”, “thể hiện sự quan tâm đối với người khác”, “tập trung vào những điều quan trọng”, “chơi đùa bằng sức mạnh của bạn và của những người khác”, “linh hoạt”, “tôn trọng thiết bị của công ty”, “tiếp tục sự nghiệp học tập của bạn”

Trên đây là một vài tóm tắt của chương “Nắm giữ các kỹ năng vô hình” mời bạn ghé nghe nội dung ở episode 49 trong podcast này https://beautyoncode.com/podcast/ Link sách tiki cho bạn nào cần mua về nghiên cứu nè https://ti.ki/M39Oj1kb/CAREER-UP

## Đạo của Warren Buffet
“The Tao of Warren Buffet” – “Đạo của Warren Buffet” là một cuốn sách mỏng chứa những lời thông thái của ông được người con dâu Mary Buffet và những người kề cận ghi lại.

Dù mình không rành về đầu tư nhưng khi đọc các nội dung này mình cảm nhận được ông là một người sống vô cùng giản dị, có những nguyên tắc sống đơn giản nhưng sâu sắc về đầu tư và cuộc sống.

Dưới đây là 6 câu nói mà mình tâm đắc nhất:

1️⃣ “Bạn nên học từ kinh nghiệm, nhưng tốt nhất nên học từ kinh nghiệm của người khác nhiều hơn.”

2️⃣ “Xây dựng danh tiếng mất 20 năm nhưng phá hủy chỉ cần năm phút. Nếu bạn nhớ đến điều này, bạn sẽ hành động khác đi.”

3️⃣ “Tôi không cố gắng nhảy qua mức xà cao trên 2 mét. Tôi nhìn quanh và kiếm những mức xà chừng vài ba tấc để bước qua.”

4️⃣ “Sợi dây xích thói quen nhẹ đến mức rất khó có thể cảm nhận nhưng cũng nặng đến mức rất khó gỡ bỏ.”

5️⃣ “Sẽ đến một lúc bạn nên bắt đầu chỉ làm những gì bạn muốn. Hãy làm một công việc bạn yêu thích. Bạn sẽ nhảy bật dậy khỏi giường mỗi buổi sớm. Tôi nghĩ bạn thật điên rồ nếu cứ tiếp tục với những công việc mình không thích chỉ để tô đẹp hồ sơ xin việc của mình. Cái này nghe sao giống như để dành ham muốn cho lúc tuổi già thế?”

6️⃣ “Quản lý sự nghiệp bản thân cũng giống như đầu tư – mức độ khó khăn không được tính đến. Vì vậy bạn có thể tiết kiệm được tiền bạc và công sức bằng cách chọn đúng chuyến tàu cần lên.”

## Từ fullstack đến devops
Làm thế nào để từ một fullstack engineer trở thành một devops và cloud engineer ?

Tác giả Quân Đỗ, một devops/cloud engineer chia sẻ những cuốn sách anh ấy đã học trên con đường này. Các chủ đề bao gồm:

Về cơ bản, bạn cần hiểu về hệ điều hành Linux với các cuốn sách: Linux for beginners Ubuntu Linux

Tiếp theo, là các chạy chương trình trên các hệ điều hành khác nhau với cuốn: Docker In Action

Học cách tự động deliver chương trình đến người dùng dễ dàng nhất(CI/CD) với cuốn: Continous Delivery with Docker and Jenkins Tìm hiểu thêm về Container Orchestration với cuốn “Kubernetes In Action”

Tìm cách vận dụng vào thực tế và đọc thêm nâng cao với các cuốn sách: Managing Kubernetes Kubernates best practice

Để trở thành một Devops Engineer tốt hơn những devops engineer khác, bạn cần biết về Cloud với các cuốn sách: Amazon Web Service In Action Terraform In Action

Và tiếp tục học nâng cao kiến thức về monitoring, elasticsearch, … Nếu bạn chọn con đường này có thể theo dõi [tác giả này](https://viblo.asia/p/side-story-nhung-cuon-sach-nen-doc-de-tro-thanh-devops-cho-nguoi-moi-bat-dau-YWOZrAqNKQ0) nhé ^^

## Quá bận để thành công
Bận rộn có phải là niềm tự hào của bạn? 

Bạn có thường ngẩng cao đầu và nói với mọi người xung quanh rằng bạn làm việc đến tối tăm mặt mày, ngày làm công sở, tối làm thêm, … Tuy nhiên, bận rộn chính là con dao 2 lưỡi.

Khi mới ra trường và bắt đầu đi làm, bạn thuộc trường phái nào trong 3 nhóm sau:  Nhóm 1: đi làm hành chính, tối về nghỉ ngơi và hưởng thụ – chiếm 70%  Nhóm 2: đi làm hành chính và nhận thêm việc về làm OT – chiếm gần 30%.  Nhóm 3: đi làm hành chính, đồng thời còn học lên & làm ngoài – chưa đến 1%.

Nhìn qua hẳn bạn đều thấy nhóm 2,3 sẽ phát triển trong sự nghiệp hơn nhóm 1. Nhưng giữa 2 và 3 thì nhóm nào tốt hơn?

Điều mà tác giả chứng kiến là nhóm 2 sẽ thăng tiến nhanh trong 5 năm đầu tiên nhưng sau đó chững lại và trong 10 năm sẽ đạt đến đỉnh cao sự nghiệp rồi dừng ở đó. Trong khi đó nhóm 3 lại chậm chạp trong 5 năm đầu tiên, mười năm sau sẽ sắp kịp nhóm 2 và con đường sự nghiệp nhóm 3 mở ra nhiều cơ hội hơn.

Bạn sẽ chọn mình trong nhóm nào?

Mời bạn đọc thêm góc nhìn của tác giả đã chọn nhóm 3 ở [bài viết này](https://www.linkedin.com/posts/nguyenlonghaisharing_qu%C3%A1-b%E1%BA%ADn-%C4%91%E1%BB%83-kh%C3%B4ng-th%E1%BB%83-th%C3%A0nh-c%C3%B4ng-b%E1%BA%ADn-r%E1%BB%99n-activity-6956878997511168000-csHp)

## 10X developers
Làm việc với lập trình viên hơn 10 năm kinh nghiệm(10x) liệu có chán không?

Bài viết sau nói đến những điều tác giả học từ 10x software developers:

### 1 Loại bỏ mọi cản trở trên đường, thay vì chỉ nói về nó

Khi những người khác chỉ mải bận nói về vấn đề thì 10x dev sẽ xem đó là thử thách thú vị và tìm cách để giải quyết

### 2 Vô cùng nghiêm túc và rất chi tiết

Bạn chỉ cần chương trình chạy và đôi khi không rõ lý do? Với 10x dev thì không hề vậy, họ sẽ fix tất cả warning khi chạy code, viết code thật clean và dễ hiểu, giải thích vấn đề chi tiết và hiểu mọi dòng họ viết.

### 3 Kết hợp giữa CEO và super dev

Nếu giao một việc và bạn nhảy vào code ngay thì hơn 80% là sẽ phải code lại lần nữa. Lý do là super dev suy nghĩ rất nhiều trước khi code, có những trường hợp nào, flow ở đây ra sao, cần thêm những gì, … Và họ tạo file, viết các lớp, phương thức, utils trống để bắt đầu hình dung trước khi đi vào chi tiết. Rồi viết test trước(TDD – Test Driven Development), tất cả fail. Rồi mới thêm chi tiết và làm tất cả test pass.

It’s magic!

Thật là thú vị quá xá khi đọc chi tiết [bài viết này](https://iorilan.medium.com/things-i-have-learned-from-the-10x-software-developers-i-worked-with-d8fabad5f3ee) về 10x developers

## Lỗi thường gặp junior developer
Bài viết của một cựu lập trình viên từng làm việc tại Amazon trong 6 năm, bắt đầu từ vị trí thực tập và phát triển lên làm lead nhiều dự án. Anh chia sẻ những lỗi mình từng mắc phải khi làm junior developer:

### Là một junior developer, bạn có quyền
Đừng ngần ngại, thiếu chủ động và tự đánh giá thấp bản thân mình. Những việc này dẫn đến thiếu trách nhiệm và thiếu nghiêm túc trong công việc. Nếu bạn viết code, hãy viết những dòng code tốt nhất của bạn dù quy mô dự án có lớn hay nhỏ.

### Là một junior developer, bạn có từng cạnh tranh với đồng đội
Đừng chỉ tìm những lỗi sai của đồng đội và chỉ ra cho bằng hết trong các buổi review! Đó là cách tệ nhất mà bạn có thể làm cho những mối quan hệ lâu dài.

Thay vào đó, hãy tìm hiểu xem đồng đội đã làm được gì, tế nhị trong việc đưa ra các góp ý, chúc mừng khi họ hoàn thành công việc và giúp đỡ khi cần. Vì sau cùng, chúng ta là đồng đội của nhau.

### Là một junior developer, bạn đã e ngại khi nói chuyện tăng lương
Bạn từng nghĩ việc yêu cầu tăng lương / thăng chức là ích kỷ, nếu làm tốt thì cuối cùng cũng sẽ được và bạn đã không hỏi. Bạn đã bắt đầu minh bạch hơn về mục tiêu và nguyện vọng nghề nghiệp của mình, bắt đầu những cuộc nói chuyện về vấn đề tế nhị này với người quản lý, vì bạn hiểu những cuộc nói chuyện như vậy vừa giúp hiểu về nghề và có tính xây dựng.

### Là một junior developer, bạn đã thiếu sự hiểu biết về dự án
Trong các cuộc họp, hầu như bạn đã không lắng nghe xem đồng đội của mình làm gì, nhưng bạn đã hối tiếc khi gặp các vấn đề khi làm việc chung sau đó hay không hiểu bức tranh chung của dự án. Bạn đã khắc phục bằng cách chủ động lắng nghe và đặt thêm nhiều câu hỏi. Điều này giúp bạn nắm bức tranh chung của dự án và dễ dàng hơn khi làm những phần khác nhau của dự án.

### Là một junior developer, bạn đã nhanh chóng tìm cách đổ lỗi cho người khác
Nếu có gì đó xảy ra với dự án như bug trên production chẳng hạn, bạn đã tìm cách đổ lỗi cho người khác hay từ chối nếu đó không phải mã của mình. Điều này từng làm khó bạn khi làm việc nhóm. Bạn đã khắc phục bằng cách tích cực hơn khi review code của đồng đội để giảm lỗi, và tạo nên một team hoạt động hiệu quả hơn.

Hi vọng bạn đọc những dòng tâm sự này sẽ nhận ra và nhanh chóng vượt qua các lỗi này nhé.

Thực sự là mình đã từng trải qua tất cả các lỗi trên và cũng có nhiều lỗi đang khắc phục dần ^^

[Link ref](https://curtiseinsmann.hashnode.dev/from-an-ex-amazon-team-lead-5-mistakes-i-made-as-a-junior-software-engineer)

## Chuyện tiếng Anh
Thời buổi này bạn phải biết tiếng Anh, nếu muốn có một vé đến với văn minh thế giới. Tiếng anh được hơn 50 nước với hơn 2 tỉ người sử dụng làm ngôn ngữ chính thức và trùng hợp là họ rất giàu.

Với dev thì lại càng gian nan vì hầu như 99% các công trình nghiên cứu, sách báo, tài liệu đều ở ngôn ngữ này.

Nhưng con đường học tiếng Anh của người Việt sao mà khổ trăm bề 😅 Mang tiếng được học tiếng Anh từ tận mẫu giáo, cấp một nhưng ruốc cuộc thì lại không phát âm nổi một chữ đơn giản chứ đừng nói là giao tiếp. Vì ở trường người ta dạy tiếng anh để thi cử, chứ không phải dạy để giao tiếp 😶 Chưa kể đến giáo viên dạy tiếng Anh ở trường dở thiệt.

✍️ Một vài kinh nghiệm học ngoại ngữ để dùng:

1. ✅ Cách học phát âm tốt nhất là bắt chước. Hãy chọn cho mình một khuôn mẫu, bạn thích giọng Anh, Mỹ, Úc hay gì đó hay idol nào đó của bạn rồi bắt chước the o Mình thầy học Duolingo and Elsa Speak cũng phát âm rất tốt, chỉ mỗi tội là nó hơi chán. Nếu bạn học thứ gì bạn thực sự thích và muốn tìm hiểu sẽ cải thiện được điểm này.

2. ✅  Quên ngữ pháp đi Vì phản xạ mà đợi ráp ngữ pháp cho đúng chắc tới … chiều, chưa kể các sách dạy ngữ pháp hay ngoại ngữ đa phần là lỗi thời.

3. ✅  Chỉ cần nói tiếng anh thôi, đừng quan tâm tới giọng(accent) Cái này nghe có vẻ ngược đời, vì hầu như mọi người đều cổ xúy chuyện phát âm cho chuẩn giọng Anh, Mỹ. Cái này chỉ là quảng cáo ở các trung tâm Anh ngữ để dễ lấy tiền hơn thôi bạn à. Tất nhiên là nếu bạn nói chuẩn thì quá tốt rồi, nhưng nếu không thì cũng không sao đâu. Tự tin quan trọng hơn ấy. Khi cần, bạn chỉ cần nói tiếng Anh là được, giọng Việt Nam hay giọng Ấn gì cũng được tuốt, lúc đó người ta quan tâm tới thông tin bạn cung cấp chứ ai hơi đâu mà để ý cái giọng, chưa kể người bản sứ họ biết rõ và tự điều chỉnh giọng họ chậm lại cho phù hợp với bạn nữa.

## Vì sao feedback rất quan trọng

🎙Feedback có thể hiểu là đưa ra ý kiến phản hồi của một ai đó về một cái gì đó, sau một chuyện gì đó.
Có 3 loại feedback thường thấy là:

🥳 Positive feedback: Phản hồi mang tính tích cực. Đưa ra để đối phương biết mình ghi nhận những cố gắng của họ rằng đang làm tốt một việc gì đó, khích lệ để tiếp tục phát huy.

✅ Constructive feeback: Phản hồi mang tính xây dựng. Đưa ra cho đối phương biết hành động của họ cần thay đổi

🤬 Destructive feedback: Đây là thể loại constructive feedback phiên bản lỗi, được đưa ra một cách vội vã, thiếu tế nhị, không đúng nơi đúng chỗ, hoặc đúng người nhưng sai thời điểm. Cũng là loại feedback phổ biến nhất trên đường, trên mạng. Tác dụng của nó là 0, còn tác hại thì vô cùng.

Vậy thì đưa ra feedback như thế nào cho hợp lý?

👨‍🦱 Be specific Đưa ra feedback đúng nơi, đúng chỗ và đúng nội dung. Và feedback như thế nào để người ta dễ take action được.
⏳ Be timely Thường thì realtime feedback là tốt nhất, nhưng nếu tình huống không cho phép thì cũng nên feedback trong 48h.

Để đưa ra feedback tốt hơn người ta nghĩ ra rất nhiều mô hình, bạn có thể search thêm với từ khóa “feedback model”. Nhìn chung các mô hình này đều xoay quanh 4 yếu tố:

👉 Context: tình huống sự việc xảy ra
👉 Behavior: hành vi những người liên quan đến vấn đề bạn đang feedback một cách khách quan nhất
👉 Impact: nói về ảnh hưởng mà hành động đó gây ra
👉 Follow up: đưa ra gợi ý cho người nhận feedback

Đây là tóm tắt nội dung của bài blog “Vì sao feedback rất quan trọng?” của anh Huy Trần trên [blog snacky.blog](https://snacky.blog/posts/giving-feedback.html)

## Hãy dành cho nó 5 phút

(Give it five minutes)

Một bài viết từ mười năm trước nhưng khi đọc vẫn thấy hay nên chia sẻ đến mọi người, đúng kiểu “old but gold”.

Tác giả chia sẻ mình là người nóng tính, khi ai nói gì không vừa ý là bật lại ngay, hay luôn là người sẽ đưa ra các ý kiến phản pháo đầu tiên.

Tuy nhiên,

“bạn càng phản ứng nhanh bao nhiêu, bạn càng thiếu suy nghĩ bấy nhiêu”.

Câu chuyện:

Trong một cuộc hội thảo nơi người viết làm diễn giả, sau bài trình bày thì có một anh bạn Richard vô cùng tốt bụng đã đến nói chuyện và gửi lời khen đến phần trình bày của người viết. Thay vì tử tế đáp lại, người viết đã nhân tiện gửi đến Richard những phản hồi (tiêu cực) về phần trình bày của anh ta.

Những điều Richard đáp lại đã làm chấn động người viết:

“Man, give it five minutes”.

Richard bảo không đồng ý hay phản đối thì tốt thôi, luôn có những quan điểm và niềm tin mạnh mẽ, quyết đoán là điều tuyệt vời, nhưng hãy cho ý kiến của tôi một thời gian để bạn hiểu hơn trước khi bạn muốn tranh luận phản đối nó.

5 phút đại diện cho suy nghĩ (“think”), không phản ứng (“react”).

Và anh ấy đã đúng, tác giả nói anh ấy thừa nhận mình tham gia tranh luận để chứng tỏ mình đúng, chứ không phải để học hỏi.

Đó là khoảnh khắc đã thay đổi cuộc sống của tác giả!

Richard đã dành ra hơn 30 năm để suy nghĩ về những vấn đề này và trình bày chúng trong vài phút. Vẫn có thể là tôi đúng còn anh ấy sai nhưng tốt hơn là nên suy nghĩ cẩn thận về điều đó.

Có sự khác nhau giữa phản ứng lại và đặt câu hỏi. Phản ứng lại là khi bạn nghĩ là bạn đã biết còn đặt câu hỏi là khi bạn muốn biết.

Học cách suy nghĩ trước khi phản ứng lại là điều cần học trong cả cuộc đời. Nếu bạn không chắc về điều này có thể đọc thêm trích dẫn sau về Steve Jobs:

And just as Steve loved ideas, and loved making stuff, he treated the process of creativity with a rare and a wonderful reverence. You see, I think he better than anyone understood that while ideas ultimately can be so powerful, they begin as fragile, barely formed thoughts, so easily missed, so easily compromised, so easily just squished.

Có hai điều trên đời này không cần đến kỹ năng:

1. tiêu tiền của người khác

2. loại bỏ một ý tưởng của người khác

Loại bỏ một ý tưởng là vô cùng dễ dàng vì nó không liên quan đến bất cứ công việc gì. Bạn có thể bỏ qua, chế giễu nó, đó là điều dễ làm. Cái khó là làm sao bảo vệ, suy nghĩ và nuôi dưỡng nó.

Ý tưởng đúng hay sai đều có thể là bắt đầu của cuộc sống.

Vì thế, lần sau khi ai đó trình bày hay đề xuất một ý tưởng, hãy dành ra năm phút để suy nghĩ về nó, bạn nhé!

https://signalvnoise.com/posts/3124-give-it-five-minutese

