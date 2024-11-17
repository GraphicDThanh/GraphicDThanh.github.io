---
title: "9 lỗi người mới học React thường gặp"
categories:
  - Frontend
tags:
  - frontend
  - react
---

![](/assets/images/2023/03/2023-03-9-loi-nguoi-moi-hoc-react-thuong-gap.webp)

Dưới đây là tóm tắt của mình cho bài viết “[Common Beginner Mistakes with React](https://www.joshwcomeau.com/react/common-beginner-mistakes/)” của tác giả Josh W. Comeau. Bạn ghé blog gốc của tác giả đọc bản tiếng anh nhé.

## Lỗi 1: Phép so sánh với 0
Giả sử bạn có một danh sách items và sẽ render nếu có ít nhất một phần tử.

`const [items, setItems] = React.useState([]);`

Bạn có viết như thế này với mong đợi là chỉ hiển thị khi danh sách có phần tử:

```jsx
<div>
  {items.length && <ShoppingList items=items>}
</div>
```

Tuy nhiên, khi items không có phần tử nào lại xuất hiện một số 0. Vì sao thể nhỉ?

Khi items.length có giá trị 0 là một giá trị falsy trong JS, kết hợp && cho ra kết quả là 0.

Trong JSX, 0 là một giá trị valid, nên nó được build ra UI.

**Cách sửa 1: sử dụng so sánh trả về giá trị boolean là true/false**

```jsx
<div>
  {items.length > 0 && <ShoppingList items=items>}
</div>
```

**Cách sửa 2: trả về null nếu không có phần tử**

```jsx
<div>
  {items.length ? <ShoppingList items=items> : null}
</div>
```

## Lỗi 2: Thay đổi giá trị của state

Giả sử cần thêm một phần tử, trong hàm xử lý khi thêm phần, có thể bạn từng làm:

```js
function handleAddItem(value) {
  items.push(value);
  setItems(items);
}
```

**Kết quả**: thêm một phần tử thì không có phần tử nào được build ra UI.

**Vấn đề**: đoạn code này vi phạm nguyên tắc cốt lõi của React, giá trị của state không được thay đổi.

**Cách sửa: cần tạo một mảng mới cho danh sách thay đổi rồi mới gán giá trị state**

```js
const nextItems = [...items, value]
setItems(nextItems)
```

## Lỗi 3: Không tạo key khi render phần tử trong danh sách
Khi bạn render danh sách các phần tử:

```jsx
{items.map(item => {
  return (
    <li>{item}</li>
   )
}
```
sẽ có lỗi là *“Warning: Each child in a list should have a unique “key” prop.”*

Bạn sẽ cần cung cấp ngữ cảnh để React phân biệt các phần tử, bằng cách cung cấp các **key** có giá trị duy nhất.

## Lỗi 4: Thiếu khoảng trắng

Ví dụ:

```jsx
<p>
  Welcome to blog!
  <a href=“/login”> Log in to continue </a>
</p>
```

Kết quả: `Welcome to blog!Log in to continue`

Cách sửa: thêm khoảng trắng `{‘ ‘}` vào giữa hai dòng.

## Lỗi 5: Truy cập vào giá trị state sau khi thay đổi

Giả sử thực hiện in ra state items sau khi đã thay đổi state từ items ban đầu là [] như sau:

```js
setItems([…items, value]);
console.log(items);
```

thì kết quả hiển thị trên màn hình là một phần tử được thêm vào.

Nhưng ở console thì kết quả vẫn là `[]`

**Lý do**: hàm setItems() là một asynchronous, tức nó không ngay lập tức thay đổi giá trị mà chỉ đang lên lịch sẽ update state này mà thôi. Do đó việc thay đổi này cần một thời gian nhất định để hoàn thành.

**Cách sửa: sử dụng một biến trung gian để truy cập**

```js
const nextItems = [...items, value]
setItems(nextItems)
console.log(nextItems)
```

## Lỗi 6: Trả về nhiều thành phần trong component
Đôi khi, bạn sẽ cần trả về nhiều thành phần, ví dụ như một thẻ label và một input. 

Nếu bạn viết kiểu như thế này:

```js
return (
  <label></label>
  <input />
)
```

thì sẽ báo lỗi “Adjacent JSX elements must be wrapped in an enclosing tag.” 

**Lý do**: JSX elements cần được bọc bởi cặp thẻ đóng mở.

**Sửa lỗi**: sử dụng `<React.Fragment></React.Fragment>`, hay viết tắt là `<></>`

## Lỗi 7: Chuyển component từ uncontrolled sang controlled
Giả sử có input là email, khi thay đổi giá trị sẽ set lại state cho biến email

```js
const [email, setEmail] = React.useState();

// …
<input
  id=“email-input”
  type=“email”
  value={email}
  onChange={e => setEmail(e.target.value)}
/>
```

Khi bạn nhập giá trị vào input sẽ gặp lỗi “Warning: A component is changing an uncontrolled input to be controlled”

Lý do là biến state email không có giá trị ban đầu nên nhận giá trị là undefined. Và khi gán value={email} mình đã bảo với React đây là một uncontrolled component.

Tuy nhiên, khi thay đổi state thì lại muốn nó hoạt động như một controlled component nên sẽ gây lỗi.

**Cách sửa: đảm bảo email có giá trị ban đầu không phải là undefined**
`const [email, setEmail] = React.useState('');`

## Lỗi 8: Thiếu dấu {} cho code style

Trong CSS, thuộc tính style dùng kiểu 
```html
<button style=“color: red; font-size: 1em”></button>
```
Nhưng trong JSX, thuộc tính style cần được bọc bởi dấu {}, và các giá trị viết theo cú pháp của object.
```{ color: 'red', fontSize: '1em' }```

Và vì nó là một giá trị của thuộc tính style, nên cần thêm 1 cặp {} để thể hiện điều đó.

```jsx
<button style={{ color: 'red', fontSize: '1em' }}></button>
```

Nếu muốn rõ ràng hơn, bạn có thể tạo một biến riêng cho style rồi dùng:

```jsx
const btnStyle = { color: “red”, fontSize: ‘1em’ };
<button style={btnStyle}></button>
```

## Lỗi 9: Async effect function

Giả sử bạn cần gọi một API trả về danh sách các items, bạn sử dụng useEffect hook và await như sau:

```js
React.useEffect(() => {
  const res = await fetch(“/api/v1/items”);
  const json = await res.json();

  setItems(json);
});
```

Đoạn code trên sẽ gây lỗi vì await chỉ được dùng với async function. Cho dù bạn thêm async vào như thế này thì sẽ vẫn bị lỗi:

```js
React.useEffect(async () => {
  const res = await fetch(“/api/v1/items”);
  const json = await res.json();

  setItems(json);
});
```

**Cách sửa: viết một hàm async riêng dành để invoke**
```js
React.useEffect(() => {
  // create async function
  async function runEffect() {
    const res = await fetch(“/api/v1/items”);
    const json = await res.json();

    setItems(json);
  }
  // invoke it
  runEffect();
});
```
**Lý do**: async function trả về một promise, mà useEffect hook lại không xử lý được với promise trả về, nên cần chuyển hàm async riêng và gọi để hàm trong useEffect được clean.

---

Bài viết tóm tắt từ [blog này](https://www.joshwcomeau.com/react/common-beginner-mistakes/) , bạn ghé đọc ủng hộ tác giả nha