---
title: "🤖 **Tự Động Hóa Hệ Thống AI Multi-Agent: Tích Hợp Qdrant, Gmail & OpenAI Với n8n - Giải Pháp Tối Ưu Cho Doanh Nghiệp**"
description: "Workflow này xây dựng hệ thống AI Multi-Agent hoàn chỉnh để tự động trích xuất, tổng hợp tài liệu từ Google Drive, tương tác với Gmail, và trả lời câu hỏi thông minh bằng RAG + OpenAI. Giúp các sếp tiết kiệm thời gian lên đến 80% trong việc xử lý thông tin và quản lý email."
slug: "tich-hop-multi-agent-n8n-qdrant-gmail-openai"
tags: [n8n, automation, ai-chatbot, document-extraction, no-code, qdrant, openai, gmail-api, langchain]
keywords: [n8n workflow multi-agent, tự động hóa AI, tích hợp Qdrant với n8n, tổng hợp tài liệu tự động, chatbot doanh nghiệp, OpenAI GPT-4o, Gmail automation]
---

# 🚀 **Xây Dựng Hệ Thống AI Multi-Agent Tự Động: Trích Xuất Tài Liệu, Quản Lý Email & Trả Lời Câu Hỏi Thông Minh**

## **📌 Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp thường phải mất **giờ đồng hồ** mỗi ngày để:
- **Tìm kiếm và tổng hợp thông tin** từ hàng trăm tài liệu trên Google Drive.
- **Quản lý email** (đọc, trả lời, tạo bản nháp) trong khi phải xử lý nhiều công việc khác.
- **Trả lời câu hỏi phức tạp** của khách hàng hoặc đồng nghiệp dựa trên kiến thức phân tán.
- **Cập nhật thông tin mới nhất** từ nguồn tin tức hoặc dữ liệu ngoài.

**Workflow này giải quyết tất cả những vấn đề trên bằng một hệ thống AI tự động hóa 100% không cần code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và tối ưu hiệu suất, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** với tài nguyên mạnh mẽ.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** trong việc xử lý tài liệu và email.
✅ **Tổng hợp thông tin chính xác** từ nhiều nguồn (Google Drive, Gmail, API tin tức).
✅ **Trả lời câu hỏi thông minh** bằng AI RAG (Retrieval-Augmented Generation) kết hợp OpenAI.
✅ **Tự động hóa tương tác email** (đọc, trả lời, tạo bản nháp) mà không cần can thiệp thủ công.
✅ **Cập nhật dữ liệu thời gian thực** từ API tin tức hoặc nguồn ngoài.
✅ **Hoạt động liên tục 24/7** trên VPS, không phụ thuộc vào máy tính cá nhân.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Mô Tả**                                                                 | **Liên Kết Đăng Ký**                          |
|----------------------|----------------------------------------------------------------------------|-----------------------------------------------|
| **Google Drive**     | Tài khoản Google để truy cập folder chứa tài liệu.                       | [Google Cloud Console](https://console.cloud.google.com/) |
| **Gmail**            | Tài khoản Gmail để tương tác (đọc, gửi, tạo bản nháp).                 | [Gmail](https://mail.google.com/)              |
| **Qdrant**           | API Key để kết nối với vector database (đã có sẵn collection mẫu).      | [Qdrant](https://qdrant.tech/)                |
| **OpenAI**           | API Key để sử dụng mô hình GPT-4o.                                        | [OpenAI API](https://platform.openai.com/api-keys) |
| **OpenRouter**       | API Key để sử dụng mô hình Gemini (nếu cần thay thế OpenAI).             | [OpenRouter](https://openrouter.ai/)          |
| **News API**         | API Key để lấy tin tức thời gian thực (tùy chọn).                       | [NewsAPI](https://newsapi.org/)               |

#### **2. Folder Google Drive**
- **Link mẫu**: [Folder chứa tài liệu](https://drive.google.com/drive/u/2/folders/1BevhU5qdgNDFbK4D9oAYGeK0Dt5sEaxQ)
- Các sếp có thể **tạo folder riêng** và cập nhật đường dẫn trong node **"Get Document"**.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [workflow gốc](https://n8n.io/workflows/11525) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.

**Bước 2:** Nhấn **"Import"** và chọn **"From JSON"** trong giao diện n8n.

```json
// (Dữ liệu JSON đầy đủ sẽ được cung cấp sau khi các sếp xác nhận)
```

**Lưu ý:** Nếu import từ file, đảm bảo **không có lỗi syntax** (dùng trình soạn thảo như VS Code để kiểm tra).

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **3 sub-agent chính** và **1 công cụ tin tức**, mỗi phần cần cấu hình kỹ lưỡng:

##### **🔹 Sub-Agent RAG (Retrieval-Augmented Generation)**
- **Node "Search Documents" (vectorStoreQdrant):**
  - Điền **Qdrant API Key** vào **credentials** (`qdrantApi`).
  - Kiểm tra **collection name** (mặc định là `n8n-rag-2437367325990310-2025-11-04-10-41-54`).
  - **Lưu ý:** Nếu sử dụng collection riêng, cập nhật tên trong **Parameters > Collection Name**.

- **Node "Get Document" (googleDrive):**
  - Chọn **credentials** (`googleDriveOAuth2Api`).
  - Điền **folder ID** từ URL Google Drive của các sếp (thay thế `1BevhU5qdgNDFbK4D9oAYGeK0Dt5sEaxQ`).
  - **Lưu ý:** Cần cấp quyền **"Google Drive API"** trong [Google Cloud Console](https://console.cloud.google.com/).

- **Node "Generate Embeddings" (embeddingsOpenAi):**
  - Chọn **credentials** (`openAiApi`).
  - Kiểm tra **model** (mặc định là `text-embedding-ada-002`).

##### **🔹 Sub-Agent Gmail**
- **Node "Get multiple messages in Gmail" & "Read a message in Gmail":**
  - Chọn **credentials** (`gmailOAuth2`).
  - **Lưu ý:** Cần **cấp quyền OAuth 2.0** cho Gmail trong [Google Cloud Console](https://console.cloud.google.com/).
  - **Scope cần chọn:**
    - `https://www.googleapis.com/auth/gmail.readonly` (đọc email)
    - `https://www.googleapis.com/auth/gmail.send` (gửi email)
    - `https://www.googleapis.com/auth/gmail.drafts` (tạo bản nháp)

- **Node "Send a message in Gmail" & "Create a draft in Gmail":**
  - **Lưu ý:** Nếu không muốn gửi email tự động, các sếp có thể **bỏ qua** hoặc cấu hình **ngăn chặn gửi** bằng cách kiểm tra `jsonata` trong node.

##### **🔹 Main AI Agent**
- **Node "Generate Summary" & "Generate Agent Response":**
  - Chọn **credentials** (`openAiApi`).
  - **Model mặc định:** `gpt-4o` (tối ưu cho tốc độ và hiệu suất).
  - **Lưu ý:** Nếu budget hạn chế, có thể thay thế bằng `gpt-3.5-turbo`.

- **Node "Generate Gmail sub-agent Response":**
  - Chọn **credentials** (`openRouterApi`).
  - **Model mặc định:** `google/gemini-2.5-flash` (tương thích với OpenRouter).

##### **🔹 Công Cụ Tin Tức (News Tool)**
- **Node "Check News or Recent Data" (httpRequestTool):**
  - Điền **API Key NewsAPI** vào `httpQueryAuth`.
  - **URL mẫu:**
    ```json
    "https://newsapi.org/v2/top-headlines?country=vn&apiKey={{$jsonata("httpQueryAuth.apiKey")}}"
    ```
  - **Lưu ý:** Nếu không cần tin tức, có thể **xóa node này** và điều hướng lại cho sub-agent.

---

#### **3. Kích Hoạt ⚡️ Workflow**
**Bước 1:** **Test Run** với dữ liệu mẫu:
- Gửi yêu cầu mẫu như:
  ```json
  {
    "query": "Tóm tắt nội dung trong file 'Tài liệu Kinh Doanh.pdf' và gửi email cho nhanvien@example.com"
  }
  ```
- Kiểm tra **log** để đảm bảo các node hoạt động bình thường.

**Bước 2:** **Bật Active** và **đặt tên workflow** (ví dụ: **"AI Multi-Agent - Doanh Nghiệp Của Tôi"**).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tối Ưu Hiệu Suất cho AI**
- **Chọn mô hình phù hợp:**
  - Nếu budget hạn chế, thay `gpt-4o` bằng `gpt-3.5-turbo` trong node `lmChatOpenAi`.
  - Sử dụng **OpenRouter** với mô hình `mistral-tiny` (rẻ hơn) nếu không cần chất lượng cao.

- **Cập nhật collection Qdrant:**
  - Thay thế **collection mẫu** bằng dữ liệu riêng bằng cách:
    ```bash
    qdrant snapshot export --host localhost --port 6333 --snapshot-path ./snapshot --collection-name <tên-collection>
    ```
  - Tải lên Qdrant mới và cập nhật tên collection trong node `vectorStoreQdrant`.

#### **2. Tích Hợp Slack/Telegram**
- **Thêm node Webhook** để nhận yêu cầu từ Slack/Telegram:
  ```json
  {
    "name": "Receive Request from Slack",
    "type": "httpRequestTool",
    "keyParameters": {
      "method": "POST",
      "url": "https://slack.com/api/chat.postMessage"
    }
  }
  ```
- **Kết nối với node `Chat with an Agent`** để xử lý yêu cầu.

#### **3. Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node `set`** để lưu lịch sử tương tác:
  ```json
  {
    "name": "Log Conversation",
    "type": "set",
    "keyParameters": {
      "jsonata": "$ => { timestamp: $datetime('now'), query: $json('query'), response: $json('response') }"
    }
  }
  ```
- **Kết nối với Google Sheets** để tự động cập nhật báo cáo.

#### **4. Cập Nhật Tin Tức Định Kỳ**
- **Sử dụng node `executeWorkflowTrigger`** để chạy công cụ tin tức hàng ngày:
  ```json
  {
    "name": "Daily News Update",
    "type": "executeWorkflowTrigger",
    "keyParameters": {
      "schedule": "0 0 * * *" // Lúc 00:00 hàng ngày
    }
  }
  ```

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow **Multi-Agent với n8n, Qdrant, Gmail & OpenAI** là **giải pháp hoàn chỉnh** để:
✔ **Tự động hóa trích xuất và tổng hợp tài liệu** từ Google Drive.
✔ **Quản lý email thông minh** (đọc, trả lời, tạo bản nháp) mà không cần can thiệp.
✔ **Trả lời câu hỏi phức tạp** bằng AI RAG kết hợp OpenAI.
✔ **Cập nhật tin tức thời gian thực** từ API.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản & API keys** (Google Drive, Gmail, Qdrant, OpenAI).
2. **Import workflow** và cấu hình các node quan trọng.
3. **Test Run** và **bật Active** để bắt đầu tự động hóa!

**🚀 Các sếp đã sẵn sàng để AI làm việc thay mình chưa?** Nếu có thắc mắc, hãy để lại comment dưới đây! 👇

---
**📌 Ghi chú cuối:**
- Workflow này **không cần code**, phù hợp cho các sếp không biết lập trình.
- **Tối ưu hiệu suất** khi chạy trên VPS (không dùng máy tính cá nhân).
- **Mở rộng khả năng** bằng cách thêm node mới (Slack, Telegram, CRM...).