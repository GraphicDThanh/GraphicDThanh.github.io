---
title: "Làm quen câu lệnh và hệ thống tập tin trong Linux"
categories:
  - Linux
tags:
  - linux
---

![](/assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux.webp)


Chào mừng bạn đến với phần 2 của series [“Linux giành cho lập trình viên”](https://beautyoncode.com/lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux/).

Trong phần Linux cơ bản, đầu tiên mình đã cùng làm quen với Linux qua bài viết [“Giới thiệu về Linux”](https://beautyoncode.com/gioi-thieu-ve-linux/), nếu bạn chưa đọc qua thì hãy dừng ít phút ghé đọc để có cái nhìn tổng quan nhé.

Tiếp theo trong bài này, tụi mình sẽ làm quen câu lệnh và hệ thống tập tin trong Linux, bao gồm:

– Cấu trúc của một câu lệnh

– Giới thiệu hệ thống tập tin

– Điều hướng trong hệ thống tập tin

Tới công chiện rồi, vào thôi! Chúc các bạn đọc nội dung vui vẻ nhé ^^

## Cấu trúc câu lệnh
Một câu lệnh sẽ bao gồm 3 phần: 
**<tên câu lệnh> <các lựa chọn> <các đối số>**

![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-1.webp)

Các options ở đây là các giá trị được định nghĩa sẵn sẽ thay đổi cách là việc của câu lệnh. 

Các đối số sẽ là các giá trị truyền thêm vào.

Ví dụ:  Xem document của câu lệnh ls với man. 

> man ls

Ở đây, **man** là tên câu lệnh(viết tắt của manual), **ls** là đối số. 

Kết quả là một document của ls xuất hiện trên màn hình.

![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-2.webp)

Để đọc document này, ngoài cách dùng chuột kéo xuống xem nội dung thì mình còn có thể sử dụng các cách như:

– **<spacebar>** : di chuyển xuống dưới một màn hình

– **<enter>** : di chuyển xuống từng dòng

– **b + <enter>** : di chuyển lùi một màn hình

– **/<từ-cần-tìm>** : tìm kiếm với <từ-cần-tìm> ở nội dung tiếp theo

– **h + <enter>** : hiển thị màn hình trợ giúp, tại đây có hướng dẫn cách điều hướng cho bạn

– **q + <enter>** : thoát khỏi màn hình hiện tại
    
## Hệ thống tập tin(filesystem)
    
Dù mục đích khi học về Linux của bạn là gì đi nữa, thì việc hiểu về hệ thống tập tin(filesystem) và di chuyển(navigate) giữa các thư mục khác nhau, cũng như việc quản lý các tập tin là điều cần biết.
    
### Hiểu thêm về filesystem

> Filesystem là cách các tập tin được tổ chức một cách có cấu trúc nằm trong những thư mục.
    
Linux có cấu trúc thư mục không phân chia theo ổ đĩa(C, D, …) như Windows mà có một thư mục gốc gọi là thư mục root(thường viết là /). 
    
![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-3.webp)

Từ / sẽ phân chia thành nhiều loại thư mục có mục đích dùng khác nhau. 

Một số thư mục hay dùng đến là:

– **/home**: chứa nội dung của người dùng user

– **/root:** chứa nội dung của người dùng root

– **/bin**, **/usr/bin**: chứa các chương trình thực thi, hầu hết các câu lệnh hệ thống được chạy. Ví dụ “ls”

– **/sbin**, **/usr/sbin**: chứa các chương trình thực thi giành cho admin
    
### Chuyện đặt tên

Nói đến hệ thống file, thì cũng nói luôn đến chuyện cân nhắc khi đặt tên cho thư mục(folder) hoặc tập tin(file) sao cho hợp lý. 

**Thường thì sẽ cân nhắc một số điểm sau:**

– ***Tên thì sẽ phân biệt viết hoa và viết thường***, ví dụ: text.txt và Text.txt sẽ là hai files khác nhau

– ***Tên được phép chứa các ký tự đặc biệt***. Tuy nhiên khi đặt tên có khoảng cách hay các ký tự đặc biệt sẽ dễ sinh vấn đề, do đó nên hạn chế.

– ***Ký tự / đại diện cho thư mục root, và cũng dùng trong đường dẫn để chia bậc, cho nên cũng hạn chế sử dụng ký tự này***.

– ***Tên được phép chứa các đuôi(extension) như là .csv, .txt, …*** Tuy nhiên, Linux và BASH shell thì không buộc có các đuôi này, nhưng nó sẽ có ích cho người dùng để dễ hiểu nội dung theo từng loại file.

– *Một số tên thư mục được định nghĩa sẵn*:

  `~` là đại diện cho thư mục home của người dùng hiện tại

   `.` là đại diện thư mục hiện tại

  `..` là đại diện thư mục cha của thư mục hiện tại
    
## Điều hướng filesystem

Khi sử dụng môi trường command-line, thường bạn sẽ cần truy cập vào một file đang ở một thư mục nào đấy, hoặc là truy cập vào một thư mục để xem trong đó có gì.

Khi mở terminal lên(hoặc chương trình shell nào đấy, ví dụ iTerm chẳng hạn), thì bạn con trỏ sẽ tự động được đứng ở thư mục home của người dùng.

![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-4.webp)
    
> Câu lệnh **pwd** giúp kiểm tra vị trí hiện tại của thư mục. 

Kết quả của câu lệnh này trên máy mình là “/Users/thanhnguyen” (máy bạn sẽ khác nha), chính là một **đường dẫn**(**path** hay **pathname**).

Thư mục mà con trỏ đang đứng thường được gọi là **working directory** hay **current directory**.

Và công việc mình muốn làm là di chuyển đến thư mục bin nằm trong usr/ chẳng hạn thì gọi là thay đổi thư mục(**change directory**).
    
### Các loại đường dẫn

Đường dẫn thể hiện cách mình có thể tham chiếu với cấu trúc thư mục. Dấu / được dùng trong đường dẫn để phân cách từng bậc của cấu trúc này.

**Có 2 loại đường dẫn bạn sẽ gặp là:**

– ***đường dẫn tuyệt đối(absolute path)*** : đường dẫn này thể hiện *vị trí của tệp liên quan đến thư mục root*, do đó luôn bắt đầu với /.
    
  Ví dụ: `/usr/bin`

– ***đường dẫn tương đối(relative path)*** : đường dẫn này thể hiện *vị trí của tệp từ thư mục hiện tại,* do đó sẽ bắt đầu từ thư mục hiện tại .

  Ví dụ: `../../usr/bin`

Vậy là có thể dễ dàng xác định loại đường dẫn bằng cách quan sát, nếu đường dẫn bắt đầu bằng **/** thì là tuyệt đối vì bắt đầu ở root, còn đường dẫn có chứa ` .` hay `..` là tương đối vì sử dụng thư mục hiện tại.

Và thêm nữa, đường dẫn có thể giúp mình đến thư mục bin có thể là /usr/bin hoặc ../user/bin.

Tùy loại nào mình thấy nó tiện hơn thì mình dùng. 

Ví dụ nếu từ thư mục hiện tại mà cần ra ngoài đến 4, 5 bậc thì mình nghĩ là absolute path sẽ tiện hơn, còn từ thư mục hiện tại chỉ ra ngoài 1,2 bậc thì sẽ ưu tiên dùng relative path.
    
### Cách điều hướng

Để điều hướng trong filesystem, sử dụng câu lệnh cd đi kèm với đường dẫn của nơi muốn đến
> cd <đường-dẫn>

Nếu `cd` không có đường dẫn sẽ mặc định về thư mục `~`
    
### Điều hướng relative path

**Cách làm:** bắt đầu từ thư mục hiện tại, mỗi lần `..` là di chuyển lên trên một bậc, là thư mục cha của thư mục hiện tại.

Ví dụ mình muốn di chuyển từ /Users/thanhnguyen đến /usr/bin

  – .. lần 1 sẽ di chuyển ra đứng ở thư mục Users

  – .. lần 2 sẽ di chuyển ra đứng ở `/`

  – sau đó truy cập vào `usr/bin` 

Nên `cd ../../user/bin` sẽ giúp mình chuyển từ thư mục hiện tại sang thư mục `user/bin`.
![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-5.webp)
    
### Điều hướng absolute path

**Cách làm**: thư mục bin nằm trong folder usr, và folder usr nằm trong folder root `/`, nên absolute path sẽ là `cd /usr/bin`

![](assets/images/2022/02/2022-02-03-lam-quen-va-dieu-huong-he-thong-tap-tin-trong-linux-6.webp)
    
---

Nội dung bài blog này đến đây tạm hết rồi, tụi mình đã làm quen với hệ thống tập tin trong Linux cũng như cách điều hướng trong hệ thống này.

Trong bài viết tiếp theo của series [“Làm quen Linux giành cho lập trình viên”][lam-quen-linux-danh-cho-lap-trinh-vien], sẽ là tìm hiểu thêm về việc quản lý hệ thống tập tin trong Linux.

[lam-quen-linux-danh-cho-lap-trinh-vien]: {{ "" | relative_url }}{% post_url linux/2022-01-29-lam-quen-linux-danh-cho-lap-trinh-vien-series-overview %}
