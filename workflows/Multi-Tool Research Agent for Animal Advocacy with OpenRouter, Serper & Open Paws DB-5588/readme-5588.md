---
title: "🚀 Xây dựng Trợ lý Nghiên cứu AI Chuyên sâu cho Bảo vệ Động vật với n8n & OpenRouter"
description: "Hướng dẫn cấu hình workflow n8n Multi-Tool Research Agent tích hợp OpenRouter, Serper, Jina AI và Open Paws DB để tự động hóa nghiên cứu và phân tích."
slug: "multi-tool-research-agent-animal-advocacy-n8n"
tags: [n8n, automation, ai-agent, openrouter, vector-search]
keywords: [n8n workflow, ai agent research, open router gemini, serper api, open paws db, tự động hóa n8n]
---

# 🚀 Xây dựng Trợ lý Nghiên cứu AI Chuyên sâu cho Bảo vệ Động vật với n8n

Các nhà hoạt động xã hội, tổ chức phi lợi nhuận (NGO) thường gặp khó khăn lớn khi phải thủ công tìm kiếm thông tin, phân tích dữ liệu, quét mạng xã hội và đánh giá hiệu quả nội dung chiến dịch bảo vệ động vật. Việc này vừa tốn thời gian vừa thiếu tính hệ thống.

Workflow **Multi-Tool Research Agent for Animal Advocacy** được phát triển bởi **Open Paws** chính là giải pháp tự động hóa toàn diện. Đây là một agent đa năng (Multi-Tool Agent) giúp tự động tìm kiếm Google, quét trang web, truy vấn cơ sở dữ liệu chuyên ngành và chấm điểm văn bản bằng AI mà không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa nghiên cứu:** Kết hợp Serper API để tìm kiếm Google thông minh và Jina AI để quét nội dung trang web nhanh chóng.
- **Truy vấn tri thức chuyên ngành:** Kết nối trực tiếp với Open Paws Database thông qua tìm kiếm vector (vector search) sử dụng OpenAI Embeddings.
- **Đánh giá nội dung thông minh:** Tích hợp sub-workflow chấm điểm văn bản (Text Scoring) để dự đoán hiệu quả chiến dịch trên mạng xã hội hoặc email.
- **Đa kênh linh hoạt:** Hỗ trợ kích hoạt qua Chat Trigger hoặc qua các workflow khác (Execute Workflow Trigger).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **OpenRouter API Key** (dùng cho LLM `google/gemini-2.5-flash-preview`)
- **Serper API Key** (dùng cho tìm kiếm web)
- **Jina AI API Key** (dùng cho Web Scraper Tool)
- **Scrapingdog API Key** (dùng cho Social Media Scrapers)
- **Hunter.io API Key** (dùng cho công cụ tìm & xác thực email)
- **OpenAI API Key** (dùng để tạo embeddings cho vector search)
- **Open Paws Database Public Key** (Khóa đọc cơ sở dữ liệu tri thức bảo vệ động vật)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow chính và upload sub-workflow **"Score Text"** lên instance n8n của các sếp.
- Import file JSON của workflow chính vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các Credentials quan trọng sau trong n8n:

- **OpenRouter Chat Model & OpenRouter Chat Model1:** Chọn credential `openRouterApi` và đảm bảo model đang trỏ tới `google/gemini-2.5-flash-preview`.
- **Database Retrieval (HTTP Request):** Sử dụng `HTTP Custom Auth` với hai header:
  ```json
  {
    "headers": {
      "Authorization": "Bearer INSERT_OPEN_PAWS_PUBLIC_KEY",
      "X-OpenAI-Api-Key": "INSERT_OPEN_AI_API_KEY"
    }
  }
  ```
- **Serper API (HTTP Request):** Sử dụng `HTTP Header Auth` với header `X-API-KEY`.
- **Web Scraper Tool (Jina AI):** Sử dụng `HTTP Header Auth` với header `Authorization: Bearer YOUR_JINA_AI_KEY`.
- **Social Media Scrapers (Twitter, Instagram, LinkedIn):** Sử dụng `HTTP Query Auth` với tham số `api_key: YOUR_SCRAPING_DOG_API_KEY`.
- **Email Finder & Email Verifier:** Sử dụng native credential loại `hunterApi`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử qua **When chat message received** (Chat Trigger) để kiểm tra phản hồi từ Agent.
- Sau khi kiểm tra các công cụ (Tools) hoạt động trơn tru, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Telegram/Slack:** Thêm node Telegram hoặc Slack ở đầu và cuối workflow để tạo bot tư vấn trực tiếp trên nhóm chat của tổ chức.
- **Mở rộng nguồn dữ liệu:** Tích hợp thêm Google Sheets hoặc Airtable để lưu trữ lại lịch sử các câu hỏi nghiên cứu và kết quả phân tích của Agent.
- **Tự động hóa định kỳ:** Thay thế Chat Trigger bằng Schedule Trigger để tự động tổng hợp tin tức nóng hổi về bảo vệ động vật mỗi sáng.

### 📌 Kết luận
Workflow **Multi-Tool Research Agent** là một mô hình kiến trúc AI agentic cực kỳ mạnh mẽ và modular. Việc áp dụng automation này giúp tiết kiệm hàng tá giờ làm việc thủ công, nâng cao chất lượng chiến dịch và tối ưu hóa nguồn lực cho các tổ chức hướng tới cộng đồng. Chúc các sếp cài đặt thành công!