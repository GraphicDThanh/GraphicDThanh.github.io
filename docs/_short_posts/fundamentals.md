---
title: "Các bài viết ngắn về Fundamentals"
---

Các bài viết ngắn về "Fundamentals":
- Giới thiệu về mã nguồn
- Internet hoạt động như thế nào?
- Học giải quyết vấn đề với Leetcode
- File .gitkeep
- Git commands should know
- Cách đặt tên file
- Viết README thế nào cho chuẩn
- Viết commit message, dễ mà khó
- Authentication là gì?
- Authorization là gì ?

## Giới thiệu về mã nguồn
Trong thế giới phần mềm, bạn sẽ hay gặp câu hỏi: “Phần mềm này là loại mã nguồn mở (open source) hay mã nguồn đóng (closed source)?”

Vậy thì mã nguồn là gì? mã nguồn mở hay mã nguồn đóng nghĩa là sao?

Mã nguồn (source code) là phần code của ứng dụng. Ví dụ đơn giản nhất là chương trình hello world, in ra một dòng “Hello Linux!”

```python
print("Hello Linux")
```
nội dung trên chính là mã nguồn của chương trình viết bằng Python.

Mã nguồn đóng(closed source) là những phần mềm độc quyền với mục đích bảo vệ mã nguồn để tránh cạnh tranh, sao chép, … (Windows, MacOS, …)

Mã nguồn mở(open source) là chương trình có mã nguồn được cung cấp sẵn (Linux, Firefox, Git, …). Open source có thể hiểu là khả năng truy cập vào mã nguồn.

Ngoài ra còn có free source, là những phần mềm được tự do copy hay có thể thay đổi của chương trình, chứ không liên quan đến giá cả.

Open source có rất nhiều lợi ích như được sự đóng góp của cộng đồng, source code tốt hơn và giảm thời gian phát triển phần mềm. Và cũng vì được mở nên sẽ tiếp cận được nhiều người hơn.

Linux thường hay được biết đến là hệ điều hành mã nguồn mở phổ biến. Tuy nhiên thực tế Linux chỉ là một phần mềm nhân (kernel). Mời bạn đọc thêm về các loại mã nguồn và giới thiệu về Linux ở [đây][gioi-thieu-ve-linux].

## Internet hoạt động như thế nào?
Bạn sử dụng internet 🌍 mỗi ngày, để làm việc , để học tập online 👩‍💻, xem phim 👀, nghe nhạc 🎧 và ngay cả lúc đang đọc bài post này ✅. 

🤔 Vậy Internet thực sự hoạt động như thế nào? 

Vì sao bạn cá mập 🦈 đâu đó ngoài biển khơi lại có thể bị đổ thừa là làm ảnh hưởng đến tốc độ truyền 😹 ?

👉 Giới thiệu đến bạn một video animation cực dễ hiểu về cách internet hoạt động. 

Bạn sẽ tham gia vào chuyến phiêu lưu ✈️ của thông tin chính là các dữ liệu 📀 ở dạng bit (1010) từ máy chủ 💾 đến các thiết bị cuối của người dùng 📲.

 ✅Trong đây bạn sẽ được hiểu thêm về một vài khái niệm như:

- trung tâm dữ liệu (data center), vệ tinh (satellite), cáp quan (fiber cable)
- SSD (solid state device), máy chủ (server)
- địa chỉ IP (IP address), tên miền(domain name)
- DNS server, protocols (HTTP/HTTPS, TCP/IP, RTP)

Mời bạn xem video dưới đây. 

<iframe width="640" height="360" src="https://www.youtube.com/watch?v=x3c1ih2NJEg" frameborder="0" allowfullscreen></iframe>

## Học giải quyết vấn đề với Leetcode

Bạn muốn học cách giải quyết vấn đề nhưng chưa biết bắt đầu từ đâu? Hay bạn rất thích cấu trúc dữ liệu và thuật toán nhưng chán ngán với mớ sách vở trên trường? Hay bạn cần tìm việc bằng cách luyện giải thuật toán để trả lời các câu hỏi phỏng vấn về kỹ thuật?

Giới thiệu đến bạn một trang mà hầu như ai giải thuật toán hay muốn học về cấu trúc dữ liệu đều sẽ tìm đến, đó là LeetCode.

LeetCode là trang web miễn phí(vài tính năng nâng cao sẽ có phí), nơi bạn có thể luyện đề algorithms cũng như học về các đề tài cấu trúc dữ liệu và thuật toán.

Bạn có thể chọn thử một đề bất kỳ ở mức easy, rồi giải theo ngôn ngữ bạn hay dùng, đó có thể là JS, Python, C++, Go, … Run code rồi submit.

Làm thế sẽ giúp bạn bắt đầu làm quen với các đọc một đề bài, các thông tin liên quan, các gợi ý(nếu có). Khi submit thì LeetCode sẽ chạy phương án code của bạn với bộ test có sẵn(rất nhiều trường hợp) để đảm bảo bạn đưa ra một phương án đủ tốt. Nếu vẫn chưa làm được bạn có thể xem đề bài liên quan đến chủ đề gì rồi tìm chủ để đó để học thêm.

Ngoài ra , trong mục thảo luận của từng bài có rất nhiều các cách giải của những người khác bạn có thể tham khảo để nâng cao dần kỹ năng giải quyết vấn đề. https://leetcode.com/

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

## Git commands should know

Git sẽ đi cùng bạn suốt thời gian làm dev, vì cứ hễ code là phải commit lên repository của github, gitlab cá nhân hay của dự án, công ty.

Làm chủ Git CLI với 30 câu lệnh mà lập trình viên nên biết với bài viết ở [link](https://levelup.gitconnected.com/top-30-git-commands-you-should-know-to-master-git-cli-f04e041779bc).

Mình sẽ tóm tắt một số câu lệnh hay sử dụng và quan trọng theo cách mình nhìn nhé.

– Setup usernane và email với “git config”. Câu lệnh này quan trọng khi bạn có nhiều repository khác nhau cần commit với tên và email khác nhau, ví dụ như repo cá nhân và công ty, dự án.

– Clone một dự án về với “git clone”, chuyển branch với “git checkout <tên branch>”

– Tạo branch mới với “git branch”, tạo mới và checkout qua luôn với “git checkout -b <tên branch>”

– Xem các branch với “git branch”, xem cả cho remote thì thêm option “-a”

– Kiểm tra code changes với “git status”

– Thêm file thay đổi lên staged với “git add”

– Commit một dòng với “git commit -m <message>”

– View commit history với “git log”, thêm option -3 sẽ xem 3 commits gần nhất, thêm -p sẽ xem thay đổi trên commit. Xem log đẹp dạng graph thì sử dụng “git log –graph –oneline –decorator”

– Xem một commit với “git show <id>”, với id có thể là 6 số đầu của một commit id

– Bỏ thay đổi của file chưa lên staged với “git checkout”, nếu lên staged rồi thì dùng “git reset”

– Rollback commit gần nhất với “git revert”

– Xoá branch đã merge với “git branch -d”, nếu có lỗi tức là branch này chưa được merge vào main branch, lúc nãy vẫn muốn xoá cần dùng option “-D”

– Xoá branch ở remote với “git push origin –delete <branch-name>”

– Merge hai branch với “git merge”, nếu cần commit merge thì thêm option “–no-ff”

## Cách đặt tên file
Bạn đặt tên một file như thế nào?

Ví dụ bạn có một tấm ảnh, bạn sẽ đặt nó tên gì? có thể là “image 1.png” hay “2022-07-12_img1_a-beautiful-dog.png”

Việc đặt tên tưởng chừng rất đơn giản, vì nó dễ làm thật, nhưng nó lại là một trong những thử thách lớn nhất của người dùng thiết bị nói chung, hay một lập trình viên nói riêng. Và cũng đã có rất nhiều thảo luận xoay quanh vấn đề này, kèm theo đó là sự ám ảnh nhẹ với cái tên “naming convention”

Việc đặt tên là quan trọng, vì nó sẽ sử dụng để nhận dạng, tìm kiếm, phân loại, … file này giữa hàng ngàn, hàng triệu file khác.

Có 3 nguyên tắc chính khi đặt tên file: machine readable: máy có thể đọc được human readable: người có thể đọc được plays well with default ordering: cái tên hoạt động tốt với những cách phân loại mặc định(phân loại theo ngày tháng, theo nhóm, …)

Giới thiệu đến bạn chi tiết và ví dụ về ba nguyên tắc trên ở [link này](http://www2.stat.duke.edu/~rcs46/lectures_2015/01-markdown-git/slides/naming-slides/naming-slides.pdf). Chúc bạn hiểu thêm về cách đặt tên sao cho chuyên nghiệp, dễ tìm kiếm và dễ phân tích dữ liệu nhé.

## Viết README thế nào cho chuẩn

README là tập tin đầu tiên được đọc trong dự án phần mềm, chứa các nội dung quan trọng nhất của dự án như mục đích của dự án, các tính năng tính, các công nghệ được áp dụng, …

Để viết một file README cho chuẩn, gợi ý đến bạn 7 vấn đề mà bạn nên quan tâm:

1. Viết một đoạn ngắn giới thiệu và mục đích của dự án

2. Sắp xếp các nội dung sao cho dễ truy cập (mục lục, phân nội dung theo từng phần, link liên kết, …)

3. Thông tin chung của dự án bổ sung thêm thông tin sau đoạn ngắn giới thiệu ở trên (dự án giải quyết vấn đề gì, dùng kỹ thuật gì: framework, database, …)

4. Hướng dẫn người dùng chạy dự án lên (các phần mềm tiên quyết, cách tải và chạy dự án)

5. Hướng dẫn cách kiểm thử (run tests) nếu có

6. Mô tả về các bugs, vấn đề của dự án đã biết (know issues)

7. Cung cấp các môi trường đã deploy để người dùng trải nghiệm (staging, prod environment)

8. Thường xuyên update README để cập nhật thông tin mới nhất

9. Cuối cùng, một điểm mình hay thấy là “Nhớ đóng vai người dùng để chạy dự án theo cách bạn đã hướng dẫn, và đảm bảo những gì bạn hướng dẫn là chính xác”.

([Ref](https://www.netguru.com/blog/how-to-write-a-perfect-readme))

## Viết commit message, dễ mà khó

A commit message shows whether a developer is a good collaborator

Một commit message thể hiện người lập trình viên có phải là một người cộng tác tốt hay không

Trong cùng một dự án thì commit message nên thống nhất với nhau về:

– Style: như nội dung bằng tiếng Anh, viết hoa chữ cái đầu tiên, …

– Content: nội dung của message

– Metadata: ticket id, pull request id, …

Luôn luôn “Keep it simple” khi viết một commit message.

Có 7 nguyên tắc giúp bạn viết một commit message tốt hơn:

– Tiêu đề(subject) cách với nội dung một dòng trống

– Tiêu đề tối đa 50 ký tự

– Viết hoa chữ đầu tiên của tiêu đề

– Không viết dấu . cuối tiêu đề

– Sử dụng câu mệnh lệnh khi viết tiêu đề(bắt đầu bằng động từ) Create, Do, Clean, Refactor, Fix, …

– Body nên tối đa 72 ký tự

– Body nên giải thích cho why and how

Mời bạn đọc thêm chi tiết và ví dụ ở [bài này](https://cbea.ms/git-commit/).

## Authentication là gì?
Là quá trình kiểm tra liệu người dùng có đúng danh tính mà hệ thống có về người ấy hay không. Nếu đúng thì sẽ cho phép người dùng truy cập vào hệ thống. Nếu không đúng thì từ chối truy cập vào hệ thống.

Vậy kiểm tra bằng cách nào?

**single factor authentication** – cách này hay sử dụng mật khẩu để đăng nhập, và sẽ có rủi ro là nếu bạn sử dụng cùng mật khẩu cho nhiều hệ thống thì nếu hacker hack được mật khẩu của một cái thì tất cả những tài khoản còn lại đều bị rủi ro về bảo mật.

**2-factor authentication** – cách này an toàn hơn và được sử dụng phổ biến hiện nay vì bên cạnh thông tin đăng nhập (username, password), bạn cần thêm một bên nữa như mã bảo mật gửi về email hay SMS.

**multi-factor authentication** – cách này còn xịn hơn cách ở trên với sự kết hợp giữa nhiều bên liên quan như thông tin đăng nhập, câu hỏi bảo mật, mã bảo mật (SMS, authenticator app) hay nhận dạng vân tay, khuôn mặt.

Tuỳ vào loại ứng dụng mà chọn cách kiểm tra phù hợp vì không lý gì một ứng dụng giải trí lại yêu cầu quá nhiều thứ từ người dùng như tài khoản ngân hàng.

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

