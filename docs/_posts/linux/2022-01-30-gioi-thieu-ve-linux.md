---
title: "Giới thiệu về Linux"
categories:
  - Linux
tags:
  - linux
---

Chào mừng bạn đến với series [“Làm quen Linux giành cho lập trình viên”](https://beautyoncode.com/lam-quen-linux-gianh-cho-lap-trinh-vien-series-overview/), đây là bài blog đầu tiên của series này nè. Hi vọng bạn ủng hộ nhé!

## Giới thiệu về thế giới mã nguồn mở
Một trong những câu hỏi quan trọng khi bạn tạo ra các sản phẩm về phần mềm là *“Phần mềm của bạn sẽ được phát hành với loại giấy phép nào?”*. 

Loại giấy phép bạn chọn sẽ quyết định các yếu tố như:

– cách người dùng sử dụng phần mềm của bạn sẽ như thế nào?

– mã nguồn của phần mềm có được xem hay không?

– những người lập trình viên khác có được sử dụng mã nguồn này không?

– người khác được quyền bán hay cải tiến và bán lại phần mềm phát triển dựa trên mã nguồn của bạn không?

Những câu hỏi trên thường được quy về một câu hỏi mà bạn chắc sẽ hay gặp: 

**“Phần mềm này là loại mã nguồn mở(open source) hay mã nguồn đóng(closed source)?”**

## Mã nguồn(source code) là gì?
Ví dụ bạn có một chương trình Python in ra một dòng là “Hello Linux” chẳng hạn, thì nó sẽ như thế này:

> print(“Hello Linux”)

nội dung trên được gọi là **source code**(mã nguồn). 

Source code này có thể được viết bằng nhiều loại ngôn ngữ khác nhau, như là HTML, CSS, SASS, JS, Python, C, C++, … 

Một số ngôn ngữ cần được biên dịch trước khi chương trình có thể chạy như C, C++, … gọi là **compiled languages**, cũng có ngôn ngữ không cần biên dịch như Python, Javascript, … gọi là **interpreted languages**

## Mã nguồn đóng(closed source)
**Closed source** hay còn gọi là “phần mềm độc quyền” với mục đích là bảo vệ mã nguồn của phần mềm này một cách chặt chẽ với lý do rõ ràng là nếu mã nguồn bị lộ thì rất nguy hiểm vì sẽ bị sao chép để cạnh tranh. 

Thường thì thuật ngữ closed source được sử dụng thay thế cho thuật ngữ commercial software(phần mềm thương mại), tức là bạn phải trả tiền để có thể sử dụng chúng. Nhưng điều này chưa đúng lắm, lý do là cả open source hay closed source đều có thể được thương mại hóa.

**Microsoft Windows, Adobe Photoshop, Apple MacOS** là các ví dụ cho loại này.

Nếu phần mềm của bạn là closed source(mã nguồn đóng) thì bạn sẽ chỉ cung cấp cho người dùng những đoạn mã sau khi đã biên dịch(nếu là compiled language), còn nếu là interpreted language thì bạn sẽ không cung cấp cho người dùng source code. 

## Mã nguồn mở(open source)
Một phần mềm được cân nhắc là **open souce** khi mà cả mã nguồn gốc và mã đã biên dịch đều được cung cấp sẵn. Tùy theo loại lisence mà phần mềm này có thể được xem, sửa đổi hay có quyền phân phối. 

**Linux, Apache HTTP Server, Firefox, Git** là các ví dụ cho loại này.

Open source có thể hiểu là khả năng truy cập vào mã nguồn, chứ không phải cách phần mềm có thể được sử dụng hoặc các chi phí liên quan đến phần mềm.

Nếu phần mềm của bạn là open source(mã nguồn mở) thì nó sẽ bao gồm tất cả source code của bạn, tức là gồm mã nguồn gốc và mã sau khi biên dịch(nếu có).

## Phần mềm "miễn phí" ("free" source)
**Free source** thường được hiểu là sự tự do copy hay sự có thể thay đổi của chương trình, chứ không liên quan đến giá cả. **FSF**(Free Software Foundation) đã đưa ra định nghĩa cho chữ “**free**” dành cho phần mềm bởi Richard Stallman:

*“Từ “free” ở đây không liên quan đến giá, nó được hiểu là sự tự do. 

**Một**, tự do sao chép chương trinh và tái phân phối đến người khác, và họ cũng có thể dùng sản phẩm như bạn. 

**Hai**, tự do thay đổi chương trình, và bạn có quyền kiểm soát thay vì nó kiểm soát bạn, điều này cũng đồng nghĩa là họ có được mã nguồn.” 
*
**Có 4 bậc của sự tự do hay gọi là FOSS, cụ thể là:**

– **Freedom 0**: Tự do chạy chương trình bạn muốn, cho bất cứ mục đích nào.

– **Freedom 1**: Tự do học cách chương trinh hoạt động và thay đổi nó để tính toán như bạn muốn. Để làm được điều này tất nhiên bạn cần có quyền truy cập vào source code trước.

– **Freedom 2**: Tự do tái phân phối những bản sao.

– **Freedom 3**: Tự do phân phối các bản sao của chương trình bạn đã chỉnh sửa cho người khác. Để làm được điều này tất nhiên bạn cần có quyền truy cập vào source code trước.

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/01/visualize-the-open-source-community.png?resize=768%2C275&ssl=1)

Sơ đồ bên trên mô tả quyền tự do sửa đổi, phân phối và sử dụng của phần mềm open source. 

Ngoài ra, việc chọn lựa các loại giấy phép cho phần mềm cũng liên quan đến các quyền tự do này. Bạn có thể tham khảo thêm ở choosealicense.com hay opensource.org nhé.

### Các lợi ích của open source
– Open source có xu hướng kêu gọi sự tin tưởng vì source code sẽ được cả cộng đồng xem.

– Open source có thể tạo ra source code tốt hơn và giảm thời gian phát triển phần mềm, nhờ các lập trình viên khác review code, cho feedback, sửa lỗi hay cải thiện sửa đổi nhanh hơn.

– Open source miễn phí có thể tiếp cận nhiều người dùng hơn, đồng nghĩa với có nhiều người thử nghiệm sản phẩm hơn.

– Bạn vẫn có thể kiếm tiền từ các open source như các dịch vụ đi kèm về đào tạo, hỗ trợ, …

## Giới thiệu về Linux
Nếu bạn tính phát triển phần mềm trên các hệ điều hành có nền tảng từ **Linux(Linux-based operating system(OS))** thì việc tìm hiểu làm thế nào có thể tương tác để quản lý OS là việc quan trọng. 

(vì trước sau gì bạn cũng sẽ ăn hành với chúng, như không biết mình đang đứng ở thư mục nào, hay thay đổi quyền của một cái file, …)

### Linux là gì
Về mặt kỹ thuật, thì Linux là một phần mềm gọi là **nhân(kernel)**. Cái kernel ni hắn làm mấy các việc như là **khởi động hệ thống** hay **tương tác với các thiết bị phần cứng**.

Còn bản thân cái kernel ni thì là không có làm việc liền với user được, mà là toàn bộ những thứ khác, thường gọi là OS bao gồm các file hệ thống và số lượng lớn các câu lệnh, mới là thứ cung cấp cho người dùng những tính năng hữu ích.

Dù cho Linux về mặt kỹ thuật chỉ là nhân, nhưng nhiều người lại hay gọi cả OS là Linux luôn. 

Thực tế thì, tập hợp các phần mềm tạo nên hệ điều hành có tên là **Linux distribution(distro)**.

### Cài đặt và sử dụng Linux
Ở phần này, mình sẽ không giới thiệu chi tiết cách cài đặt distro hay gì, mình sẽ gợi ý một số cách bạn có thể bắt đầu truy cập và sử dụng Linux trên máy tính:

– **MacOS**: Hệ điều hành MacOS có nhân là UNIX-based(cụ thể là NeXTSTEP operating system). Linux cũng có nhân là UNIX-based(cụ thể là GNU) do đó nếu bạn dùng máy Mac thì rất đơn giản, gõ vào thanh tìm kiếm “Terminal” và mở phần mềm này lên. (xem thêm ở [hình minh họa](https://upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Unix_timeline.en.svg/800px-Unix_timeline.en.svg.png))

– **Windows**: Với máy windows, trước đây thì cần cài máy ảo(virtual machine – VM) với Virtualbox để có thể sử dụng hệ điều hành khác trên máy ảo. Tuy nhiên, cách này đã cũ rồi, hiện nay nếu bạn dùng windows thì có thể cài và sử dụng [“Windows Subsystem for Linux(WSL)“](https://docs.microsoft.com/en-us/windows/wsl/)

– **Linux distro**(Ubuntu, RedHat, …): thì mở “*Terminal*” lên thôi bạn.

Mình dùng máy MacOS nên những ví dụ minh họa(nếu có) trong series này sẽ là từ máy MacOS nha mọi người.

---
Bài blog hôm nay là bài mở đầu cho [series về Linux](https://beautyoncode.com/lam-quen-linux-gianh-cho-lap-trinh-vien-series-overview/), tụi mình đã làm quen với thế giới mã nguồn mở, Linux cũng như vài gợi ý để có thể bắt đầu sử dụng Linux rồi.

Trong bài viết tiếp theo, mình và các bạn sẽ đi tìm hiểu thêm về hệ thống tập tin(filesystem) trong Linux.

Nếu bạn thấy nội dung bài blog này hữu ích hãy upvote cho bài viết cũng như series để nội dung có thể đến với các bạn khác nhé.

Hẹn gặp các bạn trong bài viết tiếp theo.
