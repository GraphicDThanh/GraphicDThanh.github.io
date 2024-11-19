---
title: "Quản lý hệ thống tập tin trong Linux"
categories:
  - Linux
tags:
  - linux
---

![](/assets/images/2022/03/2022-03-22-chuyen-huong-cau-lenh-trong-linux.webp)

Chào mừng bạn đến với blog số 4 của series [“Linux dành cho lập trình viên”](https://beautyoncode.com/lam-quen-linux-danh-cho-lap-trinh-vien-series-overview/).

Trong các blog trước, mình đã đi qua các nội dung về:

– [**“Giới thiệu về Linux”**](https://beautyoncode.com/gioi-thieu-ve-linux/)

– [**“Làm quen câu lệnh và hệ thống tập tin trong Linux”**](https://beautyoncode.com/lam-quen-cau-lenh-va-he-thong-tap-tin-trong-linux/)

– [**“Quản lý hệ thống tập tin trong Linux”**](https://beautyoncode.com/quan-ly-he-thong-tap-tin-trong-linux/)

Nếu bạn chưa đọc qua thì hãy dừng ít phút ghé đọc để có cái nhìn tổng quan và theo cùng nội dung chuỗi bài này nhé.

Tiếp theo trong bài này, tụi mình sẽ **cùng tìm hiểu thêm về việc chuyển hướng trong Linux**.

---

## Các luồng dữ liệu của một câu lệnh

Quy trình làm việc cơ bản của bất cứ câu lệnh nào chính là nó sẽ nhận **đầu vào**(input) và trả về một **đầu ra**(output). 

Một câu lệnh sẽ có 3 luồng dữ liệu gồm: 

– standard input(stdin)

– standard out(stdout)

– standard error(stderr)

### Đầu vào tiêu chuẩn(stdin)

> **Là dữ liệu được truyền vào câu lệnh.**

Stdin thường là từ bàn phím, ngoài ra còn có thể từ file hoặc một process khác

### Đầu ra tiêu chuẩn(stdout)

> **Là kết quả được trả về sau khi thực thi câu lệnh thành công.**

Stdout thường xuất ra trên màn hình, ngoài ra còn có thể xuất ra file hoặc một process khác

*Ví dụ:* khi bạn gõ ls thì đây chính là stdin, còn stdout là kết quả bạn thấy trên màn hình

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/03/stdin-stdout.png)

### Lỗi(stderr)

> **Là lỗi được trả về sau khi thực thi câu lệnh và có lỗi gì đó xảy ra.**

Stdout thường xuất ra trên màn hình, ngoài ra còn có thể xuất ra file hoặc một process khác

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/stdin-stderr.png)

## "Chuyển hướng" - Redirection là gì?
> **“Chuyển hướng”** là một tính năng trong Linux cho phép chúng ta thay đổi đầu vào tiêu chuẩn(stdin) và đầu ra tiêu chuẩn(stdout) khi thực hiện một câu lệnh.

Ví dụ: bạn chạy một câu lệnh và muốn lưu lại kết quả trả về của câu lệnh này để sử dụng trong tương lai.

### Chuyển hướng vào file
#### Chuyển hướng đầu ra(stdout) vào file với dấu >

> **Dùng dấu > để chuyển hướng cho đầu ra(stdout)**

*Ví dụ:* Chuyển kết quả của câu lệnh ls đã thành công và chuyển sdtout vào file là list.txt

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/redirection-stdout.png)

Kết quả là mình không còn thấy stdout xuất ra màn hình nữa, mà stdout này đã được xuất vào file list.txt, file này được tự động tạo(nếu chưa có) hoặc sẽ ghi đè(nếu file này đã tồn tại).

Tiếp theo ví dụ trên, giả sử mình muốn chuyển stdout của câu lệnh “cal 03 2022” vào file list.txt

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/override-stdout.png)

Vậy là kết quả của lệnh ls ban đầu đã bị ghi đè rồi. 

Nếu bạn muốn ghi thêm vào thay vì ghi đè trong trường hợp này cần **sử dụng dấu >>**. 

Theo đó kết quả mới sẽ được thêm vào như dưới đây:

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/03/adding-stdout.png)

#### Chuyển hướng lỗi(stderr) vào file với dấu 2>
> **Dùng dấu 2> để chuyển hướng cho lỗi(stderr)**

**Ví dụ:** Chuyển kết quả của câu lệnh “cal -1 2022” có lỗi(vì tháng là số âm) và chuyển sdterr vào file là cal.txt(nếu chưa có sẽ tạo mới, có file tồn tại sẽ ghi đè)

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/redirection-sdterr.png)

Thế nhưng không phải lúc nào chúng ta cũng biết chắc chắn là câu lệnh có lỗi để chuyển vào với dấu 2>, khi đó có thể tách ra nếu stdout thì chuyển vào file sdtout-cal.txt và nếu stderr thì chuyển vào file stderr-cal.txt.

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/03/stdout-or-stderr.png)

Nhắc lại chỗ này một tí là khi dùng >, thì nội dung file có sẵn sẽ bị ghi đè. Tức là khi có lỗi xảy ra ở câu lệnh số 2, thì file stdout-cal.txt sẽ bị ghi thành file rỗng, vì nó không có output ở đây.

Cuối cùng là một ví dụ cho trường hợp mình không muốn ghi đè(ôn lại) với >>, kết quả là tất cả các output đều được thêm vào.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/add-std.png)

#### Chuyển hướng tất cả output, gồm stdout và stderr vào file với dấu 2>&1
> **Để chuyển hướng output cho cả stdout và stderr thì sử dụng dấu 2>&1**

**Ví dụ:** Chuyển hướng stdout hay stderror vào file(tạo với nếu chưa có file, ghi đè nếu file đã tồn tại)

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/03/output-onefile.png) 

**Ví dụ:** Chuyển hướng stdout hay stderror thêm nội dung vào file

Một lưu ý là việc chuyển hướng tất cả đầu ra output(stdout, sdterr) vào chung một file rất thường gặp, đặc biệt là khi **chương trình cần theo dõi log(để debug lỗi) của những câu lệnh được chạy**, hoặc **khi bạn muốn chạy lệnh nhưng bỏ qua các lỗi có thể xảy ra**. Tất cả những nội dung output này sẽ được gom vào một file hay gọi là “bit bucket” hay **“black hole”**

#### Ví dụ về đầu vào tiêu chuẩn(stdin)
Hãy thử lệnh này: **tr ‘a-z’ ‘A-Z’**

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/03/tranform-text.png)

Kết quả là chương trình nó đứng im như bị treo vậy á!?

Nhưng mà không phải đâu, thực tế là nó đang đứng đợi bạn truyền đầu vào vào ấy. Thử gõ một dòng chữ: “Have a nice day” vào và enter:

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/input-transform.png)

Kết quả là một dòng chữ mới in hoa được xuất ra, và chương trình tiếp tục đợi đầu vào tiếp theo. 

Nếu muốn thoát khỏi lệnh này, bấm **Ctrl+C**.

Tại đây, chương trình đang sử dụng đầu vào tiêu chuẩn(stdin) là từ bàn phím nhập vào. Nếu đầu vào này thay đổi là một file thì sẽ tốt biết mấy, mình có thể chứa nhiều nội dung để chuyển thành chữ in hoa hơn.

### Chuyển hướng đầu vào với dấu <

> **Dùng dấu < để chuyển hướng cho đầu vào(stdin)**

**Ví dụ:** Chuyển đầu vào cho câu lệnh trên là kết quả của lệnh cal trong file mycal. Tức là mình muốn in ra màn hình lịch ở định dạng in hoa

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/03/input-redirection.png)

Tiếp theo, nếu muốn chuyển hướng cho stdout(lịch ở định dạng in hoa) và một file mynewcal thì sủe dụng > để chuyển hướng đầu ra

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/03/redirection-input-output.png)

### Chuyển hướng đầu ra của câu lệnh này thành đầu vào của câu lệnh khác

> **Dùng dấu | để chuyển hướng cho đầu ra vào câu lệnh khác**

Bạn cũng có thể chuyển hướng đầu ra của câu lệnh này vào câu lệnh khác thay vì chuyển vào file như trên. Việc này rất hữu ích khi mà có nhiều câu lệnh cần nối chuỗi với nhau hay có kết quả quá nhiều.

**Ví dụ:** Kết quả của câu lệnh “ls /etc” rất dài và làm màn hình xuất hiện thanh scroll, gây khó trong việc tìm kiếm trong kết quả nhiều như vậy. 

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/command-long-result.png)

Để giải quyết vấn đề này, chúng ta có thể gửi kết quả này vào một câu lệnh khác là more để hiện thị thành nhiều trang. Và để qua trang mới, chỉ cần bấm phím Space.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/more-command.png)

Vậy là đầu ra của câu lệnh “**ls /etc**” đã trở thành đầu vào của câu lệnh “more”.
Để thoát ra khỏi chế độ xem nhiều trang của more, bấm “q” và enter để thoát.

## Piping
Quá trình chuyển hướng đầu ra của lệnh này thành đầu vào của lệnh khác như trên được gọi là **piping**.  Bạn có thể tạm dịch nó là dạng đường ống(piping) vì nó chuyển dữ liệu(output) giống như nước chảy từ ống này sang ống khác.

Để hiểu thêm về piping, mời bạn xem qua sự so sánh hai quá trình sau:

### Quá trình của câu lệnh **"ls /etc"** với đầu vào và đầu ra tiêu chuẩn
Khi bạn gõ **“ls /etc”** từ bàn phím, kết quả sẽ được in ra màn hình. Dưới đây là quá trình này:

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/03/standard-process.png)

### Quá trình của câu lệnh **"ls /etc | more"** với piping
Khi bạn gõ **“ls /etc | more”** từ bàn phím, kết quả lệnh ls nếu có lỗi sẽ được in ra màn hình, nếu không có lỗi sẽ chuyển đầu ra thành đầu vào của lệnh more và xuất kết quả ra màn hình. 

Dưới đây là quá trình này:

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/03/piping-process.png)

---

Nội dung bài blog này đến đây tạm hết rồi, tụi mình đã tìm hiểu về cách điều hướng câu lệnh trong Linux rồi, thú vị thật nhỉ.

Trong bài viết tiếp theo của series [“Làm quen Linux giành cho lập trình viên”](https://beautyoncode.com/lam-quen-linux-gianh-cho-lap-trinh-vien-series-overview/), sẽ là tìm hiểu thêm về **“Các câu lệnh Linux thường dùng”**

Hẹn gặp các bạn trong bài viết sau.
