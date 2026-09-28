---
title: "🤖 **Tự Động Hóa Bot Telegram RAG Cục Bộ Với Google Drive, PostgreSQL & Ollama (Không Cần API AI Ngoại Vi)**"
description: "Hướng dẫn chi tiết xây dựng bot Telegram RAG hoàn toàn cục bộ, bảo mật bằng mã PIN, trả lời câu hỏi từ tài liệu cá nhân của bạn bằng Ollama (qwen2.5) và pgvector - không phụ thuộc vào API AI bên ngoài."
slug: "tay-dong-hoa-bot-telegram-rag-cuc-bo-google-drive-postgresql-ollama"
tags: [n8n, automation, ai-rag, ollama, telegram-bot, postgres, google-drive, no-code, local-llm]
keywords: [n8n workflow telegram bot, tự động hóa bot telegram, rag với ollama, bot ai cục bộ, pgvector, google drive automation, chatbot no-code]
---

# 🚀 **Xây Dựng Bot Telegram RAG Cục Bộ Với Google Drive, PostgreSQL & Ollama (Không API AI Ngoại Vi)**

## **🔍 Nỗi Đau Của Các Sếp Và Giải Pháp Của Workflow Này**
Hiện nay, nhiều doanh nghiệp và cá nhân đang gặp khó khăn khi muốn tạo một **bot Telegram thông minh** trả lời câu hỏi từ tài liệu nội bộ của mình. Các giải pháp truyền thống yêu cầu:
- **Phụ thuộc vào API AI bên ngoài** (OpenAI, Mistral...) → Chi phí cao, không bảo mật dữ liệu.
- **Khó bảo mật** → Nếu không kiểm soát chặt chẽ, tài liệu nội bộ có thể bị rò rỉ.
- **Tốn thời gian** → Cần viết code hoặc sử dụng công cụ phức tạp để xây dựng hệ thống RAG (Retrieval-Augmented Generation).

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **100% cục bộ** – Không phụ thuộc vào API AI nào, sử dụng **Ollama (qwen2.5)** chạy trên máy chủ riêng.
✅ **Bảo mật cao** – Yêu cầu **mã PIN** để truy cập, tất cả dữ liệu lưu trữ trong **PostgreSQL cục bộ**.
✅ **Tự động hóa hoàn chỉnh** – Khi có tài liệu mới trên **Google Drive**, hệ thống tự động **ngăn xép, embed và lưu trữ** để bot trả lời nhanh chóng.
✅ **Không cần code** – Sử dụng **n8n** để kết nối các dịch vụ một cách logic, dễ dàng mở rộng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Bot Telegram thông minh** trả lời câu hỏi từ tài liệu cá nhân **không phụ thuộc vào API AI bên ngoài**.
- **Bảo mật tuyệt đối** với hệ thống **mã PIN** và lưu trữ dữ liệu trong **PostgreSQL cục bộ**.
- **Tự động hóa hoàn chỉnh** – Khi có tài liệu mới trên Google Drive, hệ thống tự động **ngăn xép, embed và lưu trữ** để bot trả lời nhanh chóng.
- **Giảm chi phí** – Không cần trả phí cho API AI, chỉ cần **Ollama (miễn phí)** và **PostgreSQL (Supabase miễn phí)**.
- **Dễ dàng mở rộng** – Thêm tài liệu mới, cập nhật mô hình LLM mà không cần tái cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
#### **1. Dịch Vụ & API Keys**
| Dịch vụ | Thông tin cần thiết |
|---------|----------------------|
| **Telegram Bot** | Token bot từ [@BotFather](https://t.me/BotFather) |
| **PostgreSQL (pgvector)** | - Cổng kết nối (ví dụ: `postgres://user:pass@localhost:5432/db`) <br> - Cài đặt **pgvector** (`CREATE EXTENSION vector;`) |
| **Google Drive** | - Tài khoản Google <br> - **Folder cụ thể** để theo dõi tài liệu mới |
| **Ollama (Local LLM)** | - Cài đặt Ollama và pull mô hình: <br> ```bash <br> ollama pull nomic-embed-text <br> ollama pull qwen2.5:7b <br> ``` <br> - Đảm bảo Ollama chạy tại `http://host.docker.internal:11434` (nếu dùng Docker) |

#### **2. Cơ sở dữ liệu PostgreSQL**
Trước khi kích hoạt workflow, các sếp cần chạy **4 bảng sau** trong PostgreSQL:
```sql
-- Bảng lưu trữ thông tin người dùng (bao gồm mã PIN)
CREATE TABLE telegram_users (
  chat_id TEXT PRIMARY KEY,
  username TEXT,
  pin_code TEXT,
  is_verified BOOLEAN DEFAULT false,
  pin_attempts INT DEFAULT 0,
  verified_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Bảng lưu trữ các chunk text từ tài liệu (đã embed)
CREATE TABLE document_chunks (
  chunk_id TEXT PRIMARY KEY,
  file_id TEXT,
  file_name TEXT,
  chunk_index INT,
  chunk_text TEXT,
  embedding vector(768)
);

-- Bảng lưu trữ lịch sử truy vấn (audit)
CREATE TABLE query_log (
  id SERIAL PRIMARY KEY,
  chat_id TEXT,
  username TEXT,
  query TEXT,
  answer TEXT,
  match_count INT,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Bảng lưu trữ lịch sử ingest tài liệu
CREATE TABLE ingestion_log (
  file_id TEXT PRIMARY KEY,
  file_name TEXT,
  drive_file_id TEXT,
  status TEXT,
  ingested_at TIMESTAMP DEFAULT NOW()
);
```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/15031](https://n8n.io/workflows/15031) (chọn **Export as JSON**).
2. Trong **n8n Editor**, nhấn **Import** và dán JSON.
3. **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần trên (Telegram Bot)** → Xử lý yêu cầu từ người dùng.
- **Phần dưới (Document Ingestion)** → Tự động xử lý tài liệu mới trên Google Drive.

##### **A. Cấu Hình Telegram Bot (Phần Trên)**
| Node | Tham Số Cần Chỉnh |
|------|-------------------|
| **Telegram Webhook** | - **Path**: `rag-telegram-bot` (không đổi) <br> - **HTTP Method**: `POST` (không đổi) |
| **Register New User** | - **SQL Query**: Thay đổi `pin_code = '1234'` thành **mã PIN riêng** của bạn (ví dụ: `'AB1234'`). |
| **Send PIN Request** | - **Tham số Telegram**: Đảm bảo bot có quyền gửi tin nhắn. |
| **Ask LLM** | - **URL Ollama**: `http://host.docker.internal:11434/api/generate` (nếu dùng Docker). |
| **Send Answer** | - **Tham số Telegram**: Đảm bảo bot có quyền gửi tin nhắn. |

##### **B. Cấu Hình Document Ingestion (Phần Dưới)**
| Node | Tham Số Cần Chỉnh |
|------|-------------------|
| **Google Drive Trigger** | - **Chọn folder** trên Google Drive muốn theo dõi. |
| **Download File** | - **Google Drive OAuth2** phải được cấu hình trong **Credentials** của n8n. |
| **Embed Chunk** | - **URL Ollama**: `http://host.docker.internal:11434/api/embeddings` (nếu dùng Docker). |
| **Store Chunk** | - **SQL Query**: Đảm bảo bảng `document_chunks` đã tồn tại. |

##### **C. Cấu Hình Credentials (N8N Settings → Credentials)**
Các sếp cần thêm **3 credentials** này:
1. **Telegram API** → Dán **token bot** từ @BotFather.
2. **PostgreSQL** → Cấu hình kết nối đến PostgreSQL (ví dụ: `postgres://user:pass@localhost:5432/db`).
3. **Google Drive OAuth2** → Cấu hình OAuth2 từ Google Drive.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi `/start` đến bot Telegram để kiểm tra quá trình đăng ký và xác thực.
   - Thêm một tài liệu vào **Google Drive folder** đã chọn để kiểm tra quá trình ingest.
2. **Bật Active workflow** trong n8n.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hóa Hiệu Suất**]
- **Tăng kích thước chunk** (hiện là 500 ký tự) nếu tài liệu dài để tránh mất ngữ cảnh.
- **Sử dụng Telegram Bot API** để gửi tin nhắn định kỳ (ví dụ: báo cáo thống kê truy vấn).
- **Lưu log vào Google Sheets** thay vì PostgreSQL để dễ theo dõi.
- **Kết hợp với Slack** để thông báo khi có tài liệu mới được ingest.
- **Cập nhật mô hình Ollama** khi có phiên bản mới để cải thiện chất lượng trả lời.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tạo bot Telegram thông minh** từ tài liệu cá nhân **không phụ thuộc vào API AI bên ngoài**.
✔ **Bảo mật tuyệt đối** với hệ thống **mã PIN** và lưu trữ cục bộ.
✔ **Tự động hóa hoàn chỉnh** – Khi có tài liệu mới, hệ thống tự động **ngăn xép, embed và lưu trữ**.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian, chi phí cũng như nâng cao hiệu suất công việc!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng:**
- **Không sử dụng mã PIN mặc định (`1234`)** – Thay đổi thành **mã riêng** để bảo mật.
- **Kiểm tra log PostgreSQL** để theo dõi quá trình ingest và truy vấn.
- **Nếu Ollama không chạy**, kiểm tra lại cổng (`11434`) và cấu hình Docker.