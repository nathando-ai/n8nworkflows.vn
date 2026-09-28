---
title: "🚀 Tự động hóa cảnh báo UptimeRobot lên Telegram với hình ảnh xác minh"
description: "Hướng dẫn tự động hóa cảnh báo UptimeRobot lên Telegram với hình ảnh xác minh, tiết kiệm thời gian và nâng cao hiệu quả giám sát website"
slug: "tu-dong-hoa-canh-bao-uptimerobot-len-telegram-voi-hinh-anh-xac-minh"
tags: [n8n, automation, no-code, uptimerobot, telegram]
keywords: [n8n workflow, tự động hóa, uptimerobot, telegram, giám sát website]
---

# 🚀 Tự động hóa cảnh báo UptimeRobot lên Telegram với hình ảnh xác minh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải theo dõi nhiều website và phải xử lý cảnh báo thủ công từ UptimeRobot. Việc này tốn thời gian và có thể dẫn đến sai sót. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình, từ nhận cảnh báo đến gửi thông báo lên Telegram kèm hình ảnh xác minh, giúp giám sát website hiệu quả hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý cảnh báo thủ công
- Nâng cao hiệu quả giám sát website với hình ảnh xác minh
- Nhận thông báo tức thì trên Telegram
- Tự động hóa toàn bộ quy trình giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để nhận cảnh báo từ UptimeRobot
- API key từ UptimeRobot
- Tài khoản Telegram và bot token
- (Tùy chọn) Tài khoản ScreenshotMachine để chụp hình ảnh xác minh
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Gmail Trigger**: Cấu hình tài khoản Gmail để nhận cảnh báo từ UptimeRobot. Thiết lập thời gian kiểm tra (mặc định là mỗi 5 phút).
- **Extract ID and URL**: Node này sẽ trích xuất URL và ID của monitor từ email cảnh báo của UptimeRobot. Không cần cấu hình gì thêm.
- **Get many monitors**: Cấu hình API key từ UptimeRobot để lấy thông tin chi tiết về monitor.
- **Conf**: Thiết lập các tham số cấu hình cho workflow, bao gồm việc bật/tắt chụp hình ảnh và các tham số chụp hình ảnh.
- **Screenshotmachine-secret**: Cấu hình tài khoản ScreenshotMachine để chụp hình ảnh xác minh.
- **Send a text message**: Cấu hình bot token và chat ID của Telegram để gửi thông báo văn bản.
- **Send a photo message**: Cấu hình bot token và chat ID của Telegram để gửi hình ảnh xác minh.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo trên cả hai nền tảng.
- Lưu log các cảnh báo để theo dõi lịch sử.
- Gửi báo cáo định kỳ về trạng thái của các website được giám sát.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình giám sát website, từ nhận cảnh báo đến gửi thông báo lên Telegram kèm hình ảnh xác minh. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả giám sát website.