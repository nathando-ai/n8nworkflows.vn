---
title: "🚀 Tự động hóa tổng hợp thông tin công ty từ Glassdoor với Google Gemini và Bright Data"
description: "Hướng dẫn chi tiết cách tự động hóa việc thu thập và tổng hợp thông tin công ty từ Glassdoor bằng n8n, Google Gemini và Bright Data Web Scraper. Tiết kiệm thời gian và nâng cao hiệu quả phân tích nhân sự."
slug: "tu-dong-hoa-tong-hop-thong-tin-cong-ty-glassdoor-voi-google-gemini-bright-data"
tags: [n8n, automation, no-code, AI, HR]
keywords: [n8n workflow, tự động hóa, Google Gemini, Bright Data, phân tích nhân sự]
---

# 🚀 Tự động hóa tổng hợp thông tin công ty từ Glassdoor với Google Gemini và Bright Data

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp HR khi phải thu thập và phân tích thông tin công ty từ nhiều nguồn khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian thu thập thông tin công ty từ nhiều nguồn khác nhau
- Tự động hóa quá trình tổng hợp thông tin bằng AI (Google Gemini)
- Nhận thông báo tức thời qua webhook khi có cập nhật mới
- Dễ dàng tích hợp với các hệ thống HR hiện có
- Tăng cường hiệu quả phân tích nhân sự với dữ liệu chính xác và cập nhật liên tục
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Bright Data với API key cho Web Scraper
- URL công ty trên Glassdoor
- Webhook URL để nhận thông báo (nếu cần)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Google Gemini Chat Model**:
   - Cấu hình credentials với Google Cloud API key
   - Đảm bảo tài khoản có đủ quota để sử dụng Google Gemini Flash Exp model

2. **HTTP Request to Glassdoor**:
   - Cấu hình credentials với Bright Data Web Scraper API key
   - Thay đổi URL công ty trong node này để thu thập dữ liệu từ Glassdoor

3. **Configure Webhook Notification** (nếu cần):
   - Cập nhật webhook URL để nhận thông báo khi có cập nhật mới
   - Thiết lập các thông số như method (POST), headers và body

4. **Summarization of Glassdoor Response**:
   - Điều chỉnh các tham số như chunk size và overlap nếu cần
   - Tùy chỉnh prompt cho quá trình tổng hợp nếu cần

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo tức thời
- Lưu log các lần chạy workflow để theo dõi hiệu suất
- Tự động gửi báo cáo định kỳ về tình hình công ty đến các bộ phận liên quan
- Tích hợp với các công cụ phân tích dữ liệu khác để tạo báo cáo chi tiết hơn

### 📌 Kết luận
Workflow này giúp các sếp HR tiết kiệm thời gian đáng kể trong việc thu thập và phân tích thông tin công ty từ Glassdoor. Bằng cách tự động hóa quá trình này với AI và Bright Data Web Scraper, các sếp có thể tập trung vào các nhiệm vụ quan trọng hơn trong quản lý nhân sự. Hãy thử ngay và nâng cao hiệu quả làm việc của đội ngũ HR!