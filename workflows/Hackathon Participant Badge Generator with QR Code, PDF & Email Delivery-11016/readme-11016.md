---
title: "🚀 Tự Động Tạo Thẻ Tham Dự Hackathon Kèm Mã QR, Xuất PDF và Gửi Email Chuyên Nghiệp"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n xử lý đăng ký sự kiện Hackathon: xác thực email, tạo mã QR, xuất file PDF và gửi email tự động 100%."
slug: "tu-dong-tao-the-tham-du-hackathon-n8n"
tags: [n8n, automation, no-code, pdf-generation, email-automation, google-sheets]
keywords: [n8n workflow, tạo thẻ hackathon tự động, xuất PDF n8n, gửi email tự động n8n, quản lý sự kiện no-code]
---

# 🚀 Tự Động Tạo Thẻ Tham Dự Hackathon Kèm Mã QR, Xuất PDF và Gửi Email Chuyên Nghiệp

Việc tổ chức các sự kiện lớn như Hackathon đòi hỏi ban tổ chức phải xử lý hàng trăm, thậm chí hàng ngàn đơn đăng ký. Việc làm thủ công từ khâu kiểm tra email rác, tạo mã ID, thiết kế thẻ tham dự (Badge), tạo mã QR, xuất file PDF cho đến gửi email cá nhân hóa và lưu vào Google Sheets ngốn rất nhiều thời gian và dễ xảy ra sai sót.

Workflow n8n này chính là giải pháp tự động hóa 100% toàn bộ quy trình trên, giúp các sếp tối ưu hóa vận hành, tạo sự chuyên nghiệp tuyệt đối trong mắt người tham dự mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Tiếp nhận thông tin từ Webhook, xử lý và trả kết quả tức thì.
- **Bảo mật & Sạch dữ liệu**: Loại bỏ các email rác, email giả mạo (disposable email) nhờ bộ lọc thông minh.
- **Chuyên nghiệp hóa**: Tự động tạo thẻ Badge kèm mã QR độc nhất dạng PDF và gửi thẳng vào hộp thư người tham dự qua Gmail.
- **Đồng bộ dữ liệu chuẩn chỉnh**: Tự động ghi lại toàn bộ thông tin người tham gia, Badge ID và link PDF vào Google Sheets để dễ dàng điểm danh hoặc quản lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản & API Keys**:
  - **VerifiEmail** (tại [verifi.email](https://verifi.email)) để check sống/chết email.
  - **PDFMunk** (tại [pdfmunk.com](https://pdfmunk.com) hoặc dịch vụ HTML to PDF tương thích) qua node `HTML to PDF`.
  - **Gmail Account** (cấu hình OAuth2) để gửi email.
  - **Google Sheets** (cấu hình OAuth2) để lưu trữ log.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ kho lưu trữ hoặc copy toàn bộ JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Webhook Trigger**: Lấy URL Webhook (Production/Test) để tích hợp vào Landing Page đăng ký Hackathon (gửi phương thức `POST` chứa các trường: `name`, `email`, `team`, `event`).
- **VerifiEmail**: Kết nối tài khoản `verifiEmailApi` để hệ thống tự động loại bỏ các email không tồn tại hoặc email rác.
- **HTML to PDF**: Cấu hình credentials API từ dịch vụ chuyển đổi HTML sang PDF để render mẫu thẻ Badge kèm mã QR.
- **Send Badge via Gmail**: Kết nối tài khoản Gmail OAuth2, thiết lập nội dung email HTML hiển thị ảnh xem trước thẻ Badge và đính kèm file PDF.
- **Log to Sheets**: Kết nối tài khoản Google Sheets OAuth2, trỏ tới file Google Sheet quản lý sự kiện và chọn chế độ `append` (thêm dòng mới) để lưu: Tên, Email, Team, Badge ID, Verify URL và Link PDF.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test step` hoặc `Execute Workflow`) với dữ liệu mẫu (Payload giả lập qua Postman hoặc cURL).
- Kiểm tra email nhận được, file PDF xuất ra và dữ liệu trên Google Sheets.
- Sau khi mọi thứ hoạt động trơn tru, bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ**: Thêm node Telegram hoặc Slack ở nhánh thành công để bắn thông báo về nhóm của ban tổ chức mỗi khi có hacker mới đăng ký thành công.
- **Xử lý nhánh lỗi (Error Handling)**: Thêm nhánh phụ khi email không hợp lệ (`Email Valid?` trả về `False`) để gửi email từ chối lịch sự hoặc yêu cầu đăng ký lại bằng email chính chủ.
- **Hệ thống điểm danh Check-in**: Tận dụng `Verify URL` được tạo sẵn trên QR code để xây dựng thêm một mini-flow quét mã QR check-in tại cổng sự kiện.

### 📌 Kết luận
Workflow tạo thẻ Hackathon tự động này là một "vũ khí" đắc lực giúp các đội ngũ tổ chức sự kiện tiết kiệm hàng chục giờ làm việc thủ công, đồng thời mang lại trải nghiệm cực kỳ chuyên nghiệp cho người tham dự ngay từ giây phút họ đăng ký. "Lên đồ" và áp dụng ngay cho sự kiện tiếp theo của các sếp nhé!