---
title: "Giới thiệu về CLI và các câu lệnh làm việc với file trong Linux"
categories:
  - Linux
tags:
  - linux
---

![](/assets/images/2022/06/2022-06-14-gioi-thieu-ve-cli-va-mot-so-cau-lenh-lam-viec-voi-file-trong-linux.webp)

Chào mừng bạn đến với blog số 5 của [series “Linux dành cho lập trình viên”](https://beautyoncode.com/lam-quen-linux-danh-cho-lap-trinh-vien-series-overview/).

Trong các blog trước, mình đã đi qua các nội dung về:

– [“Giới thiệu về Linux”](https://beautyoncode.com/gioi-thieu-ve-linux/)

– [“Làm quen câu lệnh và hệ thống tập tin trong Linux”](https://beautyoncode.com/lam-quen-cau-lenh-va-he-thong-tap-tin-trong-linux/)

– [“Quản lý hệ thống tập tin trong Linux”](https://beautyoncode.com/quan-ly-he-thong-tap-tin-trong-linux/)

– [”Chuyển hướng câu lệnh trong Linux”](https://beautyoncode.com/chuyen-huong-cau-lenh-trong-linux/)

Nếu bạn chưa đọc qua thì hãy dừng ít phút ghé đọc để có cái nhìn tổng quan và theo cùng nội dung chuỗi bài này nhé.

Tiếp theo trong bài này, tụi mình sẽ **làm quen CLI và một số câu lệnh khi làm việc với tập tin(file)**

## Giới thiệu về CLI (Command Line Interface)
Trong những bài viết trước đây, chúng ta đã cùng làm quen với Linux và thực hành một số câu lệnh trên môi trường dòng lệnh(đã được mình giới thiệu ở bài [“Giới thiệu về Linux”](https://beautyoncode.com/gioi-thieu-ve-linux/)), bạn này đây:

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/01/cli-interface.png)

Môi trường này có tên đầy đủ là Command Line Interface(CLI), nơi cung cấp rất nhiều câu lệnh có thể dùng(khoảng 10,000). 

### Tại sao lại sử dụng CLI?
Thường thì mọi người sẽ sử dụng các hệ thống thiên về giao diện(GUI-based systems) như là Windows, vì nó khá dễ tiếp cận, dễ làm quen và sử dụng chỉ với vài cú nhấn chuột. Và nghĩ CLI như là một cái gì đó lỗi thời, kiểu thuộc về các thập niên trước. 

Tuy nhiên, **CLI** vẫn tồn tại và có vị trí của nó trong các hệ thống hiện đại, với các lý do:

– **Tính ổn định**: Nhiều câu lệnh Linux được dùng từ Unix và vẫn rất thiết yếu dù cả mấy thập niên đã trôi qua. Sự ổn định này giúp lập trình viên có thể tập trung vào việc làm ra nhiều công cụ hơn là phải viết lại những tính năng đã có sẵn.

– **Tốc độ phát triển sản phẩm**: Phát triển sản phẩm với CLI tốn ít thời gian hơn sử dụng GUI based tools. 

– **Tốc độ sử dụng**: Có thể bạn không tin nhưng bạn thực sự có thể làm các công việc của mình nhanh gọn với các câu lệnh. Thường thì các GUI-based tools sẽ cần sự kết hợp của chuột và bàn phím. Còn command line thì chỉ cần bàn phím là đủ.

– **Siêu năng lực**: Bạn có thể kết hợp các câu lệnh để làm nhiều việc thú vị, hoàn thành công việc nhanh gọn và hiệu quả hơn.

Trong những nội dung tiếp theo của series học Linux này, mình sẽ cùng nhau tìm hiểu những câu lệnh thông dụng mà lập trình viên nên biết và sử dụng thành thạo, đầu tiên là làm việc với tập tin.

---

Trong Linux, mọi thứ đều được hiểu là file, cả thư mục cũng là một loại file có một đặc điểm riêng thôi. Cho nên việc học những câu lệnh để xem, tìm kiếm, so sánh file là cần thiết. 

## Các lệnh sử dụng để xem file
### Lệnh "file"
Với một tập tin, việc xem định dạng của tập tin đó trước tiên có thể giúp chúng ta bước đầu xác định đó có phải là cái mình muốn tìm hay không. 

Có nhiều loại định dạng như text, code, database, …

> Lệnh **file** giúp xem kiểu định dạng của file

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/01/some-file-formats.png)

Trong ví dụ trên là một số kiểu định dạng khác nhau của file: zip, directory, ASCII text.

Những tập tin có kết quả trả về từ câu lệnh “file” có chứa “text” thì bạn có thể sử dụng những câu lệnh tiếp sau đây để xem chúng. 

### Lệnh "cat"

> Lệnh **cat** giúp xem nội dung của một file.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/01/cat-command.png)

Nếu muốn hiển thị số dòng, bạn có thể sử dụng thêm lựa chọn **-n**

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/01/cat-with-option-n.png)

Lệnh “cat” sẽ thường được dùng để mở một file nhỏ, vì khi mở file với cat thì nếu file lớn quá sẽ có thanh kéo hiện lên và để xem hết file thì bạn cần scroll ngược lên trên để xem nội dung(hình bên dưới).

Do đó, với file có kích thước lớn, việc chia trang để xem với hai câu lệnh more, less sẽ tiện hơn.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/01/cat-large-file.png)


### Lệnh "more" và "less"

> Lệnh **more** và **less** giúp hiển thị nội dung file theo từng trang

Vì sao có cả **more** và cả **less** nhỉ? Trong khi hai câu lệnh này về cơ bản là trả ra kết quả như nhau.

Dành cho ai có thắc mắc này thì câu lệnh **less** là phiên bản nâng cấp của câu lệnh **more**. (Tuy nhiên, tính năng nâng cao này mình sẽ không tìm hiểu ở đây. Cho nên, tạm thời mình cứ tạm xem hai câu lệnh này là giống nhau đi nhé.)

Bên cạnh đó, câu lệnh more hoạt động như thế nào thì mời bạn có thể xem lại nội dung trong bài [“Chuyển hướng câu lệnh trong Linux”](https://beautyoncode.com/chuyen-huong-cau-lenh-trong-linux/) để hiểu rõ hơn nhé.

Dưới đây là kết quả của câu lệnh *cat text.txt | more*
![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/01/cat-with-more.png)

Bên trên giúp mình xem nội dung với chế độ phân trang với more, less. 

Ngoài ra, bạn có thể sử dụng các câu lệnh để điều khiển việc hiển thị một phần nội dung với **head**, **tail** hay là hiển thị những thông tin thống kê như số dòng, số từ, số ký tự với lệnh **wc**

### Lệnh "head" và "tail"

> Lệnh **head** và **tail** giúp hiển thị phần đầu hay phần cuối nội dung của file

Mỗi phần nội dung mặc định là 10 dòng. Nếu muốn điều chính số dòng, sử dụng lựa chọn -n.

Ví dụ: Giả sử đây là toàn bị nội dung của file text.txt
![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/01/text-content.png)

### "head"
> Lệnh **head** giúp hiển thị phần đầu nội dung của file

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/01/head-text-content.png)

### "tail"
> Lệnh **tail** giúp hiển thị phần cuối nội dung của file

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/01/tail-text-content.png)

#### hiển thị với số dòng với -n
Muốn hiển thị với số dòng cụ thể nào đó, có thể sử dụng kết hợp với option **-n**

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/01/head-text-content-n.png)

### Lệnh "wc"

> Lệnh **wc** giúp hiển thị các thông tin thống kê của nội dung file, như số dòng, số từ, số ký tự

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/01/wc-content.png)

Kết quả của lệnh wc text.txt ở trên là file có 34 dòng, 249 từ và 898 ký tự

898 ký tự cũng có thể hiểu là 898 bytes. Vì 1 character = 1 byte

#### Các options

Lệnh “**wc**” có những lựa chọn như:

   **-c**: hiển thị số bytes

   **-m**: hiển thị số ký tự

   **-l**: hiển thị số dòng

   **-w**: hiển thị số từ
   

## Các lệnh sử dụng để tìm kiếm file
Khi muốn tìm một file nào đó mà bạn chỉ nhớ tên của nhó chứ không nhớ chính xác là nó ở đây, bạn có thể sử dụng command **locate** hoặc **find** để tìm trong hệ thống các file của máy.

### Lệnh "locate"

Câu lệnh **locate** sẽ tìm kiếm file trong một database có sẵn.

Mỗi ngày, một cơ sở dữ liệu(database) sẽ tự động tạo và chứa danh sách các tập tin và thư mục trong hệ thống. Câu lệnh **locate** sẽ giúp bạn tìm kiếm trong cơ sở dữ liệu này.

Nếu bạn còn tò mò nữa thì cơ sở dữ liệu này nằm ở “/var/db/locate.database”

Ví dụ mình muốn tìm cuốn sách của mình với “Developers.pdf”

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/07/locate-ex.png)

Câu lệnh locate sẽ trả về đường dẫn tuyệt đối. Bạn cũng có thể dùng option “**-c**” để đếm số file được tìm thấy trong database

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/07/locate-count.png)

Với câu lệnh **locate**, kết quả được trả ra khá nhanh chóng do bạn ấy tìm trên một cơ sở dữ liệu có sẵn. 

Tuy nhiên, locate có nhược điểm lớn đó là **“Data đôi khi sẽ không chính xác”**

#### Lý do 1: 
khi tìm kiếm với locate, user đi tìm sẽ là “nobody”, điều này đồng nghĩa với nó không thể tìm kiếm được những nơi mà user nobody hay group nobody không có quyền đọc thì những files này sẽ không được tìm thấy. 

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/07/locate-no-permission.png)

**Ví dụ:** Ở hình trên, thực hiện tìm “cli-interface.png” trong folder  “example-linux/file-formats”, và locate không thể tìm ra file này, lý do là vì nobody không có quyền đọc file này. 

Bài [“Quản lý hệ thống tập tin trong Linux”](https://beautyoncode.com/quan-ly-he-thong-tap-tin-trong-linux/) có giải thích về các quyền này, bạn có thể ghé đọc thêm.

#### Lý do 2: 
cơ sở dữ liệu được tạo mới mỗi ngày, do đó nếu file được tạo sau đó thì cũng sẽ không được tìm thấy vì chưa có trong cơ sở dữ liệu.
Lúc này cần phải cập nhật lại cơ sở dữ liệu bằng tay với câu lệnh 

`“sudo /usr/libexec/locate.updatedb”.`

Ví dụ: Mình muốn tìm file hello-training.sh ngay trong thư mục mình vừa mới tạo.

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/07/location-new-file.png)

Kết quả là không tìm thấy dù cho nobody có quyền thực thi như ở trên hình. Lý do mình đã nói ở trên là do những file này được tạo sau nên trong cơ sở dữ liệu của locate chưa có data, do đó tìm không thấy.

Thực hiện cập nhật cơ sở dữ liệu(chạy hơi lâu, vì là của toàn hệ thống), rồi thì tìm lại mới có thể tìm thấy được.
![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/07/locate-new-file-update-db.png)

Vì cái sự bất tiện của locate như thế, nên đã đến lúc bạn cần biết thêm về câu lệnh tìm kiếm chủ động hơn, là **find**

### Lệnh "find"
Câu lệnh **find** sẽ tìm kiếm trực tiếp trên toàn hệ thống, do đó nó sẽ tốn nhiều thời gian, nhưng nó sẽ tìm kiếm chính xác hơn. 

Cú pháp:

> **find** [vị trí bắt đầu] [các lựa chọn, đối số]

Ví dụ: Mình tìm file text.txt ở thư mục hiện tại với câu lệnh find

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/07/find-output.png)

#### Một vài gợi ý để việc tìm với find nhanh hơn:
**1. Hạn chế tìm từ root /**, hoặc folder có số lượng file quá lớn, khoanh vùng phạm vi tìm kiếm càng hẹp càng đỡ tốn thời gian.

**2. Xử lý output** để có kết quả trả về sạch sẽ hơn, bạn có thể tạm thời trả tất cả error về /dev/null black hole với 2>. 

Ví dụ:

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/07/find-error-to-dev-null.png)

Về **black hole /dev/null**, nó là một null device của unix-system, hay còn gọi là black hole hay bit bucket nơi tất cả các data đều được ghi thành công tuy nhiên sẽ không có dữ liệu nào được ghi lại. Bạn có thể tưởng tượng nó như một cái hố sâu không đáy vậy(đọc thêm ở [đây](https://www.codercrunch.com/post/2031971524/what-is-devnull)).

null device này thường được sử dụng để loại bỏ các đầu ra không mong muốn, trong tình huống này là các output về warning permission, và sử dụng kết hợp với câu lệnh chuyển hướng như ở trên.

(Đọc thêm về 2> trong cách chuyển hướng câu lệnh trong Linux ở [“Chuyển hướng câu lệnh trong Linux”](https://beautyoncode.com/chuyen-huong-cau-lenh-trong-linux/).)

**3. Sử dụng một số lựa chọn để thu hẹp loại file tìm kiếm.**

Những lựa chọn của find là:

**-name**: tìm kiếm với tên

**-delete:** tìm xong rồi xóa luôn

**-ls**: hiển thị file tìm được ở dạng long list

**-exec { } \;** thực thi một câu lệnh gì đó với kết quả tìm kiếm. Ví dụ hiển thị kết quả ở với more sẽ là: -exec more { } \;

Ví dụ:

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/07/find-options.png)

## Các lệnh sử dụng để so sánh file

Khi làm việc với file, việc cần so sánh hai file có giống nhau hay không, nếu khác nhau thì khác nhau như thế nào rất phổ biến. Mời bạn làm quen với hai câu lệnh giúp bạn công việc này “**cmp**” và “**diff**”


### Lệnh "cmp"
Nếu chỉ muốn xem hai file có khác nhau không, thì câu lệnh **cmp** là đủ.

Nếu hai file hoàn toàn giống nhau, câu lệnh trả về rỗng, nếu khác nhau sẽ trả về một số thông tin về sự khác nhau này.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/07/cmp.png)

### Lệnh "diff"
Nếu muốn xem sự khác nhau giữa hai file là gì, sử dụng câu lệnh **diff**

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/07/diff.png)

Kết quả ở trên ý nói: “Nếu bạn thay đổi dòng test.txt ở file list.txt thành test2.txt thì kết quả sẽ file text2.txt”

Còn 17c17 có nghĩa là: thay đổi(c) dòng 17 ở file đầu tiên để giống với dòng 17 của file số hai.

---

Nội dung bài blog này đến đây tạm hết rồi, tụi mình đã tìm hiểu thêm về CLI và một số câu lệnh cần dùng khi làm việc với file.

Trong bài viết tiếp theo của series [“Làm quen Linux giành cho lập trình viên”](https://beautyoncode.com/lam-quen-linux-gianh-cho-lap-trinh-vien-series-overview/), sẽ là tìm hiểu thêm về “Shell Variables và Permission” nhé.