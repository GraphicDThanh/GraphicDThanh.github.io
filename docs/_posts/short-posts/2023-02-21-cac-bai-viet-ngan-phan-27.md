---
title: "Các bài viết ngắn - phần 27"
categories:
  - Short Posts
tags:
  - short-posts
  - career-development
  - news
  - javascript
  - django
---
![](/assets/images/2023/02/2023-02-21-cac-bai-viet-ngan-phan-27-1.webp)

## What we look for in resume?
Đầu năm mình muốn giới thiệu đến bạn một bài viết rất hay của chị Huyền Chip (tác giả cuốn sách Designing Machine Learning Systems - Amazon #1 bestseller in AI).

Ở góc nhìn nhà tuyển dụng, thì mong muốn điều gì ở ứng viên? Hay cách bạn nên xây dựng hồ sơ cá nhân (CV, linkedin profile, ...) như thế nào để gây ấn tượng.
Bởi nhà tuyển dụng luôn tìm kiếm điều gì đó trong hồ sơ của bạn để nói “Yes!”

Một vài điểm mình thấy khá thú vị khi đọc bài viết:
- Thường các bạn liệt kê các từ khoá một cách vô tội vạ. Tuy nhiên khoảng cách giữa biết một cái gì và làm tốt nó rất là xa.
Một số cách tốt hơn việc liệt kê từ khoá
- Mô tả các kỹ năng chính của bạn với ngữ cảnh hay câu chuyện giúp người tuyển dụng muốn biết thêm về những điều bạn làm trong buổi phỏng vấn.
- Hồ sơ stackoverflow, PRs vào open source, blog posts, … là các dẫn chứng thuyết phục việc bạn thực sự biết.

- Nhà tuyển dụng tìm kiếm những người có thể giải quyết công việc “get things done”, ngay cả khi công việc chưa có tên như khi bạn thấy một vấn đề và chủ động giải quyết.
- Nhà tuyển dụng tìm kiếm các góc nhìn khác biệt, các dự án sáng tạo thay vì các bài toán và cách giải quyết cũ kỹ.
- Nhà tuyển dụng quan tâm đến sự ảnh hưởng của bạn, không phải các con số vô nghĩa.

Mời bạn đọc thêm ở [bài viết sau](https://huyenchip.com/2023/01/24/what-we-look-for-in-a-candidate.html) trên blog của chị Huyền Chip nhé.

## Giới thiệu Astro
Astro là một frontend framework được thiết kế với tốc độ load trang nhanh với kiến trúc Astro Island.

Astro Island đại diện cho sự thay đổi kiến trúc xây dựng website ở phần giao diện. Bằng cách trích xuất trang web ra thành các phần nhỏ hơn, biệt lập hơn. JavaScript không sử dụng sẽ thay thế bằng HTML nhẹ hơn, đảm bảo việc load trang và tương tác nhanh hơn.

Ba điểm nổi trội:
- Zero JavaScript Runtime
- The Power of Islands
- Lazy-loading Islands

Astro được thiết kế dành cho các loại nội dung đa dạng như CMS, markdown, MDX, API. ...

Astro cho phép kết hợp với các loại thư viện JS phổ biến để xây dựng component như React, VueJS, Svelte, TailwindCSS, ...

Astro hỗ trợ việc deploy linh hoạt, cả static output (SSG) và server output (SSR)

Bạn ghé vào [trang chủ Astro](https://astro.build/) để tìm hiểu thêm nhé.

## Copy object với structuredClone()
Việc sao chép một object là một công việc thường gặp của front-end developer.

Bạn đang dùng cách nào để clone object?

Nếu chỉ cần một bản shallow copy, bạn có thể dùng *spread operator* (dấu ...).

Ví dụ:
```js
const user = {
  "name": "Thanh",
  "socialAccounts": ["facebook", "linkedin"]
}
const shallowCopyUser = {..., user}
```

Với *JSON.parse(JSON.stringify(obj))* thì Date sẽ chuyển qua string, hay Set sẽ chuyển qua `{}`, nên bạn sẽ cần một bước convert các loại data này.

Chưa hết, cách trên còn bỏ qua các loại giá trị như `undefined`, hay `function`, `File`, `Error`.

Với `_.cloneDeep(obj)` của `lodash` thì giải quyết vấn đề khá triệt để.
Tuy nhiên việc cài thêm một thư viện bên thứ ba có kích thước 17.4k khi chỉ `import lodash/cloneDeep`. Và kích thước 71.5k khi `import lodash` và chỉ sử dụng mỗi hàm này thì là lãng phí tài nguyên dự án.

Vì thế, nên ưu tiên sử dụng `structuredClone()` khi có thể.


Thế `structuredClone()` không thể clone những gì?
- Function
- DOM nodes
- các thuộc tính getter, setters
- prototype

Cuối cùng, khi sử dụng bất cứ gì bạn đều nên kiểm tra sự hỗ trợ của các loại trình duyệt để đảm bảo dự án chạy tốt mà không bị ảnh hưởng. Hiện tại structuredClone() hỗ trợ hầu hết các loại trình duyệt, và cả NodeJS hay Deno.

Đọc thêm ở [bài viết sau](https://www.builder.io/blog/structured-clone).

## Ra mắt Astro 2.0
Astro là một front-end framework được xây dựng phục vụ các trang web chú trọng về mặt nội dung. Với Astro giúp tăng 33% tốc độ tải trang và JavaScript giảm 90% đồng thời sử dụng cùng với các thư viện phổ biến như React, Vue, Svelte.

Astro 2.0 là framework đầu tiên cung cấp type-safe hoàn chỉnh cho markdown, MDX. Bản Astro 2.0 này thực sự thay đổi cuộc chơi cho bất cứ ai xài markdown trên web.

Các điểm nổi bật trong bản Astro 2.0 bao gồm:

Automate typesafety cho markdown và MDX

Astro 2.0 mô phỏng lại trải nghiệm của nhà phát triển nội dung với Content Collection API. Bằng cách sắp xếp các file markdown và MDX vào các bộ sưu tập khác nhau như blogs, newsletter, products và

Astro sẽ lo các phần còn lại:
* Schema validation
* SEO best practices
* Informative error messages
* Automatic generated types
* Inline type errors, autocomplete, ...

Hybrid Rendering cho phép bạn chọn cả static rendering (SSG) và dynamic rendering (SSR) thay vì chỉ chọn một trong hai như trước đây. Việc kết hợp này mở ra các khả năng mới bao gồm:
- Cải thiện hiệu suất render của các trang phổ biến
- Cải thiện hiệu suất xây dựng các trang web lớn
- Thêm API vào trang web tĩnh

Error Overlay là lớp hiển thị lỗi được cải tiến giúp cho lập trình viên dễ dàng debug chương trình kèm theo các kiến thức gợi ý và có thể dẫn bạn đến dòng mã đang bị lỗi trên editor

Hot Module Reload (HMR) được nâng cao hiệu suất và độ tin cậy

Phiên bản mới nhất Vite 4.0 được áp dụng

Astro 2.0 đã sẵn sàng trên npm, cài đặt với "npm i astro@latest"

Đọc thêm tại [bài viết sau](https://astro.build/blog/astro-2/).

## Tạo file pdf với reportlab trong ứng dụng Django

Thế vì sao lại cần tạo pdf từ backend?
Như ứng dụng của mình làm là vì 2 vấn đề sau:
1. ở mobile app không thể export file pdf
2. khi thực hiện thao tác in đồng loại, web app gặp gấn đề timeout nên không thể thực hiện in
Vì thế, việc in ấn trên mobile và thực hiện đồng loạt được chuyển đổi qua phía backend, idea là sẽ tạo pdf file rồi gửi mail cho người dùng link để tải về.

Và reportlab là một công cụ hỗ trợ làm công việc trên.

Reportlab là một thư viện hỗ trợ việc tạo tài liệu pdf với ngôn ngữ Python. Bạn có thể cài đặt reportlab từ pip.

Mình muốn giới thiệu đến bạn 2 thành phần cơ bản của reportlab:

**canvas**
canvas là công cụ thuộc mô-đun pdfgen, giúp bạn vẽ các thành phần trên trang ở các vị trí nhất định.
Thử tưởng tượng bạn cầm cây bút là canvas, di chuyển đến vị trí nhất định và bắt đầu vẽ, chính là cách canvas hoạt động.canvas có thể giúp bạn vẽ nhiều loại đa dạng như text, line, shape, image, table, form, ...

**platypus**
platypus là viết tắt của Page Layout and Typography using Scripts. Là thư viện khá đầy đủ giúp bạn xây dựng các tài liệu phức tạp.
platypus có 4 thành phần chính phân từ tổng quát đến chi tiết:
1. DocTemplates
2. PageTemplates
3. Frames
4. Flowables
5. pdfgen.canvas

Hình ảnh đính kèm mô tả các khái niệm PageTemplates, Frames, Flowables của platypus.
![](/assets/images/2023/02/2023-02-21-cac-bai-viet-ngan-phan-27-2.webp)

Còn DocTemplates là bao gồm nhiều PageTemplates.
Flowables chỉ các thành phần nội dung động sẽ được thêm vào trên trang theo flow của trang.

Để dễ hiểu bạn có thể hình dung mình cần tạo một file pdf với các trang chẵn và lẻ có các layout khác nhau.
Khi đó bạn sẽ có một DocTemplates chứa các PageTemplate là các template cần cho trang chẵn, lẻ.

Mỗi PageTemplate này chứa hai loại nội dung:
- các nội dung cố định trên layout, sẽ được xây bằng canvas.
- các nội dung động được tự động sắp xếp lên các Frames. Là các flowables.

Đây là cách mình có thể tạo file pdf từ code backend với Python.
Bạn có thể lưu lại tham khảo khi dự án cần dùng đến nhé.
Ghé vào [docs.reportlab.com](https://docs.reportlab.com/reportlab/userguide/ch1_intro/) để đọc thêm nhé.
