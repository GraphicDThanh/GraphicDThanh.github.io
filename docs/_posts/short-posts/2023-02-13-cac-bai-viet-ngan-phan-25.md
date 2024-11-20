---
title: "Các bài viết ngắn - phần 25"
categories:
  - Short Posts
tags:
  - short-post
---
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2023/01/25.png)
## Chọn id cho khóa chính CSDL
Một trong các công việc đầu tiên khi thiết kế database schema là việc chọn loại khóa chính cần sử dụng.

Lập trình viên thường đứng trước 2 lựa chọn chính là:
– UUID
– Auto Increment Integer hay Serial – id tăng dần

Việc chọn loại khóa chính sẽ phụ thuộc vào yêu cầu của sản phẩm cũng như các hệ thống khác liên quan.
Giới thiệu đến bạn các đặc điểm của từng loại để thêm kiến thức cho việc lựa chọn.

### UUID

Hai loại uuid được sử dụng phổ biến là v4 (random UUID) và v1 (timestamp UUID)

**Đặc điểm:**
– Duy nhất ở tất cả mọi nơi (global unique)
– Có thể tạo mà không phụ thuộc điều kiện gì
– Không phù hợp để đọc
– Khó phân loại hay sắp xếp
– Với SQL, Oracle nếu uuid v4 làm khóa chính có thể ảnh hưởng performance insert, bởi yêu cầu sắp xếp lại trong clustered index. Còn PostgresSQL thì lại không ảnh hưởng

### Auto Increment Integer hay Serial

**Đặc điểm:**
– Được các loại database hỗ trợ mặc định
– MySQL – AUTO_INCREMENT
– PosrgresSQL – SERIAL
– SQLite – AUTOINCREMENT
– Dễ đọc
– Ít bộ nhớ (uuid thì luôn chiến 16 bytes, còn id tăng dần với số long forrmat chỉ chiếm 8 bytes)
– Không thể sử dụng làm id trong hệ thống distributed system gồm nhiều server do việc trùng id.
– Khi tạo cần có số id phía trước để tăng lên 1
– Rủi ro về bảo mật

Vậy nên chọn loại nào để làm khóa chính?

Thực tế là có đến 95% sử dụng Auto Increment Integer vì các lợi ích về tính dễ đọc, đơn giản, dễ nhớ và ứng dụng không nằm trong hệ thống lớn.

Ứng dụng nhiều nhất của UUID là các hệ thống log và các ứng dụng nằm trong hệ thống có nhiều servers (distributed system).

Bạn đọc thêm ở [bài viết sau](https://www.bytebase.com/blog/choose-primary-key-uuid-or-auto-increment) nha.

## Các cách để tạo UUID trong JS
**UUID** là viết tắt của Universally Unique IDentifier.
UUID có dạng là một chuỗi string gồm 32 ký tự ASCII (16 bytes), ra đời nhằm khắc phục các điểm yếu của id tăng dần (Auto Increment Integer) như:
– không phù hợp với nhiều hệ thống server (distributed system)
– rủi ro về bảo mật
– cần phụ thuộc vào số id phía trước để tăng lên 1

Tuy nhiên UUID thì lại khó đọc, nên sẽ không ưu tiên khi muốn khóa chính dễ đọc.
Ví dụ UUID v4 random: `f6ca05c0-fad5-46fc-a237-a8e930e7cb49UUID`

Các cách để tạo UUID trong JavaScript:

### Sử dụng thư viện uuid
Thư viện uuid sử dụng tạo uuid như sau

```js
import { v4 as uuidv4 } from 'uuid';
uuidv4();
```

### Sử dụng crypto API
`crypto.randomUUID()`

hiện tại đã support global trên 90% kiểm tra support ở [Can I Use](https://caniuse.com/mdn-api_crypto_randomuuid)

Sử dụng một utils tự định nghĩa
```js
function uuidv4() {
  return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
    (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
  );
}
```

(ref from this question (https://stackoverflow.com/a/2117523) on StackOverflow)

Ngoài ra, cũng có một thư viện giúp tạo unique ID tương tự uuid là nanoid với 2 điểm khác so với uuid là:

– sử dụng ký tự lớn hơn (bigger alphabet) nên chỉ có 21 ký tự thay vì 36
– nhẹ hơn uuid 4 lần vì sử dụng ít ký tự hơn (130 bytes thay vì 423 bytes)

Bạn có đang sử dụng cách nào khác nữa thì chia sẻ với mình nhé.
—
Gửi bạn thêm một bài viết mà mình đọc về uuid và serial khá hay và chi tiết
https://devforth.io/blog/why-your-software-should-use-uuids/

## Bốn bước để học và viết

Bốn bước để học và viết trong thời gian dài

**01. Làm tốt công việc của bạn**
Nếu bạn làm tốt nhất công việc của mình, tập ghi chép lại, chắc chắc sẽ có nhiều điều cần viết xuống.

**02. Hỗ trợ đồng nghiệp, chia sẻ kiến thức**
Có rất là nhiều cách tạo ảnh hưởng, cho bản thân bạn và cho những người bạn quan tâm. Chia sẻ là một chìa khóa an toàn nhất mà mình biết được.

**03. Đọc, học hàng ngày, hàng tuần**
Việc cập nhật các kiến thức mới hàng ngày sẽ giúp bạn khác biệt với những người khác.

**04. Yêu thích công việc bạn làm và cứ thoải mái thôi (take it easy)**
Suy cho cùng, bạn hay mình đều dành 8 tiếng làm việc nơi công sở, hay ở nhà thì cũng trên máy tính. Học tập và làm việc, đi chơi là cuộc sống của tụi mình.
Nếu không yêu nó thì mình sống kiểu gì mới được, đúng không? ^^

Hi vọng một số bước này có thể gợi ý thêm cho bạn nha, ghé bài viết dưới đây mình có vẻ infographic minh hoạ dễ thương tặng bạn ý.

https://beautyoncode.com/bon-buoc-de-hoc-va-viet-trong-thoi-gian-dai/

## SOLID với ví dụ cùng Python

**SOLID** là 5 nguyên tắc nền tảng trong lập trình hướng đối tượng OOP (Object Oriented Programming)
SOLID giúp thiết kế chương trình hướng đối tượng linh động, dễ hiểu và dễ duy trì.


**SOLID** là viết tắt của 5 chữ cái đầu của mỗi nguyên tắc sau:
S: Single Responsibility Principle (SRP)
O: Open-Closed principle (OCP)
L: Liskov Substitution Principle (LSP)
I: Interface Segregation Principle (ISP)
D: Dependency Inversion Principle (DIP)

Mình từng chia sẻ qua về SOLID với các ví dụ dành cho JS qua [bài viết này](https://careerly.vn/comments/4974?utm_campaign=self-share).

Tiếp tục tìm hiểu kỹ hơn về SOLID, và thực hành cùng Python
Bài viết dưới đây đưa ra một ứng dụng Python đơn giản và chia mỗi nguyên tắc thành các nội dung cụ thể gồm:
– Giới thiệu nội dung của nguyên tắc
– Thực hành: bao gồm giải thích lý do vi phạm, và hướng cải thiện cụ thể trên code.

Bạn ghé blog đọc thêm chi tiết nha.
Bài viết hơi dài nhưng mình tin là bạn sẽ thích vì nó vô cùng hữu ích phù hợp với thực tiễn trong dự án

https://beautyoncode.com/solid-trong-oop-voi-python

## Phát huy thế mạnh thay vì cải thiện điểm yếu

Bạn đã nghe cụm từ trên ở đâu rồi phải không?

Thực ra là có một bài kiểm tra “The CliftonStrengths assessment” giúp bạn xác định 5 thế mạnh nổi trội nhất của mình.
Và một cuốn sách Strengths Finder 2.0 mô tả chi tiết từng loại thế mạnh, các gợi ý giúp phát huy và cách làm việc với những người có các loại cụ thể này.

Các thể mạnh này có một cách tự nhiên trong chính mỗi người từ khi sinh ra và hầu như là không thay đổi nhiều theo thời gian.

Clifton Strengths 34 là 34 loại thế mạnh phổ biến nhất, phân loại thành 4 nhóm:
+ Suy nghĩ chiến lược (Strategic Thinking)
+ Thực thi (Executing)
+ Ảnh hưởng (Influencing)
+ Xây dựng mối quan hệ (Relationship Building)

Mình đã làm bài kiểm tra này vào năm 2019 và từ đó hiểu về bản thân hơn, ngày càng tiến bộ hơn, trở thành phiên bản tốt hơn của mình.
Mình thuộc nhóm “Relationship Building”, top 5 thế mạnh của mình bao gồm:
1. Lạc quan, tích cực (Positivity)
2. Học hỏi (Learner)
3. Xây dựng, nhìn thấy tiềm năng của người khác (Developer)
4. Có niềm tin mọi thứ đều có mối liên hệ (Connectedness)
5. Tôn trọng tính cá nhân (Individualization)

Hành trình tìm ra những thế mạnh này không dễ dàng, đôi lúc mình cũng từ chối các bạn ấy. Đầu năm mình có tâm sự trên blog dưới đây.

Nếu bạn còn thấy lạc lối thì có thể thử cách mình làm này nhé.
Chúc mọi người luôn làm những điều mình thoả mái nhất và đạt nhiều thành công vang dội nhất.

—
Đầu năm kể chuyện tìm đường – BeautyOnCode
https://beautyoncode.com/phat-huy-diem-manh-thay-vi-khac-phuc-diem-yeu/