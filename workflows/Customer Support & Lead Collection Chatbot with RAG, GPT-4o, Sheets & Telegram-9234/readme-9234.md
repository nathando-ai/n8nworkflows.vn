---
title: "🚀 Xây dựng Chatbot Chăm sóc Khách hàng & Thu thập Lead tự động với RAG, GPT-4o, Google Sheets và Telegram"
description: "Hướng dẫn xây dựng chatbot AI thông minh ứng dụng RAG, GPT-4o để trả lời câu hỏi doanh nghiệp, tự động thu thập thông tin khách hàng và bắn thông báo về Telegram."
slug: "chatbot-cskh-rag-gpt4o-google-sheets-telegram"
tags: [n8n, automation, no-code, ai-agent, openai, telegram, google-sheets]
keywords: [n8n workflow, chatbot cskh, rag pinecone, gpt-4o n8n, thu thập lead tự động]
---

# 🚀 Xây dựng Chatbot Chăm sóc Khách hàng & Thu thập Lead tự động với RAG, GPT-4o, Google Sheets và Telegram

Các sếp có đang gặp tình trạng nhân sự quá tải vì phải trả lời những câu hỏi lặp đi lặp lại từ khách hàng (FAQs, giá cả, chính sách)? Việc bỏ lỡ các tin nhắn ngoài giờ hành chính có thể khiến doanh nghiệp mất đi những cơ hội ngàn vàng. 

Giải pháp cho các sếp đây: Một workflow n8n cực kỳ mạnh mẽ đóng vai trò như một **trợ lý ảo AI trực chiến 24/7**. Trợ lý này không chỉ tự động giải đáp mọi thắc mắc của khách hàng dựa trên dữ liệu thực tế của doanh nghiệp (RAG) mà còn khéo léo xin thông tin liên hệ (Lead) và đồng bộ ngay lập tức vào Google Sheets, đồng thời bắn thông báo chớp nhoáng về Telegram cho đội ngũ sale. Tất cả hoàn toàn tự động và không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Phản hồi khách hàng ngay lập tức bất kể ngày đêm, giảm tải 80% công việc cho đội ngũ support.
- **Chính xác tuyệt đối (RAG):** AI trả lời dựa trên kho tri thức thực tế của doanh nghiệp (Pinecone) thay vì "chém gió".
- **Thu thập Lead mượt mà:** Sau khi giải đáp xong, AI tự động chuyển hướng khéo léo để lấy thông tin Tên, Email, SĐT và nhu cầu của khách.
- **Báo cáo tức thì:** Đổ dữ liệu thẳng vào Google Sheets và gửi thông báo tóm tắt cuộc trò chuyện kèm contact về Telegram nhóm kinh doanh để chốt đơn nóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản OpenAI:** Lấy API Key (dùng cho GPT-4o và mô hình Embedding).
- **Tài khoản Pinecone:** Đã tạo Vector Index chứa dữ liệu tri thức của công ty (FAQs, tài liệu, chính sách, bảng giá...).
- **Google Sheets:** Tạo sẵn một file Google Sheet với các cột cơ bản: `Name`, `Email`, `Phone`, `Interested in`.
- **Telegram Bot:** Tạo bot qua `@BotFather`, lấy Bot Token và `chatId` của nhóm/cá nhân nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow này, dán trực tiếp vào n8n Editor hoặc import file JSON tải từ trang quản trị.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp nhớ cấu hình các node quan trọng sau:

- **AI Agent:** 
  - Thay thế cụm `[INSERT_YOUR_COMPANY_NAME_HERE]` trong system message bằng tên công ty thực tế của các sếp.
  - Tinh chỉnh giọng văn (prompt tone) cho phù hợp với văn hóa thương hiệu.
- **Main Chat Model & Company Answering Model:**
  - Chọn credentials `openAiApi`.
  - Đảm bảo model được chọn là `gpt-4o` (hoặc model LLM ưa thích khác).
- **Generate Embeddings (OpenAI) & Pinecone Vector Store (Company KB):**
  - Kết nối `openAiApi` credentials cho node Embedding.
  - Kết nối `pineconeApi` credentials và trỏ đúng tên Index/Namespace chứa dữ liệu công ty của các sếp.
- **Save Lead to Google Sheets:**
  - Chọn credentials `googleSheetsOAuth2Api`.
  - Trỏ đúng file Google Sheet ID và tên Sheet (Tab) đã chuẩn bị. Map các trường dữ liệu (Name, Email, Phone, Nhu cầu) khớp với các cột trong Sheet.
- **Send Lead to Telegram:**
  - Cấu hình credentials `telegramApi` với Bot Token.
  - Điền chính xác `chatId` nơi đội ngũ sale sẽ nhận thông báo lead mới.

#### 3. Kích hoạt ⚡️
- Bấm nút **Chat Trigger** để mở giao diện chat thử nghiệm, nhập vài câu hỏi mẫu để kiểm tra xem RAG và AI Agent hoạt động đã chuẩn chưa.
- Kiểm tra xem dữ liệu có đẩy vào Google Sheets và Telegram thành công không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để đưa bot lên mây chạy thật!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM chuyên sâu:** Thay vì chỉ lưu Google Sheets, các sếp có thể thay thế/mở rộng bằng node HubSpot, Pipedrive hoặc Salesforce để quản lý khách hàng tiềm năng bài bản hơn.
- **Gửi Email tự động cho khách:** Thêm node Gmail ngay sau khi thu thập Lead để gửi thư cảm ơn tự động kèm tài liệu giới thiệu sản phẩm.
- **Kiểm tra trùng lặp (Duplicate Check):** Thêm một bước check số điện thoại/email trong Google Sheets trước khi ghi nhận để tránh lưu trùng lead.
- **Báo cáo tổng kết ngày:** Tạo một cron job chạy vào cuối ngày để thống kê tổng số lead thu được trong ngày gửi về Telegram.

### 📌 Kết luận
Một trợ lý AI vừa biết trả lời kiến thức công ty, vừa biết "săn" lead và báo cáo tức thì về Telegram chắc chắn sẽ là vũ khí bí mật giúp các sếp tối ưu hóa vận hành và bứt phá doanh số. Triển khai ngay hôm nay thôi các sếp ơi!