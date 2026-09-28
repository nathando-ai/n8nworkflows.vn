---
title: "🚀 Tự Động Chuyển Đổi & Tóm Tắt Tin Nhắn Giọng Nói Telegram sang Google Docs bằng OpenAI & DeepSeek"
description: "Workflow nhận tin nhắn giọng nói trên Telegram, chuyển thành văn bản, tóm tắt bằng AI và lưu ngay vào Google Docs chỉ trong vài giây."
slug: "transcribe-summarize-telegram-voice-notes"
tags: [n8n, automation, no-code, AI, Telegram, Google-Drive]
keywords: [n8n workflow, tự động hóa, transcription, summarization, OpenAI, DeepSeek, Telegram, Google Docs]
---

# 🚀 Tự Động Chuyển Đổi & Tóm Tắt Tin Nhắn Giọng Nói Telegram sang Google Docs bằng OpenAI & DeepSeek

Bạn có bao giờ phải **nghe lại hàng chục tin nhắn giọng nói trên Telegram**, gõ lại nội dung rồi tự tay viết bản tóm tắt?  
Công việc này vừa tốn thời gian, vừa dễ sai sót, đặc biệt khi cần chia sẻ nhanh cho đồng nghiệp hoặc lưu trữ.  

**Workflow này** sẽ giải quyết toàn bộ quy trình **100% tự động**:  
1️⃣ Nhận tin nhắn giọng nói từ Telegram →  
2️⃣ Dùng OpenAI Whisper chuyển thành văn bản →  
3️⃣ Dùng DeepSeek Chat tóm tắt nội dung →  
4️⃣ Tạo một tài liệu Google Docs chứa bản gốc + bản tóm tắt →  
5️⃣ Gửi lại link tài liệu cho người gửi ngay trong chat.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải nghe và gõ lại, chỉ cần gửi voice, mọi thứ tự động diễn ra.  
- **Độ chính xác cao**: Whisper và DeepSeek cung cấp bản chuyển đổi và tóm tắt chuẩn ngữ cảnh.  
- **Tự động lưu trữ**: Mỗi tin nhắn được ghi lại trong Google Docs, dễ tìm kiếm và chia sẻ.  
- **Hoạt động liên tục 24/7**: Khi n8n được triển khai trên VPS, workflow luôn sẵn sàng nhận tin mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token** (tạo bot qua @BotFather).  
- **Chat ID** hoặc **Username** của nhóm/kênh muốn nhận voice.  
- **OpenAI API Key** (có quyền sử dụng Whisper).  
- **DeepSeek API Key** (đăng ký tại deepseek.com).  
- **Google Drive OAuth credentials** (hoặc Service Account) có quyền **tạo file & Google Docs**.  
- **Folder ID** trên Google Drive nơi lưu các tài liệu (có thể để trống, workflow sẽ tạo thư mục mới).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc từ repo).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → Nhấn **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán nội dung JSON và **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **7 node** cần cấu hình chi tiết:

| Node | Loại | Cấu hình quan trọng |
|------|------|----------------------|
| **Telegram Trigger1** | `telegramTrigger` | - **Credentials**: Bot Token.<br>- **Chat ID**: Chỉ nhận tin từ nhóm/kênh muốn.<br>- **Event**: `Voice Message`. |
| **Telegram1** | `telegram` | - **Credentials**: Bot Token (cùng như trên).<br>- **Chat ID**: Để trả lời người gửi (có thể dùng `{{ $json["chat"]["id"] }}`). |
| **OpenAI2** | `openAi` | - **Credentials**: OpenAI API Key.<br>- **Model**: `whisper-1` (hoặc `gpt-4o-mini` nếu dùng transcription).<br>- **Input**: Đường dẫn file voice từ Telegram (được lưu tạm thời trong `binaryData`). |
| **DeepSeek Chat Model1** | `lmChatDeepSeek` | - **Credentials**: DeepSeek API Key.<br>- **Model**: `deepseek-chat`.<br>- **Prompt**: “Tóm tắt nội dung sau trong 3‑5 câu ngắn gọn, giữ nguyên ý chính.” |
| **AI Agent1** | `agent` | - **Chain**: Kết nối **OpenAI2** → **DeepSeek Chat Model1**.<br>- **Mode**: `Sequential` (đầu tiên transcribe, sau đó summarize). |
| **Google Drive** | `googleDrive` | - **Credentials**: Google OAuth.<br>- **Operation**: `Upload` (để lưu file voice gốc nếu muốn).<br>- **Folder ID**: Nhập ID thư mục lưu trữ (có thể để trống để tạo mới). |
| **Google Drive2** | `googleDrive` | - **Credentials**: Google OAuth.<br>- **Operation**: `Create` → **File Type**: `Google Docs`.<br>- **File Name**: `{{ $json["message_id"] }}_transcript.docx`.<br>- **Content**: Kết hợp **transcript** + **summary** (sử dụng expression `{{ $json["transcript"] }}\n\n---\n\n{{ $json["summary"] }}`). |

> **Lưu ý:**  
> - Đảm bảo **binary data** của voice được truyền từ `Telegram Trigger1` sang `OpenAI2`.  
> - Khi tạo Google Docs, bật **"Convert to Google Docs format"** để file có thể chỉnh sửa trực tiếp.  
> - Kiểm tra **scopes** trong Google OAuth: `https://www.googleapis.com/auth/drive.file` và `https://www.googleapis.com/auth/documents`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một voice note thử vào Telegram. Kiểm tra log của từng node trong n8n để chắc chắn dữ liệu được truyền đúng.  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Theo dõi **Execution Log** để phát hiện lỗi (nếu có) và điều chỉnh lại credentials hoặc folder ID.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack để gửi báo cáo mỗi khi có tài liệu mới được tạo.  
- **Lưu trữ raw transcript**: Dùng một Google Sheet để ghi lại thời gian, người gửi, và bản transcript gốc.  
- **Báo cáo định kỳ**: Dùng node **Cron** để tổng hợp các tài liệu trong tuần và gửi email tóm tắt.  
- **Xử lý lỗi**: Thêm node **Error Trigger** để gửi thông báo khi bất kỳ bước nào thất bại.  
- **Mở rộng ngôn ngữ**: Thay đổi model OpenAI sang `whisper-1` (hỗ trợ đa ngôn ngữ) và DeepSeek sang `deepseek-coder` nếu muốn tóm tắt code.

### 📌 Kết luận
Với workflow **“Transcribe & Summarize Telegram Voice Notes”**, các sếp có thể biến **một tin nhắn giọng nói** thành **tài liệu Google Docs** được tóm tắt chỉ trong vài giây, giảm thiểu công việc thủ công, tăng độ chính xác và lưu trữ thông tin một cách có hệ thống.  

👉 **Hãy triển khai ngay** trên VPS của mình, import workflow, cấu hình các credentials và để n8n tự động hoá công việc!  

Chúc các sếp thành công và luôn “voice‑first” mà không phải “type‑first”. 🚀