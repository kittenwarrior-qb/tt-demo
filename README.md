# T&T Home: bản mock UI thương mại điện tử (mobile-first)

Bản prototype HTML gói gọn trong 1 file, mô phỏng trọn luồng mua hàng: từ đăng ký đến huỷ đơn và hoàn tiền. Hỗ trợ 2 ngôn ngữ: tiếng Việt và tiếng Anh.

## Cách mở

Mở trực tiếp `index.html` bằng Chrome hoặc Safari. Không cần build và không cần cài thêm gì.

### Deploy lên Vercel

Đây là site tĩnh, không cần build.

1. Vào [vercel.com/new](https://vercel.com/new) → **Import Git Repository** → chọn repo `tt-demo`.
2. Framework Preset để **Other**. Build Command và Output Directory để trống.
3. Bấm **Deploy**.

### 2 chế độ hiển thị

- **Mặc định (bản deploy):** chạy như web app thật. Trên điện thoại app chiếm toàn màn hình; trên desktop app hiển thị thành một cột giữa màn hình. Không có khung điện thoại, không có checklist. Nút **▶** nhỏ ở mép phải dùng để mở phần **Tự chạy demo**, kèm bảng dữ liệu test để tự thao tác tay.
- **Thêm `?panel` vào URL** (ví dụ `https://…vercel.app/?panel`): hiện khung điện thoại và checklist 22 bước, dùng khi demo nội bộ.

### Tự chạy demo

Bấm **▶**, chọn tốc độ Chậm / Vừa / Nhanh, rồi bấm **Bắt đầu tự chạy**. App sẽ đặt lại dữ liệu rồi tự đi qua 19 bước, mất khoảng 2–3 phút ở tốc độ Vừa:

1. Đổi ngôn ngữ
2. Đăng ký, nhập OTP
3. Lọc danh mục, tìm kiếm và lọc giá
4. Xem sản phẩm, chọn biến thể, xem đánh giá
5. Thêm vào giỏ, áp mã giảm giá
6. Trượt để thanh toán
7. Nhập địa chỉ, chọn giao nhanh
8. Thử thẻ bị từ chối, rồi thanh toán bằng thẻ 4242 qua 3DS
9. Xem tracking, huỷ đơn và xem hoàn tiền
10. Hỏi T&T Assist
11. Đăng xuất, đăng nhập lại

Thanh điều khiển ở đầu màn hình có nút **Dừng / Tiếp / Thoát**. Mỗi lần chạm được đánh dấu bằng vòng tròn để người xem dễ theo dõi.

- **Trên desktop:** app hiển thị trong khung điện thoại, bên phải là panel **Kịch bản demo**.
- **Trên mobile hoặc cửa sổ hẹp hơn 900px:** app chiếm toàn màn hình. Mở panel demo bằng tab nhỏ ở mép phải.
- **Cần có internet** để tải font (Google Fonts) và ảnh sản phẩm (Unsplash). Ảnh nào tải lỗi sẽ tự hiện placeholder xám, layout không bị vỡ.
- **Dữ liệu lưu trong `localStorage`:** tài khoản, giỏ hàng, đơn hàng, địa chỉ. Nút **Reset demo** trong panel sẽ xoá toàn bộ để chạy lại từ đầu.

## Dữ liệu test

| Mục | Giá trị |
|---|---|
| Tài khoản demo | `demo@tt.shop` / `Demo1234` (có sẵn trong gợi ý "Tài khoản đã lưu" ở màn Đăng nhập) |
| OTP khi đăng ký | `123456` |
| Mã giảm giá | `WELCOME10` (giảm 10%), `FREESHIP` (miễn phí giao hàng) |
| Thẻ thanh toán thành công (có bước 3DS) | `4242 4242 4242 4242`, mã 3DS `123456` |
| Thẻ bị từ chối | `4000 0000 0000 0002` |
| Thẻ không đủ số dư | `4000 0000 0000 9995` |
| Ngày hết hạn / CVC | Ngày bất kỳ trong tương lai / 3 số bất kỳ |

Tài khoản demo có sẵn 4 đơn mẫu để demo đủ mọi trạng thái: đang đóng gói, đang vận chuyển, đã giao, đã huỷ.

## Luồng màn hình (18 màn + T&T Assist)

```
01 Welcome → 02 Đăng ký → 03 OTP → 04 Đăng nhập (+ Quên mật khẩu)
→ 05 Trang chủ → 06 Tìm kiếm / Lọc → 07 Chi tiết sản phẩm → 08 Đánh giá
→ 09 Giỏ hàng → 10 Checkout (Địa chỉ → Giao hàng) → 11 Thanh toán kiểu Stripe → 12 3DS → 13 Đặt hàng thành công
→ 14 Đơn hàng → 15 Tracking → 16 Huỷ đơn → 17 Đã huỷ / Hoàn tiền
→ 18 Tài khoản (yêu thích, sổ địa chỉ, phương thức thanh toán, ngôn ngữ, đăng xuất)
```

## Checklist demo

Checklist này cũng có trong panel demo của app. Bấm vào một bước sẽ nhảy tới màn tương ứng, và bước tự được đánh dấu xong khi làm đúng thao tác.

**Luồng chính**
1. Mở Welcome, đổi VI ↔ EN và thấy giá đổi giữa ₫ và $
2. Đăng ký tài khoản và nhập OTP
3. Vào trang chủ, lọc danh mục "Đèn"
4. Tìm "mug" và chọn khoảng giá trong bottom sheet lọc
5. Mở chi tiết sản phẩm, chọn biến thể
6. Xem đánh giá, lọc review 5★
7. Thêm vào giỏ (hoặc Mua ngay)
8. Tăng số lượng, áp mã WELCOME10
9. Checkout: nhập địa chỉ, chọn Giao nhanh
10. Thanh toán trên trang kiểu Stripe bằng thẻ 4242…
11. Xác thực 3DS và tới màn Thành công
12. Mở Đơn hàng, xem timeline tracking
13. Huỷ đơn: chọn lý do, xác nhận, xem trạng thái hoàn tiền
14. Đăng xuất, đăng nhập lại, đơn hàng vẫn còn

**Nhánh lỗi**

15. Đăng nhập sai mật khẩu, lỗi hiện ngay dưới ô nhập. Sai 3 lần thì app gợi ý đặt lại mật khẩu.
16. Quên mật khẩu: gửi link đặt lại
17. Thẻ bị từ chối, rồi thanh toán lại thành công
18. Nhập mã giảm giá không hợp lệ
19. Giỏ hàng trống
20. Đơn đã giao thì không huỷ được, chỉ còn Trả hàng hoặc Mua lại

**T&T Assist**

21. Mở T&T Assist từ trang sản phẩm, xem xếp hạng theo thói quen
22. Thêm vào giỏ từ người bán được đề xuất

## T&T Assist: trợ lý so sánh giá (tính năng mới)

- **Cách mở:** bong bóng ✨ ở góc phải màn Trang chủ / Tìm kiếm / Sản phẩm / Đánh giá, hoặc nút **"So sánh giá từ N người bán"** trên trang chi tiết sản phẩm.
- **Tìm kiếm:** tìm cùng một sản phẩm (cùng mã SKU) từ 4 người bán trên sàn T&T, rồi so sánh giá, đánh giá (có tính thêm số lượt review), thời gian giao, chính sách đổi trả và độ uy tín.
- **Điểm phù hợp 0–100:** tính theo trọng số **học từ thói quen của khách**:

| Hành vi của khách | Ưu tiên được tăng |
|---|---|
| Chọn giao nhanh khi đặt hàng | Tốc độ giao |
| Lọc hoặc sắp xếp theo đánh giá 5★ | Đánh giá |
| Dùng mã giảm giá, lọc giá thấp | Giá |
| Bấm Mua ngay | Tốc độ giao |
| Chọn người bán nào trong trợ lý | Tiêu chí nổi trội của người bán đó |

- **Minh bạch:** thẻ "Thói quen mua sắm của bạn" ghi rõ dữ liệu đã học kèm bằng chứng. Khách có thể chuyển sang xếp hạng cân bằng bất cứ lúc nào.
- **Huy hiệu:** Phù hợp nhất / Rẻ nhất / Nhanh nhất / Đánh giá cao nhất. Mỗi dòng có "Vì sao?" phân tích điểm theo từng tiêu chí.
- **Hỏi tiếp:** gõ tự do (ví dụ "đèn", "dưới 1tr", "ai giao nhanh nhất") hoặc bấm chip gợi ý.
- **Thêm vào giỏ từ người bán bất kỳ:** giỏ hàng ghi "Bán bởi …" kèm đúng giá của người bán đó.
- **Chạy offline:** thuật toán mô phỏng ngay trong file, không gọi API bên ngoài.

## Ghi chú thiết kế

- **Design tokens** lấy từ `DESIGN-stripe.md`, đã giảm độ rực: màu chính là indigo dịu `#5b55c4`, các màu trạng thái cũng dùng tông dịu.
- **Font:** Montserrat cho tiêu đề, Nunito Sans cho nội dung. Cả hai đều hỗ trợ đầy đủ tiếng Việt.
- **Hình khối:** ô nhập và nút bo pill, thẻ (card) bo góc 12px.
- **Logo:** khối lập phương isometric 3D, mặt trên là hai chữ T đan nhau (file `favicon.svg`).
- **Component sheet:** mở từ panel demo, tổng hợp toàn bộ component của app.
