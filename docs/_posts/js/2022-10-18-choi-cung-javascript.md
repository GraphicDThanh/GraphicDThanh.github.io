---
title: "Chơi cùng JavaScript"
excerpt_separator: <!--more-->
categories:
  - js
tags:
  - js, debug
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

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/10/node-run-js.png?w=1280&ssl=1)

Cách này sẽ tiện hơn nếu muốn chạy một chương trình JS nhỏ không liên quan đến DOM. 

Một tip được bạn [hung.dev](https://hung.dev/) chia sẻ là có thể sử dụng gói `nodemon` để tự động load lại khi mình có chỉnh sửa trên file. Cám ơn nha bạn Hưng ^^

Chạy câu lệnh: `npx nodemon example.js` để vừa cài gói `nodemon` vừa thực thi code.

Bạn sẽ thấy dòng `“Hello nodemon”` bên dưới là code thực thi sau khi code trong file `example.js` của mình thay đối.

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/10/nodemon-auto-reload.png?w=713&ssl=1)

## Cách 3: Sử dụng tab "Console" trên trình duyệt Chrome
Sử dụng browser `Chrome`, mở `Console` tab và thử nghiệm trực tiếp trên đó. 

Cách này sẽ rất tiện khi mình muốn kiểm tra nhanh hay demo nhanh các đoạn code hay cú pháp của JS, vì trình duyệt có tích hợp sẵn để dùng. 

Đặc biệt bạn có thể chơi với [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) như DOM, … 

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/10/console-chrome.png?w=1008&ssl=1)

## Cách 4: Sử dụng snippets
Nhờ một comment trên Viblo post, nhắc mình mới nhớ đến bạn này. 

Snippets dành cho JavaScript trên Chrome là một công cụ mạnh mẽ giúp bạn lưu một đoạn code JS và chạy trên bất cứ trang nào mà không bị mất code khi reload như khi mình viết ở Console.

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/10/snippets-js.png)

Bạn có thể tạo một snippets bằng cách vào Sources > Snippets và chọn “+ New snippet”. Để chạy chương trình, bấm Cmd + Enter hoặc nút Run như trên hình.

Đọc thêm document Snippets ở [đây](https://developer.chrome.com/docs/devtools/javascript/snippets/).

## Cách 5: Sử dụng editor trên trang w3schools.com
Tương tự cách 1 tuy nhiên có thể thực hiện trên [w3schools.com](https://www.w3schools.com/) vì trên đây có một editor có sẵn để thử nghiệm. 

Dù công cụ này không được hiện đại lắm nhưng việc ôn nhanh kiến thức cơ bản và thử nghiệm ngay tức thì trên trang này cũng rất hữu ích.

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/10/w3schools-editor.png?w=1198&ssl=1)

## Cách 6: Sử dụng javascript.makeup
[javascript.markup](https://javascript.makeup/) cũng là một cách để có thể chơi với JS và kết quả cũng khá dễ nhìn.

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/10/js-markup-1.png?w=748&ssl=1)

## Cách 7: Các công cụ online giúp viết và chia sẻ chương trình
Một số công cụ online như: JSBin, JSFiddle, Repl.it 

Các công cụ này thường yêu cầu tài khoản để lưu và chia sẻ chương trình.

### JSBin
https://jsbin.com/ 

![](https://i2.wp.com/beautyoncode.com/wp-content/uploads/2022/10/jsbin.png?w=1280&ssl=1)

### JSField
https://jsfiddle.net/

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/10/jsfield.png?w=1280&ssl=1)

### Replit
https://replit.com/

![](https://i1.wp.com/beautyoncode.com/wp-content/uploads/2022/10/replit.png?w=1280&ssl=1)


### Playcode.io
https://playcode.io/

![](https://i0.wp.com/beautyoncode.com/wp-content/uploads/2022/10/play.io_.png?w=1280&ssl=1)

---

Trên đây là một số cách mình biết và hay sử dụng.

Còn bạn thì sao, bạn hay thử nghiệm JS như thế nào? 