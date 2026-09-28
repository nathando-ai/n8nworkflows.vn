---
title: "🚀 Theo dõi tín hiệu tuyển dụng LinkedIn với Bright Data, OpenAI, Airtable, HubSpot và Slack"
description: "Tự động hóa việc theo dõi tuyển dụng LinkedIn, phân tích tín hiệu tuyển dụng bằng AI và đồng bộ dữ liệu với HubSpot và Slack"
slug: "theo-doi-tin-hieu-tuyen-dung-linkedin-voi-n8n"
tags: [n8n, automation, no-code, LinkedIn, AI, HubSpot, Slack]
keywords: [n8n workflow, tự động hóa, LinkedIn, AI, HubSpot, Slack]
---

# 🚀 Theo dõi tín hiệu tuyển dụng LinkedIn với Bright Data, OpenAI, Airtable, HubSpot và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho việc theo dõi tuyển dụng trên LinkedIn hàng ngày
- Phân tích tự động tín hiệu tuyển dụng bằng AI, giúp xác định cơ hội kinh doanh tiềm năng
- Đồng bộ dữ liệu với HubSpot để quản lý cơ hội kinh doanh hiệu quả hơn
- Nhận thông báo tức thời trên Slack khi có tín hiệu tuyển dụng mới
- Tự động hóa quy trình từ việc thu thập dữ liệu đến tạo cơ hội kinh doanh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [Bright Data](https://brightdata.com) với Web Unlocker zone
- API key [OpenAI](https://platform.openai.com)
- Bảng [Airtable](https://airtable.com) với bảng `Searches` chứa các trường `LinkedIn URL`, `Active`, `Last Run`
- Tài khoản [HubSpot](https://hubspot.com)
- Workspace [Slack](https://slack.com)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15533](https://n8n.io/workflows/15533)
2. Click vào nút "Import" để tải xuống file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình thời gian chạy hàng ngày (mặc định là 9am)

2. **Get Active Searches**:
   - Kết nối với Airtable credentials
   - Chọn bảng `Searches` và cấu hình các trường cần thiết (`LinkedIn URL`, `Active`, `Last Run`)

3. **Scrape LinkedIn with Bright Data**:
   - Kết nối với Bright Data credentials
   - Đảm bảo đã cấu hình đúng Web Unlocker zone

4. **Extract Jobs (AI)** và **Score Signal & Draft Email**:
   - Kết nối với OpenAI credentials
   - Đảm bảo đã chọn đúng model (GPT-5.4-mini hoặc GPT-4o-mini)

5. **Create HubSpot Deal**:
   - Kết nối với HubSpot credentials
   - Cấu hình các trường dữ liệu cần thiết cho cơ hội kinh doanh

6. **Notify Slack**:
   - Kết nối với Slack credentials
   - Chọn kênh Slack để nhận thông báo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Discord, Teams, Telegram để nhận thông báo
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Tự động gửi báo cáo hàng tuần về các tín hiệu tuyển dụng mới
- Tích hợp với các công cụ CRM khác như Salesforce, Pipedrive, Attio, Close, Notion...
- Sử dụng các model LLM khác như Claude, Gemini, Mistral, Groq...

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi tuyển dụng trên LinkedIn, phân tích tín hiệu tuyển dụng bằng AI và đồng bộ dữ liệu với HubSpot và Slack. Với việc áp dụng workflow này, các sếp có thể tiết kiệm thời gian và công sức, đồng thời tăng hiệu quả trong việc quản lý cơ hội kinh doanh.