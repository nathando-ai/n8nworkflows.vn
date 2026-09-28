---
title: "🚀 Tự động quét Lead doanh nghiệp từ Google Maps bằng Apify, GPT-4o-mini và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động hóa trích xuất dữ liệu doanh nghiệp từ Google Maps sử dụng Apify, làm sạch dữ liệu trùng lặp, dùng AI trích xuất email từ website và lưu trữ vào Google Sheets 100% tự động."
slug: "tu-dong-quet-lead-google-maps-apify-gpt4-google-sheets"
tags: [n8n, automation, apify, openai, google-sheets, lead-generation]
keywords: [n8n workflow, quét lead google maps, apify google maps scraper, gpt-4o-mini trích xuất email, tự động hóa lead generation]
---

# 🚀 Tự động quét Lead doanh nghiệp từ Google Maps bằng Apify, GPT-4o-mini và Google Sheets

Các sếp có đang mệt mỏi vì phải ngồi copy-paste thông tin doanh nghiệp, tìm kiếm số điện thoại, website và email từ Google Maps một cách thủ công? Việc này vừa tốn hàng chục giờ đồng hồ, vừa dễ xảy ra sai sót và bỏ lỡ nhiều khách hàng tiềm năng chất lượng.

Đừng lo! Workflow n8n siêu cấp này từ **SpaGreen Creative** sẽ giúp các sếp tự động hóa toàn bộ quy trình: Từ việc cào dữ liệu Google Maps thông qua **Apify**, loại bỏ dữ liệu trùng lặp (`Remove Duplicates`), sử dụng **OpenAI (GPT-4o-mini)** để phân tích website trích xuất email và tạo mô tả doanh nghiệp, cho đến việc lưu trữ gọn gàng vào **Google Sheets** và gửi thông báo cáo qua Telegram/Slack/Teams.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh tra cứu thủ công từng quán ăn, công ty, cửa hàng trên Google Maps.
- **Dữ liệu sạch & chuẩn hóa:** Tự động lọc bỏ các kết quả trùng lặp nhờ node `Remove Duplicates`.
- **Sức mạnh AI thông minh:** Sử dụng OpenAI để cào HTML website, trích xuất chính xác email doanh nghiệp và tự viết mô tả ngắn gọn về công ty.
- **Đồng bộ hóa tức thì:** Toàn bộ thông tin (Tên, Địa chỉ, SĐT, Website, Email, Mô tả) được lưu tự động vào Google Sheets và thông báo qua Telegram/Slack.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Apify Account & API Token:** Tài khoản Apify để chạy công cụ cào Google Maps (`Google Maps Scraper` actor).
- **OpenAI API Key:** Để sử dụng các node GPT-4o-mini trích xuất email và tạo mô tả doanh nghiệp.
- **Google Sheets:** Tài khoản Google có quyền truy cập Google Drive/Sheets để lưu trữ leads.
- **Kênh thông báo (Tùy chọn):** Telegram Bot Token & Chat ID, Slack, hoặc Microsoft Teams để nhận thông báo tiến trình.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình canvas của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các credentials và tham số quan trọng sau tại các node tương ứng:

- **Apify Nodes (`Get list of actors`, `Get list of tasks`, `HTTP (Run Scraper Task)`):**
  - Thêm `apifyApi` credentials với API Token của sếp.
  - Kiểm tra lại actor ID của Google Maps Scraper (`compass/crawler-google-places`) để đảm bảo task chạy đúng mục tiêu tìm kiếm.
- **OpenAI Nodes (`Extract Business Email from Website HTML (GPT-4)`, `AI Company Description Generator`):**
  - Cấu hình `openAiApi` credentials.
  - Chọn model phù hợp (khuyên dùng `gpt-4o-mini` để tối ưu chi phí và tốc độ).
- **Google Sheets Nodes (`Sheet (Store google maps/lead data)`, `Sheet (Update Email form website)`):**
  - Kết nối `googleSheetsOAuth2Api`.
  - Trỏ đến file Google Sheet chuẩn bị sẵn và chọn đúng Sheet Name để lưu thông tin Lead và Email.
- **Notification Nodes (`Notification message` - Telegram / Slack / Microsoft Teams):**
  - Thêm credentials tương ứng và điền Chat ID / Channel ID để nhận báo cáo khi hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** bằng node `Start by clicking` (Manual Trigger) với một vài từ khóa mẫu để test hệ thống.
- Sau khi kiểm tra dữ liệu trả về trong Google Sheets chính xác, hãy gạt công tắc sang **Active** để bật chế độ chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh chăm sóc:** Kết hợp thêm node Rapiwa (WhatsApp) hoặc Telegram để tự động gửi tin nhắn chào hàng (Cold Outreach) ngay sau khi quét được thông tin lead.
- **Lưu trữ nâng cao:** Thay vì Google Sheets, các sếp có thể chuyển hướng lưu vào CRM như HubSpot, Notion hoặc Airtable để dễ dàng quản lý pipeline bán hàng.
- **Lên lịch định kỳ (Cron):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để hệ thống tự động quét lead mới theo tuần hoặc theo tháng một cách hoàn toàn tự động.

### 📌 Kết luận
Workflow "Extract Google Maps business leads with Apify, GPT-4o-mini and Google Sheets" là vũ khí cực mạnh cho các đội ngũ Sales và Marketing thời đại số. Hãy cài đặt ngay hôm nay để tối ưu hóa phễu tìm kiếm khách hàng và bứt phá doanh số cho doanh nghiệp của các sếp!