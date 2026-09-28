---
title: "🤖 Tự Động Hóa Trợ Lý AI Bảo Mật Trên Telegram Với Ollama & Whisper - Không Cần Code!"
description: "Workflow này tự động hóa việc tạo trợ lý AI đa phương tiện (text + voice) trên Telegram, sử dụng mô hình Ollama (cài đặt offline) và công nghệ transcribe Whisper để xử lý âm thanh thành văn bản. Giúp các sếp tiết kiệm thời gian, bảo mật dữ liệu và tương tác tự nhiên với khách hàng 24/7."
slug: "tay-dong-hoa-tro-ly-ai-telegram-ollama-whisper"
tags: [n8n, automation, ai-chatbot, ollama, whisper, telegram-bot]
keywords: [n8n workflow ai, tự động hóa trợ lý ai, ollama n8n, whisper asr n8n, bot telegram tự động]
---

# 🚀 **Tạo Trợ Lý AI Bảo Mật Trên Telegram Với Ollama & Whisper (Không Cần Code!)**

### **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hiện nay, nhiều doanh nghiệp và cá nhân đang gặp khó khăn khi:
- **Tương tác với khách hàng qua âm thanh** (gọi điện, voice message) nhưng phải chuyển đổi thủ công sang văn bản.
- **Sử dụng AI chatbot** nhưng phải phụ thuộc vào cloud (OpenAI, Mistral), gây lo ngại về **bảo mật dữ liệu**.
- **Không có giải pháp tự động hóa** để xử lý cả **text và voice** trong Telegram một cách liên tục.

**Workflow này giải quyết tất cả!** Nó cho phép bạn:
✅ **Xử lý âm thanh → văn bản** (Whisper) và **văn bản → AI trả lời** (Ollama) **tự động**.
✅ **Cài đặt hoàn toàn offline** (Ollama chạy trên máy chủ riêng), **không phụ thuộc vào cloud**.
✅ **Bảo mật cao** (chỉ người được ủy quyền mới có thể sử dụng).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chuyển đổi âm thanh thành văn bản thủ công.
- **Tương tác tự nhiên**: Khách hàng có thể gửi **text hoặc voice**, trợ lý AI trả lời ngay lập tức.
- **Bảo mật dữ liệu**: Tất cả xử lý diễn ra **offline** (không gửi dữ liệu lên cloud).
- **Hoạt động liên tục**: Trợ lý AI **chạy 24/7** mà không cần người quản lý.
- **Cá nhân hóa**: AI nhớ lịch sử hội thoại (thông qua `memoryBufferWindow`).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Telegram Bot** (để tạo bot và lấy `API Token`).
✔ **API Key Ollama** (để kết nối với mô hình `llama3.2:1b`).
✔ **Mô hình Ollama đã cài đặt** (cần cài đặt mô hình `llama3.2:1b` trước).
✔ **Whisper API** (sử dụng `httpRequest` để transcribe âm thanh).
✔ **VPS hoặc máy chủ riêng** (để chạy n8n **self-hosted** 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import từ file JSON** hoặc **copy/paste JSON** vào n8n Editor.

#### **Cách import từ file JSON:**
1. Tải workflow từ [đây](https://n8n.io/workflows/6012) (nếu có link trực tiếp).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. Chọn **Create New Workflow** → Đặt tên (ví dụ: `AI_Assistant_Telegram`).

#### **Cách copy/paste JSON:**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Dán JSON từ [workflow gốc](https://n8n.io/workflows/6012) (hoặc file JSON đã tải).
3. Nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Telegram Trigger**
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi`.
  - **Chat ID**: Đặt là `@username_bot` (hoặc ID chat cụ thể).
  - **Event**: Chọn `message` (để bắt tất cả tin nhắn mới).

#### **🔹 Node 2: Get Voice File (Nếu có âm thanh)**
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi`.
  - **Resource**: `file` (để lấy file âm thanh).
  - **Lưu ý**: Chỉ hoạt động khi người dùng gửi **voice message**.

#### **🔹 Node 3: Message Type Switch**
- **Cấu hình**:
  - **Switch Condition**:
    - Nếu `type` == `voice` → Chuyển sang **Whisper ASR**.
    - Nếu `type` == `text` → Chuyển sang **AI Agent**.

#### **🔹 Node 4: Authorization Check If**
- **Cấu hình**:
  - **Condition**: Kiểm tra `chat.id` có trong danh sách **người được phép** (ví dụ: `chat.id == "123456789"`).
  - **Nếu không thỏa mãn**: Gửi tin nhắn **"Bạn không có quyền sử dụng trợ lý này!"** (sử dụng **Send a text message**).

#### **🔹 Node 5: Whisper ASR HTTP Request**
- **Cấu hình**:
  - **URL**: `http://localhost:9000/api/v1/audio` (nếu sử dụng Whisper API cục bộ).
  - **Headers**:
    ```json
    {
      "Content-Type": "multipart/form-data"
    }
    ```
  - **Body**: Chọn `file` (file âm thanh từ Telegram).
  - **Lưu ý**: Nếu không có Whisper API, có thể sử dụng **Ollama + Whisper** (cài đặt mô hình `whisper` trong Ollama).

#### **🔹 Node 6: Ollama Chat Model**
- **Cấu hình**:
  - **Credentials**: `ollamaApi`.
  - **Model**: `llama3.2:1b` (mô hình đã cài đặt trong Ollama).
  - **Prompt**: Cấu hình như sau:
    ```json
    {
      "role": "user",
      "content": "Tôi là trợ lý AI bảo mật. Hãy trả lời tin nhắn của người dùng một cách thân thiện và chuyên nghiệp."
    }
    ```
  - **Lưu ý**: Nếu không có `ollamaApi`, cần tạo **credentials mới** trong n8n:
    - **Type**: `ollama`.
    - **Host**: `http://localhost:11434`.

#### **🔹 Node 7: Simple Memory (memoryBufferWindow)**
- **Cấu hình**:
  - **Window Size**: `5` (lưu 5 tin nhắn gần nhất).
  - **Key**: `chat_history` (để AI nhớ lịch sử hội thoại).

#### **🔹 Node 8: Rename Transcription Key**
- **Cấu hình**:
  - **Old Key**: `transcription` (tên key từ Whisper).
  - **New Key**: `text` (để AI xử lý dễ dàng).

#### **🔹 Node 9: Send Response (Telegram)**
- **Cấu hình**:
  - **Credentials**: `telegramApi`.
  - **Text**: Sử dụng `{{ $json["response"] }}` (trả lời từ AI).
  - **Lưu ý**: Nếu là **âm thanh**, có thể gửi file âm thanh transcribe lại.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một **text hoặc voice message** từ Telegram đến bot.
   - Kiểm tra nếu AI trả lời đúng.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Email**
- Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** để gửi báo cáo hoặc thông báo khi có tin nhắn mới.

### **🔹 Lưu Log Tất Cả Hội Thoại**
- Thêm **node `n8n-nodes-base.database`** (SQLite) để lưu tất cả lịch sử hội thoại.

### **🔹 Cập Nhật Mô Hình Ollama**
- Nếu muốn sử dụng mô hình mới, chỉ cần **cài đặt mô hình mới trong Ollama** và thay đổi `model` trong **Ollama Chat Model**.

### **🔹 Bảo Mật Nâng Cao**
- Thêm **node `n8n-nodes-base.if`** để kiểm tra **IP hoặc token** trước khi cho phép truy cập.

---

## 📌 **Kết Luận**
Workflow này giúp các sếp **tạo một trợ lý AI bảo mật, tự động hóa hoàn toàn** trên Telegram, xử lý cả **text và voice** mà không cần code. **Không phụ thuộc vào cloud**, đảm bảo **bảo mật cao** và **hoạt động 24/7**.

**Hãy áp dụng ngay và tự động hóa tương tác với khách hàng của mình!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** để chạy workflow ổn định: [TinoHost](https://tino.vn/vps-n8n?affid=388)
- **Hỏi đáp cộng đồng n8n**: [Discord n8n](https://discord.gg/n8n)