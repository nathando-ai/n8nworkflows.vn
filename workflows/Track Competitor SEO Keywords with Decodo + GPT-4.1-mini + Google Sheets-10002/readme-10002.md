---
title: "🚀 Theo dõi từ khóa SEO của đối thủ với Decodo + GPT-4.1-mini + Google Sheets"
description: "Tự động hóa nghiên cứu SEO đối thủ bằng cách thu thập từ khóa, phân tích bằng AI và lưu kết quả vào Google Sheets để theo dõi xu hướng"
slug: "theo-doi-tu-khoa-seo-doi-thu-voi-decodo-gpt41-mini-google-sheets"
tags: [n8n, automation, no-code, seo, ai]
keywords: [n8n workflow, tự động hóa, seo, từ khóa, google sheets]
---

# 🚀 Theo dõi từ khóa SEO của đối thủ với Decodo + GPT-4.1-mini + Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian nghiên cứu SEO đối thủ từ 80% trở lên
- Phân tích tự động các từ khóa quan trọng và xu hướng SEO
- Lưu trữ dữ liệu có cấu trúc trong Google Sheets cho phân tích dài hạn
- Theo dõi sự thay đổi của nội dung đối thủ theo thời gian
- Nhận được báo cáo chi tiết về sức mạnh SEO của đối thủ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ OpenAI (đặc biệt là model GPT-4.1-mini)
- API Key từ Decodo cho dịch vụ web scraping
- URL của trang web đối thủ cần phân tích
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "When clicking ‘Execute workflow’"**:
   - Đây là điểm khởi đầu của workflow. Các sếp có thể kích hoạt thủ công hoặc lập lịch chạy định kỳ.

2. **Node "Set the Input Fields"**:
   - Cấu hình các trường đầu vào cần thiết:
     - `url`: URL của trang web đối thủ cần phân tích
     - `geo`: Vị trí địa lý để phân tích (ví dụ: "US", "UK", "VN")

3. **Node "Decodo"**:
   - Cấu hình credentials cho Decodo API
   - Đảm bảo API key đã được kích hoạt và có quyền truy cập vào dịch vụ web scraping

4. **Node "OpenAI Chat Model for Keyword Analysis"**:
   - Cấu hình credentials cho OpenAI API
   - Chọn model "gpt-4o-mini" trong danh sách các model có sẵn
   - Đảm bảo tài khoản OpenAI có đủ credit để thực hiện các yêu cầu API

5. **Node "Google Sheets Append Row"**:
   - Cấu hình credentials cho Google Sheets API
   - Chọn spreadsheet và worksheet cụ thể để lưu trữ dữ liệu
   - Đảm bảo tài khoản Google có quyền chỉnh sửa spreadsheet đã chọn

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập lịch chạy định kỳ để theo dõi sự thay đổi của đối thủ hàng tuần
- Kết hợp với Slack/Telegram để nhận thông báo khi phát hiện thay đổi quan trọng
- Lưu log các lần chạy để kiểm tra lịch sử phân tích
- Tạo báo cáo định kỳ từ dữ liệu trong Google Sheets để chia sẻ với đội ngũ

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc nghiên cứu SEO đối thủ, giúp các sếp tiết kiệm thời gian và nhận được thông tin chi tiết về sức mạnh SEO của đối thủ. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào các chiến lược quan trọng hơn thay vì phải phân tích thủ công từng trang web.