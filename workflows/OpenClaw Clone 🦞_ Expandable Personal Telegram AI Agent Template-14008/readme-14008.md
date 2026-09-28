---
title: "🦞 OpenClaw Clone: Tạo AI Agent Telegram Tự Động Hóa Siêu Cường (Mẫu Template Expandable)"
description: "Workflow này giúp các sếp xây dựng một AI Agent Telegram tự động hóa công việc phức tạp, tích hợp AI Gemini, OpenAI, Google Workspace và nhiều công cụ khác. Giúp tiết kiệm thời gian, tăng hiệu suất và cá nhân hóa tương tác 24/7."
slug: "openclaw-clone-ai-agent-telegram-tieu-dong-hoa"
tags: [n8n, automation, ai-agent, telegram-bot, google-workspace, openai, gemini-ai]
keywords: [n8n workflow telegram ai, tự động hóa công việc với ai, agent gemini telegram, template n8n expandable, google drive automation, openclaw clone]
---

# 🦞 **OpenClaw Clone: AI Agent Telegram Tự Động Hóa Siêu Cường (Mẫu Template Expandable)**

## **Giới Thiệu**
Hãy tưởng tượng một AI Agent Telegram **tự động hóa mọi công việc phức tạp** cho doanh nghiệp của các sếp: từ **tìm kiếm thông tin**, **quản lý lịch Google**, **tạo báo cáo Google Docs**, **xử lý email Gmail**, cho đến **tương tác với người dùng bằng giọng nói hoặc hình ảnh**. **OpenClaw Clone** là một **mẫu template AI Agent** được xây dựng trên nền tảng **n8n**, tích hợp **Google Gemini, OpenAI, PostgreSQL, Qdrant, và hàng chục công cụ khác** để giúp các sếp **giảm thiểu công việc thủ công**, **tăng tốc độ phản hồi** và **cá nhân hóa tương tác** một cách hoàn hảo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100% công việc lặp đi lặp lại** (quản lý email, lịch, tài liệu Google, tìm kiếm web, xử lý giọng nói/hình ảnh).
✅ **Tương tác đa dạng** (nhận tin nhắn văn bản, giọng nói, hình ảnh và trả lời tự động hoặc bằng giọng nói).
✅ **Tích hợp AI Gemini & OpenAI** để phân tích, tổng hợp và trả lời thông minh.
✅ **Lưu trữ trí nhớ (PostgreSQL)** để AI nhớ lịch sử tương tác và cải thiện chất lượng phản hồi.
✅ **Kết nối với Google Workspace** (Gmail, Drive, Docs, Calendar, Slides, Sheets) để tự động hóa quản lý dữ liệu.
✅ **Mở rộng vô hạn** bằng cách thêm **sub-workflows, RAG (Retrieval-Augmented Generation), và công cụ mới**.
✅ **Escalation tự động** khi AI không xử lý được (chuyển sang người hỗ trợ).
:::

---

## **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ/Công cụ**       | **Yêu cầu** |
|---------------------------|-------------|
| **Telegram Bot**          | Bot Token từ [@BotFather](https://t.me/BotFather) + Telegram User ID (của người dùng được phép sử dụng). |
| **OpenAI**                | API Key (để sử dụng **text-to-speech, transcribe audio, embeddings**). |
| **Google Cloud**          | API Key + Service Account (để truy cập **Google Drive, Docs, Sheets, Calendar, Slides**). |
| **Google Workspace**      | Email doanh nghiệp + quyền quản lý tài liệu. |
| **PostgreSQL**            | Database để lưu trữ **trí nhớ chat** của AI. |
| **Qdrant**                | Vector Database để **RAG (Retrieval-Augmented Generation)**. |
| **Perplexity API**        | API Key (để tìm kiếm web tự động). |
| **ScrapeGraphAI**         | API Key (để **scraping website** và xử lý dữ liệu). |
| **Cohere Reranker**       | API Key (để **tối ưu hóa kết quả tìm kiếm**). |
| **FTP Server**            | Để lưu trữ **tạm thời hình ảnh** từ Telegram. |

### **2. Cài đặt bổ sung**
- **n8n Self-hosted** (trên VPS) để workflow hoạt động **24/7**.
- **MCP Server** (Multi-Client Platform) để quản lý **sub-workflows** và **escalation**.
- **Node.js & npm** (nếu cần cài đặt các **custom nodes**).

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/14008](https://n8n.io/workflows/14008).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc copy toàn bộ JSON** và dán vào **"Import from JSON"** trong Editor.

:::note[Lưu ý]
- **Không kích hoạt workflow ngay lập tức** sau khi import, vì cần **cấu hình các node quan trọng** trước.
- **Không sử dụng phiên bản n8n cloud** nếu muốn workflow **ổn định 24/7**.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "Webhook" (Trigger đầu vào)**
- **Path**: `56c7aeae-eb8a-4d2e-a149-dfe02b586d18` (không thay đổi).
- **Cấu hình**:
  - Chọn **HTTP Request** (POST).
  - **Credentials**: Tạo mới (nếu chưa có).
  - **Active**: Bật để nhận **tin nhắn từ Telegram**.

#### **🔹 Node "Telegram Trigger" (Nhận tin nhắn)**
- **Credentials**: Thiết lập **Telegram Bot Token** và **User ID** (của người dùng được phép sử dụng).
- **Lưu ý**:
  - **User ID** có thể lấy từ [@userinfobot](https://t.me/userinfobot).
  - **Bot Token** từ [@BotFather](https://t.me/BotFather).

#### **🔹 Node "Code" (Xác thực người dùng)**
- **Mã JavaScript**:
  ```javascript
  // Kiểm tra User ID có trong danh sách được phép không
  const allowedUsers = ["123456789", "987654321"]; // Thay bằng User ID của các sếp
  if (!allowedUsers.includes($input.json().message.from.id)) {
    return { json: { error: "User not authorized" } };
  }
  ```
- **Lưu ý**: Thay `allowedUsers` bằng **danh sách User ID** của các sếp.

#### **🔹 Node "Google Gemini Chat Model" (AI Core)**
- **Credentials**: Thiết lập **Google Cloud API Key**.
- **Prompt**: Cần **cập nhật** để phù hợp với mục đích sử dụng (ví dụ:
  ```plaintext
  Bạn là một AI trợ lý thông minh. Hãy trả lời mọi câu hỏi một cách chi tiết và chính xác.
  Nếu cần, hãy sử dụng các công cụ sau:
  - Websearch (Perplexity)
  - Scraper (ScrapeGraphAI)
  - Google Drive
  - Google Calendar
  - Google Docs
  ```
- **Lưu ý**:
  - **Không để trống prompt**, vì nó quyết định **cách AI phản hồi**.
  - **Thêm/loại bỏ công cụ** trong prompt nếu không cần.

#### **🔹 Node "Postgres Chat Memory" (Lưu trí nhớ)**
- **Credentials**: Thiết lập **PostgreSQL Connection**.
- **Cấu hình**:
  - **Database Name**: `n8n_memory`
  - **Table Name**: `chat_history`
  - **Columns**: `user_id, message, response, timestamp`

#### **🔹 Node "OpenAI (Transcribe Audio)"**
- **Credentials**: Thiết lập **OpenAI API Key**.
- **Lưu ý**:
  - **Mime Type** của file âm thanh phải đúng (nếu không, sử dụng **Node "Fix mimeType for Audio"** để sửa).

#### **🔹 Node "FTP" (Upload hình ảnh)**
- **Credentials**: Thiết lập **FTP Server** (ví dụ: FileZilla, AWS S3).
- **Path**: `=/XXX/{{ $binary.data.fileName }}` → Thay `XXX` bằng **folder đích** trên FTP.

#### **🔹 Node "MCP Triggers" (Sub-workflows)**
- **Credentials**: Thiết lập **MCP Server URL** (ví dụ: `http://localhost:5678`).
- **Path**:
  - **MCP Gmail Trigger**: `63975752-0598-4992-9422-165a84c8798c`
  - **MCP Calendar Trigger**: `0f72eb90-2a1c-403e-98e1-901d76c2825c`
  - **MCP Docs Trigger**: `1f35317d-7b8e-48b9-a419-936ea5b63ae6`
  - **MCP Drive Trigger**: `031809b0-c277-4ff1-b65a-9e72294b1ff1`
  - **MCP Slides Trigger**: `1f35317d-7b8e-48b9-a419-936ea5b63ae6`

#### **🔹 Node "Agent" (OpenClaw Agents)**
- **Credentials**: Thiết lập **PostgreSQL, Qdrant, OpenAI, Gemini**.
- **Lưu ý**:
  - **Không để trống "Tools"** trong cấu hình Agent.
  - **Thêm công cụ mới** nếu cần (ví dụ: `toolCalculator`, `toolWorkflow`).

#### **🔹 Node "Schedule Trigger" (Gửi tin nhắn định kỳ)**
- **Cron Expression**: Ví dụ `0 8 * * *` (gửi tin nhắn lúc 8h sáng hàng ngày).
- **Message**: Thay bằng **nội dung muốn gửi** (ví dụ: `"Send me the latest news on AI"`).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Gửi **tin nhắn văn bản** (ví dụ: *"Hôm nay có sự kiện nào trong lịch?"*).
   - Gửi **tin nhắn giọng nói** (AI sẽ chuyển giọng nói thành văn bản).
   - Gửi **hình ảnh** (AI sẽ xử lý và trả lời).
2. **Kiểm tra log** trong **n8n Dashboard** để phát hiện lỗi.
3. **Bật Active** workflow khi **tất cả test thành công**.

---

## **✍️ Mẹo & gợi ý nâng cao**

### **1. Mở rộng chức năng với Sub-workflows**
- **Tạo sub-workflows** riêng cho từng chức năng (ví dụ: **quản lý email**, **tạo báo cáo**, **xử lý hợp đồng**).
- **Kết nối với MCP Server** để quản lý nhiều sub-workflows từ một nơi.

### **2. Tích hợp Escalation Agent**
- Khi AI không xử lý được, **chuyển sang người hỗ trợ** thông qua **Telegram Hitl Tool**.
- **Cấu hình**:
  - Thiết lập **User ID của nhân viên hỗ trợ**.
  - **Tin nhắn chuyển tiếp** có thể tự động gửi đến **Slack/Email** nếu cần.

### **3. Cập nhật RAG (Retrieval-Augmented Generation)**
- Sử dụng **Qdrant + OpenAI Embeddings** để **tìm kiếm thông tin từ Google Drive/Docs**.
- **Mẹo**: Tạo **các vector store** từ **tài liệu quan trọng** để AI trả lời chính xác hơn.

### **4. Tích hợp Google Workspace tự động hóa**
- **Gmail**: Tự động **xóa email spam**, **tạo draft**, **trả lời tự động**.
- **Google Calendar**: **Tạo sự kiện**, **kiểm tra lịch**, **cập nhật lịch**.
- **Google Drive**: **Tạo file mới**, **di chuyển file**, **tải xuống**.
- **Google Docs/Sheets/Slides**: **Tạo báo cáo**, **cập nhật nội dung**, **chỉnh sửa trình chiếu**.

### **5. Chuyển giọng nói thành giọng nói (Text-to-Speech)**
- Sử dụng **OpenAI TTS** để **AI trả lời bằng giọng nói** thay vì văn bản.
- **Cấu hình**:
  - Chọn **voice model** (ví dụ: `echo`, `onyx`).
  - **Upload audio** vào Telegram bằng `sendAudio`.

### **6. Log & Monitoring**
- **Tạo log** cho mỗi tương tác bằng **Google Sheets/Google Docs**.
- **Gửi báo cáo định kỳ** (ví dụ: **"Báo cáo hoạt động AI hàng ngày"**).

---

## **📌 Kết luận**
**OpenClaw Clone** là **mẫu template AI Agent Telegram mạnh mẽ nhất** hiện nay, giúp các sếp **tự động hóa mọi công việc phức tạp** một cách **không cần code**. Với **tích hợp AI Gemini, OpenAI, Google Workspace và hàng chục công cụ khác**, workflow này **giúp tiết kiệm thời gian, tăng hiệu suất và cá nhân hóa tương tác** một cách hoàn hảo.

:::success[**Hành động ngay hôm nay!**]
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và **cấu hình các node quan trọng**.
3. **Test với tin nhắn văn bản, giọng nói và hình ảnh**.
4. **Mở rộng chức năng** bằng cách thêm **sub-workflows, RAG, Escalation Agent**.
5. **Áp dụng ngay** để **tự động hóa doanh nghiệp** của các sếp!

👉 **Xem video hướng dẫn chi tiết