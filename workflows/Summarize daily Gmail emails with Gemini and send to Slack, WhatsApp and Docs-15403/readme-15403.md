---
title: "📧 Tự động hóa tổng hợp email hàng ngày với Gemini và gửi đến Slack, WhatsApp và Google Docs"
description: "Hướng dẫn chi tiết cách tự động tổng hợp email hàng ngày từ Gmail, lọc thông tin nhạy cảm và gửi báo cáo tóm tắt đến nhiều kênh khác nhau như Slack, WhatsApp và Google Docs."
slug: "tu-dong-hoa-tong-hop-email-hang-ngay-voi-gemini"
tags: [n8n, automation, no-code, email, ai, google, slack, whatsapp]
keywords: [n8n workflow, tự động hóa email, tổng hợp email, Gemini AI, Google Docs, Slack, WhatsApp]
---

# 📧 Tự động hóa tổng hợp email hàng ngày với Gemini và gửi đến Slack, WhatsApp và Google Docs

[Các sếp] nhận hàng trăm email mỗi ngày, nhưng lại không có thời gian để đọc hết và tóm tắt nội dung quan trọng. Với workflow này, các sếp có thể tự động tổng hợp email hàng ngày từ Gmail, lọc thông tin nhạy cảm và gửi báo cáo tóm tắt đến nhiều kênh khác nhau như Slack, WhatsApp và Google Docs.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp email hàng ngày mà không cần phải đọc từng email.
- **Tăng hiệu quả làm việc**: Nhận được báo cáo tóm tắt email hàng ngày một cách nhanh chóng và chính xác.
- **Cá nhân hóa**: Gửi báo cáo đến nhiều kênh khác nhau như Slack, WhatsApp và Google Docs.
- **Bảo mật thông tin**: Lọc thông tin nhạy cảm trước khi gửi báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ.
- API key của Google Gemini.
- Tài khoản Google Docs.
- Tài khoản Slack.
- Tài khoản WhatsApp Business API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [n8n.io/workflows/15403](https://n8n.io/workflows/15403).
2. Nhấn vào nút "Import" để tải xuống file JSON của workflow.
3. Trong n8n Editor, nhấn vào nút "Import from File" và chọn file JSON vừa tải xuống.

Hoặc, các sếp có thể copy/paste JSON từ trang n8n.io/workflows/15403 vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**: Cấu hình thời gian chạy workflow hàng ngày.
2. **⚙️ Set Configuration**: Cập nhật các thông tin cấu hình như `targetEmail`, `slackUserId`, `whatsappNumber` và các kênh nhận báo cáo.
3. **Gmail: Fetch Primary Emails**: Kết nối tài khoản Gmail và cấu hình các tham số cần thiết.
4. **Generate AI Summary**: Kết nối API key của Google Gemini.
5. **Google Docs: Create New Doc**: Kết nối tài khoản Google Docs và cấu hình các tham số cần thiết.
6. **Slack: Post Overview Alert**: Kết nối tài khoản Slack và cấu hình các tham số cần thiết.
7. **WhatsApp: Send Overview Alert**: Kết nối tài khoản WhatsApp Business API và cấu hình các tham số cần thiết.

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Test Workflow" để kiểm tra workflow.
2. Sau khi kiểm tra thành công, nhấn vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh phạm vi tổng hợp**: Các sếp có thể chỉnh sửa các nhãn email trong node Gmail để lọc các email quan trọng.
- **Lọc email**: Các sếp có thể cấu hình các bộ lọc theo chủ đề hoặc người gửi trong node "⚙️ Set Configuration".
- **Tùy chỉnh giọng điệu AI**: Các sếp có thể chỉnh sửa prompt trong node "Build LLM Prompt" để thay đổi giọng điệu của báo cáo tóm tắt.

### 📌 Kết luận
Workflow này giúp các sếp tự động tổng hợp email hàng ngày, lọc thông tin nhạy cảm và gửi báo cáo tóm tắt đến nhiều kênh khác nhau. Với workflow này, các sếp có thể tiết kiệm thời gian và tăng hiệu quả làm việc.