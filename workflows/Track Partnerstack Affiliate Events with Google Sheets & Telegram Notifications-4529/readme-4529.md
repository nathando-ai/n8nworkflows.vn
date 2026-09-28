---
title: "🚀 Theo dõi sự kiện liên kết Partnerstack với Google Sheets & Thông báo Telegram"
description: "Hướng dẫn tự động hóa theo dõi sự kiện liên kết Partnerstack, lưu dữ liệu vào Google Sheets và nhận thông báo Telegram - giải pháp tiết kiệm thời gian cho marketing team"
slug: "theo-doi-su-kien-lien-ket-partnerstack-voi-google-sheets-va-telegram"
tags: [n8n, automation, no-code, marketing, google-sheets]
keywords: [n8n workflow, tự động hóa marketing, theo dõi liên kết, Partnerstack, Google Sheets, Telegram]
---

# 🚀 Theo dõi sự kiện liên kết Partnerstack với Google Sheets & Thông báo Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của marketing team khi theo dõi thủ công các sự kiện liên kết. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu trữ dữ liệu sự kiện liên kết vào Google Sheets
- Nhận thông báo Telegram tức thì khi có sự kiện mới
- Giảm thiểu công việc thủ công và lỗi nhập liệu
- Theo dõi hiệu suất liên kết một cách chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Partnerstack với quyền truy cập Postbacks
- Tài khoản Google với quyền truy cập Google Sheets
- Tài khoản Telegram và ID chat để nhận thông báo
- API keys cho Google Sheets và Telegram
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4529)
2. Click vào nút "Import" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đảm bảo đường dẫn webhook duy nhất: `32a160b4-df74-447a-ab12-c98abe411862`
   - Phương thức HTTP: POST

2. **Node Append Row in Sheets**:
   - Thiết lập credentials Google Sheets OAuth2
   - Chọn Spreadsheet ID và Sheet Name phù hợp
   - Đảm bảo tài khoản Google có quyền chỉnh sửa bảng tính

3. **Node Set Chat Id**:
   - Thay thế giá trị mặc định bằng Telegram Chat ID của bạn
   - Đảm bảo bot Telegram có quyền gửi tin nhắn đến chat này

4. **Node Send Notification**:
   - Thiết lập credentials Telegram API
   - Tùy chỉnh nội dung thông báo theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Thiết lập Postback trong Partnerstack:
   - Truy cập Partnerstack > My account > Postbacks > Create a postback
   - Dán URL webhook của bạn
   - Đặt tên và chọn các sự kiện cần theo dõi
   - Lưu Postback

2. Test workflow:
   - Gửi một sự kiện test từ Partnerstack
   - Kiểm tra dữ liệu đã được lưu vào Google Sheets
   - Xác nhận thông báo Telegram đã nhận được

3. Bật Active workflow:
   - Chọn workflow trong n8n Editor
   - Click vào nút "Activate"

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Google Sheets để tạo báo cáo hàng tuần tự động
- Kết hợp với Slack để nhận thông báo bổ sung
- Thiết lập các quy tắc lọc sự kiện trong Telegram
- Tạo các báo cáo tùy chỉnh trong Google Sheets dựa trên dữ liệu sự kiện

### 📌 Kết luận
Workflow này giúp marketing team tự động hóa việc theo dõi và quản lý các sự kiện liên kết Partnerstack một cách hiệu quả. Bằng cách tích hợp Google Sheets và Telegram, các sếp có thể nhận được dữ liệu thời gian thực và thông báo tức thì, giúp tối ưu hóa chiến dịch marketing một cách chuyên nghiệp. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!