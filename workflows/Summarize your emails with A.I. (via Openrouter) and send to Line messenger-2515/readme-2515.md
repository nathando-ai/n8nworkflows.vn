---
title: "📧 Tự động hóa tóm tắt email bằng trí tuệ nhân tạo và gửi đến Line Messenger"
description: "Hướng dẫn chi tiết cách tự động hóa việc đọc email, tóm tắt nội dung bằng AI và gửi kết quả đến Line Messenger bằng n8n"
slug: "tu-dong-hoa-tom-tat-email-bang-ai-va-gui-den-line-messenger"
tags: [n8n, automation, no-code, ai, line messenger]
keywords: [n8n workflow, tự động hóa email, tóm tắt nội dung, line messenger, openrouter]
---

# 📧 Tự động hóa tóm tắt email bằng trí tuệ nhân tạo và gửi đến Line Messenger

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đọc email không quan trọng
- Nhận tóm tắt nội dung email chính xác và nhanh chóng
- Tự động hóa toàn bộ quy trình từ đọc email đến gửi thông báo
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tích hợp với các công cụ thông tin hiện đại như Line Messenger
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản email với quyền truy cập IMAP (ví dụ: Gmail)
- Tài khoản OpenRouter.ai để sử dụng dịch vụ AI tóm tắt
- Tài khoản Line Developer với quyền truy cập Messaging API
- API key từ OpenRouter.ai và Channel Access Token từ Line
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2515)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Read emails (IMAP)"**:
   - Tạo credential mới cho IMAP
   - Điền thông tin IMAP của email server (xem hướng dẫn [ở đây](https://www.getmailspring.com/setup/access-gmail-via-imap-smtp) cho Gmail)
   - Chọn credential vừa tạo trong node này

2. **Node "Send email to A.I. to summarize"**:
   - Tạo credential mới cho HTTP Header Auth
   - Username: `Authorization`
   - Password: `Bearer {your_openrouter_api_key}` (thay thế bằng API key của bạn từ OpenRouter.ai)
   - Chọn credential vừa tạo trong node này
   - Đảm bảo URL trong node trỏ đến endpoint của OpenRouter AI

3. **Node "Send summarized content to messenger"**:
   - Tạo credential mới cho HTTP Header Auth
   - Username: `Authorization`
   - Password: `Bearer {your_line_channel_access_token}` (thay thế bằng Channel Access Token từ Line Developer Console)
   - Chọn credential vừa tạo trong node này
   - Đảm bảo URL trong node trỏ đến endpoint của Line Messaging API

#### 3. Kích hoạt ⚡️
1. Thử chạy workflow với dữ liệu mẫu để kiểm tra kết nối
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy theo lịch trình được thiết lập (mặc định là mỗi 15 phút)

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi tần suất chạy workflow bằng cách chỉnh sửa tham số "Interval" trong node "Read emails (IMAP)"
- Kết hợp với Slack hoặc Telegram để nhận thông báo thay vì Line Messenger
- Thêm node để lưu log các email đã được xử lý
- Tùy chỉnh prompt tóm tắt để phù hợp với nhu cầu cụ thể của bạn
- Sử dụng nhiều model AI khác nhau từ OpenRouter để so sánh kết quả tóm tắt

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quy trình đọc email, tóm tắt nội dung và gửi thông báo. Với việc tích hợp AI và các dịch vụ thông tin hiện đại, các sếp có thể tiết kiệm thời gian và tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!