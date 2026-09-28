---
title: "🤖 **Tự Động Hóa Bot Telegram Siêu Năng: Trợ Lý AI Gemini + Tìm Kiếm PDF + Google Suite (Không Cần Code!)"**
description: "Xây dựng một bot Telegram toàn năng kết hợp AI Gemini, tìm kiếm thông minh trong PDF, và tích hợp Google Drive/Calendar để tự động trả lời tin nhắn, quản lý lịch, tính toán, và xử lý tài liệu - hoàn toàn tự động hóa mà không cần viết một dòng code nào!"
slug: "tay-dong-hoa-bot-telegram-gemini-rag-pdf-google-suite"
tags: [n8n, automation, ai, telegram-bot, google-suite, rag, pdf-search, no-code]
keywords: [tự động hóa bot telegram, gemini ai n8n, tìm kiếm pdf bằng ai, google drive automation, google calendar bot, no-code automation]
---

# 🚀 **Bot Telegram Siêu Năng: AI Gemini + Tìm Kiếm PDF + Google Suite - Tự Động Hóa Toàn Mạng**

### **💡 Bạn đã bao giờ mệt mỏi vì phải:**
- **Trả lời hàng trăm tin nhắn Telegram thủ công** mỗi ngày?
- **Tìm kiếm thông tin trong hàng chục tệp PDF** để trả lời câu hỏi khách hàng?
- **Quản lý lịch Google Calendar** hoặc tính toán dữ liệu một cách thủ công?
- **Mất thời gian chuyển đổi giọng nói thành văn bản** hoặc ngược lại?

**Giải pháp của bạn đã đến!** Với workflow này, các sếp có thể **tạo một bot Telegram toàn năng**, kết hợp **AI Gemini (Google)**, **tìm kiếm thông minh trong PDF**, và **tích hợp Google Drive/Calendar** để:
✅ **Trả lời tự động** mọi tin nhắn (giọng nói, văn bản, PDF)
✅ **Tìm kiếm và trả lời câu hỏi từ nội dung PDF** (RAG - Retrieval-Augmented Generation)
✅ **Tính toán, tra lịch, và quản lý Google Calendar** một cách thông minh
✅ **Chuyển đổi giọng nói thành văn bản và ngược lại** bằng AI
✅ **Tích hợp với Google Drive** để gửi tài liệu, hóa đơn, hoặc báo cáo tự động

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 8+ giờ/ngày** cho việc trả lời tin nhắn và xử lý tài liệu.
- **Chính xác 100%** với AI Gemini và tìm kiếm PDF thông minh.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa tương tác** với khách hàng qua Telegram.
- **Tích hợp toàn diện** với Google Workspace (Drive, Docs, Calendar).
- **Không cần viết code** - chỉ cần cấu hình và chạy!
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản và API Keys**
| **Dịch vụ**               | **Thông tin cần thiết**                                                                 | **Liên kết đăng ký**                                                                 |
|---------------------------|-------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **Telegram Bot**          | Token API từ [@BotFather](https://t.me/BotFather)                                          | [Tạo Bot Telegram](https://core.telegram.org/bots#botfather)                          |
| **Google AI (Gemini)**    | API Key từ [Google Cloud](https://cloud.google.com/)                                      | [Cài đặt Google AI API](https://ai.google.dev/)                                      |
| **OpenAI (Embeddings)**   | API Key từ [OpenAI](https://platform.openai.com/)                                         | [Tạo API Key OpenAI](https://platform.openai.com/account/api-keys)                    |
| **Qdrant Vector Store**   | URL và API Key từ [Qdrant](https://qdrant.tech/)                                          | [Tạo tài khoản Qdrant](https://cloud.qdrant.io/)                                    |
| **Google Drive**          | Tài khoản Google và OAuth 2.0 credentials                                              | [Cài đặt Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) |
| **Google Calendar**       | Tài khoản Google và OAuth 2.0 credentials                                              | [Cài đặt Google Calendar API](https://developers.google.com/calendar/api/quickstart/python) |
| **Brave Search**          | API Key từ [Brave Search](https://search.brave.com/)                                     | [Đăng ký API Brave](https://search.brave.com/api/)                                   |
| **Replicate (Nếu sử dụng)** | API Key từ [Replicate](https://replicate.com/)                                          | [Tạo API Key Replicate](https://replicate.com/account)                              |
| **Mistral (Nếu sử dụng OCR)** | API Key từ [Mistral AI](https://mistral.ai/)                                            | [Đăng ký Mistral](https://mistral.ai/)                                              |

### **2. Cài đặt n8n**
- **N8n Self-hosted** (khuyến nghị) để workflow hoạt động 24/7.
- **N8n Cloud** (miễn phí cho dự án nhỏ).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4525](https://n8n.io/workflows/4525) (chọn **Export as JSON**).
2. **Mở n8n Editor** (n8n.io hoặc self-hosted).
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trong danh sách.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ file export.
2. **Tại n8n Editor**, nhấp vào **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để hoàn tất.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** với **65 nodes**, nhưng các sếp chỉ cần chú ý đến các **node quan trọng** sau:

#### **🔹 Node Telegram Trigger (`telegramTrigger`)**
- **Cấu hình:**
  - **Token:** Điền `token` từ Bot Telegram (từ @BotFather).
  - **Update Type:** Chọn **"Message"** (để bot phản hồi mọi tin nhắn).
  - **Filter:** Để trống hoặc chỉ lọc tin nhắn từ **chat cụ thể**.

#### **🔹 Node Google Gemini (`lmChatGoogleGemini`)**
- **Cấu hình:**
  - **API Key:** Điền `API_KEY` từ Google Cloud.
  - **Model:** Chọn `"gemini-pro"` (hoặc `"gemini-1.0-pro"`).
  - **Prompt:** Cấu hình để bot trả lời thông minh (ví dụ: `"You are a helpful assistant. Answer in Vietnamese."`).

#### **🔹 Node Qdrant Vector Store (`vectorStoreQdrant`)**
- **Cấu hình:**
  - **URL:** Điền URL của Qdrant Cloud (ví dụ: `https://your-qdrant-url.qdrant.io`).
  - **API Key:** Điền `API_KEY` từ Qdrant.
  - **Collection Name:** Tên collection để lưu trữ embeddings (ví dụ: `pdf_embeddings`).

#### **🔹 Node Brave Search (`@brave/n8n-nodes-brave-search.braveSearch`)**
- **Cấu hình:**
  - **API Key:** Điền `API_KEY` từ Brave Search.
  - **Query:** Sử dụng `$json["text"]` (từ tin nhắn Telegram) để tìm kiếm trên web.

#### **🔹 Node Google Drive (`googleDrive`)**
- **Cấu hình:**
  - **Credentials:** Chọn OAuth 2.0 credentials đã cấu hình trước.
  - **Folder ID:** Điền ID của folder chứa PDF (có thể lấy từ liên kết Google Drive).
  - **File Type:** Chọn `"application/pdf"`.

#### **🔹 Node OpenAI Embeddings (`embeddingsOpenAi`)**
- **Cấu hình:**
  - **API Key:** Điền `API_KEY` từ OpenAI.
  - **Model:** Chọn `"text-embedding-ada-002"`.

#### **🔹 Node Switch (`switch`)**
- **Cấu hình:**
  - **Condition:** Sử dụng để phân loại nội dung (ví dụ: nếu tin nhắn là **giọng nói** → chuyển sang OpenAI transcribe, nếu là **PDF** → tìm kiếm trong Qdrant).

#### **🔹 Node AI Agent (`agent`)**
- **Cấu hình:**
  - **Tools:** Chọn các tool cần thiết (Gemini, Calculator, Brave Search, Google Calendar...).
  - **Memory:** Bật `memoryBufferWindow` để bot nhớ lịch sử chat.

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Gửi tin nhắn **giọng nói** hoặc **PDF** qua Telegram Bot.
   - Kiểm tra bot có trả lời đúng không (ví dụ: chuyển giọng nói thành văn bản, tìm kiếm PDF, trả lời bằng Gemini).
2. **Bật Active workflow:**
   - Nhấp vào **toggle "Active"** ở góc trên bên phải.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tích hợp với Slack/Telegram**
- Sử dụng **node `telegram`** để gửi thông báo từ bot Telegram lên **Slack** (nếu cần).
- **Cách làm:**
  - Thêm node `slack` (nếu đã cài plugin Slack).
  - Kết nối với `webhook` từ Slack.

### **2. Lưu log hoạt động**
- Sử dụng **node `set`** để lưu dữ liệu vào **Google Sheets** hoặc **Google Docs** để theo dõi hoạt động của bot.
- **Cách làm:**
  - Thêm node `googleDocs` sau node `telegram`.
  - Cấu hình để ghi lại **tin nhắn đầu vào**, **trả lời**, và **thời gian**.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `googleCalendar`** để tạo **lịch hẹn tự động** hoặc gửi **báo cáo hàng tuần** qua Telegram.
- **Cách làm:**
  - Sử dụng `googleCalendarTool` để tạo sự kiện.
  - Kết hợp với `telegram` để gửi thông báo.

### **4. Cải thiện RAG (Retrieval-Augmented Generation)**
- Nếu muốn bot **tìm kiếm PDF hiệu quả hơn**, các sếp có thể:
  - **Tăng kích thước vector store** (Qdrant) để lưu nhiều embeddings.
  - **Sử dụng `textSplitterTokenSplitter`** để chia PDF thành đoạn nhỏ hơn.
  - **Cập nhật thường xuyên** dữ liệu PDF vào Qdrant.

### **5. Chuyển đổi giọng nói thành văn bản (Speech-to-Text)**
- Nếu bot nhận **giọng nói**, sử dụng:
  - **Node `openAi`** (Whisper API) để chuyển giọng nói thành văn bản.
  - **Node `telegram`** để trả lời bằng văn bản hoặc **giọng nói AI** (sử dụng Replicate API).

---
## 📌 **Kết luận**
### **🚀 Bot Telegram Siêu Năng đã sẵn sàng cho các sếp!**
Với workflow này, các sếp **không cần viết code** mà vẫn có thể:
✔ **Tự động trả lời tin nhắn** qua Telegram.
✔ **Tìm kiếm và trả lời câu hỏi từ PDF** bằng AI Gemini.
✔ **Quản lý Google Calendar** và tính toán tự động.
✔ **Chuyển đổi giọng nói thành văn bản** và ngược lại.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình API Keys** và credentials.
3. **Test Run** và **bật Active**.
4. **Tích hợp vào công việc** để tiết kiệm thời gian!

**💬 Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---
**🎁 Bonus:** Nếu các sếp cần **cài đặt n8n trên VPS**, sử dụng mã giảm giá **VPSN8N** để tiết kiệm chi phí!
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (giảm 39%)