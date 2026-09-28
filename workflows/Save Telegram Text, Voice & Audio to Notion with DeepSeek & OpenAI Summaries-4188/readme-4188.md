---
title: "🚀 Lưu Tin Nhắn, Giọng Nói & Audio Telegram vào Notion + Tóm Tắt AI DeepSeek & OpenAI"
description: "Tự động lưu mọi tin nhắn, file âm thanh từ Telegram vào Notion và nhận bản tóm tắt thông minh bằng DeepSeek & OpenAI chỉ trong vài giây."
slug: "luu-telegram-notion-tom-tat-ai"
tags: [n8n, automation, no-code, telegram, notion, AI]
keywords: [n8n workflow, tự động hóa, telegram, notion, AI summarization]
---

# 🚀 Lưu Tin Nhắn, Giọng Nói & Audio Telegram vào Notion + Tóm Tắt AI DeepSeek & OpenAI

Bạn có bao giờ phải **chép sao** từng tin nhắn, file âm thanh từ Telegram vào Notion để lưu trữ?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, mất dữ liệu và **không thể** tạo ra bản tóm tắt nhanh chóng cho các cuộc họp, brainstorming.  

**Workflow** này sẽ giải quyết toàn bộ vấn đề:  
- **Tự động** nhận mọi tin nhắn, voice, audio từ Telegram.  
- **Lưu** nguyên bản vào Notion (văn bản, file âm thanh).  
- **Chuyển đổi** voice/audio thành văn bản bằng OpenAI Whisper.  
- **Tóm tắt** nội dung bằng mô hình DeepSeek hoặc OpenAI GPT.  
- **Gửi lại** kết quả tóm tắt ngay trên Telegram để bạn và đồng nghiệp ngay lập tức nắm bắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn copy‑paste thủ công, mọi tin nhắn tự động vào Notion.  
- **Độ chính xác cao**: Voice & audio được chuyển thành văn bản bằng Whisper, giảm lỗi nhập liệu.  
- **Tóm tắt nhanh**: AI tạo bản tóm tắt trong vòng 5‑10 giây, giúp quyết định nhanh hơn.  
- **Hoạt động liên tục 24/7**: Workflow chạy trên server riêng, không phụ thuộc vào máy cá nhân.  
- **Dễ mở rộng**: Thêm Slack, Email, hoặc lưu file vào S3 chỉ bằng vài node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token** (tạo bot qua @BotFather).  
- **Chat ID** của nhóm hoặc cá nhân mà bot sẽ lắng nghe.  
- **Notion Integration Token** và **Database ID** nơi lưu trữ tin nhắn.  
- **OpenAI API Key** (để dùng Whisper & GPT).  
- **DeepSeek API Key** (để dùng mô hình DeepSeek).  
- **n8n** đã cài đặt (đề nghị phiên bản >= 1.0).  
- **Kết nối internet ổn định** cho các API AI.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Dashboard → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `Save_Telegram_Text_Voice_Audio_to_Notion.json` (được cung cấp ở phần cuối).  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard** → **Import**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là danh sách **17 node** trong workflow và các tham số quan trọng cần cấu hình:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Telegram Trigger** | telegramTrigger | - **Bot Token** (Credentials) <br> - **Chat ID** (Allowed Updates) |
| **DeepSeek Chat Model** | lmChatDeepSeek | - **API Key** <br> - **Model** (e.g., `deepseek-chat`) |
| **AI Agent** | agent | - **LLM**: chọn DeepSeek hoặc OpenAI <br> - **Prompt**: `Summarize the following text in 3 bullet points.` |
| **Notion1** | notion | - **Credentials** (Integration Token) <br> - **Database ID** (đối với tin nhắn text) |
| **Switch1** | switch | - **Rules**: <br> 1️⃣ `type === "text"` → route tới node Telegram (reply) & Notion1 <br> 2️⃣ `type === "voice"` → route tới OpenAI (Whisper) → DeepSeek → Notion2 <br> 3️⃣ `type === "audio"` → route tương tự voice |
| **Telegram** | telegram | - **Credentials** (Bot Token) <br> - **Chat ID** (để gửi phản hồi tóm tắt) |
| **Notion** | notion | - **Database ID** cho **voice transcription** (cột: `Transcription`, `Summary`) |
| **OpenAI** | openAi | - **API Key** <br> - **Operation**: `Transcription (Whisper)` <br> - **Audio URL**: lấy từ Telegram file |
| **Telegram1** | telegram | - **Credentials** <br> - **Chat ID** (gửi bản tóm tắt) |
| **Notion2** | notion | - **Database ID** cho **audio transcription** |
| **OpenAI2** | openAi | - **API Key** <br> - **Operation**: `Chat Completion` (tóm tắt) nếu muốn dùng OpenAI thay DeepSeek |
| **DeepSeek Chat Model1** | lmChatDeepSeek | - **API Key** <br> - **Model**: DeepSeek (tóm tắt voice) |
| **AI Agent1** | agent | - **Prompt**: `Summarize the transcribed voice message.` |
| **Notion3** | notion | - **Database ID** cho **summary** của voice |
| **DeepSeek Chat Model2** | lmChatDeepSeek | - **API Key** <br> - **Model**: DeepSeek (tóm tắt audio) |
| **AI Agent2** | agent | - **Prompt**: `Summarize the transcribed audio file.` |
| **Notion4** | notion | - **Database ID** cho **summary** của audio |

**Lưu ý quan trọng**  
- Đảm bảo **Credentials** được tạo trong n8n → **Credentials** → **Add New** → chọn loại (Telegram API, Notion API, OpenAI, DeepSeek).  
- Các **Database ID** trong Notion có thể lấy từ URL của database (`https://www.notion.so/yourworkspace/xxxxxxxxxxxx`).  
- Khi workflow nhận file âm thanh, Telegram sẽ trả về **file_id**; node `Telegram` sẽ tự động tải file về và truyền URL cho OpenAI Whisper.  
- Kiểm tra **quota** API (OpenAI Whisper và DeepSeek) để tránh bị gián đoạn.  

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một tin nhắn text, một voice và một audio từ Telegram tới bot. Kiểm tra:
   - Tin nhắn xuất hiện trong Notion (cột `Content`).  
   - Voice/audio được chuyển thành văn bản và lưu trong Notion.  
   - Bot trả lại bản tóm tắt trên Telegram.  
2. Khi mọi thứ hoạt động ổn → **Toggle** nút **Active** ở góc trên bên phải workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Discord**: Thêm node Slack để đồng thời gửi bản tóm tắt tới kênh làm việc.  
- **Báo cáo định kỳ**: Dùng node **Cron** để mỗi ngày 9h gửi báo cáo tổng hợp các tin nhắn đã lưu trong Notion qua email.  
- **Lưu trữ file gốc**: Thêm node **AWS S3** hoặc **Google Drive** để lưu bản audio gốc, chỉ lưu link trong Notion.  
- **Logging chi tiết**: Kích hoạt node **Set** + **Function** để ghi log vào Notion hoặc Google Sheets, giúp theo dõi số lượng tin nhắn, thời gian xử lý.  

### 📌 Kết luận
Với workflow **“Save Telegram Text, Voice & Audio to Notion with DeepSeek & OpenAI Summaries”**, các sếp sẽ **không còn mất công sao chép** tin nhắn, **ngay lập tức có bản tóm tắt** thông minh, và **tất cả dữ liệu được lưu trữ có thể truy xuất** trong Notion. Hãy triển khai ngay để nâng cao năng suất làm việc và giảm thiểu lỗi con người! 🚀