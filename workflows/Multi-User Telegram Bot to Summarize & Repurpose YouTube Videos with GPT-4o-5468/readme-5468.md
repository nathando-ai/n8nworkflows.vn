---
title: "🚀 Bot Telegram Đa Người Dùng Tóm Tắt & Tái Sử Dụng Video YouTube với GPT‑4o"
description: "Tự động nhận link YouTube từ Telegram, lấy transcript, tóm tắt và chuyển đổi nội dung thành bài viết, tweet, LinkedIn post chỉ bằng một tin nhắn."
slug: "bot-telegram-tom-tat-youtube-gpt4o"
tags: [n8n, automation, no-code, content-creation, ai, telegram]
keywords: [n8n workflow, tự động hóa, tóm tắt video youtube, chatbot telegram, openai gpt-4o]
---

# 🚀 Bot Telegram Đa Người Dùng Tóm Tắt & Tái Sử Dụng Video YouTube với GPT‑4o

Bạn đã bao giờ phải sao chép link YouTube, mở trình duyệt, tìm transcript, rồi mới có thể tạo nội dung cho blog, LinkedIn hay Twitter?  
Quá trình này tốn thời gian, dễ sai sót và không thể thực hiện 24/7.  

**Workflow n8n** này biến mọi tin nhắn Telegram thành một trợ lý AI thông minh:  
- Khi người dùng gửi link YouTube → tự động lấy transcript → tóm tắt → trả về kết quả ngay trong chat.  
- Khi người dùng gửi câu hỏi thường, bot trả lời ngay bằng GPT‑4o.  
- Hỗ trợ các lệnh “rút gọn”, “tạo bài LinkedIn”, “tạo chuỗi tweet” chỉ bằng một câu lệnh.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: 1 tin nhắn → 1 bản tóm tắt trong vài giây.  
- **Độ chính xác cao**: Dùng transcript gốc và GPT‑4o để hiểu ngữ cảnh.  
- **Tùy biến nội dung**: Chuyển đổi nhanh thành LinkedIn post, tweet thread, hoặc email.  
- **Hoạt động liên tục**: Không cần can thiệp, bot luôn sẵn sàng 24/7.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Telegram Bot Token** – tạo bot qua @BotFather.  
- **OpenAI API Key** – lấy tại https://platform.openai.com/account/api-keys.  
- **RapidAPI Key & Host** – dùng để gọi API transcript (`X‑RapidAPI-Key`, `X‑RapidAPI-Host`).  
- **n8n** – cài đặt (Docker, VPS, hoặc n8n.cloud).  
- **Credentials trong n8n**:  
  - `telegramApi` (Bot Token)  
  - `openAiApi` (OpenAI Key)  
  - `rapidApi` (Key + Host) – tạo custom credential nếu cần.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `Multi-User_Telegram_Bot_Summarize_YouTube.json` (được cung cấp trong mục tải về).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **Trigger: Telegram Bot Message** | Nhận mọi tin nhắn từ bot | Chọn credential **telegramApi** (Bot Token). |
| **Check: Is YouTube Link?** (IF) | Kiểm tra có chứa link YouTube không | Điều kiện: `{{$json["text"]?.match(/(youtu\.be\/|youtube\.com\/watch\?v=)[\w-]+/)}}` → **True** nếu có. |
| **Extract Chat & Video ID** (Set) | Tách video ID và lưu nội dung chat | Thiết lập fields: `videoId` = `{{$json["text"].match(/(?:v=|\/)([0-9A-Za-z_-]{11})/)[1]}}`; `chatMessage` = `{{$json["text"]}}`. |
| **Fetch YouTube Transcript (via RapidAPI)** (HTTP Request) | Gọi API RapidAPI lấy transcript | - Method: **GET** <br> - URL: `https://youtube-transcript3.p.rapidapi.com/video/${$node["Extract Chat & Video ID"].json["videoId"]}` <br> - Headers: `X-RapidAPI-Key`, `X-RapidAPI-Host`. |
| **Clean Transcript Symbols** (Set) | Làm sạch ký tự HTML entity | Thiết lập field `cleanTranscript` = `{{$json["transcript"]?.replace(/&#39;/g, "'").replace(/&quot;/g, '"') }}`. |
| **OpenAI Chat Model** (lmChatOpenAi) | Gửi transcript (hoặc câu hỏi) tới GPT‑4o | - Model: **gpt-4o-mini** (hoặc gpt‑4o) <br> - Credential: **openAiApi** <br> - Prompt: `Summarize the following transcript in 3‑5 bullet points. If user asks for a specific format (LinkedIn, tweet, etc.), follow the request.` |
| **Simple Memory** (memoryBufferWindow) | Lưu ngữ cảnh hội thoại | Window size: **5** (có thể tăng nếu muốn nhớ lâu hơn). |
| **AI Chat & Summarizer Agent** (Agent) | Kết hợp memory + OpenAI để trả lời | - Input: `{{$node["OpenAI Chat Model"].json["response"]}}` <br> - Memory: **Simple Memory**. |
| **Clean AI Output Formatting** (Code) | Xóa markdown không hỗ trợ Telegram (`**bold**`, `*italic*`) | ```js\nreturn {cleaned: $json["response"].replace(/\*\*/g, '').replace(/\*/g, '')};``` |
| **Send Reply to Telegram** (Telegram) | Gửi tin nhắn trả lời cho người dùng | Credential **telegramApi**; Chat ID = `{{$json["chatId"]}}`; Text = `{{$node["Clean AI Output Formatting"].json["cleaned"]}}`. |

> **Lưu ý:** Đảm bảo các node **OpenAI Chat Model**, **Simple Memory**, và **Agent** được nối đúng thứ tự, nếu có lỗi “undefined” thường do thiếu kết nối hoặc credential chưa chọn.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với một tin nhắn thử (ví dụ: gửi link YouTube tới bot).  
2. Kiểm tra log từng node, xác nhận transcript được lấy và tóm tắt.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải).  

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Discord**: Dùng node `Slack` hoặc `Discord` để đồng thời gửi kết quả tới các kênh làm việc.  
- **Lưu log vào Google Sheets**: Thêm node `Google Sheets` sau `Send Reply` để ghi lại thời gian, video ID, và nội dung tóm tắt.  
- **Báo cáo định kỳ**: Dùng node `Cron` + `HTTP Request` tới webhook Slack để gửi báo cáo tổng hợp các video đã được tóm tắt trong tuần.  
- **Tùy chỉnh Prompt**: Thêm node `Set` trước `OpenAI Chat Model` để cho phép người dùng chọn “short”, “detailed”, “bullet” qua từ khóa trong tin nhắn.  

### 📌 Kết luận
Với workflow này, các sếp có thể biến Telegram thành một trợ lý nội dung AI mạnh mẽ, tự động tóm tắt và tái sử dụng video YouTube chỉ trong vài giây. Đừng để công việc thủ công làm mất năng suất – **cài ngay**, **test**, và **đưa vào vận hành 24/7** để tăng tốc quá trình sáng tạo nội dung! 🚀