---
title: "🚀 Xây dựng Trợ lý Nghiên cứu Chứng khoán Indonesia tự động với n8n, Gemini và Tavily"
description: "Hướng dẫn chi tiết triển khai workflow n8n tự động hóa tra cứu thị trường chứng khoán Indonesia, tích hợp AI Agent, Google Gemini, Supabase Vector Store và Telegram bot."
slug: "nghien-cuu-chung-khoan-indonesia-n8n-gemini-tavily"
tags: [n8n, automation, ai-agent, google-gemini, telegram, supabase]
keywords: [n8n workflow, trợ lý chứng khoán ai, google gemini n8n, tavily search, tự động hóa n8n]
---

# 🚀 Xây dựng Trợ lý Nghiên cứu Chứng khoán Indonesia tự động với n8n, Gemini và Tavily

Việc cập nhật thông tin, phân tích dữ liệu ngành và báo cáo tài chính từ thị trường chứng khoán (như IDX - Indonesia Stock Exchange) theo cách thủ công thường tốn rất nhiều thời gian và dễ bỏ lỡ các biến động thị trường quan trọng. 

Workflow này là một giải pháp tự động hóa toàn diện (All-in-one AI Research Agent) giúp các nhà đầu tư và chuyên gia tài chính tra cứu dữ liệu doanh nghiệp, phân tích nhóm ngành, tìm kiếm thông tin thời gian thực qua Web Search và trò chuyện trực tiếp qua **Telegram Bot**, **n8n Chat UI** hoặc **Webhook**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Dăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa kênh tương tác:** Hỗ trợ người dùng tra cứu qua Telegram, Native n8n Chat UI hoặc Custom Webhook.
- **AI Agent thông minh:** Sử dụng Google Gemini làm cốt lõi để phân tích câu hỏi, điều phối công việc cho các Sub-Agent chuyên biệt (Sectors App và Web Grounding).
- **Truy vấn dữ liệu chuyên sâu:** Tích hợp API Sectors App để lấy dữ liệu công ty, subsectors, báo cáo tài chính và dữ liệu giao dịch hàng ngày.
- **Kiểm chứng thông tin thời gian thực:** Kết hợp Tavily Web Search và Google Grounding để tìm kiếm tin tức mới nhất, đảm bảo tính chính xác cho các báo cáo đầu tư.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Hỗ trợ LangChain nodes).
- **Google Gemini API Key** (Dành cho Chat Model và Embeddings).
- **Supabase Account** (Lưu trữ Vector Store cho dữ liệu tài liệu doanh nghiệp).
- **Postgres Database** (Lưu trữ Chat Memory cho AI Agent).
- **Telegram Bot Token** (Nếu muốn sử dụng kênh Telegram).
- **Sectors App API Key & Tavily API Key** (Xác thực qua HTTP Header Auth).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n.
- Mở n8n Editor, chọn **Workflows** -> **Import from File** (hoặc paste trực tiếp mã JSON vào giao diện).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm hệ thống 37 nodes được chia thành các phân vùng logic rõ ràng. Các sếp cần cấu hình kỹ các điểm sau:
- **Google Gemini Chat Model / Embeddings:** Cấu hình `googlePalmApi` credentials cho toàn bộ các node Gemini (`Google Gemini Chat Model`, `Embeddings Google Gemini`, v.v.).
- **Postgres Chat Memory:** Kết nối database Postgres của các sếp để lưu lịch sử hội thoại (`Postgres Chat Memory`).
- **Supabase Vector Store:** Nhập URL và Service Role Key của Supabase để cấu hình `VectorStore-CompanyKnowledge` và `Supabase Vector Store`.
- **Telegram Trigger & Send a text message:** Thêm `telegramApi` credentials và cấu hình Bot Token.
- **HTTP Request Tools (Sectors App & Tavily):** Cấu hình `httpHeaderAuth` cho các node như `GetCompanies`, `GetSubsectors`, `GetDailyTransData`, `GetCompanyReport`, và `WebSeach - Tavily` với các API key tương ứng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) bằng cách gửi một câu hỏi mẫu qua Chat UI hoặc Telegram.
- Kiểm tra kết quả trả về từ Main Agent và các Sub-Agent.
- Bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết nối thêm Slack hoặc Discord Node để gửi các bản tin tóm tắt thị trường tự động định kỳ vào các khung giờ vàng.
- **Lưu lịch sử nghiên cứu:** Thiết lập thêm Google Sheets hoặc Airtable node để lưu lại các câu hỏi và báo cáo mà AI đã tạo ra, giúp dễ dàng tra cứu lại lịch sử phân tích.
- **Tùy biến Prompt cho Agent:** Tinh chỉnh system prompt trong `AI Agent` để phù hợp hơn với phong cách đầu tư cá nhân (ví dụ: tập trung vào cổ phiếu giá trị, cổ phiếu tăng trưởng hoặc phân tích kỹ thuật).

### 📌 Kết luận
Với workflow n8n kết hợp AI mạnh mẽ này, các sếp đã sở hữu ngay một "phòng phân tích tài chính" tự động thu nhỏ, giúp tiết kiệm hàng giờ tra cứu thủ công mỗi ngày. Hãy triển khai ngay hôm nay để nâng cấp năng lực đầu tư chứng khoán của mình!