---
title: "🎙️ Xây Dựng Telegram Bot AI Đa Phương Tiện (Voice & Text) với GPT-4.1-Mini"
description: "Hướng dẫn chi tiết tạo Telegram Bot thông minh có khả năng nghe hiểu giọng nói (qua Gemini) và trả lời bằng cả văn bản lẫn giọng nói (qua OpenAI TTS) hoàn toàn không cần code."
slug: "telegram-bot-ai-voice-text-gpt-gemini"
tags: [n8n, telegram-bot, ai-chatbot, voice-ai, openai, gemini]
keywords: [n8n telegram bot, voice to text ai, gpt-4.1 mini, gemini transcription, tự động hóa chatbot]
---

# 🎙️ Xây Dựng Telegram Bot AI Đa Phương Tiện (Voice & Text) với GPT-4.1-Mini

Trong kỷ nguyên của AI, việc tương tác chỉ bằng văn bản đôi khi trở nên kém hiệu quả và thiếu tự nhiên. Các sếp có bao giờ nghĩ đến việc tạo ra một trợ lý ảo trên Telegram, nơi người dùng có thể **gửi tin nhắn thoại** và nhận lại **câu trả lời bằng giọng nói** hoặc văn bản một cách mượt mà?

Làm điều này thủ công sẽ đòi hỏi kiến thức sâu về xử lý âm thanh (Audio Processing), tích hợp API phức tạp và quản lý trạng thái hội thoại. Nhưng với **n8n**, tất cả trở nên đơn giản. Workflow này kết hợp sức mạnh của **GPT-4.1-Mini** (cho suy luận và tạo giọng nói) và **Google Gemini** (cho khả năng chuyển giọng nói thành văn bản cực kỳ chính xác) để tạo ra một trải nghiệm chatbot "thật" hơn bao giờ hết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là khi xử lý các file audio có thể nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác tự nhiên:** Hỗ trợ cả tin nhắn văn bản và tin nhắn giọng nói (Voice Message).
- **Đa phương tiện đầu ra:** Bot có thể trả lời bằng văn bản hoặc tự động chuyển thành file audio (TTS) tùy theo cấu hình.
- **Trí tuệ nhân tạo mạnh mẽ:** Sử dụng GPT-4.1-Mini để đảm bảo câu trả lời chính xác, logic và có ngữ cảnh (Memory).
- **Không cần code:** Toàn bộ quy trình xử lý audio, gọi API AI và gửi tin nhắn được tự động hóa hoàn toàn trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị 3 tài khoản/API keys sau:
1. **Telegram Bot Token:** Tạo qua @BotFather.
2. **Google Gemini API Key:** Lấy miễn phí tại [Google AI Studio](https://aistudio.google.com/).
3. **OpenAI API Key:** Lấy tại [OpenAI Platform](https://platform.openai.com/). *Lưu ý: Cần nạp ít nhất 5$ để sử dụng các model GPT-4.1 và TTS.*
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc [n8n.io/workflows/12003](https://n8n.io/workflows/12003) hoặc copy toàn bộ code JSON bên dưới.
- Mở n8n Editor.
- Chọn **Import from URL** hoặc **Import from File**.
- Dán JSON vào và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá phức tạp với 14 nodes, nhưng logic chia làm 2 nhánh chính: **Xử lý Text** và **Xử lý Voice**. Các sếp cần cấu hình credentials và tham số cho các node sau:

**A. Cấu hình Credentials (Quan trọng nhất)**
Trong n8n, các sếp cần tạo 3 bộ credentials mới:
1. `telegramApi`: Dán Token từ @BotFather.
2. `googlePalmApi`: Dán Gemini API Key.
3. `openAiApi`: Dán OpenAI API Key.
*(Sau khi tạo xong, n8n sẽ tự động áp dụng credentials này cho tất cả các node liên quan).*

**B. Cấu hình Nodes Chi Tiết**

1. **Node: Telegram Trigger**
   - Đây là điểm bắt đầu. Đảm bảo nó đang ở chế độ `Webhook` hoặc `Polling` (tùy hạ tầng).
   - Chọn credentials `telegramApi` đã tạo ở trên.

2. **Node: If (Phân luồng)**
   - Node này kiểm tra xem tin nhắn đến là **Text** hay **Voice**.
   - Mặc định workflow đã cấu hình tốt, nhưng các sếp nên kiểm tra điều kiện: Nếu `message.voice` tồn tại thì đi nhánh Voice, ngược lại đi nhánh Text.

3. **Nhánh Voice (Giọng nói):**
   - **Node: Get a file**: Tải file audio từ Telegram về n8n.
   - **Node: Transcribe a recording**: 
     - Chọn credentials `googlePalmApi`.
     - Model: Chọn model Gemini hỗ trợ audio (ví dụ: `gemini-1.5-flash` hoặc `gemini-1.5-pro`).
     - Resource: `audio`.
     - *Lưu ý:* Node này sẽ chuyển giọng nói thành văn bản để AI hiểu.
   - **Node: AI Agent1**: 
     - Sử dụng model `gpt-4.1-mini`.
     - Chỉnh sửa **System Prompt** ở đây để định hình tính cách của Bot khi trả lời bằng giọng nói (ví dụ: "Trả lời ngắn gọn, súc tích vì sẽ được đọc thành tiếng").
   - **Node: Generate audio**:
     - Chọn credentials `openAiApi`.
     - Resource: `audio`.
     - Model TTS: Chọn `tts-1` hoặc `tts-1-hd` (HD chất lượng cao hơn nhưng tốn credit hơn).
     - Voice: Chọn giọng đọc (Alloy, Echo, Fable, Onyx, Nova, Shimmer).
   - **Node: Send an audio file**: Gửi file audio vừa tạo về Telegram.

4. **Nhánh Text (Văn bản):**
   - **Node: AI Agent**:
     - Sử dụng model `gpt-4.1-mini`.
     - **System Prompt**: Đây là "linh hồn" của bot. Các sếp nên viết chi tiết vai trò của bot (ví dụ: "Bạn là trợ lý khách hàng thân thiện...").
   - **Node: Simple Memory**: Lưu lịch sử hội thoại để bot nhớ ngữ cảnh.
   - **Node: Guardrails**: Kiểm tra an toàn nội dung (tùy chọn, có thể bỏ qua nếu không cần kiểm duyệt chặt chẽ).
   - **Node: Send a text message**: Gửi câu trả lời văn bản về Telegram.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Save** để lưu workflow.
2. Nhấn nút **Active** (góc trên bên phải) để kích hoạt.
3. Mở Telegram, tìm bot của bạn và thử:
   - Gửi một tin nhắn văn bản đơn giản.
   - Nhấn giữ nút mic và nói một câu hỏi, gửi đi.
4. Quan sát n8n Execution để xem dữ liệu chạy qua các node.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh giọng đọc:** Trong node `Generate audio`, các sếp có thể thử nghiệm các giọng nói khác nhau của OpenAI TTS để tìm giọng phù hợp nhất với thương hiệu.
- **Tối ưu chi phí:** GPT-4.1-Mini rất rẻ, nhưng TTS (Text-to-Speech) có thể tốn credit. Nếu ngân sách hạn hẹp, các sếp có thể cấu hình để bot chỉ trả lời bằng giọng nói khi người dùng yêu cầu, hoặc giới hạn độ dài câu trả lời trước khi chuyển sang TTS.
- **Thêm hình ảnh:** Mở rộng workflow bằng cách thêm node `OpenAI DALL-E` để bot có thể tạo và gửi hình ảnh minh họa kèm theo câu trả lời.
- **Lưu log hội thoại:** Thêm node `Google Sheets` hoặc `Postgres` để lưu lại toàn bộ lịch sử chat, giúp các sếp phân tích hành vi người dùng và cải thiện prompt.

### 📌 Kết luận
Việc xây dựng một Telegram Bot có khả năng "nghe" và "nói" từng là thách thức lớn đối với các lập trình viên, nhưng với n8n, nó chỉ mất chưa đầy 15 phút để thiết lập. Workflow này không chỉ là một demo kỹ thuật mà là một công cụ thực chiến, giúp các sếp nâng cao trải nghiệm khách hàng và hiện đại hóa quy trình hỗ trợ. Hãy import, cấu hình và bắt đầu tương tác với AI theo cách tự nhiên nhất ngay hôm nay!