---
title: "🚀 Bot Telegram Đa Ngôn Ngữ Giọng Nói & Văn Bản với ElevenLabs TTS và LangChain"
description: "Tự động chuyển đổi tin nhắn Telegram thành văn bản hoặc giọng nói đa ngôn ngữ, trả lời thông minh bằng AI mà không cần viết code."
slug: "bot-telegram-danh-ngon-giong-noi-van-ban-elevenlabs-langchain"
tags: [n8n, automation, no-code, telegram, AI, chatbot]
keywords: [n8n workflow, tự động hóa, bot telegram, ElevenLabs, LangChain, AI chatbot]
---

# 🚀 Bot Telegram Đa Ngôn Ngữ Giọng Nói & Văn Bản với ElevenLabs TTS và LangChain

Doanh nghiệp ngày càng cần giao tiếp nhanh chóng, chính xác với khách hàng trên Telegram. Tuy nhiên, việc **xử lý đồng thời tin nhắn văn bản và giọng nói, hỗ trợ nhiều ngôn ngữ** thường đòi hỏi lập trình phức tạp, chi phí cao và thời gian bảo trì lâu dài.  

Workflow này giải quyết toàn bộ vấn đề:  
- **Nhận tin nhắn** (văn bản hoặc file âm thanh) từ Telegram.  
- **Tự động nhận dạng ngôn ngữ** và chuyển đổi giọng nói → văn bản bằng ElevenLabs STT.  
- **Xử lý ngữ cảnh** bằng các mô hình AI (Google Gemini, Groq) qua LangChain Agent.  
- **Trả lời** dưới dạng văn bản hoặc giọng nói (ElevenLabs TTS) tùy theo loại tin nhắn ban đầu.  
- **Hoạt động 24/7** mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Tự động trả lời ngay lập tức, không cần nhân viên nhập liệu.  
- **Độ chính xác cao**: Nhận dạng ngôn ngữ và chuyển đổi giọng nói nhờ ElevenLabs đa ngôn ngữ.  
- **Cá nhân hoá trải nghiệm**: AI hiểu ngữ cảnh, trả lời phù hợp từng người dùng.  
- **Hoạt động liên tục**: Không ngừng chạy trên server, không bị gián đoạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Telegram Bot Token** (tạo bot qua @BotFather).  
- **ElevenLabs API Key** (đăng ký tại https://elevenlabs.io).  
- **Google Gemini API Key** (Google Cloud → Vertex AI).  
- **Groq API Key** (đăng ký tại https://groq.com).  
- **n8n** đã được cài đặt (Docker, VPS hoặc n8n.cloud).  
- **Domain/HTTPS** (đối với webhook Telegram).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor** → nhấn **Import** (biểu tượng mũi tên lên).  
2. Dán **JSON** của workflow (tải từ link gốc https://n8n.io/workflows/5511) hoặc **Upload file**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình quan trọng |
|------|------|----------------------|
| **Telegram Input** | Trigger nhận tin nhắn từ Telegram. | Chọn **Telegram Credential** (Bot Token) và **Webhook URL** (HTTPS). |
| **Adds SessionId** (Set) | Tạo `sessionId` dựa trên `chatId` để lưu ngữ ngữ cảnh. | Thiết lập `sessionId = $json.message.chat.id`. |
| **Switch** | Kiểm tra tin nhắn có **text** hay **voice**. | Điều kiện: `{{ $json.message.text }}` **is empty** → đi tới nhánh Voice, ngược lại Text. |
| **Get Voice File** (Telegram) | Lấy file âm thanh từ Telegram. | Resource: **file**, File ID: `{{ $json.message.voice.file_id }}`. |
| **Transcribe ElevenLabs** | Chuyển giọng nói → văn bản. | Operation: **speechToText**, Resource: **speech**, Model: **eleven_multilingual_v2**, API Key: ElevenLabs. |
| **Edit Fields** (Set) | Đánh dấu `voice = true` và chuẩn hoá `text`. | `voice = true`, `text = $json.transcript`. |
| **Aggregate** | Gom lại lịch sử hội thoại (max 10 tin nhắn). | Mode: **Append**, Field to aggregate: `text`. |
| **Google Gemini Chat Model** | Xử lý ngữ cảnh bằng Gemini. | Credential: Google Gemini API Key, Model: **gemini-pro**. |
| **Groq Chat Model** | Dự phòng mô hình Groq (DeepSeek). | Credential: Groq API Key, Model: **deepseek-r1-distill-llama-70b**. |
| **Voice Assistant** (Agent) | LangChain Agent quyết định dùng mô hình nào và trả về `answer`. | System Message: tùy chỉnh để thêm **tools** (xem phần “Custom Tools”). |
| **If voice** (If) | Kiểm tra flag `voice` để quyết định trả lời dạng nào. | Condition: `{{ $json.voice === true }}`. |
| **ElevenLabs** (TTS) | Chuyển văn bản trả lời → giọng nói. | Resource: **speech**, Model: **eleven_multilingual_v2**, Language: `{{ $json.message.from.language_code }}` (hoặc `languageCode` tùy chỉnh). |
| **Telegram Send Message** | Gửi trả lời dạng **text**. | Chat ID: `{{ $json.message.chat.id }}`, Text: `{{ $json.answer }}`. |
| **Telegram send voice message** (HTTP Request) | Gửi file âm thanh trả lời. | Method: **POST**, URL: `https://api.telegram.org/bot{{ $credentials.botToken }}/sendVoice`, Body: `form-data` với `voice` là URL của file TTS (ElevenLabs trả về `audio_url`). |
| **Voice Assistant Memory** (Memory Buffer Window) | Lưu ngữ ngữ cảnh cho mỗi `sessionId`. | Size: **10**, Key: `sessionId`. |

> **Lưu ý quan trọng**  
> - Đảm bảo **ElevenLabs model** được đặt là `eleven_multilingual_v2` để hỗ trợ đa ngôn ngữ.  
> - Nếu muốn ép ngôn ngữ cố định, thêm trường `languageCode` trong node ElevenLabs TTS.  
> - Kiểm tra **Webhook URL** của Telegram phải có chứng chỉ SSL hợp lệ (Let's Encrypt OK).  

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi tin nhắn (text & voice) tới bot, quan sát log trong n8n để chắc chắn các node chạy đúng.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Kiểm tra lại trên Telegram: bot trả lời bằng **text** hoặc **voice** tùy vào loại tin nhắn gửi vào.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Discord**: Thêm node `Slack` hoặc `Discord` để đồng bộ tin nhắn giữa các kênh.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại `sessionId`, `userMessage`, `botReply`, thời gian.  
- **Báo cáo định kỳ**: Sử dụng `Cron` + `Google Docs` để tạo báo cáo tổng hợp số lượng tin nhắn, ngôn ngữ phổ biến.  
- **Thêm công cụ tùy chỉnh**: Tham khảo phần “Custom Tools Integration” trong canvas, viết hàm Python/JS và expose qua HTTP Request để Agent có thể gọi API nội bộ (ví dụ: tra cứu đơn hàng, kiểm tra tồn kho).  

### 📌 Kết luận
Với workflow **Multilingual Voice & Text Telegram Bot**, các sếp có thể triển khai ngay một trợ lý ảo đa ngôn ngữ, hỗ trợ cả tin nhắn văn bản và giọng nói, giảm tải bộ phận hỗ trợ khách hàng và nâng cao trải nghiệm người dùng. Đừng chần chừ, hãy **import, cấu hình và bật hoạt động** ngay hôm nay để cảm nhận sức mạnh của tự động hoá không code! 🚀