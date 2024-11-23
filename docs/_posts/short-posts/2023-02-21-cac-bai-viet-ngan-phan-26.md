---
title: "Các bài viết ngắn - phần 26"
categories:
  - Short Posts
tags:
  - short-posts
  - concepts
  - linux
  - documentation
  - django
---
![](/assets/images/2023/02/2023-02-21-cac-bai-viet-ngan-phan-26-1.webp)

## Don't repeat yourself hay DRY
Bạn có nghĩ giai đoạn bảo trì (maintenance) là sau khi chương trình được phát hành (release)? Và trong giai đoạn này là các công việc như fix bugs, hay cải thiện các tính năng?

Mình cũng từng nghĩ vậy, nhưng nghĩ vậy là chưa đúng.

Lập trình viên luôn ở trong giai đoạn bảo trì. Bởi sự hiểu của chúng ta thay đổi mỗi ngày, yêu cầu dự án, môi trường, … cũng thường xuyên cập nhật trong khi bạn đang thiết kế, đang code.
Vì thế vấn đề về lặp code cũng dễ dàng xảy ra, và đó là vấn đề lớn nhất thường gặp gây khó khăn cho việc bảo trì.
Cách tốt nhất để giúp chương trình dễ hiểu và dễ bảo trì, là tuân theo nguyên tắc DRY – Don’t Repeat YourSelf.

Khi đó bạn thay đổi một chỗ, sẽ không cần nhớ phải đổi 2,3 chỗ tương tự. Hay tệ hơn nữa là đổi một chỗ mà những chỗ khác bị sai đi. Và chắc chắn là sẽ có lúc bạn không thể nhớ hết được tất cả các nơi, vậy nên ngay từ đầu hãy viết code theo nguyên tắc DRY.
Nhưng vì sao code ngày càng bị lặp?

**Có 4 lý do chính:**

### Lặp vì không thể tránh khỏi
Đôi khi có yêu cầu viết code rõ ràng, lặp nhau vì những mục tiêu cụ thể của dự án (ví dụ như nhiều nền tảng) hay những ngôn ngữ yêu cầu như vậy.
Khi đó có một số cách để giúp bạn cải thiện như sử dụng chung các loại tài liệu chung (database chema, pseudo code), comment code, viết document, …

### Lặp vì không biết nó bị lặp
Điều này thường xảy ra. Ban đầu, bạn thiết kế chương trình theo yêu cầu A, sau đó chương trình thay đổi yêu cầu sang B và code bạn thiết kế không phù hợp nữa dẫn đến bị lặp.
Các quy tắc chuẩn hoá cơ sở dữ liệu, các nguyên tắc trong lập trình hướng đối tượng như SOLID là những cách giúp bạn cải thiện việc thiết kế chương trình.

### Lặp vì không cẩn thận, vội vàng
Mọi dự án đều có áp lực về thời gian, và dễ dàng thúc đẩy bạn đi đường nào ngắn nhất để “xong”.
Tuy nhiên, sự vội vàng này sẽ mang hậu quả lâu dài. Bạn có thể tiết kiệm thêm 5 phút bây giờ nhưng mất vài tiếng hay thậm chí vài ngày để sửa một con bug (vì không nhớ mình duplicate ra bao nhiêu nơi), hay thậm chí có thể gây dự án thất bại.

### Lặp vì có nhiều thành viên và mỗi người code một phần trùng nhau
Làm việc chung nhiều dev dễ dẫn đến trùng lặp. Ví dụ như việc kiểm tra id truyền vào có phải là số hay không, mỗi người làm ở những nơi khác nhau lại thực hiện kiểm tra này khác nhau.
Để giảm thiểu tình trạng này, việc review code lẫn nhau trở nên quan trọng trong việc duy trì tính thống nhất của dự án. Các thiết kế chung, các buổi thảo luận sẽ giúp cập nhật, một nơi chung cho những utils dùng lại sẽ có ích.

Vì thế, hãy viết code dễ dàng tái sử dụng.
—
Lược dịch từ sách “Dragmatic Programmer”

## Orthogonality (trực giao)
Orthogonality (trực giao) là khái niệm từ hình học chỉ hai đường thẳng vuông góc. Tức là khi một giá trị chạy dọc theo đường này thì giá trị của đường kia không thay đổi.

Ví dụ như hai trục x, y là trực giao với nhau tại 0. Tức giá trị nào trên x cũng có y là 0 và ngược lại.

Trong máy tính, khái niệm này đại diện cho hai thành phần hay đối tượng độc lập nhau. Tức là nếu thay đổi thành phần này sẽ không làm thay đổi thành phần kia.
Orthogonality giúp xây dựng dự án dễ thiết kế, chạy, kiểm thử và mở rộng.
Ví dụ việc thay đổi interface như DBMS (database management system) sẽ không ảnh hưởng đến database.

Orthogonality trong thiết kế phần mềm còn là sự kết hợp của hai nguyên tắc: strong cohesion (gắn kết chặt chẽ) và loose coupling (khớp nối lỏng lẻo).
Strong cohesion ý chỉ bên trong mỗi thành phần nên được kết nối chặt chẽ. Nếu một thành phần mà có nhiều bộ phận rời rạc thì cũng nên được tách ra thành các thành phần riêng lẻ.
Loose coupling ý chỉ giữa các thành phần nên có ít khớp nối. Nếu hai thành phần có kết nối chặt chẽ thì chúng nên gộp lại làm một hoặc nên tách chia theo cách khác để có nhiều thành phần độc lập hơn.

**Lợi ích của thiết kế theo hướng trực giao:**

**Tăng hiệu suất**

– thay đổi diễn ra độc lập giữa các thành phần nên chỉ cần thay đổi và kiểm thử cụ thể trên thành phần đó, giảm thời gian lập trình.

– các thành phần độc lập nên dễ tái sử dụng

– kết hợp các thành phần độc lập cũng dễ dàng hơn

**Giảm rủi ro**

– giảm code liên quan giữa các thành phần

– nếu một thành phần bị lỗi thì sẽ không ảnh hưởng nhiều đến cả hệ thống, dễ debug

– dễ kiểm thử từng thành phần

– hạn chế bị phụ thuộc

**Áp dụng tính trực giao trong lập trình:**
– Giữ mã code tách rời nhau
– Tránh dữ liệu toàn cục
– Tránh các hàm tương tự nhau

Tập thói quen quan sát và cân nhắc code của bạn, tìm cách để cải thiện cấu trúc và tăng tính trực giao.

Đọc thêm về cặp đôi hủy diệt code xấu DRY và Orthogonality ở [bài viết sau][cap-doi-huy-diet-code-xau-dry-va-orthogonality]

## Bạn biết bao nhiêu Linux command?

Bạn biết bao nhiêu Linux command?

Các nhóm lệnh được phân loại theo:

**Các câu lệnh file cơ bản:**
ls – xem danh sách file
cp – copy file
mv – sửa tên hay di chuyển file
rm – xoá file
ln – tạo link cho file
shred – xoá nội dung file khi delete

**Các câu lệnh thư mục:**
cd – thay đổi thư mục hiện tại
pwd – in đường dẫn thư mục hiện tại
basename – in phần cuối của đường dẫn file
dirname – in đường dẫn trừ tên file
mkdir – tạo thư mực
rmdir – xoá thư mục trống
rm -r xoá thư mục có nội dung

**Xem file**
cat, less, head, tail, nl, strings, od, xxd, acroread, gv, xdvi
**Tạo file và sửa**
emacs, vim, soffice, abiword, gnumeric
**Các thuộc tính của file**
stat, wc, du, file, touch, chown, chgrp, chmod, unmask, chattr, isattr
**Vị trí file**
find, xargs, locate, which, type, whereis
**Các thao tác với nội dung file text**
grep, cut, paste, tr, sort, uniq, teete
**Nén file và đóng gói**
tar, gzip, gunzip, bzip2, bunzip2, bzcat, compresss, uncompresss, zcat, zip, unzip, metamail
**So sánh file**: diff, comm, cmp, md5sum
In file: lpr, lpq, lprm

**Lập kế hoạch công việc**
sleep (đợi và không làm gì)
watch(chạy chương trình sau một khoảng thời gian cụ thể)
at (chạy tại một thời điểm tương lai)
crontab (chạy tại nhiều thời điểm tương lai)

**Kiểm tra chính tả**: look, aspell, spell
**Video**: mplayer, gxine, kino, HandBrake
**Audio**: amarok, rhythmbox, xmms, audacity, lame, …
**Đồ hoạ**: eog, geequie, ksnapshot, dia, …
**Ngày tháng**: xclock, cal, date, ntpdate
**Tính toán**: xcalc, expr, dc
**Xuất ra màn hình**: echo, printf, seq, clear
**Gửi tin**: gaim, talk, write, mesg, tty
**Network**: traceroute, ifconfig, netstat, who, ping, …
**Sao lưu**: dump, restore, …
**Xem các quá trình**: ps, uptime, top, free
**Kiểm soát các process**: kill (kết thúc một quá trình), killall, nice (gọi với độ ưu tiên)

**Vị trí máy chủ**: host, whois, ping, traceroute
**Thông tin máy chủ**: uname, hostname, dnsdomainname, domainname, nisdomainname, ip, ifconfig
**Trình duyệt Web**: firefox, lynx, wget
**Email**: thunderbird, evolution, mutt, mail, mailq
**Kết nối mạng**: ssh, telnet, scp, sftp, ftp

**Quản lý nhóm**: groups, groupadd, groupdel, groupmod
**Quản lý người dùng**: useradd, userdel, usermod, passwd, chfn, chsh
**Môi trường của người dùng**: logname, whoami, id, who, users, finger, last, printenv
Login, logout, shutdown: shutdown

[Sơ đồ được chia sẻ từ ByteByteGo Newletters](https://blog.bytebytego.com/p/ep-40-git-workflow)

## Obsidian todo list

Bạn có đang loay hoay tìm cách quản lý công việc hàng ngày của mình sao cho hiệu quả?
Mình cũng vậy, vẫn loay hoay với chuyện làm sao có thể ba đầu sáu tay mà hoàn thành công việc.

Các công việc thường ngày của mình bao gồm ba nhóm chính:
– việc dự án: các cuộc họp, làm task, thảo luận, review code, quản lý ticket release, chat các kênh với team, jira, …
– việc hướng dẫn: theo dõi quá trình training của các bạn mentee, hỗ trợ, code review, email, các cuộc nói chuyện
– việc tự học: công việc training cá nhân, các khoá học, viết blog, …

Và mỗi ngày đều trôi qua thật nhanh, đều xoay như chong chóng, việc này vấp việc kia. Và tất nhiên là thường xuyên cảm thấy không đủ thì giờ.

Gần đây mình có thử sử dụng daily note tự thiết kế theo hướng dẫn từ bài viết sau đây, và thấy nó khá hiệu quả trong việc biết mỗi ngày mình cần làm gì.
Nó như là một chiếc bản đồ để mình không bị lạc, mình cũng ít bị quên hay ít phải tự nhủ “ủa”, “chết cha! quên rồi”, …

Mỗi ngày làm việc sẽ bắt đầu như sau:
Mở máy lên, việc đầu tiên là bấm vào icon cái lịch để tạo todo list cho ngày hôm nay
Một danh sách các nội dung được soạn sẵn:
1. “Hôm nay tâm trạng ấy ra sao?”
2. “Rồi, dù sao đi nữa thì hãy điền vào cái template sau để không bị lạc hôm nay nha.”Và kèm theo đó là link bài hát mình yêu thích để bắt đầu buổi sáng, hay các câu danh ngôn mà mình sưu tầm.
3. Sau khi đã điền xong và sắp thứ tự ưu tiên(15p) thì mình sẽ bắt tay vào làm và tick vào mỗi khi xong. (Cảm giác tick vào nó đã lắm :)) và cũng thấy mình cần làm gì tiếp theo luôn)
4. Nếu có công việc đột xuất thì mình sẽ lại viết thêm và sắp xếp thứ tự đặt bạn ấy vào đâu tuỳ vào mức độ ưu tiên
5. Cuối ngày mình sẽ viết ra các công việc ngày mai sẽ làm tiếp để hôm sau cọp qua cho nhanh.

Hướng dẫn còn chỉ cho bạn cách sử dụng plugin dataview, cái mà mình vô cùng ưng ý.
Ví dụ release này mình có 10 tasks, mình tạo note cho 10 bạn ấy, sẵn tiện hồi sẽ note tất cả các thông tin liên quan vào như phân tích, test case, … Và gán tag là #todo chẳng hạn, thì cái template của mình cũng tự động hiện được các dữ liệu này.
Cái nào cần làm, cái nào đang làm, đã làm cần review, đã merge cần test, … mình đều biết cả.

Cuối cùng là mình có được cái cảm giác an tâm, dù công việc chưa xong, nhưng ít nhất là mình biết mình đã và cần sẽ làm gì ^^

Bạn tham khảo xem nếu thích thì thử nghen, chúc bạn quản lý công việc ngày càng tốt hơn.

([Ref link setup obsidian daily job](https://heymichellemac.com/obsidian-daily-note-2022))

## Django model permission, object permission

Django là một web framework (open source) viết bằng Python giúp phát triển các ứng dụng web một cách nhanh chóng, code sạch và các thiết kế hữu dụng.
Django authentication system là một hệ thống xử lý cả việc xác thực (authentication) và phân quyền (authorization).
Hệ thống này bao gồm các thành phần chính như: Users, Permissions, Groups, hệ thống password hashing, các forms và công cụ cho phép người dùng truy cập và giới hạn nội dung, …

Django cung cấp cho bạn “Model Level Permisisions”

Khi bạn có app “django.contrib.auth” trong INSTALLED_APPS setting, thì sẽ có 4 quyền mặc định được thêm vào cho mỗi loại model, bao gồm: add, change, delete, view.
Và các loại phân quyền này được sử dụng trong Django Admin cho phép:
– người dùng có quyền “view”, “change” có thể xem các objects của loại model.
– người dùng có quyền “add” có thể thêm object của loại model.
– người dùng có quyền “delete” có thể xoá object của loại model.

Các quyền này cũng có thể được sử dụng trên app tương tự như trong Django Admin.
Một lưu ý ở đây là các loại permission này được áp dụng cho toàn bộ các objects trong model, hay toàn bộ hàng trong bảng.
Tức là nếu user có quyền delete trong model Product, thì user có quyền delete bất cứ sản phẩm nào trong bảng Product.

—
Vì thế, mặc định các quyền này chưa đủ chặt chẽ để giải quyết các bài toán dự án thực tế nơi mà cần phân quyền cho từng object cụ thể trong model – “Object Level permissions”
Ví dụ user chỉ có quyền xoá các sản phẩm mà user ấy tạo mà thôi. Hay một người dùng nhất định chỉ có thể truy cập vào một số các đối tượng nhất định mà thôi.
Khi đó, bạn sẽ cần giải quyết vấn đề “Object-level permissions” với một số thư viện bên thứ ba như “django-guardian”, “django-object-permission”

Bạn có thể lưu lại để nhớ đến giải pháp này khi dự án của mình cần nhé.

—
Một số video sau giới thiệu và thực hành hands-on giúp bạn nắm rõ về Django Permission và Django Guardian
1. [Django Permissions | Model Level Permissions | Admin Site ](https://www.youtube.com/watch?v=wlYaUvfXJD)
2. [Django Guardian | Object Level Permissions | Admin Site](https://www.youtube.com/watch?v=2jhQyWeEVHc)
3. [Django Guardian | Object Level | View and Templates](https://www.youtube.com/watch?v=KpuDBudtSrg)


[cap-doi-huy-diet-code-xau-dry-va-orthogonality]: {{ "" | relative_url }}{% post_url principles/2023-01-01-cap-doi-huy-diet-code-xau-dry-va-orthogonality %}