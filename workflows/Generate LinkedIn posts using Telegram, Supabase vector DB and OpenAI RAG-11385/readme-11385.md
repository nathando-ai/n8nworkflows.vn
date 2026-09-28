---
title: "🚀 Tự động hóa sáng tạo nội dung LinkedIn viral bằng Telegram, Supabase Vector DB và OpenAI RAG trên n8n"
description: "Xây dựng hệ thống AI tự động thu thập bài viết viral qua Telegram, lưu trữ vào Supabase Vector DB và tạo nội dung LinkedIn triệu view bằng Multi-Agent RAG."
slug: "tao-bai-dang-linkedin-viral-telegram-supabase-openai-rag-n8n"
tags: [n8n, automation, ai-agents, vector-database, openai, telegram, supabase, ragger]
keywords: [n8n workflow, linkedin post generator, supabase vector db, telegram bot scraping, openai rag ai, automation content creator]
keywords: [n8n workflow, tạo bài đăng linkedin, supabase vector db, telegram bot, openai rag, tự động hóa marketing]
---

# 🚀 Hệ thống AI Tự động Tạo Bài Viết LinkedIn Viral với RAG và Supabase

Các sếp có đang mệt mỏi mỗi ngày phải ngồi nghĩ ý tưởng viết bài LinkedIn, loay hoay không biết viết hook sao cho giật gân, hay tốn hàng giờ nghiên cứu xem bài nào đang "triệu view" để học tập? Việc làm thủ công này không chỉ ngốn thời gian mà còn dễ cạn kiệt sáng tạo.

Giải pháp là đây! Workflow n8n mạnh mẽ này sẽ giúp các sếp xây dựng một **"Cơ sở tri thức bài viết viral" (Viral Content Vector Database)** cá nhân. Bất cứ khi nào thấy một bài viết hay trên LinkedIn, chỉ cần gửi link qua Telegram, AI sẽ tự động phân tích và lưu vào cơ sở dữ liệu. Sau đó, khi cần viết bài mới, hệ thống Multi-Agent tích hợp RAG sẽ tự động học hỏi từ kho tài liệu đó và viết ra những bài đăng chuẩn chỉnh, cực kỳ thu hút. 100% tự động, không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thu thập thông minh:** Biến mọi link bài viết hay thành dữ liệu huấn luyện chỉ bằng một tin nhắn Telegram đơn giản.
- **Lưu trữ Vector hiện đại:** Tự động tạo Embeddings và lưu trữ vào Supabase Vector Database để tìm kiếm ngữ nghĩa cực nhanh.
- **Hệ thống 3 AI Agent chuyên biệt:** Phân tích Hook, lên dàn ý (Structure), và tổng hợp RAG để viết bài chuẩn văn phong viral.
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn từ khâu thu thập ý tưởng đến lúc xuất bản bài viết lên LinkedIn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Telegram Bot Token** (tạo qua BotFather).
- **Supabase Account** (đã bật extension `vector`).
- **OpenAI API Key** (cho Embeddings và các mô hình GPT-4o-mini / GPT-5-nano).
- **Google Gemini API Key** (tùy chọn để fallback mô hình 2.5-flash).
- **LinkedIn Developer Account** (nếu muốn tự động publish bài trực tiếp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp mã nguồn JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 2 module chính với các điểm cần cấu hình quan trọng:

* **Module 1: Thu thập bài viết qua Telegram**
  - **Node `On Telegram Message` & `Typing....`, `Wrong URL`, `Unable to Scrape`, `✅ Post Scrapped Sucessfully`**: Cấu hình credentials `telegramApi` bằng Bot Token của các sếp.
  - **Node `Upload Document` & `Supabase Vector Store`**: Kết nối tài khoản Supabase qua `supabaseApi`, trỏ tới bảng `linkedin_post` đã cài đặt sẵn kiểu dữ liệu vector (1536 chiều).
  - **Node `Embeddings` & `Embeddings.`**: Cấu hình OpenAI API Key để vector hóa nội dung bài viết.

* **Module 2: AI Agent tạo bài viết (RAG)**
  - **Node `Hook Analyse Agent`, `Post Structure Agent`, `Post Generator Agent`**: Cấu hình các Agent LangChain kết hợp với các mô hình ngôn ngữ lớn.
  - **Node `4o mini`, `2.5-flash`, `5 nano`**: Thiết lập model LLM chính (GPT-4o-mini, Gemini 2.5-flash) và model tối ưu cấu trúc (GPT-5-nano) bằng OpenAI/Google credentials.
  - **Node `Create a post`**: Cấu hình tài khoản LinkedIn OAuth2 nếu muốn tự động đăng bài, hoặc ngắt kết nối node này nếu các sếp chỉ muốn nhận text qua form để chỉnh sửa thủ công.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một URL bài viết LinkedIn bất kỳ vào Telegram Bot để kiểm tra luồng lưu trữ vector.
- Mở Web Form từ node **`LinkedIn Form`** để test tính năng tạo bài viết AI.
- Bật công tắc **Active** để đưa workflow vào vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram Notification:** Thêm node gửi thông báo về kênh riêng mỗi khi có bài viết mới được tạo thành công hoặc khi hệ thống quét lỗi scrape URL.
- **Báo cáo định kỳ:** Tạo một nhánh phụ quét Supabase Vector DB hàng tuần để thống kê các chủ đề bài viết nào được lưu trữ nhiều nhất.
- **Đa kênh hóa:** Mở rộng workflow để tự động đăng đồng thời bài viết lên Twitter/X hoặc Facebook thay vì chỉ mỗi LinkedIn.

### 📌 Kết luận
Với hệ thống tự động hóa RAG kết hợp Supabase Vector DB và Multi-Agent AI này, các sếp không chỉ xây dựng được một "bộ não thứ hai" chứa đầy các bí quyết viral mà còn tiết kiệm hàng chục giờ lên ý tưởng mỗi tuần. Hãy thiết lập ngay hôm nay để tối ưu hóa chiến lược Content Marketing của doanh nghiệp!