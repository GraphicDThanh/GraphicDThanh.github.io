---
title: "Chơi cùng JavaScript"
excerpt_separator: <!--more-->
categories:
  - js
tags:
  - js
  - debug
---

Khi học JavaScript bạn thử nghiệm các đoạn code nhỏ bằng các cách nào ?

Thử xem bạn đã dùng cách nào trong các cách sau nhé! 

## Cách 1: Chạy chương trình với browser
Tạo file `index.html` để chứa code của trang web. 

Bạn có thể mở trực tiếp file hoặc `“Go Live”` với extension [“Live Server”](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) trên VSCode. 

### Cách 1.1: Viết nội dung JS trong thẻ `<script></script>`
File `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Central Music</title>
  </head>
  <script>
    console.log('Hello');
  </script>
  <body>
  </body>
</html>
```

### Cách 1.2: Viết nội dung JS file `main.js`
Viết một file `main.js` rồi sử dụng làm source, và dùng thuộc tính `src` của thẻ script truyền đường dẫn đến file `main.js` để sử dụng

```html
<script src="./main.js"></script>
```

Cách này thì khá cồng kềnh khi muốn thử nghiệm nhanh một đoạn logic nhỏ.  Tuy nhiên sẽ cần thiết nếu bạn thực hành liên quan đến `DOM`, styles.

Cách này không chia sẻ code online được.

## Cách 2: Chạy chương trình với nodejs
Cài nodejs trên máy (thường sẽ có sẵn vì dev thường sử dụng npm)

Chạy lệnh `node <filename>.js` ở command line để thực thi

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-1.webp)

Cách này sẽ tiện hơn nếu muốn chạy một chương trình JS nhỏ không liên quan đến DOM. 

Một tip được bạn [hung.dev](https://hung.dev/) chia sẻ là có thể sử dụng gói `nodemon` để tự động load lại khi mình có chỉnh sửa trên file. Cám ơn nha bạn Hưng ^^

Chạy câu lệnh: `npx nodemon example.js` để vừa cài gói `nodemon` vừa thực thi code.

Bạn sẽ thấy dòng `“Hello nodemon”` bên dưới là code thực thi sau khi code trong file `example.js` của mình thay đối.

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-2.webp)

## Cách 3: Sử dụng tab "Console" trên trình duyệt Chrome
Sử dụng browser `Chrome`, mở `Console` tab và thử nghiệm trực tiếp trên đó. 

Cách này sẽ rất tiện khi mình muốn kiểm tra nhanh hay demo nhanh các đoạn code hay cú pháp của JS, vì trình duyệt có tích hợp sẵn để dùng. 

Đặc biệt bạn có thể chơi với [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) như DOM, … 

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-3.webp)

## Cách 4: Sử dụng snippets
Nhờ một comment trên Viblo post, nhắc mình mới nhớ đến bạn này. 

Snippets dành cho JavaScript trên Chrome là một công cụ mạnh mẽ giúp bạn lưu một đoạn code JS và chạy trên bất cứ trang nào mà không bị mất code khi reload như khi mình viết ở Console.

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-4.webp)

Bạn có thể tạo một snippets bằng cách vào Sources > Snippets và chọn “+ New snippet”. Để chạy chương trình, bấm Cmd + Enter hoặc nút Run như trên hình.

Đọc thêm document Snippets ở [đây](https://developer.chrome.com/docs/devtools/javascript/snippets/).

## Cách 5: Sử dụng editor trên trang w3schools.com
Tương tự cách 1 tuy nhiên có thể thực hiện trên [w3schools.com](https://www.w3schools.com/) vì trên đây có một editor có sẵn để thử nghiệm. 

Dù công cụ này không được hiện đại lắm nhưng việc ôn nhanh kiến thức cơ bản và thử nghiệm ngay tức thì trên trang này cũng rất hữu ích.

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-5.webp)

## Cách 6: Sử dụng javascript.makeup
[javascript.markup](https://javascript.makeup/) cũng là một cách để có thể chơi với JS và kết quả cũng khá dễ nhìn.

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-6.webp)

## Cách 7: Các công cụ online giúp viết và chia sẻ chương trình
Một số công cụ online như: JSBin, JSFiddle, Repl.it 

Các công cụ này thường yêu cầu tài khoản để lưu và chia sẻ chương trình.

### JSBin
https://jsbin.com/ 

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-7.webp)

### JSField
https://jsfiddle.net/

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-8.webp)

### Replit
https://replit.com/

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-9.webp)


### Playcode.io
https://playcode.io/

![](/assets/images/2022/10/2022-10-18-choi-cung-javascript-10.webp)

---

Trên đây là một số cách mình biết và hay sử dụng.

Còn bạn thì sao, bạn hay thử nghiệm JS như thế nào? 