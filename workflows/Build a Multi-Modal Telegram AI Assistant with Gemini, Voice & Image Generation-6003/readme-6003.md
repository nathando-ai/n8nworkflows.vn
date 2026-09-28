---
title: "🤖 **Tự Động Hóa Trợ Lý AI Telegram Multi-Mô Hình: Nhận Văn Bản, Âm Thanh & Tạo Hình - Sử Dụng Gemini, MongoDB & TTS**"
description: "Xây dựng một trợ lý AI Telegram thông minh hỗ trợ 3 mô hình: xử lý văn bản thông minh với Gemini, chuyển âm thanh thành văn bản + tạo hình từ âm thanh, và lưu trữ trí nhớ thông minh trên MongoDB. Giúp các sếp tự động hóa hỗ trợ khách hàng, quản lý công việc và tạo nội dung 24/7 mà không cần code."
slug: "tay-dong-hoa-tro-ly-ai-telegram-multi-modal-gemini"
tags: [n8n, automation, ai-chatbot, google-gemini, multi-modal, telegram-bot, mongodb, voice-to-text, image-generation, no-code]
keywords: [n8n workflow telegram ai, tự động hóa trợ lý ai, gemini api n8n, chuyển âm thanh thành văn bản tự động, tạo hình từ âm thanh, lưu trí nhớ ai trên mongodb, tự động hóa hỗ trợ khách hàng]
---

# **🚀 Xây Dựng Trợ Lý AI Telegram Multi-Mô Hình: Nhận Văn Bản, Âm Thanh & Tạo Hình**

## **💡 Giới Thiệu: Giải Pháp AI "Tất Tài" Cho Doanh Nghiệp & Cá Nhân**
Hiện nay, các sếp và doanh nghiệp thường phải mất nhiều thời gian để:
- **Trả lời khách hàng** qua Telegram một cách chậm chạp và không đồng nhất.
- **Quản lý công việc** bằng cách ghi nhớ thông tin qua nhiều ứng dụng khác nhau (Google Calendar, Google Tasks, Google Sheets).
- **Tạo nội dung** từ âm thanh hoặc hình ảnh mà không cần chuyển đổi thủ công.
- **Lưu trữ trí nhớ** của AI một cách logic và có thể truy xuất lại.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Xử lý văn bản thông minh** với Google Gemini (AI đa nhiệm hàng đầu).
✅ **Chuyển âm thanh thành văn bản** và **tạo hình từ âm thanh** (sử dụng API chuyển đổi âm thanh và mô hình tạo hình).
✅ **Lưu trí nhớ AI** trên MongoDB để hỗ trợ các cuộc trò chuyện sau này.
✅ **Trả lời bằng âm thanh** (TTS - Text-to-Speech) để tăng trải nghiệm người dùng.
✅ **Tích hợp với Google Workspace** (Calendar, Tasks, Sheets) để tự động hóa quản lý công việc.
✅ **Hỗ trợ đa nhiệm** với các lệnh như `/gf_on` (chế độ ghi nhớ tự động) và `/gf_off`.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Trợ lý AI trả lời khách hàng và xử lý công việc thay vì các sếp.
- **Chính xác & cá nhân hóa**: AI nhớ lại lịch sử trò chuyện và sử dụng trí nhớ để trả lời thông minh.
- **Hỗ trợ đa kênh**: Nhận cả văn bản, âm thanh và tạo hình từ âm thanh.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, tự động hóa toàn bộ quy trình.
- **Tích hợp sâu**: Kết nối với Google Workspace, Telegram và MongoDB để quản lý dữ liệu hiệu quả.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
- **Telegram Bot Token**: [Tạo bot Telegram](https://core.telegram.org/bots#botfather) và lấy `API Token`.
- **Google Cloud API**:
  - [Google Gemini API](https://ai.google.dev/gemini-api/docs/quickstart) (miễn phí 1 triệu credit/tháng).
  - [Google Cloud Natural Language API](https://cloud.google.com/natural-language) (phân tích cảm xúc, tóm tắt văn bản).
  - [Google Tasks API](https://developers.google.com/tasks) (quản lý công việc).
  - [Google Calendar API](https://developers.google.com/calendar) (quản lý lịch).
  - [Google Sheets API](https://developers.google.com/sheets) (lưu trạng thái chế độ ghi nhớ).
- **MongoDB Atlas**: [Đăng ký miễn phí](https://www.mongodb.com/atlas/database) để lưu trí nhớ AI.
- **Edge-TTS API** (hoặc [ElevenLabs](https://elevenlabs.io/)): Chuyển văn bản thành âm thanh.
- **API Chuyển Âm Thanh Thành Văn Bản** (ví dụ: [ACRCloud](https://www.acrcloud.com/) hoặc [Whisper API](https://platform.openai.com/docs/guides/text-to-speech)).
- **API Tạo Hình Từ Văn Bản** (ví dụ: [Stable Diffusion API](https://stability.ai/) hoặc [DALL·E 3](https://platform.openai.com/docs/guides/images)).

#### **2. Cấu Hình N8n**
- **Self-hosted n8n** (khuyến nghị) để lưu trữ dữ liệu riêng tư.
- **Docker** (nếu tự cài đặt) hoặc sử dụng [n8n Cloud](https://n8n.io/) (miễn phí 1000 credit/tháng).
- **Google Workspace Account**: Để kết nối với Google Tasks, Calendar và Sheets.

#### **3. Cấu Hình MongoDB**
- Tạo một **database** mới và **collection** (`user_memory`, `memory_auto`) để lưu trí nhớ AI.
- Cấu hình **credentials** trong n8n với URI MongoDB và tên database.

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/6003](https://n8n.io/workflows/6003) (chọn "Export").
2. **Mở n8n Editor** và nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn "Create New Workflow"** và nhấn **"Import"**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên và mở bằng Notepad++/VS Code.
2. **Copy toàn bộ nội dung JSON**.
3. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"** và dán nội dung.
4. **Chọn "Create New Workflow"** và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** với 84 nodes, nhưng sau đây là **các bước quan trọng** cần chú ý:

#### **🔹 1. Cấu Hình Telegram Trigger**
- **Node: `Telegram Trigger1`**
  - Điền `Telegram Bot Token` vào `Bot Token`.
  - Chọn `Update` (để bắt tất cả tin nhắn mới).
  - **Lưu ý**: Cần **thêm bot vào Telegram** và gửi tin nhắn thử để kích hoạt trigger.

#### **🔹 2. Cấu Hình MongoDB**
- **Nodes: `Fetch User Memory2`, `MongoDB Chat Memory1`, `Save Conversation Memory on user_memory1`**
  - **URI MongoDB**: `mongodb+srv://<username>:<password>@cluster0.example.mongodb.net/database?retryWrites=true&w=majority`
  - **Database Name**: Tên database của bạn (ví dụ: `n8n_ai_memory`).
  - **Collections**:
    - `user_memory` (lưu trí nhớ cá nhân).
    - `memory_auto` (lưu trí nhớ tự động).
  - **Operation**: Đảm bảo `insert` và `find` hoạt động đúng.

#### **🔹 3. Cấu Hình Google Gemini**
- **Nodes: `Google Gemini Chat Model7`, `Google Gemini Chat Model8`, ...**
  - **API Key**: Lấy từ [Google Cloud Console](https://console.cloud.google.com/apis/credentials).
  - **Model**: Chọn `gemini-pro` (mô hình mạnh nhất).
  - **Prompt Template**: Các node `chainLlm` và `agent` sử dụng **cấu trúc prompt** để phân tích ý định (intent) và xây dựng context. **Không chỉnh sửa** trừ khi biết rõ cấu trúc.

#### **🔹 4. Cấu Hình API Chuyển Âm Thanh Thành Văn Bản**
- **Nodes: `HTTP Request Fetch Voice Message Audio1`, `Submit Audio Transcription Job1`**
  - **API Endpoint**: Ví dụ với ACRCloud:
    ```json
    {
      "url": "https://api.acrcloud.com/convert",
      "method": "POST",
      "headers": {
        "Content-Type": "application/json",
        "Authorization": "Bearer YOUR_ACR_API_KEY"
      },
      "body": {
        "format": "json",
        "file": "${{ $json['file'] }}",
        "lang": "en"
      }
    }
    ```
  - **Lưu ý**: Cần **upload file âm thanh** từ Telegram vào API trước khi chuyển đổi.

#### **🔹 5. Cấu Hình Edge-TTS (Text-to-Speech)**
- **Nodes: `Run Edge-TTS1`, `Read MP3 File1`**
  - **API Endpoint**: Ví dụ với Edge-TTS:
    ```json
    {
      "url": "https://api.edgetts.com/v1/text-to-speech",
      "method": "POST",
      "headers": {
        "Authorization": "Bearer YOUR_EDGE_TTS_API_KEY",
        "Content-Type": "application/json"
      },
      "body": {
        "text": "${{ $json['text'] }}",
        "voice": "en-US-Neural2-A"
      }
    }
    ```
  - **Lưu ý**: File âm thanh sẽ được gửi về Telegram dưới dạng `sendAudio`.

#### **🔹 6. Cấu Hình Google Workspace**
- **Nodes: `Google Tasks`, `Google Calendar`, `Google Sheets`**
  - **Service Account Email**: Tạo trong [Google Cloud Console](https://console.cloud.google.com/).
  - **JSON Key File**: Upload vào n8n để xác thực.
  - **Google Sheets**:
    - **Sheet Name**: `GF_Mode` (để lưu trạng thái chế độ ghi nhớ tự động).
    - **Range**: `A1:A1` (để ghi `TRUE`/`FALSE`).

#### **🔹 7. Cấu Hình Chế Độ Ghi Nhớ Tự Động (`/gf_on` & `/gf_off`)**
- **Nodes: `Check GF Mode Status1`, `Google Sheets:Set GF Mode TRUE1/FALSE1`**
  - Khi người dùng gửi `/gf_on`, hệ thống sẽ **ghi nhớ tất cả cuộc trò chuyện** vào MongoDB.
  - Khi gửi `/gf_off`, hệ thống **ngừng ghi nhớ** và **xóa dữ liệu cũ** (nếu cần).

#### **🔹 8. Cấu Hình Tạo Hình Từ Âm Thanh**
- **Nodes: `HTTP Request for image generation on voice input1`**
  - Sử dụng API như **DALL·E 3** hoặc **Stable Diffusion**:
    ```json
    {
      "url": "https://api.openai.com/v1/images/generations",
      "method": "POST",
      "headers": {
        "Authorization": "Bearer YOUR_OPENAI_API_KEY",
        "Content-Type": "application/json"
      },
      "body": {
        "prompt": "${{ $json['prompt'] }}",
        "n": 1,
        "size": "1024x1024"
      }
    }
    ```
  - **Lưu ý**: Prompt sẽ được tạo từ **tóm tắt âm thanh** (node `Summarize Voice Message1`).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Gửi tin nhắn văn bản hoặc âm thanh đến bot Telegram.
   - Kiểm tra:
     - AI có trả lời đúng không?
     - Trí nhớ có được lưu không?
     - Âm thanh được chuyển đổi thành văn bản và tạo hình thành công không?

2. **Bật Active Workflow**:
   - Nhấn **"Active"** trên n8n Editor.
   - **Monitor Logs** để đảm bảo không có lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Trí Nhớ AI**
- **Sử dụng `Google Cloud Natural Language`** để phân tích **cảm xúc** trong cuộc trò chuyện và điều chỉnh phản hồi.
- **Tạo các "Intent Template"** riêng cho doanh nghiệp (ví dụ: phân tích yêu cầu hỗ trợ khách hàng).

### **2. Tích Hợp Slack/Email**
- **Thêm node `webhook`** để nhận tin nhắn từ Slack/Email và chuyển sang Telegram.
- **Cấu hình `HTTP Request`** để gửi phản hồi về Slack/Email.

### **3. Lưu Log & Báo Cáo**
- **Thêm node `Set`** để lưu **log hoạt động** vào MongoDB hoặc Google Sheets.
- **Tạo báo cáo hàng tuần** về:
  - Số lượng cuộc trò chuyện.
  - Thời gian phản hồi trung bình.
  - Top các câu hỏi thường gặp.

### **4. Cập Nhật Mô Hình AI**
- Khi Google phát hành **Gemini Pro Vision** (hỗ trợ hình ảnh), cập nhật **prompt** trong nodes `chainLlm` để xử lý hình ảnh.

### **5. Bảo Mật Dữ Liệu**
- **Mã hóa API Key** trong n8n bằng `n8n-nodes-base.encrypt`.
- **Xóa dữ liệu nhạy cảm** sau một thời gian (ví dụ: 30 ngày).

---
## **📌 Kết Luận: Áp Dụng Ngay Để Tự Động Hóa Trợ Lý AI**
Workflow này là **giải pháp hoàn chỉnh** để các sếp:
✔ **Tự động hóa hỗ trợ khách hàng** 24/7.
✔ **Quản lý công việc** thông minh với Google Workspace.
✔ **Tạo nội dung từ âm thanh** mà không cần chuyển đổi thủ công.
✔ **Lưu trí nhớ AI** để cuộc trò chuyện trở nên cá nhân hóa hơn.

**🚀 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để lưu trữ dữ liệu riêng tư).
2. **Import workflow** và cấu hình các API.
3. **Test với dữ liệu mẫu** và bật hoạt động.

---
### **🔗 Tài Nguyên Tham Khảo**
- [Tutorial Cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting/)
- [Google Gemini API Docs](https://ai.google.dev/gemini-api/docs/quick