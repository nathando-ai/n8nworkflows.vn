---
title: "🚀 Tự Động Hóa Tạo Thẻ Tập Thử Gym Kèm Mã QR, Xuất PDF & Gửi Email với n8n"
description: "Xây dựng hệ thống đăng ký tập thử gym tự động 100%: xác thực email, tạo mã QR độc nhất, thiết kế thẻ HTML, xuất file PDF/Image và gửi trực tiếp cho khách hàng."
slug: "tu-dong-hoa-tao-the-tap-thu-gym-qr-code-n8n"
tags: [n8n, automation, no-code, google-sheets, gmail, qr-code, pdf-export]
keywords: [n8n workflow, tự động hóa phòng gym, tạo thẻ tập thử tự động, verifiemail, html to pdf n8n]
---

# 🚀 Tự Động Hóa Tạo Thẻ Thẻ Tập Thử Gym Kèm Mã QR, Xuất PDF & Gửi Email

Các chủ phòng gym hay đội ngũ vận hành thường gặp nỗi đau lớn khi xử lý đăng ký tập thử (Trial Pass) thủ công: mất thời gian kiểm tra email rác, thiết kế thẻ thủ công, tạo mã QR, gửi email và cập nhật Google Sheets. Điều này dễ dẫn đến sai sót, phản hồi chậm trễ và bỏ lỡ khách hàng tiềm năng.

Workflow n8n này sẽ thay thế hoàn toàn quy trình thủ công đó bằng một hệ thống tự động hóa khép kín, chuyên nghiệp và hoạt động 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Xử lý ngay lập tức khi có khách hàng đăng ký qua Webhook.
- **Xác thực thông minh:** Loại bỏ ngay email ảo, email rác nhờ tích hợp công cụ kiểm tra độ tin cậy.
- **Cá nhân hóa chuyên nghiệp:** Tự động tạo thẻ tập có mã QR riêng, hình ảnh và định dạng PDF cao cấp gửi thẳng vào hộp thư khách hàng.
- **Đồng bộ dữ liệu:** Tự động lưu trữ toàn bộ thông tin đăng ký lên Google Sheets để đội ngũ Sales dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail** (để cấu hình OAuth2 gửi email).
- **Google Sheets** (tạo sẵn bảng tính để lưu log).
- **API Keys từ các dịch vụ bên thứ ba:**
  - `VerifiEmail` (verifi.email) để lọc email.
  - `HTMLCSSToImage` (htmlcsstoimg.com) để chuyển thiết kế thành ảnh.
  - `HTMLCSSToPDF` (pdfmunk.com hoặc dịch vụ tương đương) để xuất file PDF.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc copy/paste trực tiếp đoạn mã JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Webhook:** Nhận dữ liệu POST với các trường thông tin: `name`, `email`, `photo_url`, `start_date`, `valid_till`. Test thử qua Postman trước khi kết nối với Landing Page.
- **Verifi Email:** Kết nối credentials API của dịch vụ verifi.email để lọc các email không hợp lệ.
- **IF Email Valid:** Nhánh logic phân chia luồng. Nếu email hợp lệ sẽ đi tiếp, nếu không sẽ chạy qua node **Send Error Response** (trả về lỗi 400).
- **Generate Pass Details (Code Node):** Tạo mã Pass ID độc nhất và định dạng ngày tháng hiển thị trên thẻ.
- **HTML/CSS to Image & HTML to PDF:** Cấu hình credentials tương ứng để chuyển đổi thiết kế thẻ tập sang định dạng hình ảnh và PDF chất lượng cao.
- **Send Email with Pass (Gmail):** Kết nối tài khoản Gmail qua OAuth2, thiết lập nội dung email đính kèm file PDF thẻ tập cho học viên.
- **Log to Google Sheets:** 
  - Chọn tài khoản Google Sheets OAuth2.
  - Chỉ định Sheet có tên: `Gym Trial Passes 2025`
  - Đảm bảo các cột trong bảng gồm: `Name`, `Email`, `Pass ID`, `Start Date`, `Valid Till`, `Issued At`, `Email Verified`, `Status`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng dữ liệu mẫu để kiểm tra toàn bộ luồng từ nhận Webhook đến gửi email.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ:** Thêm node Telegram hoặc Slack ở nhánh thành công để gửi thông báo ngay cho đội ngũ Sales mỗi khi có khách hàng mới đăng ký tập thử thành công.
- **Tự động nhắc lịch:** Kết hợp thêm node Schedule Trigger để quét Google Sheets và gửi email nhắc nhở trước ngày thẻ tập hết hạn 1 ngày.
- **Lưu trữ cloud:** Tải file PDF thẻ tập lưu trữ lên Google Drive cá nhân của phòng gym thay vì chỉ đính kèm trong email.

### 📌 Kết luận
Workflow tự động hóa tạo thẻ tập thử gym này không chỉ giúp tiết kiệm hàng giờ thao tác thủ công mỗi ngày mà còn mang lại trải nghiệm chuyên nghiệp tuyệt vời cho khách hàng ngay từ điểm chạm đầu tiên. Áp dụng ngay để tối ưu hóa quy trình vận hành phòng gym của các sếp nhé!