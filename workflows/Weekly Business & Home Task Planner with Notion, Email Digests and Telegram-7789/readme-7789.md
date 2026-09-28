---
title: "🚀 Tự động hóa kế hoạch công việc hàng tuần với Notion, Email và Telegram"
description: "Workflow n8n giúp tự động tổng hợp và gửi kế hoạch công việc hàng tuần từ Notion, email và Telegram một cách hoàn toàn không cần code."
slug: "tu-dong-hoa-ke-hoach-cong-viec-hang-tuan-notion-email-telegram"
tags: [n8n, automation, no-code, notion, telegram]
keywords: [n8n workflow, tự động hóa, kế hoạch công việc, notion, telegram]
---

# 🚀 Tự động hóa kế hoạch công việc hàng tuần với Notion, Email và Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng việc quản lý và theo dõi công việc hàng tuần thường tốn nhiều thời gian và dễ gây nhầm lẫn? Với workflow này, các sếp có thể tự động tổng hợp và gửi kế hoạch công việc hàng tuần từ Notion, email và Telegram một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động tổng hợp và gửi kế hoạch công việc hàng tuần.
- Chính xác: Dữ liệu được lấy từ Notion, đảm bảo tính chính xác cao.
- Cá nhân hóa: Kế hoạch công việc được gửi đến từng người theo yêu cầu.
- Hoạt động liên tục: Workflow chạy tự động hàng tuần, không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Notion với danh sách công việc hàng tuần.
- Tài khoản email để gửi và nhận kế hoạch công việc.
- Tài khoản Telegram để nhận thông báo.
- API keys cho Notion, email và Telegram.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Weekly Cron**: Cấu hình lịch chạy hàng tuần (ví dụ: mỗi Chủ Nhật lúc 8h sáng).
- **Manual Trigger**: Sử dụng để kiểm tra workflow trước khi chạy tự động.
- **Set: User Config**: Cấu hình các thông số như email người nhận, ID Notion, Telegram chat ID.
- **Function: Sample Tasks**: Chỉnh sửa danh sách công việc mẫu nếu không sử dụng Notion.
- **If: Notion Enabled?**: Kích hoạt hoặc vô hiệu hóa việc lấy dữ liệu từ Notion.
- **Notion: Get Tasks**: Cấu hình API key và ID Notion để lấy dữ liệu.
- **Function: Extract Notion Tasks**: Chỉnh sửa hàm để trích xuất dữ liệu từ Notion.
- **Function: Build Weekly Plan**: Chỉnh sửa hàm để xây dựng kế hoạch công việc hàng tuần.
- **Email: Send to You**: Cấu hình email người nhận và nội dung email.
- **If: Partner Enabled?**: Kích hoạt hoặc vô hiệu hóa việc gửi email cho đối tác.
- **Email: Send to Partner**: Cấu hình email đối tác và nội dung email.
- **If: Telegram Enabled?**: Kích hoạt hoặc vô hiệu hóa việc gửi thông báo Telegram.
- **Telegram: Notify**: Cấu hình API key và chat ID để gửi thông báo.
- **On Error**: Cấu hình để xử lý lỗi và gửi email thông báo lỗi.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để gửi thông báo công việc hàng tuần.
- Lưu log hoạt động của workflow để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về tiến độ công việc cho quản lý.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi trong việc quản lý công việc hàng tuần. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!