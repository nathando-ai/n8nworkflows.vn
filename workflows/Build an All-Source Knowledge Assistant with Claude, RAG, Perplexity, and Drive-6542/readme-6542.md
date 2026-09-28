---
title: "🤖 **Tự Động Hóa Trợ Lý Tri Thức Toàn Mạng với Claude, RAG, Perplexity & Google Drive - Cách Sử Dụng Workflow AI Tối Đa Hiệu Quả**"
description: "Workflow này tự động hóa việc xây dựng một trợ lý tri thức toàn diện kết hợp Claude AI, công nghệ RAG (Retrieval-Augmented Generation), Perplexity API và Google Drive để trả lời câu hỏi phức tạp từ nhiều nguồn dữ liệu khác nhau. Giúp các sếp tiết kiệm thời gian tìm kiếm thông tin, tăng độ chính xác và cá nhân hóa trả lời cho nhân viên."
slug: "tay-dong-hoa-tro-ly-tri-thuc-toan-mang-claude-rag-perplexity"
tags: [n8n, automation, ai-rag, google-drive, anthropic-claude, perplexity-api, vector-database, postgres]
keywords: [n8n workflow ai, tự động hóa trợ lý tri thức, Claude AI + RAG, Perplexity API, Google Drive tự động hóa, vector database Supabase, PostgreSQL chat memory]
---

# 🚀 **Tự Động Hóa Trợ Lý Tri Thức Toàn Mạng với Claude, RAG, Perplexity & Google Drive**

## **Giới Thiệu: Giải Pháp AI "Tự Động Hóa" Thay Thế Tìm Kiếm Thông Tin Thủ Công**
Các sếp đã từng gặp phải tình huống này chưa?
- Nhân viên phải mất **30 phút** tìm kiếm thông tin trong Google Drive, Wiki nội bộ hoặc các tài liệu PDF để trả lời câu hỏi của khách hàng?
- Các câu trả lời từ AI **không chính xác** vì thiếu ngữ cảnh hoặc dựa trên dữ liệu cũ?
- Các bộ phận phải **lặp đi lặp lại** cùng một công việc tìm kiếm thông tin, dẫn đến **sai sót và mất thời gian**?

Workflow này là **giải pháp tự động hóa hoàn chỉnh** kết hợp **Claude AI (Anthropic), công nghệ RAG (Retrieval-Augmented Generation), Perplexity API và Google Drive** để xây dựng một **trợ lý tri thức toàn diện**, trả lời câu hỏi từ **nhiều nguồn dữ liệu khác nhau** (PDF, CSV, hình ảnh, âm thanh, cơ sở dữ liệu PostgreSQL) với **độ chính xác cao và ngữ cảnh liên tục**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian tìm kiếm**: Trợ lý tự động tra cứu thông tin từ **Google Drive, cơ sở dữ liệu PostgreSQL, và web (Perplexity)** trong **vài giây** thay vì **phút giờ**.
✅ **Độ chính xác cao**: Sử dụng **RAG + Claude AI** để trả lời dựa trên **dữ liệu chính xác** thay vì hallucinate (ảo tưởng).
✅ **Nhớ ngữ cảnh**: **PostgreSQL Chat Memory** lưu trữ toàn bộ lịch sử trò chuyện, giúp trả lời liên tục và logic.
✅ **Hỗ trợ nhiều định dạng file**: **PDF, CSV, hình ảnh, âm thanh** đều được xử lý tự động và chuyển thành văn bản.
✅ **Cập nhật thông tin thời gian thực**: Kết hợp với **Perplexity API** để tra cứu thông tin mới nhất từ web.
✅ **Hoạt động 24/7**: Workflow tự động hóa hoàn toàn, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
| **Tài Khoản/Dịch Vụ**       | **Mô Tả**                                                                 | **Lưu Ý**                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Google Drive OAuth 2.0**  | Tài khoản Google Drive để đọc/tải xuống file (PDF, CSV, hình ảnh, âm thanh). | Cần cấp quyền **Drive API** trong [Google Cloud Console](https://console.cloud.google.com/). |
| **OpenAI API Key**          | Để tạo **embeddings** (vector) và sử dụng **GPT-4o-mini** (transcribe, analyze image). | Mua gói API tại [OpenAI](https://platform.openai.com/account/api-keys).       |
| **Anthropic API Key**       | Để sử dụng **Claude 3.5 Sonnet** (model chính trong workflow).             | Đăng ký tại [Anthropic](https://www.anthropic.com/api).                   |
| **Cohere API Key**          | Để **rerank** (sắp xếp lại) kết quả tìm kiếm theo độ tương quan.          | Đăng ký tại [Cohere](https://cohere.com/).                              |
| **Perplexity API Key**      | Để tra cứu thông tin **thời gian thực** từ web khi dữ liệu nội bộ không đủ. | Đăng ký tại [Perplexity](https://www.perplexity.ai/api).                 |
| **Supabase API Key**        | Để lưu trữ **vector database** (bộ nhớ tri thức).                         | Tạo tại [Supabase](https://supabase.com/).                              |
| **PostgreSQL Database**    | Để lưu **lịch sử trò chuyện** và **các query SQL**.                      | Cài đặt tại [ElephantSQL](https://www.elephantsql.com/) hoặc [Neon](https://neon.tech/). |
| **MCP Server (Google Drive)** | Server để **quản lý file** trong Google Drive.                          | Xem hướng dẫn tại [n8n.io/workflows/3634](https://n8n.io/workflows/3634). |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
**Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/6542](https://n8n.io/workflows/6542).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON → Nhấn **Import**.
3. Workflow sẽ xuất hiện trong danh sách workflows của bạn.

**Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create Workflow** → Chọn **Import from JSON**.
2. Dán toàn bộ mã JSON từ [n8n.io/workflows/6542](https://n8n.io/workflows/6542) vào ô.
3. Nhấn **Import**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **A. Cấu Hình Credentials (Tài Khoản API)**
Mỗi node yêu cầu **credentials** riêng. Các sếp cần:
1. **Tạo credentials** trong **n8n Settings** → **Credentials**.
2. Điền **API Key** tương ứng vào từng node.

| **Node**                     | **Credentials Cần Thiết**               | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------------|----------------------------------------|----------------------------------------------------------------------------------------|
| `Anthropic Chat Model`       | `anthropicApi`                        | Điền **API Key** từ Anthropic vào credentials.                                       |
| `Embeddings OpenAI`          | `openAiApi`                            | Điền **API Key** từ OpenAI vào credentials.                                           |
| `Reranker Cohere`            | `cohereApi`                            | Điền **API Key** từ Cohere vào credentials.                                           |
| `Perplexity Tool`            | `perplexityApi`                        | Điền **API Key** từ Perplexity vào credentials.                                       |
| `Google Drive`               | `googleDriveOAuth2Api`                 | Cấu hình OAuth 2.0 từ Google Drive.                                                   |
| `Postgres Chat Memory`       | `postgres`                             | Điền **URL, Username, Password** của PostgreSQL.                                      |
| `General knowledge` (Supabase)| `supabaseApi`                          | Điền **API Key** và **URL** của Supabase.                                             |
| `Google Drive MCP Server`    | (Không cần credentials)                | Chỉ cần **path** của MCP Server (được tạo từ workflow [n8n.io/workflows/3634](https://n8n.io/workflows/3634)). |

##### **B. Cấu Hình Node Quan Trọng**
###### **1. `When chat message received` (Trigger)**
- **Loại trigger**: Chọn **`chatTrigger`** (nếu sử dụng Slack/Telegram) hoặc **`manualTrigger`** (nếu muốn kích hoạt thủ công).
- **Credentials**: Nếu sử dụng Slack/Telegram, điền **token** vào credentials tương ứng.

###### **2. `Postgres Chat Memory`**
- **Database Configuration**:
  - **Host**: `your-postgres-url.neon.tech` (hoặc IP của PostgreSQL).
  - **Database**: Tên cơ sở dữ liệu (ví dụ: `n8n_chat_memory`).
  - **Username/Password**: Tài khoản đã tạo trong PostgreSQL.
  - **Table Name**: `chat_history` (nếu khác, cần chỉnh sửa trong node).

###### **3. `General knowledge` (Supabase Vector DB)**
- **Supabase Configuration**:
  - **URL**: `https://[project-ref].supabase.co` (từ Supabase Dashboard).
  - **API Key**: `supabase key` từ **Project Settings** → **API**.
  - **Table Name**: `documents` (nếu khác, cần chỉnh sửa trong node).

###### **4. `Knowledge Agent` (Agent Node)**
- **Tool Registration**:
  - Workflow đã tự động đăng ký **tất cả công cụ** (Claude, PostgreSQL, Google Drive, Perplexity...).
  - **Không cần chỉnh sửa** trừ khi muốn thêm/bỏ công cụ.

###### **5. `Read File From GDrive` (Sub-workflow)**
- **File ID**: Khi tìm kiếm file trong Google Drive, **fileId** sẽ tự động truyền vào node này.
- **Lưu ý**:
  - Nếu file **không phải PDF/CSV**, workflow sẽ tự động chuyển sang **analyze image** hoặc **transcribe audio**.

###### **6. `Message a model in Perplexity`**
- **Prompt Template**:
  ```json
  {
    "prompt": "Search the web for the most recent information about {{query}} and provide a concise summary."
  }
  ```
  - **Không cần chỉnh sửa** trừ khi muốn thay đổi cách Perplexity trả lời.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Kiểm Tra Trước Khi Bật)**
   - Nhấn **Run Workflow** với **dữ liệu mẫu**:
     - **Câu hỏi**: *"Tóm tắt nội dung file 'Tài liệu Quý 1.pdf' trong Google Drive?"*
     - **Kiểm tra**:
       - Workflow có **tải file** từ Google Drive không?
       - **Extract text** từ PDF có thành công không?
       - **Claude AI** có trả lời logic không?

2. **Bật Active Workflow**
   - Sau khi test thành công, **nhấn Active** để workflow chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Cập Nhật Dữ liệu Tự Động**
- **Lưu ý**: Workflow hiện tại **không tự động cập nhật** dữ liệu mới từ Google Drive.
- **Giải pháp**:
  - Tạo **workflow phụ** để **scan và update** file mới vào Supabase Vector DB hàng ngày.
  - Sử dụng **n8n Schedule Node** để chạy định kỳ.

#### **2. Kết Nối với Slack/Telegram**
- **Cách làm**:
  1. Thay `When chat message received` bằng **`Slack Webhook`** hoặc **`Telegram Bot`**.
  2. Cấu hình **credentials** cho Slack/Telegram.
  3. Workflow sẽ tự động **trả lời trên Slack/Telegram** thay vì n8n Editor.

#### **3. Lưu Log Trò Chuyện**
- **Sử dụng `Postgres Tool`** để lưu **tất cả lịch sử trò chuyện** vào bảng `chat_logs`.
- **Cấu trúc bảng**:
  ```sql
  CREATE TABLE chat_logs (
    id SERIAL PRIMARY KEY,
    user_id VARCHAR(255),
    message TEXT,
    response TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
  );
  ```

#### **4. Gửi Báo Cáo Định Kỳ**
- **Tạo workflow phụ** để:
  - **Tra cứu** các câu hỏi thường gặp trong **Postgres Chat Memory**.
  - **Gửi báo cáo** về **Slack/Email** hàng tuần.

#### **5. Sử Dụng Model Claude Mới Nhất**
- **Cập nhật model** trong node `Anthropic Chat Model`:
  ```json
  {
    "model": {
      "__rl": true,
      "mode": "list",
      "value": "claude-3-5-sonnet-20240620",  // Thay đổi model mới nhất
      "cachedResultName": "Claude 3.5 Sonnet"
    }
  }
  ```

---

### 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Độ Chính Xác**
Workflow này là **giải pháp hoàn chỉnh** để các sếp:
✔ **Tự động hóa tìm kiếm thông tin** từ nhiều nguồn khác nhau.
✔ **Giảm thiểu sai sót** nhờ **RAG + Claude AI**.
✔ **Tiết kiệm thời gian** cho nhân viên bằng cách **trả lời tự động**.
✔ **Cập nhật thông tin thời gian thực** với **Perplexity API**.

**Hành động ngay hôm nay**:
1. **Import workflow** và cấu hình credentials.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động.
3. **Bật Active** và **chia sẻ với team** để tối ưu hóa công việc!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp **lỗi API rate limit**, các sếp nên **cập nhật gói API** (OpenAI, Anthropic, Perplexity).
- **Backup dữ liệu** trong PostgreSQL và Supabase định kỳ.
- **Mở rộng** workflow bằng cách thêm **công cụ mới** (ví dụ: Zoom API, Notion, Airtable).

**Chia sẻ ý kiến** của các sếp về cách tối