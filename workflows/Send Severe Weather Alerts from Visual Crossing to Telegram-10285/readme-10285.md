---
title: "🌪️ Tự động cảnh báo thời tiết khẩn cấp từ Visual Crossing sang Telegram"
description: "Hướng dẫn tự động hóa cảnh báo thời tiết khẩn cấp hàng giờ từ Visual Crossing sang Telegram bằng n8n, giúp các sếp nhận thông báo kịp thời mà không cần theo dõi thủ công."
slug: "tu-dong-canh-bao-thoi-tiet-khan-cap-tu-visual-crossing-sang-telegram"
tags: [n8n, automation, no-code, weather, telegram]
keywords: [n8n workflow, tự động hóa thời tiết, cảnh báo khẩn cấp, Visual Crossing, Telegram]
---

# 🌪️ Tự động cảnh báo thời tiết khẩn cấp từ Visual Crossing sang Telegram

[Các sếp] có bao giờ phải theo dõi thời tiết hàng giờ để biết có cảnh báo khẩn cấp không? Với workflow này, các sếp sẽ tự động nhận thông báo thời tiết khẩn cấp từ Visual Crossing ngay trên Telegram mà không cần phải mở trang web hay ứng dụng thời tiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận cảnh báo thời tiết khẩn cấp kịp thời (mưa lớn, lốc xoáy, sét đánh...).
- Tiết kiệm thời gian theo dõi thời tiết thủ công.
- Nhận thông báo trên Telegram ngay lập tức.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Visual Crossing với API Key.
- Tài khoản Telegram và Bot Token.
- ID của kênh/nhóm Telegram muốn nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/10285).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Home Weather"**:
   - Thay đổi URL API để lấy dữ liệu thời tiết cho vị trí của các sếp.
   - Thêm API Key của Visual Crossing vào phần Headers (Authorization: Bearer [API_KEY]).

2. **Node "Check for Home Weather Alerts"**:
   - Kiểm tra và chỉnh sửa hàm JavaScript để lọc các cảnh báo thời tiết khẩn cấp phù hợp với nhu cầu.

3. **Node "Send Home Weather Alert"**:
   - Thêm Telegram Credentials (Bot Token và Chat ID).
   - Chỉnh sửa nội dung thông báo theo ý muốn.

4. **Node "Hourly Trigger"**:
   - Đảm bảo node này được cấu hình để chạy hàng giờ.

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu.
2. Bật Active workflow để bắt đầu nhận cảnh báo thời tiết khẩn cấp.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email để nhận cảnh báo thời tiết khẩn cấp qua email.
- Kết hợp với Slack để nhận thông báo trên Slack.
- Lưu log các cảnh báo thời tiết để theo dõi lịch sử.
- Thêm nhiều vị trí thời tiết để theo dõi.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc nhận cảnh báo thời tiết khẩn cấp từ Visual Crossing sang Telegram, tiết kiệm thời gian và đảm bảo an toàn. Hãy áp dụng ngay để không bỏ lỡ bất kỳ cảnh báo nào!