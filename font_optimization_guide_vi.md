Best practices for fonts

# Best practices for fonts

## Bài viết này được chia thành ba phần: font loading, font delivery và font rendering
Mỗi phần giải thích cách một khía cạnh nhất định của vòng đời font hoạt động và cung cấp các phương pháp hay nhất tương ứng.

## Font loading
Font thường là nguồn tài nguyên quan trọng, vì nếu không có chúng, người dùng có thể không thể xem nội dung trang.
Do đó, các phương pháp hay nhất cho việc tải font thường tập trung vào việc đảm bảo rằng font được tải càng sớm càng tốt.
Cần phải chú ý đặc biệt đến font được tải từ các trang web bên thứ ba vì việc tải xuống các tệp font này đòi hỏi thiết lập kết nối riêng biệt.

Nếu bạn không chắc liệu font của trang bạn có được yêu cầu kịp thời hay không, kiểm tra tab Timing trong bảng Network của Chrome DevTools để biết thêm thông tin.

![image](https://github.com/mid-guy/web.dev/assets/99194082/9037da74-282a-4428-b6ed-7df4681952d7)
Ảnh chụp màn hình của tab Timing trong DevTools

## Hiểu về @font-face
Trước khi đào sâu vào các phương pháp hay nhất cho việc tải font, điều quan trọng là phải hiểu cách @font-face hoạt động và ảnh hưởng đến việc tải font như thế nào.

Khai báo @font-face là một phần thiết yếu khi làm việc với bất kỳ font web nào.
Ít nhất, nó khai báo tên sẽ được sử dụng để tham chiếu đến font và chỉ ra vị trí của tệp font tương ứng.

```css
@font-face {
  font-family: "Open Sans";
  src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2");
}
```

Một quan niệm sai lầm phổ biến là font được yêu cầu khi gặp một khai báo @font-face—điều này không đúng.
Chỉ riêng khai báo @font-face không kích hoạt việc tải font.
Thực tế, một font chỉ được tải xuống nếu nó được tham chiếu bởi styling được sử dụng trên trang. Ví dụ, như sau:

```css
@font-face {
  font-family: "Open Sans";
  src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2");
}

h1 {
  font-family: "Open Sans"
}
```

Nói cách khác, trong ví dụ trên, Open Sans chỉ được tải xuống nếu trang chứa một phần tử <h1>.

Lưu ý: Các cách khác để tải font bao gồm gợi ý tài nguyên preload và Font Loading API.
Do đó, khi suy nghĩ về tối ưu hóa font, điều quan trọng là phải xem xét các bảng định kiểu cũng như các tệp font.
Thay đổi nội dung hoặc cách cung cấp bảng định kiểu có thể có ảnh hưởng lớn đến thời điểm font đến.
Tương tự, việc loại bỏ CSS không sử dụng và chia nhỏ bảng định kiểu có thể giảm số lượng font được tải bởi một trang.
