---
title: "🚀 Tự động tạo thẻ ưu đãi cá nhân hóa và xác thực email với n8n"
description: "Xây dựng hệ thống tự động nhận thông tin đăng ký mã giảm giá, xác thực email chống spam, tạo hình ảnh thẻ promo độc quyền và gửi qua Gmail kèm ghi nhận Google Sheets."
slug: "tu-dong-tao-the-uu-dai-ca-nhan-hoa-va-xac-thuc-email"
tags: [n8n, automation, no-code, gmail, google-sheets, marketing-automation]
keywords: [n8n workflow, tạo thẻ ưu đãi tự động, xác thực email, html to image, google sheets automation]
keywords: [n8n workflow, tự động hóa, tạo thẻ ưu đãi, xác thực email, google sheets, html to image]
---

# 🚀 Tự động tạo thẻ ưu đãi cá nhân hóa và xác thực email với n8n

Các sếp có bao giờ đau đầu khi chạy các chiến dịch tặng mã giảm giá (promo code)? Khách hàng điền email ảo, email rác, hay việc phải thiết kế thủ công từng chiếc thẻ giảm giá gửi cho khách hàng tốn quá nhiều thời gian? 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia Jitesh Dugar. Hệ thống này sẽ tự động hóa từ A-Z: nhận thông tin đăng ký, kiểm tra độ sống/chết của email, tự động thiết kế hình ảnh thẻ ưu đãi (Promo Card) bắt mắt, gửi email chúc mừng kèm hình ảnh, và cuối cùng là lưu log toàn bộ vào Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chặn đứng email rác/ảo:** Tích hợp bộ lọc xác thực email thông minh, bảo vệ hệ thống khỏi bot và spam.
- **Trải nghiệm cá nhân hóa đỉnh cao:** Khách hàng nhận được hình ảnh thẻ ưu đãi riêng biệt có tên, mã giảm giá và QR code thanh toán ngay lập tức.
- **Tự động hóa 100%:** Từ lúc khách hàng bấm submit form cho đến khi email kèm hình ảnh nhảy vào hộp thư chỉ mất chưa đầy phút.
- **Quản lý dữ liệu tập trung:** Mọi lịch sử phát hành mã ưu đãi được ghi nhận tự động vào Google Sheets để dễ dàng thống kê.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn:
1. **n8n Instance** (Cloud hoặc Self-hosted).
2. **Verifi Email API Key**: Lấy tại [verifi.email](https://verifi.email) để kiểm tra email.
3. **HTML to Image API Key**: Lấy tại [htmlcsstoimg.com](https://htmlcsstoimg.com) để render hình ảnh thẻ promo.
4. **Gmail Account (OAuth2)**: Để gửi email tự động tới khách hàng và thông báo admin khi có lỗi.
5. **Google Sheets**: Tạo sẵn một file Google Sheets để lưu log dữ liệu phân phối.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào n8n editor, chọn **Import from JSON** và dán vào là xong phần khung xương.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **WEBHOOK**: Endpoint nhận dữ liệu POST từ form đăng ký của sếp với cấu trúc JSON mẫu:
  ```json
  {
    "name": "John Doe",
    "email": "customer@email.com",
    "promo_code": "SAVE20",
    "discount_value": "20%"
  }
  ```
- **Edit Fields**: Làm sạch dữ liệu đầu vào (cắt bỏ khoảng trắng thừa, chuẩn hóa định dạng giảm giá, thêm timestamp).
- **Validate Email** *(Verifi Email Node)*: Kết nối tài khoản Verifi Email để kiểm tra tính hợp lệ của cú pháp và sự tồn tại của hộp thư.
- **Validation Gateway** *(IF Node)*: Kiểm tra kết quả từ bước trên. Nếu `valid = true` sẽ đi tiếp luồng thành công, ngược lại chuyển sang luồng lỗi.
- **Generate Promo Card Image** *(HTML to Image Node)*: Sử dụng dịch vụ HTMLCssToImage kết hợp template để sinh ảnh kích thước 400x500px chứa tên khách hàng, mã code và QR code.
- **Success Path** *(Gmail Node)*: Cấu hình gửi email chúc mừng tới địa chỉ của khách hàng (`{{email}}`), tiêu đề hấp dẫn và đính kèm hình ảnh thẻ ưu đãi vừa tạo.
- **Log Promo Distribution** *(Google Sheets Node)*: Chọn file Google Sheets và ánh xạ các cột (Timestamp, Tên khách hàng, Email, Mã giảm giá, Trạng thái giao hàng).
- **Error Path** *(Gmail Node)*: Gửi email cảnh báo về hộp thư của Admin (`YOUR_ADMIN_EMAIL_HERE`) nếu phát hiện email không hợp lệ hoặc lỗi hệ thống.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test Step** từng node với dữ liệu mẫu để đảm bảo API keys hoạt động chính xác.
- Bật công tắc **Active** ở góc trên bên phải để workflow chính thức trực tuyến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo phụ:** Nối thêm một node Telegram hoặc Slack vào Error Path để đội ngũ Sale/Support nhận cảnh báo ngay lập tức trên điện thoại khi có sự cố.
- **Lưu trữ ảnh Cloud:** Lưu hình ảnh thẻ ưu đãi vừa tạo lên Google Drive hoặc Cloudinary trước khi gửi email để dễ dàng tra cứu lại sau này.
- **Tự động nhắc nhở (Follow-up):** Kết hợp thêm node Wait và thêm một email nhắc nhở trước khi mã giảm giá hết hạn để tối ưu tỷ lệ chuyển đổi.

### 📌 Kết luận
Với workflow n8n này, các sếp không chỉ tự động hóa hoàn toàn quy trình tặng mã giảm giá mà còn nâng tầm chuyên nghiệp cho thương hiệu của mình trong mắt khách hàng. Triển khai ngay hôm nay để tiết kiệm hàng giờ thao tác thủ công mỗi ngày nhé!