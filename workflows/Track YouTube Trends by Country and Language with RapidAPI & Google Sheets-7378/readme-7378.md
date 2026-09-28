---
title: "📊 Theo dõi xu hướng YouTube theo quốc gia và ngôn ngữ với RapidAPI & Google Sheets"
description: "Tự động hóa việc theo dõi xu hướng YouTube theo quốc gia và ngôn ngữ, lưu kết quả vào Google Sheets một cách nhanh chóng và chính xác."
slug: "theo-doi-xu-huong-youtube-theo-quoc-gia-va-ngon-ngu"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, youtube trends, google sheets, rapidapi]
---

# 📊 Theo dõi xu hướng YouTube theo quốc gia và ngôn ngữ với RapidAPI & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình trạng phải theo dõi xu hướng YouTube theo quốc gia và ngôn ngữ một cách thủ công, tốn nhiều thời gian và công sức. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách nhanh chóng và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức khi theo dõi xu hướng YouTube.
- Dữ liệu được lưu trữ và quản lý một cách chính xác trên Google Sheets.
- Tự động hóa toàn bộ quá trình, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để kết nối với Google Sheets.
- API Key từ RapidAPI để truy cập YouTube Trend Finder API.
- Biết cách tạo và cấu hình form trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **On form submission**: Cấu hình form để nhập `country` và `language`.
- **Trend Finder API Request**: Cấu hình API Key từ RapidAPI và các tham số cần thiết.
- **Re format output**: Cấu hình code để trích xuất và định dạng dữ liệu từ API response.
- **Google Sheets**: Cấu hình tài khoản Google và tên sheet để lưu trữ dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có xu hướng mới.
- Lưu log các lần chạy workflow để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về xu hướng YouTube cho các bộ phận liên quan.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi xu hướng YouTube một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và công sức!