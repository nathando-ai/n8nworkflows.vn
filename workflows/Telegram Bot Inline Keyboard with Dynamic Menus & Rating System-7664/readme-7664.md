---
title: "🤖 Tự động hóa Telegram Bot với Menu động và Hệ thống Đánh giá"
description: "Hướng dẫn chi tiết cách tự động hóa Telegram Bot với menu động, hệ thống đánh giá 1-5 sao và nhiều tính năng tương tác khác bằng n8n"
slug: "tu-dong-hoa-telegram-bot-menu-dong-danh-gia"
tags: [n8n, automation, no-code, telegram, chatbot]
keywords: [n8n workflow, tự động hóa, telegram bot, menu động, đánh giá]
---

# 🤖 Tự động hóa Telegram Bot với Menu động và Hệ thống Đánh giá

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý bot thủ công
- Cung cấp trải nghiệm tương tác cao cho người dùng
- Thu thập phản hồi khách hàng một cách hiệu quả
- Tự động hóa hoàn toàn quy trình tương tác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot token (hướng dẫn lấy ở phần dưới)
- Credentials Telegram trong n8n
- Kiến thức cơ bản về n8n workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7664)
2. Click vào nút "Import" và chọn "Import into n8n"
3. Hoặc copy JSON từ trang web và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **TG Trigger node**:
   - Cấu hình credentials Telegram
   - Đảm bảo bot token đã được kích hoạt trong Telegram

2. **Set Bot Token API KEY**:
   - Thay thế `[ADD YOU BOT TOKET IN SET NODE]` bằng bot token thực tế của bạn
   - Hướng dẫn lấy token:
     1. Mở Telegram
     2. Tìm kiếm @BotFather
     3. Gửi `/newbot` hoặc sử dụng bot hiện có
     4. Copy token nhận được

3. **Prepare Magic Response**:
   - Node này xử lý logic tạo menu động
   - Có thể tùy chỉnh các mục menu trong phần switch statement

4. **Is CALLBACK?**:
   - Node này kiểm tra xem tin nhắn đến có phải là callback (nhấn nút) hay không
   - Không cần cấu hình gì thêm

5. **Send to Telegram API**:
   - Node này gửi tin nhắn với menu động
   - Đảm bảo bot token đã được cấu hình đúng

6. **Answer Callback**:
   - Node này xử lý phản hồi khi người dùng nhấn nút
   - Đảm bảo node này luôn chạy để tránh loading vô hạn

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu
2. Kích hoạt workflow bằng cách bật toggle ON
3. Gửi tin nhắn đến bot để kiểm tra menu động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm tính năng lưu log các tương tác của người dùng
- Kết nối với Google Sheets để lưu trữ đánh giá
- Tạo báo cáo tự động về đánh giá hàng tuần
- Kết nối với Slack để thông báo khi có đánh giá mới

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh để tự động hóa Telegram Bot với menu động và hệ thống đánh giá. Các sếp có thể tùy chỉnh và mở rộng theo nhu cầu cụ thể của mình. Hãy thử ngay để nâng cao trải nghiệm tương tác với khách hàng!