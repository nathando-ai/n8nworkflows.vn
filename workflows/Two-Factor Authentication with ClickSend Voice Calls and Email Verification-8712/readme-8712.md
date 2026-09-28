---
title: "🔐 Xác thực 2 yếu tố với cuộc gọi thoại và xác minh qua email - Workflow n8n hoàn chỉnh"
description: "Tự động hóa xác thực 2 yếu tố với cuộc gọi thoại qua ClickSend và xác minh qua email - Giảm thiểu rủi ro bảo mật với giải pháp không cần code"
slug: "xac-thuc-2-yeu-toi-clicksend-email"
tags: [n8n, automation, no-code, security, voice-verification]
keywords: [n8n workflow, tự động hóa xác thực, xác thực 2 yếu tố, voice call verification, email verification]
---

# 🔐 Xác thực 2 yếu tố với cuộc gọi thoại và xác minh qua email - Workflow n8n hoàn chỉnh

[Các sếp đang gặp khó khăn khi triển khai hệ thống xác thực 2 yếu tố (2FA) cho ứng dụng của mình. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình xác thực với cuộc gọi thoại qua ClickSend và xác minh qua email, giúp tăng cường bảo mật mà không cần viết code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình xác thực 2 yếu tố
- Tăng cường bảo mật với hai phương thức xác thực (gọi thoại + email)
- Giảm thiểu rủi ro bảo mật với hệ thống xác thực tự động
- Tiết kiệm thời gian và công sức cho đội ngũ IT
- Hỗ trợ tích hợp với nhiều hệ thống khác thông qua n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ClickSend với API Key (đăng ký [tại đây](https://clicksend.com/?u=586989) và nhận 2€ miễn phí)
- Tài khoản email SMTP để gửi email xác thực
- Số điện thoại để nhận cuộc gọi thoại xác thực
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/8712)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Send Voice"**:
   - Tạo credentials "Basic Auth" với:
     - Username: Email đăng ký ClickSend
     - Password: API Key từ ClickSend
   - Cấu hình các tham số:
     - Method: POST
     - URL: `https://rest.clicksend.com/v3/voice/send`
     - Headers: `Content-Type: application/json`
     - Body: JSON với các trường cần thiết (xem chi tiết trong workflow)

2. **Node "Send Email"**:
   - Cấu hình credentials SMTP cho email xác thực
   - Đặt địa chỉ email gửi (Sender)

3. **Node "Set voice code" và "Set email code"**:
   - Thiết lập mã xác thực cho cả hai phương thức (gọi thoại và email)
   - Đảm bảo mã xác thực là duy nhất và có thời gian hết hạn

4. **Node "Verify voice code" và "Verify email code"**:
   - Cấu hình form để người dùng nhập mã xác thực
   - Thiết lập các trường nhập liệu phù hợp

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu
2. Kiểm tra cuộc gọi thoại và email xác thực
3. Bật Active workflow khi đã kiểm tra và xác nhận hoạt động bình thường

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để thông báo kết quả xác thực
2. Thêm log lưu trữ các lần xác thực thành công/không thành công
3. Tích hợp với hệ thống CRM để lưu trữ thông tin người dùng
4. Thiết lập báo cáo định kỳ về các lần xác thực thất bại

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc triển khai xác thực 2 yếu tố với hai phương thức xác thực (gọi thoại và email). Với việc tự động hóa hoàn toàn quá trình này, các sếp có thể tăng cường bảo mật cho hệ thống mà không cần viết code. Hãy áp dụng ngay để nâng cao bảo mật cho ứng dụng của mình!