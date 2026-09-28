---
title: "🚀 Xây dựng hệ thống xác thực đa yếu tố (MFA) qua Cuộc gọi Thoại và Email với n8n, ClickSend và SMTP"
description: "Tự động hóa toàn bộ quy trình xác thực người dùng (MFA) bằng cuộc gọi thoại Text-to-Speech qua ClickSend kết hợp xác thực qua Email SMTP một cách chuyên nghiệp."
slug: "mfa-multi-factor-authentication-voice-call-email-clicksend-smtp"
tags: [n8n, automation, no-code, mfa, security, clicksend, smtp]
keywords: [n8n workflow, xác thực đa yếu tố, mfa n8n, clicksend voice call, tự động hóa bảo mật, smtp email verification]
---

# 🚀 Xây dựng hệ thống xác thực đa yếu tố (MFA) qua Cuộc gọi Thoại và Email với n8n

Các sếp có bao giờ đau đầu khi phải xây dựng một hệ thống xác thực người dùng (MFA) vừa bảo mật, vừa đa dạng phương thức (gọi điện thoại và gửi email) nhưng lại tốn quá nhiều chi phí và thời gian lập trình từ đầu? Việc tích hợp các cổng SMS hay Voice Gateway thủ công thường rất phức tạp và đắt đỏ.

Đừng lo! Workflow n8n này sẽ giúp các sếp dựng ngay một hệ thống **Xác thực đa yếu tố (MFA)** chuyên nghiệp kết hợp giữa **Cuộc gọi Thoại tự động (Text-to-Speech)** qua **ClickSend** và **Xác thực qua Email (SMTP)**, hoạt động hoàn toàn tự động 100% không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tối ưu:** Cung cấp lớp xác thực kép (Multi-factor authentication) qua cả kênh thoại và email.
- **Trải nghiệm chuyên nghiệp:** Người dùng nhận được cuộc gọi thoại đọc mã xác thực (TTS) và email xác thực gần như tức thì.
- **Tiết kiệm chi phí:** Tận dụng ClickSend với chi phí cực rẻ và SMTP có sẵn của doanh nghiệp.
- **Tự động hoàn toàn:** Từ khâu thu thập thông tin qua form, tạo mã, gửi thông báo đến khâu kiểm tra và phản hồi thành công/thất bại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản ClickSend:** Đăng ký tại [ClickSend](https://clicksend.com/?u=586989) để lấy API Key và nhận credits trải nghiệm.
- **Tài khoản SMTP:** Thông tin kết nối máy chủ email (Gmail, SendGrid, Amazon SES, v.v.) để gửi email xác thực.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sao chép toàn bộ mã JSON từ n8n và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để hệ thống hoạt động trơn tru:

- **Node `On form submission` (Form Trigger):** Điểm khởi đầu nơi người dùng nhập thông tin (số điện thoại, email) để nhận mã xác thực.
- **Node `Set voice code` & `Set email code`:** Cấu hình nội dung và mã PIN/OTP sẽ được phát trong cuộc gọi thoại và gửi qua email.
- **Node `Send Voice` (HTTP Request):** 
  - Kết nối với API của ClickSend.
  - Cấu hình **Credentials** loại `Basic Auth` với **Username** tài khoản ClickSend của các sếp và **Password** chính là **API Key** lấy từ trang quản trị ClickSend.
- **Node `Send Email` (Email Send):** 
  - Cấu hình **Credentials** loại `SMTP` với thông tin máy chủ email của doanh nghiệp.
  - Điền địa chỉ người gửi (Sender) phù hợp.
- **Các Node Form xác thực (`Verify voice code`, `Verify email code`, `Success`, `Fail voice code`, `Fail email code`):** Xử lý luồng nhập lại mã xác thực của người dùng và hiển thị thông báo thành công hay thất bại.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử submit form mẫu để test luồng gọi điện thoại và gửi email.
- Kiểm tra xem cuộc gọi TTS có đọc đúng mã và email có về hộp thư không.
- Sau khi test ngon lành, hãy gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ:** Nối thêm node Telegram hoặc Slack vào nhánh `Success` để đội ngũ vận hành nhận được thông báo ngay khi có user xác thực thành công.
- **Lưu lịch sử:** Lưu toàn bộ log xác thực (số điện thoại, thời gian, trạng thái thành công/thất bại) vào Google Sheets hoặc Airtable để dễ dàng kiểm tra (Audit Log).
- **Random hóa mã OTP:** Thay vì dùng mã tĩnh, các sếp có thể dùng node `Code` để sinh mã OTP ngẫu nhiên 6 chữ số cho mỗi lần request.

### 📌 Kết luận
Hệ thống MFA kết hợp Voice Call và Email này là một giải pháp bảo mật cực kỳ chuyên nghiệp và dễ triển khai nhờ n8n. Hãy áp dụng ngay vào dự án của các sếp để nâng tầm bảo mật và trải nghiệm người dùng nhé!