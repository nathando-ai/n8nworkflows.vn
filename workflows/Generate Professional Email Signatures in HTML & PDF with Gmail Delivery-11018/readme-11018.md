---
title: "🚀 Tự động tạo chữ ký email chuyên nghiệp dạng HTML & PDF và gửi qua Gmail bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình nhận thông tin, tạo chữ ký email HTML cao cấp, chuyển đổi sang PDF và gửi trực tiếp qua Gmail."
slug: "tu-dong-tao-chu-ky-email-html-pdf-n8n"
tags: [n8n, automation, no-code, gmail, pdf, html]
keywords: [n8n workflow, tạo chữ ký email, html to pdf, tự động hóa gmail, webhook n8n]
---

# 🚀 Tự động tạo chữ ký email chuyên nghiệp dạng HTML & PDF và gửi qua Gmail

Các sếp có bao giờ cảm thấy mất quá nhiều thời gian để thiết kế, chuẩn hóa và đồng bộ chữ ký email cho toàn bộ nhân sự trong công ty? Việc làm thủ công không chỉ tốn thời gian mà còn dễ lệch font chữ, sai thông tin liên hệ hoặc thiếu các liên kết mạng xã hội quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia *Jitesh Dugar*. Workflow này giúp tự động hóa 100% quy trình: nhận dữ liệu từ Webhook, tạo chữ ký HTML cao cấp, chuyển đổi thành file PDF sắc nét và tự động gửi thẳng vào hộp thư của người dùng qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập thông tin đầu vào là có ngay chữ ký email chuyên nghiệp kèm file PDF.
- **Đồng bộ thương hiệu:** Đảm bảo toàn bộ công ty dùng chung một chuẩn thiết kế chữ ký đẹp mắt, tích hợp icon mạng xã hội.
- **Đa dạng định dạng:** Vừa có mã HTML để gắn trực tiếp vào cài đặt Gmail, vừa có file PDF chất lượng cao để lưu trữ hoặc in ấn.
- **Phản hồi tức thì:** Webhook trả về kết quả JSON kèm `pdf_url` ngay sau khi xử lý xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** để cấu hình OAuth2 gửi email tự động.
- Tài khoản và API Key tại dịch vụ **HTML to PDF** (ví dụ: [Pdfmunk](https://pdfmunk.com)) để xử lý việc chuyển đổi.
- Công cụ test API như **Postman** hoặc cURL.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này từ kho lưu trữ n8n chính thức và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Webhook - Signature Request**: 
  - Cấu hình phương thức `POST` với đường dẫn `/email-signature`.
  - Nhận dữ liệu JSON bao gồm các trường: `name` (tên), `designation` (chức vụ), `email`, `phone` (số điện thoại), và các liên kết mạng xã hội (`social links`).
- **Extract Inputs** (Node Code): 
  - Đảm bảo code trích xuất và làm sạch dữ liệu đầu vào chính xác để tạo các biến sạch cho HTML.
- **Build HTML Signature** (Node Set): 
  - Tùy chỉnh giao diện HTML theo ý muốn (chèn logo công ty, màu sắc thương hiệu, bố cục icon). Thay thế URL logo mặc định bằng logo của công ty các sếp.
- **HTML to PDF**: 
  - Kết nối tài khoản thông qua `htmlcsstopdfApi` (lấy API key từ [pdfmunk.com](https://pdfmunk.com)). Node này sẽ xử lý font chữ, icon SVG và trả về một đường dẫn `pdf_url` bảo mật.
- **Download binary data** (Node HTTP Request): 
  - Tải file từ `pdf_url` vừa nhận được và chuyển thành dữ liệu nhị phân (binary data).
- **Send Email via Gmail**: 
  - Cấu hình kết nối `gmailOAuth2`. Thiết lập tiêu đề, nội dung và đính kèm file PDF vừa tạo để gửi trực tiếp cho người dùng.
- **Success Response** (Node Respond to Webhook): 
  - Trả về thông báo thành công dưới dạng JSON kèm theo đường dẫn file PDF cho hệ thống gọi API.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu qua Postman để test thử toàn bộ luồng dữ liệu.
- Kiểm tra hộp thư Gmail xem đã nhận được email đính kèm chữ ký PDF chưa.
- Nếu mọi thứ chạy mượt, hãy bật công tắc **Active** cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết nối Webhook này với Telegram Bot hoặc Slack, nhân viên chỉ cần gõ lệnh là tự động nhận được chữ ký email cá nhân hóa.
- **Lưu trữ Cloud:** Thay vì chỉ gửi qua email, có thể tích hợp thêm node Google Drive hoặc Airtable để lưu trữ tất cả các file PDF chữ ký của nhân sự.
- **Báo cáo định kỳ:** Thêm một node đếm số lượng chữ ký được tạo và gửi báo cáo tổng kết về Slack cho bộ phận HR mỗi tháng.

### 📌 Kết luận
Với workflow n8n này, việc quản lý và cấp phát chữ ký email chuyên nghiệp cho toàn doanh nghiệp trở nên nhanh chóng và tự động hóa hoàn toàn. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình vận hành của doanh nghiệp các sếp nhé!