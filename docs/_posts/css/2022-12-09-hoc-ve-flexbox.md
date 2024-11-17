---
title: "Học về Flexbox"
categories:
  - CSS
tags:
  - frontend
  - css
---

![](/assets/images/2022/12/2022-12-hoc-ve-flexbox.webp)
Flexbox ra đời giúp cho việc thiết kế layout trên trang web trở nên dễ dàng và ngắn gọn hơn rất nhiều so với thời dùng float.

Vậy flexbox và gì và thuật toán bên dưới hoạt động như thế nào?


## Về Flexbox

CSS có nhiều loại layout khác nhau, được gọi là **“layout mode”**.

Layout mặc định là “flow layout”, có thể hiểu các phần tử sẽ xếp theo thứ tự lần lượt nhau.
docs/_posts/css/2022-12-09-hoc-ve-flexbox.md
Để chuyển layout mặc định qua flex, bạn sẽ dùng **“display: flex;”** gán vào phần tử cha. 

Khi đó, CSS hiểu phần tử cha này sẽ có “flex formatting context”, và sẽ áp dụng thuật toán của flex cho các phần tử con bên trong nó.

Mỗi thuật toán của layout được thiết kế giúp giải quyết một vấn đề cụ thể.

Như “flow layout” có nghĩa là tạo tài liệu online, nó thuật toán layout cơ bản của Microsoft Word. Tiêu đề và các đoạn văn như các khối được xếp theo chiều dọc, còn chữ, các link và hình ảnh sẽ nằm bên trong các khối .

*Vậy còn flexbox sẽ giúp giải quyết vấn đề gì?*

Flexbox giải quyết vấn đề sắp xếp một nhóm các thành phần theo hàng (row) hay cột (column).

Đúng như tên của nó, flexbox rất linh hoạt flexibility. Nó cho phép kiểm soát và phân phối các thành phần và khoảng cách giữa chúng.

## Các trục (axis)

Có 2 loại trục: **“primary axis”** và **“cross axis”**.

Tạm dịch là trục chính và trục chéo (vuông góc với trục chính).

Mọi thứ trong flexbox sẽ dựa trên một trục chính, đó là lý do bạn có thể chuyển layout theo chiều ngang hay dọc một các dễ dàng.

Chỉ có một trục chính và có nhiều trục chéo vuông góc với trục chính cho từng thành phần.

Các thành phần con sẽ được bố trí dựa trên hai nguyên tắc của hai loại trục này:

– **trục chính**: các thành phần sẽ bắt đầu xếp theo hướng của trục chính

– **trục chéo**: các thành phần sẽ kéo giãn theo trục chéo để lấp đầy khung chứa bên ngoài


## Xác định hướng trục chính với flex direction

**“flex-direction”** giúp xác định hướng của trục chính

“flex-direction” có thể nhận giá trị:

– **“row”**: trục ngang, hướng từ trái sang phải

– **“column”**: trục dọc, hướng từ trên xuống dưới

## Căn chỉnh (alignment)

**“justify-content”** và **“align-items”** được sử dụng cho phần tử cha (container), giúp căn chỉnh toàn bộ nội dung bên trong (nhóm tất cả phần tử con)

**“align-self”** được sử dụng cho phần tử con, giúp căng chỉnh riêng phần tử đó.

### justify-content

“justify-content” giúp phân phối các thành phần trên trục chính.

Các giá trị: flex-start, flex-end, center, space-between, space-around, space-evenly


### align-items

“align-items” giúp phân phối các thành phần trên trục chéo.

Các giá trị: stretch, flex-start, center, flex-end,  baseline

### align-self

“align-self” được sử dụng cho phần tử con, cho phép thay đổi phần tử con trên trục chéo.

“align-self” có các giá trị thuộc tính tương tự “align-items” và cũng hoạt động tương tự, chỉ khác là nó chỉ áp dụng cho một phần tử.

---

Vì sao có “align-items”, “align-self” nhưng lại không có “justfy-content” và “justify-self”?

Vậy sao không có “justify-self”?

### Content với items

Như đã nói ở trên, chỉ có duy nhất một trục chính nối các thành phần với nhau, như một xiên thịt vậy.

Và có nhiều trục chéo, bạn có thể tưởng tượng một dĩa trái cây đã cắt sẵn với nhiều cây tăm được cắm lên trên là các trục chéo.

Qua đó, có thể thấy các trục chéo này giúp các thành phần tách biệt với nhau, do đó có thể align từng thành phần.

Còn trục chính thì các thành phần nối vào nhau nên nếu kéo một thành phần trên trục chính các thành phần khác sẽ ảnh hưởng, do đó sẽ không có “justify-self”

Có 4 thuật ngữ:

– justify: đặt vị trí theo trục chính

– align: đặt vị trí theo trục chéo

– content: một nhóm các thành phần được xếp

– items: các thành phần được xếp độc lập



Tóm lại, “justify-content” là phân phối nhóm các thành phần theo trục chính và không có “justify-self”

## Kích thước giả thuyết (hypothetical size)

Một thành phần dù được gán width vô cùng lớn, thì khi nó nằm trong flexbox, kích thước của nó sẽ được điều chỉnh phù hợp với kích thước của cha nó chứ không giữ độ rộng cố định được gán.

## Giãn và co (grow and shrink)
### flex-grow

Mặc định, nếu phần tử không đủ độ rộng / dài của phần tử cha thì sẽ có một khoảng trống còn lại.

**“flex-grow: 1”** giúp một phần tử có thể chiếm luôn khoảng trống còn lại này. 0 là giá trị mặc định.

Nếu có nhiều phần tử gán giá trị flex-grow, thì khoảng trống còn lại sẽ được chia cho các thành phần này dựa trên giá trị được gán.


### flex-shrink

Phần tử có kích thước quá rộng so với khung chứa, các phần tử sẽ bị co lại theo tỉ lệ tương ứng. Nếu bạn không muốn điều này xảy ra, flex-shrink có thể giúp điều chỉnh tỉ lệ co của từng phần tử.

---

Có thể thấy **“flex-grow”** và **“flex-shrink”** khá trái ngược nhau.

– “flex-grow” là thành phần cộng thêm khoảng không gian thừa còn lại của khung chứa.

– “flex-shink” là thành phần bị trừ đi khoảng không gian bị thiếu của khung chứa.

Điều này cũng đồng nghĩ với nếu có không gian thừa thì “flex-shink” vô tác dụng và nếu thiếu không gian thì “flex-grow” vô tác dụng.

### Làm sao nếu không muốn phần tử bị co lại?

Khi bạn không muốn phần tử bị co lại, hãy gán “flex-shink:0”, mặc định nó có giá trị là 1.

Sử dụng min-width cũng có thể giải quyết vấn đề này

## Kích thước tối thiểu (min width)

Đôi khi, khi kích thước của khung chứa giảm và nội dung bên trong bị tràn dù mặc định flex-shrink là 1.
Vì sao nội dung không co lại như mình nghĩ?

*Vấn đề là ở đây:*

Bên cạnh kích thước giả thuyết (hypothetical size), có một kích thước khác mà thuật toán flexbox quan tâm đó là kích thước tối thiểu (minimum size)

Thuật toán flexbox từ chối co phần tử lại khi phần tử ở kích thước tối thiểu của nó, khi đó, nội dung sẽ bị tràn cho dù bạn có gán flex-shink lớn bao nhiêu đi nữa.

**Vậy kích thước tối thiểu được tính như thế nào?**

Với phần tử là input, chính là kích thước mặc định mà trình duyệt gán cho nó, nếu với chữ, thì là độ dài lớn nhất của một từ.

 
Và để giải quyết vấn đề này, bạn có thể tái định nghĩa min-width cho phần tử đó.

## Các khoảng cách (gap)

Gap cho phép gán khoảng cách giữa các phần tử dọc theo trục chính.

## Auto margin

Trong flexbox, margin tương tự như flex-grow ở chỗ nó lấy không gian thừa còn lại của khung chứa, nhưng flex-grow lấy không gian cho vào nội dung còn margin sẽ lấy không gian cho vào margin (khoảng cách giữa nó và các phần tử khác).

Điều này sẽ hữu dụng khi bạn muốn giữ nguyên phần nội dung phần tử nhưng thay đổi không gian xung quanh nó.

margin left và right auto sẽ giúp phần tử đi ra chính giữa phần không gian còn lại.

Một ví dụ hay gặp là header của trang với logo bên trái và phần navigation bên phải, bạn có thể sử dụng margin-right: auto cho logo là xong.

## flex-wrap

Cuối cùng, nãy giờ là nói chuyện layout trên một hàng hay một cột. 

Nếu bạn muốn các phần tử có thể nhảy xuống hàng số hai khi kích thước khung chứa nhỏ lại, có thể dùng

**“flex-wrap: wrap”**

Khi đó, phần tử sẽ không bị co lại khi kích thước giảm hơn so với kích thước giả thuyết của nó.

Điều này có nghĩa là với flexbox và flex-wrap bạn hoàn toàn có thể làm một layout hai chiều tương tự như grid.

*Cơ mà nếu thế thì câu chuyện chỉ có một trục chính sẽ được hiểu sao đây?*

Với flex-wrap: wrap, mỗi hàng / cột sẽ được hiểu là một môi trường flex riêng, một khung chứa riêng, tức là sẽ có nhiều khung chứa và mỗi khung chứa này sẽ có một trục chính của nó.

Và các khung chứa này nằm trong một khung chứa lớn hơn bên ngoài (phần tử cha nơi gán flex-wrap:wrap)

Tóm lại với flex-wrap sẽ có:

– nhiều hàng / cột

– với mỗi hàng / cột, flex-items sẽ giúp bố trí  phần tử trên hàng / cột đó

– các hàng / cột này vẫn nằm trong khung chứa cha, và được nhóm lại với nhau

– và để bố trí tất cả nội dung của các hàng này so với khung chứa cha, sẽ cần sử dụng “align-content”

---

Vậy là bạn đã cùng mình học xong về flexbox rồi.

Chắc bạn cũng thấy lạ là vì sao nói về flexbox mà lại không có một mẩu minh hoạ hình ảnh nào ^^

Thực ra đó là mình muốn bạn ghé đọc bài viết tiếng anh và thực hành các demo của tác giả.

Một bài viết siêu hay về Flexbox kèm các ví dụ trực quan trên các loại màn hình, bạn vào link để đọc bản tiếng Anh và thử nghiệm trên máy tính để có trải nghiệm tốt nhất nhé.

Ref: [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/)
