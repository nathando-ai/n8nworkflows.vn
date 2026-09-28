---
title: "🎙️ Tự Động Chuyển Ngữ Âm Telegram Sang Văn Bản Với OpenAI Whisper & Google Workspace (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi tất cả tin nhắn âm thanh Telegram thành văn bản bằng OpenAI Whisper, lưu trữ log trên Google Sheets và sao lưu âm thanh trên Google Drive - giúp các sếp tiết kiệm thời gian ghi chép và tìm kiếm thông tin nhanh chóng."
slug: "tich-hop-telegram-voice-voi-openai-whisper"
tags: [n8n, automation, no-code, ai-chuyen-doi-ngu-am, google-workspace, openai-whisper]
keywords: [n8n workflow tự động hóa, chuyển âm thanh Telegram thành văn bản, OpenAI Whisper tự động, lưu log Google Sheets, sao lưu âm thanh Google Drive]
---

# 🚀 **Tự Động Chuyển Ngữ Âm Telegram Sang Văn Bản Với AI (Không Cần Code)**

## **💥 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải:
- **Ghi chép tay** những cuộc gọi, phỏng vấn hoặc ghi chú âm thanh từ Telegram, mất thời gian và dễ bị lỗi.
- **Khó tìm kiếm** lại nội dung cũ trong hàng trăm tin nhắn âm thanh.
- **Không có bản sao lưu** cho các cuộc trò chuyện quan trọng.

Workflow này **giải quyết tất cả** bằng cách:
✅ **Chuyển tự động** mọi tin nhắn âm thanh Telegram thành văn bản chính xác.
✅ **Lưu log** trên Google Sheets với thời gian, độ dài, văn bản và liên kết tải âm thanh.
✅ **Sao lưu âm thanh** trên Google Drive để không mất dữ liệu.
✅ **Gửi phản hồi** ngay cho người dùng với kết quả và liên kết tải.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian** ghi chép so với cách thủ công.
- **Tìm kiếm nhanh** bằng cách tra cứu trên Google Sheets.
- **Chất lượng cao** với công nghệ OpenAI Whisper (độ chính xác >95%).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Bảo mật** với sao lưu âm thanh và log rõ ràng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Cấu hình bot trong n8n với **credentials `telegramApi`**.
2. **Google Workspace**:
   - Cấu hình **Google Drive** và **Google Sheets** với OAuth2 (credentials `googleDriveOAuth2Api` và `googleSheetsOAuth2Api`).
  . **OpenAI API Key**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm vào n8n với credentials `openAiApi`.
4. **File Google Sheets**:
   - Tạo một sheet mới với **cột: DateTime, Duration, Transcript, AudioURL**.
5. **n8n Self-hosted** (khuyến cáo):
   - Để workflow hoạt động liên tục, các sếp nên cài n8n trên **VPS** (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7123](https://n8n.io/workflows/7123) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  // (Dữ liệu JSON đầy đủ sẽ được cung cấp sau)
  ```
- **Nhấn "Import"** và chọn **Active** để kích hoạt workflow.

### **2. Các Bước Cấu Hình Bắt Buộc 📌**
#### **🔹 Node 1: Telegram Trigger**
- **Chọn credentials**: `telegramApi` (đã cấu hình trước).
- **Cài đặt Webhook URL**: Nếu self-hosted, sử dụng URL của máy chủ n8n (ví dụ: `https://your-domain.com/webhook`).
- **Test**: Gửi tin nhắn âm thanh đến bot để kiểm tra.

#### **🔹 Node 2: Is Audio Message? (If Condition)**
- **Điều kiện**: `$json["message"]["voice"] !== undefined`.
- **Nếu không phải âm thanh**, bot sẽ gửi tin nhắn: *"Chỉ chấp nhận tin nhắn âm thanh!"*.

#### **🔹 Node 3: Download Audio Message**
- **Chọn credentials**: `telegramApi`.
- **Tham số**: `$json["message"]["voice"]["file_id"]` (tự động lấy từ Telegram).
- **Lưu ý**: File âm thanh sẽ được tải về dưới dạng `.oga`.

#### **🔹 Node 4: Transcribe with OpenAI Whisper**
- **Chọn credentials**: `openAiApi`.
- **Tham số**:
  - `operation`: `transcribe`.
  - `resource`: Binary audio file từ node trước.
- **Mẹo**: Nếu muốn cải thiện độ chính xác, thêm **prompt** trong `parameters` (ví dụ: `"Transcribe this audio in Vietnamese"`).

#### **🔹 Node 5: Upload to Google Drive**
- **Chọn credentials**: `googleDriveOAuth2Api`.
- **Tham số**:
  - `fileName`: `$node["Download audio message"]["$json"]["file_name"]`.
  - `fileData`: Binary audio từ node 3.
- **Lưu ý**: Chọn **folder** sao lưu (ví dụ: `Voice Messages`).

#### **🔹 Node 6: Merge Outputs**
- **Kết hợp**:
  - Dữ liệu từ **transcription** (OpenAI).
  - Metadata từ **Google Drive** (liên kết tải file).
  - Thông tin từ **Telegram** (người gửi, thời gian).

#### **🔹 Node 7: Transform to Row Format (Code Node)**
- **Mã JavaScript**:
  ```javascript
  // Chuyển đổi dữ liệu thành định dạng phù hợp cho Google Sheets
  return {
    DateTime: new Date($node["Is audio message?"]["json"]["message"]["date"]).toISOString(),
    Duration: $node["Download audio message"]["json"]["duration"],
    Transcript: $node["Transcribe a recording"]["json"]["text"],
    AudioURL: $node["Upload file"]["json"]["webViewLink"]
  };
  ```

#### **🔹 Node 8: Log to Google Sheets**
- **Chọn credentials**: `googleSheetsOAuth2Api`.
- **Tham số**:
  - `sheetName`: `Voice_Transcripts` (hoặc tên sheet của các sếp).
  - `operation`: `append`.
- **Lưu ý**: Đảm bảo **cột đầu tiên** trong sheet là `DateTime` để n8n biết cách append.

#### **🔹 Node 9: Inform User via Telegram**
- **Thông báo cho người dùng**:
  ```json
  {
    "text": `🎤 Transcription completed!\n\n📝 Transcript:\n${$node["Transform the output"]["json"]["Transcript"]}\n\n🔗 Audio: ${$node["Transform the output"]["json"]["AudioURL"]}`
  }
  ```

---

### **⚡ Kích Hoạt Workflow**
1. **Test Run**:
   - Gửi tin nhắn âm thanh đến bot và kiểm tra:
     - Văn bản được transcribe chính xác không?
     - File âm thanh được upload lên Drive không?
     - Log được ghi vào Google Sheets không?
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để hoạt động liên tục.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM TIẾP]
1. **Thêm GPT-4 cho Tagging**:
   - Sử dụng **LangChain OpenAI** để tự động **tag** nội dung (ví dụ: "Quản lý dự án", "Khách hàng").
   ```javascript
   // Thêm vào Code Node trước khi log
   const response = await $node["openAi"]["execute"]({
     operation: "chat",
     parameters: {
       messages: [{ role: "user", content: `Tag this transcript: ${$node["Transform"]["json"]["Transcript"]}` }]
     }
   });
   return { ...$node["Transform"]["json"], Tags: response.json.choices[0].message.content };
   ```
2. **Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp từ Google Sheets qua Email/Telegram.
3. **Kết Nối Với Notion/Airtable**:
   - Thay thế Google Sheets bằng **Notion API** hoặc **Airtable** để quản lý dữ liệu linh hoạt hơn.
4. **Phân Loại Ngôn Ngữ**:
   - Thêm **ngôn ngữ mặc định** trong OpenAI Whisper (ví dụ: `"language": "vi"`).
5. **Sao Lưu Lịch Sử**:
   - Dùng **Google Drive** lưu phiên bản cũ của tin nhắn âm thanh.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc ghi chép thủ công, đồng thời **tăng cường tính chuyên nghiệp** với log rõ ràng và sao lưu an toàn. **Không cần code**, chỉ cần cấu hình theo hướng dẫn trên!

👉 **Bắt đầu ngay**:
1. Import workflow.
2. Cấu hình credentials.
3. Test và bật hoạt động!

**Cần hỗ trợ?** Liên hệ với tác giả tại [lets@automatewith.me](mailto:lets@automatewith.me) hoặc comment bên dưới. 🚀

---
**#n8n #Automation #AI #GoogleWorkspace #OpenAIWhisper**