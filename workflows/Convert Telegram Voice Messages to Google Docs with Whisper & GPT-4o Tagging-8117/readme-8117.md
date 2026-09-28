---
title: "🚀 Chuyển Tin Nhắn Giọng Nói Telegram → Google Docs bằng Whisper & GPT‑4o"
description: "Tự động chuyển file âm thanh Telegram thành văn bản, tóm tắt và gắn thẻ bằng AI, lưu ngay vào Google Docs chỉ trong vài giây."
slug: "chuyen-telegram-voice-to-google-docs"
tags: [n8n, automation, no-code, ai, telegram, google-docs]
keywords: [n8n workflow, tự động hóa, telegram voice, whisper, gpt-4o, google docs]
---

# 🚀 Chuyển Tin Nhắn Giọng Nói Telegram → Google Docs bằng Whisper & GPT‑4o

Bạn có bao giờ phải lắng nghe hàng chục tin nhắn thoại trên Telegram, sao chép nội dung ra giấy, rồi mới có thể chia sẻ hay lưu trữ?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, đặc biệt khi cần **tóm tắt nhanh** hoặc **gắn thẻ nội dung** để tìm kiếm sau này.  

**Workflow này** sẽ tự động:

1. Nhận tin nhắn thoại từ Telegram.  
2. Dùng **OpenAI Whisper** chuyển âm thanh thành văn bản.  
3. Gửi văn bản tới **GPT‑4o** để tóm tắt và gắn thẻ.  
4. Lưu kết quả vào **Google Docs** và gửi xác nhận lại cho người gửi.  

Tất cả diễn ra **100 % không cần viết code** – chỉ cần cấu hình một vài node trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần gửi tin nhắn thoại, nội dung đã có sẵn trong Google Docs ngay lập tức.  
- **Độ chính xác cao**: Whisper chuyển giọng nói thành văn bản với độ lỗi <5 %.  
- **Tự động tóm tắt & gắn thẻ**: GPT‑4o tạo tiêu đề, từ khóa và tóm tắt ngắn gọn.  
- **Hoạt động liên tục 24/7**: Không cần can thiệp thủ công, workflow tự động xử lý mọi tin nhắn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token** (tạo bot qua @BotFather).  
- **Chat ID** của nhóm hoặc cá nhân mà bot sẽ nhận tin nhắn.  
- **OpenAI API Key** (có quyền sử dụng Whisper & GPT‑4o).  
- **Google Docs OAuth2 credentials** (đăng nhập Google, cấp quyền `https://www.googleapis.com/auth/documents`).  
- **Google Document ID** (tài liệu sẽ được cập nhật).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `convert-telegram-voice-to-google-docs.json` (hoặc copy toàn bộ JSON từ nguồn).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần thay đổi |
|------|-----------|-----------------------|
| **Telegram Sprachnachricht Empfang** (Telegram Trigger) | Nhận tin nhắn thoại từ Telegram | - Chọn **Credentials** → `telegramApi` (Bot Token). <br> - Đặt **Chat ID** (hoặc để trống để nhận mọi tin). |
| **Get a file** (Telegram) | Lấy file âm thanh từ Telegram | - Credentials: `telegramApi`. <br> - **Resource**: `file`. <br> - Đầu vào: `file_id` từ trigger. |
| **Check if Audio file** (If) | Kiểm tra loại file có phải là audio không | - **Condition**: `{{$json["mime_type"]?.startsWith("audio/")}}` (hoặc `{{$json["file_name"].endsWith(".ogg")}}`). |
| **OpenAI Whisper Transkription** | Chuyển file âm thanh → văn bản | - Credentials: `openAiApi`. <br> - **Operation**: `transcribe`. <br> - **Resource**: `audio`. <br> - Đầu vào: URL file từ node “Get a file”. |
| **Text formatieren** (Function) | Định dạng lại văn bản (loại bỏ ký tự thừa) | - Code mẫu: <br>```js\nreturn { json: { text: $json["transcription"].trim() } };\n``` |
| **Message a model** (OpenAI) | Gửi văn bản tới GPT‑4o để tóm tắt & gắn thẻ | - Credentials: `openAiApi`. <br> - **Model**: `gpt-4o`. <br> - **Prompt** ví dụ: <br>```text\nBạn là trợ lý AI. Hãy tóm tắt nội dung sau trong 2‑3 câu và đưa ra 3‑5 từ khóa (cách nhau bằng dấu phẩy). Nội dung:\n{{ $json["text"] }}\n``` |
| **In Google Doc speichern** (Google Docs) | Cập nhật Google Doc với kết quả | - Credentials: `googleDocsOAuth2Api`. <br> - **Operation**: `update`. <br> - **Document ID**: ID của tài liệu mục tiêu. <br> - **Content**: Dùng biểu thức `{{$json["response"]}}` (kết quả GPT‑4o). |
| **Bestätigung senden** (Telegram) | Gửi tin nhắn xác nhận tới người gửi | - Credentials: `telegramApi`. <br> - **Chat ID**: `{{$json["chat_id"]}}`. <br> - **Message**: “✅ Đã chuyển và lưu tin nhắn của bạn vào Google Docs!” |
| **Set field** (Set) | Đặt các trường phụ trợ (nếu cần) | - Thêm trường `documentUrl` = `https://docs.google.com/document/d/{{DocumentID}}/edit`. |

> **Lưu ý:** Đảm bảo **các node được nối đúng thứ tự**: Trigger → Get a file → If → Whisper → Function → OpenAI → Google Docs → Telegram (xác nhận). Nếu có lỗi, kiểm tra log ở góc phải màn hình n8n.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với một tin nhắn thoại mẫu để kiểm tra.  
2. Kiểm tra Google Docs: nội dung, tóm tắt, thẻ đã được chèn.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo hàng ngày**: Thêm node **Cron** + **Google Sheets** để tổng hợp số lượng tin nhắn đã xử lý.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để lưu bản ghi JSON vào S3 hoặc Dropbox.  
- **Kết nối Slack/Discord**: Thêm node **Slack** hoặc **Discord** để thông báo khi có lỗi hoặc khi đạt mốc xử lý.  
- **Tùy chỉnh Prompt**: Thêm tham số “ngôn ngữ” hoặc “độ dài tóm tắt” để phù hợp với từng nhóm làm việc.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá hoàn toàn** quy trình chuyển đổi tin nhắn thoại Telegram thành tài liệu Google Docs có tóm tắt và thẻ, giảm thiểu công việc thủ công và tăng năng suất. Hãy **import ngay**, cấu hình các credentials cần thiết và để n8n làm phần còn lại – công việc của bạn sẽ trở nên “siêu nhanh” và “siêu thông minh”! 🚀