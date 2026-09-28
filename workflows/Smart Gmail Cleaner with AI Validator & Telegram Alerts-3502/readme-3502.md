---
title: "🚀 Tự động xóa email rác với AI và cảnh báo Telegram - Giải pháp hoàn hảo cho người dùng Gmail"
description: "Workflow n8n tự động lọc và xóa email rác, spam với AI Gemini của Google, kết hợp cảnh báo Telegram - Tiết kiệm thời gian và giảm stress cho người dùng Gmail"
slug: "tu-dong-xoa-email-rac-voi-ai-va-canh-bao-telegram"
tags: [n8n, automation, no-code, gmail, telegram]
keywords: [n8n workflow, tự động hóa email, xóa email rác, AI Gemini, cảnh báo Telegram]
---

# 🚀 Tự động xóa email rác với AI và cảnh báo Telegram - Giải pháp hoàn hảo cho người dùng Gmail

[Các sếp] có biết rằng trung bình mỗi người dùng Gmail nhận khoảng 121 email rác mỗi ngày? Với workflow này, các sếp có thể tự động hóa quá trình lọc và xóa email rác, giảm thiểu thời gian và công sức thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lọc và xóa email rác, spam với độ chính xác cao nhờ AI Gemini của Google
- Nhận cảnh báo tức thì trên Telegram khi có email bị xóa
- Giảm thiểu thời gian và công sức thủ công trong việc quản lý hộp thư
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tiết kiệm thời gian quý giá cho các sếp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập đầy đủ
- API Key từ Google Cloud Platform để sử dụng Google Gemini
- Bot Telegram và Chat ID để nhận cảnh báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3502)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON vừa sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Gmail Get Email"**: Cần cấu hình credentials cho tài khoản Gmail của các sếp
- **Node "Google Gemini Chat Model"**: Cần cấu hình credentials với API Key từ Google Cloud Platform
- **Node "Telegram Sent Email Deleted Notification"**: Cần cấu hình credentials với Bot Token và Chat ID của Telegram
- **Node "AI Check Email"**: Cần điều chỉnh prompt để phù hợp với tiêu chí lọc email của các sếp
- **Node "Unwanted Email Output Parser"**: Cần cấu hình schema phù hợp với đầu ra của AI

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, các sếp nên test workflow với nút "Test workflow"
2. Kiểm tra kết quả trên Telegram để đảm bảo cảnh báo hoạt động đúng
3. Sau khi xác nhận hoạt động ổn định, các sếp có thể kích hoạt workflow bằng cách bật nút "Active"

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể kết hợp với các dịch vụ khác như Slack để nhận cảnh báo
- Có thể lưu log các email đã xóa vào Google Sheets để theo dõi lịch sử
- Có thể cấu hình gửi báo cáo định kỳ về số lượng email đã xóa qua email
- Có thể mở rộng để xử lý các loại email khác như email quảng cáo, email khuyến mãi...

### 📌 Kết luận
Workflow "Smart Gmail Cleaner with AI Validator & Telegram Alerts" là giải pháp hoàn hảo cho các sếp muốn tự động hóa việc quản lý hộp thư Gmail. Với sự kết hợp của AI Gemini và Telegram, các sếp có thể tiết kiệm thời gian quý giá và giảm thiểu stress khi quản lý email hàng ngày. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!