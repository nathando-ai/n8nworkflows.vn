---
title: "🚀 Tự động hóa Enrich và Score Leads với Claude AI, PDL và Perplexity"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình làm giàu dữ liệu (enrichment), nghiên cứu khách hàng và chấm điểm lead bằng AI, giúp tiết kiệm 95% thời gian."
slug: "tu-dong-hoa-enrich-va-score-leads-voi-claude-ai-pdl-perplexity"
tags: [n8n, automation, ai-agent, claude-ai, crm, lead-generation]
keywords: [n8n workflow, enrich leads, score leads, claude ai, perplexity, people data labs, hubspot automation]
---

# 🚀 Tự động hóa Enrich và Score Leads với Claude AI, PDL và Perplexity

Chào các sếp! Việc nghiên cứu thủ công thông tin khách hàng tiềm năng (lead research), đối chiếu chân dung khách hàng lý tưởng (ICP) và chấm điểm lead đang ngốn của đội ngũ Sales bao nhiêu thời gian mỗi ngày? Trung bình mất từ 15-20 phút cho mỗi lead, dẫn đến việc phản hồi chậm trễ và bỏ lỡ cơ hội vàng.

Đừng lo, workflow n8n cực kỳ mạnh mẽ mang tên **"Enrich and Score Leads Automatically with Claude AI, PDL and Perplexity"** do tác giả Connor Provines phát triển sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong 30-60 giây mỗi lead, với chi phí siêu rẻ chỉ từ $0.08 - $0.15/lead!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ xử lý thần tốc:** Chỉ mất 30-60 giây để enrich, nghiên cứu sâu và phân loại lead thay vì 20 phút làm tay.
- **Phân loại thông minh (Routing):** 
  - *Hot Leads (Điểm 8-10):* Bắn thông báo tức thì qua Slack kèm bản nháp email cá nhân hóa.
  - *Warm Leads (Điểm 5-7):* Gom vào kênh Slack digest để chăm sóc sau.
  - *Cold Leads (Điểm 0-4):* Tự động đẩy vào CRM để lưu trữ.
- **Chấm điểm chuẩn xác:** Dựa trên tiêu chí ICP (Ideal Customer Profile) thực tế của doanh nghiệp nhờ sức mạnh của AI Agent (Claude Sonnet).
- **Hoạt động 24/7:** Tự động bắt sự kiện từ Webhook bất cứ lúc nào có lead mới đăng ký.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
Các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted trên VPS).
- **People Data Labs (PDL) API Key:** Dùng cho node `PDL Enrich` (hoặc dùng Apollo/Clearbit thay thế).
- **Perplexity API Key:** Dùng cho node `Individual Research` và `Company Research`.
- **Anthropic API Key:** Dùng cho node `Anthropic Chat Model` (Claude 4 Sonnet).
- **Google Gemini API Key (Google Palm API):** Dùng cho các node format nội dung (`GoogleGemini`).
- **Google Docs API & OAuth2:** Chứa file tài liệu quy tắc ICP (`ICP & Use Case`).
- **Slack OAuth2 API:** Gửi tin nhắn cảnh báo Hot/Warm lead.
- **Gmail OAuth2:** Gửi email chăm sóc lead nóng.
- **Apify Account (Tùy chọn):** Scrape profile LinkedIn (`LinkedIn Profile Scraper`).
- **HubSpot CRM (Tùy chọn):** Đồng bộ dữ liệu lead (`Upsert to HubSpot CRM`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy đoạn JSON gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình chính xác các điểm mấu chốt sau:
- **Node `Webhook`**: Kiểm tra đường dẫn path mặc định (`lead-intake`) và phương thức `POST`. Đây là điểm nhận dữ liệu đầu vào với định dạng JSON mẫu:
  ```json
  {"email": "lead@company.com", "name": "Optional Name"}
  ```
- **Node `PDL Enrich`**: Cần tạo Header Auth credential với:
  - Tên Header: `X-Api-Key`
  - Giá trị: API Key của People Data Labs.
- **Node `ICP & Use Case`**: Thay thế đường dẫn `documentURL` mặc định thành link Google Doc chứa quy tắc ICP và Use Case của công ty các sếp.
- **AI & LLM Nodes (`Anthropic Chat Model`, `GoogleGemini`)**: Thêm credentials tương ứng cho Anthropic (Claude) và Google Gemini.
- **Nodes Thông báo & CRM (`Send Hot Lead Slack Alert`, `Send Hot Lead Email`, `Upsert to HubSpot CRM`)**: Kết nối tài khoản Slack workspace, cấu hình kênh nhận tin, kết nối tài khoản Gmail cá nhân/doanh nghiệp và kết nối HubSpot CRM (hoặc Salesforce/Pipedrive tùy chọn).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi một request POST mẫu qua Postman hoặc cURL đến Webhook URL để test thử.
- Sau khi test thành công và dữ liệu chảy qua các nhánh mượt mà, gạt công tắc sang **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Ngoài Slack, các sếp có thể nhân bản node thông báo sang Telegram để đội ngũ sales nhận ping trên điện thoại nhanh hơn.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets trước hoặc sau node CRM để lưu lại lịch sử toàn bộ lead đã quét nhằm làm báo cáo tuần/tháng.
- **Tối ưu chi phí AI:** Tùy chỉnh tham số token trong Claude AI Agent để cân bằng giữa độ chi tiết của nghiên cứu và chi phí API.

### 📌 Kết luận
Workflow tự động hóa này là một "vũ khí bí mật" giúp tối ưu hóa phễu bán hàng (Sales Funnel) ngay từ những bước đầu tiên. Thay vì để nhân sự tốn hàng giờ cào dữ liệu thủ công, hãy để AI và các công cụ tự động làm thay bạn việc đó. Chúc các sếp cài đặt thành hình và chốt thật nhiều deal lớn!