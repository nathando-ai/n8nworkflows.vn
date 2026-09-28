---
title: "📊 Theo dõi lượt tải npm qua Telegram: Tự động hóa báo cáo và cảnh báo"
description: "Hướng dẫn tự động hóa theo dõi lượt tải npm qua Telegram với báo cáo hàng tuần, hàng tháng và cảnh báo mốc quan trọng - giải pháp tiết kiệm thời gian cho nhà phát triển và quản lý dự án"
slug: "theo-doi-luot-tai-npm-qua-telegram"
tags: [n8n, automation, no-code, npm, telegram, developer-tools]
keywords: [n8n workflow, tự động hóa, npm downloads, telegram bot, developer analytics]
---

# 📊 Theo dõi lượt tải npm qua Telegram: Tự động hóa báo cáo và cảnh báo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà phát triển khi phải theo dõi thủ công lượt tải npm. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 20+ giờ mỗi tháng với báo cáo tự động
- Nhận cảnh báo tức thì khi gói vượt mốc quan trọng
- Theo dõi xu hướng sử dụng gói hàng tuần/tháng
- Tăng nhận thức về hiệu suất gói trong cộng đồng
- Tự động phát hiện gói mới khi phát hành
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản npm với các gói cần theo dõi
- Telegram bot token (tạo qua BotFather)
- ID chat Telegram để nhận báo cáo
- Tài khoản n8n (Cloud hoặc Self-hosted)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/13945)
2. Chọn "Import" và sao chép JSON vào n8n Editor
3. Hoặc tải file JSON về và import qua n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Telegram Trigger"**:
   - Thêm credentials "telegramApi" với bot token của bạn
   - Đảm bảo bot có quyền gửi tin nhắn đến chat của bạn

2. **Node "Fetch Trending", "Fetch Monthly Digest", "Check Milestones"**:
   - Thay đổi biến `NPM_USERNAME` thành tên người dùng npm của bạn
   - Tùy chỉnh mảng `MILESTONES` trong node "Check Milestones" để đặt các mốc cảnh báo

3. **Các node gửi Telegram (Send Trending, Send Weekly Digest...)**:
   - Cập nhật `chatId` trong các node này để gửi báo cáo đến đúng chat

4. **Lịch trình (Schedule Triggers)**:
   - Điều chỉnh thời gian trong các node "1st of Month 6PM", "Every Friday 6PM", "Milestone (daily check 9AM)" nếu cần

#### 3. Kích hoạt ⚡️
1. Chạy test với lệnh `/help` để kiểm tra bot hoạt động
2. Kích hoạt workflow và bắt đầu theo dõi

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack để nhận báo cáo cùng lúc
2. Thêm node lưu log vào Google Sheets để phân tích dài hạn
3. Tạo báo cáo định kỳ gửi email cho quản lý dự án
4. Mở rộng theo dõi thêm các chỉ số như số sao, số issue trên GitHub

### 📌 Kết luận
Workflow này biến theo dõi lượt tải npm từ công việc thủ công thành báo cáo tự động, giúp các sếp nhà phát triển tập trung vào phát triển sản phẩm hơn là theo dõi số liệu. Hãy thử ngay và tiết kiệm thời gian quý giá!