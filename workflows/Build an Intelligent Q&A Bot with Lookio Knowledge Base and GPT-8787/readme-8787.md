---
title: "🤖 Xây Dựng Chatbot Q&A Thông Minh Với Lookio & GPT - Tự Động Hóa Hỗ Trợ Khách Hàng"
description: "Hướng dẫn chi tiết cách tạo chatbot AI trả lời câu hỏi dựa trên cơ sở dữ liệu Lookio, kết hợp GPT-4.1-mini để tiết kiệm chi phí và tăng tốc độ phản hồi."
slug: "chatbot-qa-lookio-gpt-n8n"
tags: [n8n, automation, no-code, ai-agent, lookio, openai]
keywords: [n8n workflow, chatbot ai, lookio integration, tự động hóa hỗ trợ khách hàng, ai agent n8n]
---

# 🤖 Xây Dựng Chatbot Q&A Thông Minh Với Lookio & GPT - Tự Động Hóa Hỗ Trợ Khách Hàng

Trong môi trường kinh doanh hiện đại, việc khách hàng đặt ra những câu hỏi lặp đi lặp lại về sản phẩm, chính sách đổi trả hay hướng dẫn sử dụng là điều không thể tránh khỏi. Nếu đội ngũ hỗ trợ của các sếp phải trả lời thủ công từng tin nhắn, không chỉ gây tốn kém nhân sự mà còn dễ dẫn đến sự thiếu nhất quán trong thông tin.

Workflow n8n này là giải pháp "chìa khóa trao tay" giúp các sếp xây dựng một **AI Agent thông minh**. Nó sử dụng **Lookio** (nền tảng quản lý cơ sở dữ liệu tri thức doanh nghiệp) làm nguồn dữ liệu và **OpenAI (GPT-4.1-mini)** làm bộ não xử lý ngôn ngữ. Điểm đặc biệt là agent được thiết kế để tự xử lý các lời chào đơn giản và chỉ gọi API Lookio khi thực sự cần tra cứu thông tin chuyên sâu, giúp tối ưu hóa chi phí API và tốc độ phản hồi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí API:** Agent thông minh chỉ gọi Lookio khi cần, tránh lãng phí token cho các cuộc hội thoại đơn giản.
- **Độ chính xác cao:** Trả lời dựa trên tài liệu nội bộ đã được index trong Lookio, giảm thiểu lỗi "hallucination" (bịa đặt) của AI.
- **Trải nghiệm liền mạch:** Kết hợp bộ nhớ hội thoại (Memory) để AI hiểu ngữ cảnh câu hỏi trước đó.
- **Dễ dàng tùy chỉnh:** Chỉ cần thay đổi API Key và Assistant ID là có thể áp dụng cho bất kỳ bộ dữ liệu nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Lookio:** Các sếp cần có tài khoản Lookio, đã tạo một Assistant và upload tài liệu (PDF, Word, v.v.) vào đó.
- **Lookio API Key & Assistant ID:** Lấy từ dashboard của Lookio.
- **Tài khoản OpenAI:** Cần có API Key để kết nối với model GPT-4.1-mini (hoặc bất kỳ model nào khác).
- **n8n Instance:** Đã cài đặt và chạy n8n (có thể là cloud hoặc self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào và nhấn **Import**. Workflow sẽ hiển thị 5 nodes chính: Trigger, Memory, LLM, Agent, và Tool.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng mà các sếp cần cấu hình để workflow hoạt động:

**1. Node: `When chat message received` (Chat Trigger)**
- Đây là điểm bắt đầu. Các sếp có thể kết nối node này với các kênh chat khác (Slack, Telegram, Webhook) nếu muốn, hoặc giữ nguyên để test trực tiếp trong n8n.

**2. Node: `OpenAI Chat Model`**
- **Credentials:** Chọn hoặc tạo mới credentials OpenAI.
- **Model:** Mặc định là `gpt-4.1-mini`. Các sếp có thể đổi sang `gpt-4o` hoặc `gpt-3.5-turbo` tùy theo ngân sách và yêu cầu độ phức tạp.
- **Lưu ý:** Đảm bảo API Key có quyền truy cập vào model đã chọn.

**3. Node: `Query knowledge base` (HTTP Request Tool)**
- Đây là node quan trọng nhất để kết nối với Lookio.
- **URL:** Kiểm tra URL API của Lookio (thường là endpoint `/assistants/{assistant_id}/chat`).
- **Headers:**
  - `Authorization`: Điền `Bearer <your-lookio-api-key>`.
  - `Content-Type`: `application/json`.
- **Body:**
  - Thay thế placeholder `<your-lookio-api-key>` và `<your-assistant-id>` bằng thông tin thực tế của các sếp.
  - Đảm bảo cấu trúc JSON body phù hợp với API documentation của Lookio (thường bao gồm `message` và `conversation_id` nếu có).

**4. Node: `AI Knowledge Agent`**
- **System Message:** Đây là nơi các sếp "lên đồ" cho AI.
  - Ví dụ: *"Bạn là trợ lý hỗ trợ khách hàng của [Tên Công Ty]. Hãy trả lời ngắn gọn, lịch sự. Nếu câu hỏi không liên quan đến sản phẩm, hãy từ chối lịch sự. Chỉ sử dụng công cụ 'Query knowledge base' khi cần tra cứu thông tin cụ thể."*
- **Tools:** Đảm bảo node `Query knowledge base` đã được gắn vào phần Tools của Agent.

**5. Node: `Simple Memory`**
- Node này giúp AI nhớ ngữ cảnh hội thoại. Mặc định là `BufferWindowMemory`. Các sếp có thể điều chỉnh `contextWindowLength` nếu muốn AI nhớ nhiều tin nhắn hơn.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để test với một câu hỏi mẫu (ví dụ: "Chính sách đổi trả là gì?").
2. Kiểm tra output xem AI có trả lời đúng dựa trên tài liệu Lookio không.
3. Nếu ổn, bật công tắc **Active** ở góc trên bên phải để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp đa kênh:** Thay vì chỉ dùng Chat Trigger, các sếp có thể thay bằng **Slack Trigger** hoặc **Telegram Trigger** để đưa chatbot vào kênh giao tiếp chính của công ty.
- **Log hoạt động:** Thêm một node **Google Sheets** hoặc **Airtable** sau Agent để lưu lại mọi câu hỏi và câu trả lời, giúp phân tích xu hướng hỏi đáp của khách hàng.
- **Cá nhân hóa theo user:** Nếu các sếp có hệ thống CRM, hãy thêm bước lấy thông tin khách hàng trước khi gửi vào Agent để AI có thể xưng hô thân mật hơn (ví dụ: "Chào anh Minh, ...").
- **Fallback mechanism:** Trong System Message, hãy chỉ định rõ cách AI phản hồi khi không tìm thấy thông tin trong Lookio (ví dụ: "Tôi không tìm thấy thông tin này, vui lòng liên hệ nhân viên hỗ trợ qua email...").

### 📌 Kết luận
Với workflow này, các sếp có thể biến bất kỳ bộ tài liệu nội bộ nào thành một chatbot thông minh, phản hồi tức thì và chính xác. Không cần code, không cần lo lắng về việc đội ngũ hỗ trợ quá tải. Hãy bắt đầu ngay hôm nay để nâng cao trải nghiệm khách hàng và tối ưu hóa vận hành doanh nghiệp!