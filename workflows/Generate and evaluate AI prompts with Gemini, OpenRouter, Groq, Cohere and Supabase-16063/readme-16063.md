---
title: "🚀 Tự động tạo và đánh giá AI Prompt đỉnh cao với Gemini, OpenRouter, Groq, Cohere và Supabase"
description: "Hướng dẫn chi tiết xây dựng workflow n8n sử dụng đa mô hình AI (Gemini, OpenRouter, Groq, Cohere) để tạo, so sánh và chọn ra prompt tối ưu nhất cho mọi mục tiêu."
slug: "tu-dong-tao-va-danh-gia-ai-prompt-da-mo-hinh-n8n"
tags: [n8n, automation, ai-agents, gemini, groq, openrouter, cohere, supabase]
keywords: [n8n workflow, tao prompt ai tu dong, multi-model evaluation, gemini cohere groq openrouter, supase automation]
---

# 🚀 Tự động tạo và đánh giá AI Prompt đỉnh cao với đa mô hình AI

Các sếp có bao giờ đau đầu khi viết prompt cho AI? Viết xong thấy chưa chuẩn, sửa đi sửa lại tốn rất nhiều thời gian mà kết quả vẫn hên xui? Việc tạo ra một câu lệnh (prompt) xuất sắc đòi hỏi tư duy đa chiều từ nhiều góc nhìn: sáng tạo, marketing, hay kỹ thuật chuyên sâu. 

Làm thế nào để tự động hóa hoàn toàn quy trình này? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tận dụng sức mạnh của **Google Gemini, OpenRouter, Groq, Cohere và Supabase** để sinh ra, đối chiếu và chọn ra prompt hoàn hảo nhất chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các request gọi đồng thời nhiều LLM chạy mượt mà 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu hóa đa chiều:** Yêu cầu được xử lý song song bởi 3 Agent chuyên biệt: Sáng tạo (Gemini), Marketing (OpenRouter), và Kỹ thuật (Groq).
- **Đánh giá khách quan:** Sử dụng Cohere làm "giám khảo" để chọn ra prompt tốt nhất kèm theo lý do thuyết phục.
- **Lưu trữ tự động:** Mọi kết quả đều được tự động lưu vào cơ sở dữ liệu Supabase để tra cứu, tái sử dụng sau này.
- **Tốc độ chớp nhoáng:** Tích hợp API qua Webhook giúp ứng dụng/chatbot của các sếp gọi trực tiếp và nhận kết quả ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain/AI nodes).
- **API Keys / Credentials:**
  - Google Gemini API (dùng cho Creative Agent & Gemini Chat Model)
  - OpenRouter API (dùng cho Marketing Agent & OpenRouter Chat Model)
  - Groq API (dùng cho Technical Agent & Groq Chat Model)
  - Cohere API (dùng cho Best Prompt Evaluator & Cohere Chat Model)
  - Supabase API (chuẩn bị sẵn 1 bảng tên là `prompts` với các cột: `goal`, `best_prompt`)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor (hoặc import file JSON tải từ nguồn cấp). Workflow gồm tổng cộng 14 nodes kết hợp chặt chẽ giữa Webhook, Code, Merge, Supabase và các AI Agent.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Webhook Node:** Nhận yêu cầu POST với định dạng JSON chứa mục tiêu `{ "goal": "..." }`.
- **3 Agent Nodes (Creative, Marketing, Technical):** Liên kết lần lượt với các mô hình `Google Gemini Chat Model`, `OpenRouter Chat Model` (`liquid/lfm-2.5-1.2b-instruct:free`), và `Groq Chat Model` (`llama-3.3-70b-versatile`). Hãy đảm bảo các sếp đã chọn đúng Credentials cho từng node mô hình tương ứng.
- **Best Prompt Evaluator Agent:** Sử dụng `Cohere Chat Model` (`c4ai-aya-expanse-32b`) để đọc kết quả tổng hợp từ node `Combine Agent Outputs` và chấm điểm, chọn ra prompt chiến thắng.
- **Create a row (Supabase):** Chọn đúng credential Supabase, trỏ tới bảng `prompts` và map đúng 2 trường dữ liệu `goal` và `best_prompt`.
- **Respond to Webhook:** Trả về kết quả JSON cuối cùng cho người gọi.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và dùng Postman hoặc cURL gửi một request POST mẫu chứa `{"goal": "Viết một bài quảng cáo áo phông"}` tới URL Webhook để test thử.
- Nếu mọi thứ trả về kết quả mượt mà, các sếp bấm nút **Active** để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Nối Webhook đầu vào trực tiếp với Telegram Bot hoặc Slack để nhân viên trong công ty có thể gõ lệnh `/taoprompt [mục tiêu]` và nhận ngay prompt xịn.
- **Mở rộng thêm mô hình:** Các sếp hoàn toàn có thể thêm Claude (Anthropic) hoặc OpenAI GPT-4 vào làm một Agent độc lập để cuộc thi tạo prompt thêm phần phong phú.
- **Bổ hoả báo cáo:** Thêm node gửi thông báo qua email hoặc Slack mỗi khi có một prompt điểm 10/10 được tạo ra.

### 📌 Kết luận
Việc viết prompt giờ đây không còn là thử thách tốn thời gian nữa. Với workflow tự động hóa kết hợp đa mô hình AI này, các sếp đã có trong tay một "phòng thí nghiệm prompt" thu nhỏ, tự động tinh chỉnh và chọn lọc ra câu lệnh tối ưu nhất cho doanh nghiệp. Triển khai ngay thôi nào các sếp!