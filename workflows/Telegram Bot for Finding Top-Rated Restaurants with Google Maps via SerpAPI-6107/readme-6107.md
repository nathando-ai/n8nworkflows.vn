---
title: "🍽️ Tự động tìm nhà hàng hàng đầu bằng Telegram Bot với Google Maps qua SerpAPI"
description: "Hướng dẫn chi tiết cách tự động tìm và gửi thông tin 5 nhà hàng hàng đầu theo khu vực yêu cầu thông qua Telegram Bot, kết hợp Google Maps và SerpAPI"
slug: "tu-dong-tim-nha-hang-hang-dau-bang-telegram-bot"
tags: [n8n, automation, no-code, telegram, google-maps]
keywords: [n8n workflow, tự động hóa, telegram bot, tìm nhà hàng, google maps, serpapi]
---

# 🍽️ Tự động tìm nhà hàng hàng đầu bằng Telegram Bot với Google Maps qua SerpAPI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tìm kiếm thủ công
- Nhận thông tin nhà hàng hàng đầu một cách nhanh chóng
- Tự động hóa quy trình tìm kiếm nhà hàng
- Kết quả được gửi trực tiếp đến Telegram
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot Telegram
- API key từ SerpAPI
- Tên quốc gia (ví dụ: Egypt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6107)
2. Copy nội dung JSON của workflow
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán nội dung JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Chọn credentials "telegramApi"
   - Đảm bảo bot Telegram đã được cấu hình đúng

2. **Parse Area**:
   - Node này xử lý đầu vào từ người dùng
   - Không cần cấu hình thêm

3. **Find Restaurants (SerpAPI)**:
   - Node này sử dụng SerpAPI để tìm kiếm nhà hàng
   - Cần cấu hình API key từ SerpAPI
   - Tham số quan trọng: `q` (từ khóa tìm kiếm) và `location` (khu vực)

4. **Geocode (Nominatim)**:
   - Node này chuyển đổi khu vực thành tọa độ bản đồ
   - Không cần cấu hình thêm

5. **Format Reply**:
   - Node này chuẩn bị nội dung phản hồi
   - Không cần cấu hình thêm

6. **Send to Telegram**:
   - Node này gửi kết quả đến Telegram
   - Chọn credentials "telegramApi"

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo
- Lưu log tìm kiếm để theo dõi lịch sử
- Gửi báo cáo định kỳ về các nhà hàng hàng đầu
- Tích hợp với Google Sheets để lưu trữ dữ liệu

### 📌 Kết luận
Workflow này giúp các sếp tự động tìm kiếm và nhận thông tin về 5 nhà hàng hàng đầu một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả công việc!