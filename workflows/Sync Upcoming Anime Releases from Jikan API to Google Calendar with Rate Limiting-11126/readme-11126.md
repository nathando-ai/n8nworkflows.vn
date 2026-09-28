---
title: "🎬 Tự động đồng bộ lịch phát sóng anime sắp tới vào Google Calendar với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc theo dõi lịch phát sóng anime của diễn viên lồng tiếng yêu thích và đồng bộ vào Google Calendar với n8n"
slug: "tu-dong-dong-bo-lich-phat-song-anime-google-calendar"
tags: [n8n, automation, anime, google calendar, personal productivity]
keywords: [n8n workflow, tự động hóa anime, google calendar, Jikan API, diễn viên lồng tiếng]
---

# 🎬 Tự động đồng bộ lịch phát sóng anime sắp tới vào Google Calendar với n8n

[Các sếp] có bao giờ muốn theo dõi lịch phát sóng anime của diễn viên lồng tiếng yêu thích mà không phải tự tay kiểm tra mỗi ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ tìm kiếm thông tin đến thêm sự kiện vào Google Calendar - hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra lịch phát sóng anime mỗi ngày
- **Chính xác**: Thông tin được cập nhật tự động từ Jikan API
- **Tiện lợi**: Sự kiện được thêm tự động vào Google Calendar của bạn
- **Tùy chỉnh**: Có thể theo dõi nhiều diễn viên lồng tiếng khác nhau
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar đã kích hoạt API
- Credentials Google Calendar OAuth2 trong n8n
- Tên diễn viên lồng tiếng cần theo dõi (ví dụ: "Mamoru Miyano")
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/11126)
2. Click vào nút "Copy Workflow to Clipboard"
3. Trong n8n Editor, click vào "Import from Clipboard" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Search Voice Actor"**:
   - Mở node này và chỉnh sửa tham số `q` thành tên diễn viên lồng tiếng cần theo dõi (ví dụ: "Mamoru Miyano")

2. **Node "Create an event"**:
   - Chọn credentials Google Calendar OAuth2 đã cấu hình
   - Có thể tùy chỉnh tên sự kiện, mô tả, v.v. theo ý muốn

3. **Node "Rate Limit Protection" và "Batch Rate Limit Wait"**:
   - Đảm bảo thời gian chờ (wait time) không bị thay đổi để tránh bị chặn bởi Jikan API

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate Workflow" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- **Theo dõi nhiều diễn viên**: Có thể sao chép và chỉnh sửa workflow cho từng diễn viên khác nhau
- **Thông báo nhắc nhở**: Kết hợp với Slack/Telegram để nhận thông báo khi có anime mới
- **Lưu log hoạt động**: Thêm node để lưu log các sự kiện đã được thêm vào Google Calendar
- **Tự động gửi báo cáo**: Tạo báo cáo hàng tuần về các anime sắp tới của diễn viên yêu thích

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi lịch phát sóng anime của diễn viên lồng tiếng yêu thích. Với việc tích hợp Google Calendar, các sếp có thể dễ dàng quản lý và nhận thông báo về các anime sắp tới một cách hiệu quả. Hãy thử ngay và tiết kiệm thời gian cho những việc quan trọng hơn nhé!