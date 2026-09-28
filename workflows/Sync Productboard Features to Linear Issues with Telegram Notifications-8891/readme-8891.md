---
title: "🚀 Tự động đồng bộ Features từ Productboard sang Linear với thông báo Telegram"
description: "Hướng dẫn chi tiết cách tự động đồng bộ Features từ Productboard sang Linear và gửi thông báo Telegram khi có Feature mới được tạo. Tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ Feature quan trọng nào."
slug: "tu-dong-dong-bo-features-tu-productboard-sang-linear-voi-thong-bao-telegram"
tags: [n8n, automation, no-code, productboard, linear, telegram]
keywords: [n8n workflow, tự động hóa, productboard, linear, telegram, đồng bộ dữ liệu]
---

# 🚀 Tự động đồng bộ Features từ Productboard sang Linear với thông báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi và quản lý Features từ nhiều nền tảng khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để đồng bộ dữ liệu giữa Productboard và Linear, đồng thời gửi thông báo Telegram khi có Feature mới được tạo.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ Features từ Productboard sang Linear mà không cần can thiệp thủ công.
- Đảm bảo không bỏ sót: Chỉ các Features mới được tạo mới được đồng bộ, tránh lặp lại dữ liệu cũ.
- Thông báo tức thì: Nhận thông báo Telegram ngay khi có Feature mới được đồng bộ, giúp quản lý dự án hiệu quả hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Productboard và API Key để truy cập dữ liệu Features.
- Tài khoản Linear và API Key để tạo Issues.
- Tài khoản Telegram và Bot Token để gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **📅 Schedule Trigger**: Cấu hình thời gian chạy workflow (ví dụ: hàng ngày lúc 9h sáng).
- **🌐 HTTP Request to Productboard**: Cấu hình API Key và URL để truy cập dữ liệu Features từ Productboard.
- **💻 Code (Transform Features)**: Chỉnh sửa mã JavaScript để xử lý dữ liệu từ Productboard (loại bỏ HTML, định dạng ngày tháng, trích xuất các trường quan trọng).
- **⚖️ If (Filter New Features)**: Cấu hình điều kiện để chỉ đồng bộ các Features mới được tạo.
- **📝 Create Linear Issue**: Cấu hình API Key và Team ID trong Linear để tạo Issues.
- **📢 Success Notification (Telegram)**: Cấu hình Bot Token và Chat ID trong Telegram để gửi thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để gửi thông báo cùng lúc.
- Lưu log các Features đã được đồng bộ để theo dõi lịch sử.
- Gửi báo cáo định kỳ về số lượng Features đã được đồng bộ.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian và đảm bảo không bỏ sót bất kỳ Feature quan trọng nào. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý dự án của bạn!