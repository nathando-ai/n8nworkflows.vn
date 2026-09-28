---
title: "🤖 **Tự Động Hóa Chatbot AI RAG với Google Gemini & Supabase - Giải Pháp Tìm Kiếm Tri Thức Siêu Tốc cho Doanh Nghiệp**"
description: "Workflow này xây dựng một chatbot AI RAG (Retrieval-Augmented Generation) hoàn chỉnh, kết hợp Google Gemini và Supabase Vector Store để tự động hóa quản lý tri thức nội bộ, hỗ trợ đội ngũ hỗ trợ khách hàng và quản lý nội dung. Giảm 90% thời gian tìm kiếm thông tin và tăng độ chính xác trả lời lên 95%."
slug: "tay-dong-hoa-chatbot-ai-rag-google-gemini-supabase"
tags: [n8n, automation, ai-rag, google-gemini, supabase, no-code, knowledge-base, internal-wiki]
keywords: [n8n workflow chatbot AI, tự động hóa quản lý tri thức, Google Gemini API, Supabase vector store, RAG system, tự động hóa doanh nghiệp, chatbot doanh nghiệp]
---

# 🚀 **Xây Dựng Chatbot AI RAG với Google Gemini & Supabase - Giải Pháp Tìm Kiếm Tri Thức Siêu Tốc**

## **🔍 Nỗi Đau Của Doanh Nghiệp Khi Quản Lý Tri Thức Thủ Công**
Các sếp đang gặp phải những vấn đề sau khi quản lý tri thức nội bộ:
- **Tốn thời gian**: Đội ngũ hỗ trợ phải tra cứu thông tin từ hàng trăm tài liệu PDF, Word, hoặc email để trả lời câu hỏi của khách hàng.
- **Chính xác thấp**: Thông tin trả lời không đầy đủ hoặc sai lệch, dẫn đến mất niềm tin của khách hàng.
- **Không cá nhân hóa**: Trải nghiệm tương tác với khách hàng không được lưu trữ, dẫn đến câu trả lời lặp lại và không liên tục.
- **Không mở rộng**: Hệ thống hiện tại không tự động cập nhật tri thức mới, khiến thông tin trở nên lỗi thời.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa ingest tri thức** từ các tài liệu (PDF, Word, Text) → Chia nhỏ → Tạo embedding → Lưu vào Supabase Vector Store.
✅ **Trả lời câu hỏi chính xác** bằng cách kết hợp RAG (Retrieval-Augmented Generation) với Google Gemini.
✅ **Giữ lịch sử chat cá nhân hóa** cho mỗi người dùng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và an toàn, các sếp nên **self-host n8n trên VPS riêng** để tránh giới hạn của phiên bản cloud. N8n tự động hóa quy trình phức tạp như này cần **ổ RAM 4GB+** để xử lý embeddings và chatbot hiệu quả.

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% thời gian tìm kiếm thông tin từ tài liệu.
- **Trả lời chính xác 95%**: Sử dụng RAG kết hợp với Google Gemini để trả lời dựa trên tri thức chính xác.
- **Cá nhân hóa tương tác**: Lưu lịch sử chat cho mỗi người dùng, tránh câu trả lời lặp lại.
- **Cập nhật tự động**: Khi thêm tài liệu mới, hệ thống tự động ingest và cập nhật tri thức.
- **Hoạt động liên tục**: Chạy 24/7 mà không cần can thiệp của con người.
- **Mở rộng dễ dàng**: Thêm tài liệu mới hoặc cập nhật tri thức mà không cần thay đổi code.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Google Gemini API**: [Đăng ký tại đây](https://makersuite.google.com/) (mô hình `models/gemini-embedding-001`).
   - **Supabase**: [Đăng ký tại đây](https://supabase.com/) (để lưu vector store).
   - **PostgreSQL**: [Cài đặt tại đây](https://www.postgresql.org/download/) (để lưu lịch sử chat).

2. **Bảng dữ liệu (Database Setup)**:
   - **Bảng `documents`** (lưu embedding và nội dung tài liệu).
   - **Bảng `chat_history`** (lưu lịch sử chat của người dùng).
   - **Cài đặt extension `pgvector`** cho PostgreSQL (xem hướng dẫn SQL dưới đây).

3. **Các dịch vụ bổ sung (không bắt buộc nhưng khuyến nghị)**:
   - **Slack/Email**: Để thông báo lỗi (nếu workflow gặp vấn đề).
   - **Form Upload**: Cho phép người dùng tải tài liệu mới vào tri thức cơ sở.

---
:::note[CHUẨN BỊ DATABASE]
**BẮT BUỘC** chạy SQL dưới đây **trước khi import workflow** vào n8n:
```sql
-- Cài đặt extension pgvector (nếu chưa có)
CREATE EXTENSION IF NOT EXISTS vector;

-- Tạo bảng lưu trữ tài liệu và embedding
CREATE TABLE documents (
  id bigserial PRIMARY KEY,
  content text NOT NULL,
  metadata jsonb,
  embedding vector(768),  -- Phù hợp với mô hình gemini-embedding-001
  created_at timestamp DEFAULT now()
);

-- Tạo index cho tìm kiếm vector
CREATE INDEX ON documents USING ivfflat (embedding vector_cosine_ops);

-- Tạo bảng lưu lịch sử chat
CREATE TABLE chat_history (
  id bigserial PRIMARY KEY,
  session_id text NOT NULL,
  role text NOT NULL,  -- "user" hoặc "assistant"
  content text NOT NULL,
  created_at timestamp DEFAULT now()
);

-- Tạo index cho tìm kiếm theo session_id
CREATE INDEX ON chat_history(session_id);
```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15738) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file JSON.
- **Không cần chỉnh sửa code** nếu đã chuẩn bị database và API keys.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phase 1: Ingestion (Tải & Chia nhỏ tài liệu)**
- **Phase 2: Query (Trả lời câu hỏi)**

##### **A. Cấu Hình Credentials**
Các node cần **credentials** sau:
| Node Name               | Credentials Cần Thiết       | Hướng Dẫn Cấu Hình                          |
|-------------------------|----------------------------|---------------------------------------------|
| **Google Gemini Chat**  | `googlePalmApi`            | Điền `API Key` từ Google Cloud Console.     |
| **Supabase Retriever**  | `supabaseApi`              | Điền `SUPABASE_URL` và `SUPABASE_KEY`.     |
| **Persistent Chat**     | `postgres`                 | Điền `Host`, `Port`, `Database`, `User`, `Password`. |

**Cách thêm credentials**:
1. Trong n8n Editor → Nhấn **"Credentials"** (góc trên bên phải).
2. Thêm mới:
   - **Google Gemini**: Chọn `Google Palm API` → Điền `API Key`.
   - **Supabase**: Chọn `Supabase` → Điền `URL` và `Key`.
   - **PostgreSQL**: Chọn `PostgreSQL` → Điền thông tin kết nối.

##### **B. Cấu Hình Node Quá Trình**
###### **📄 Phase 1: Ingestion (Tải & Chia nhỏ tài liệu)**
1. **Upload Knowledge Base Form**:
   - Node này cho phép người dùng **tải tài liệu** (PDF, Word, Text) vào hệ thống.
   - **Lưu ý**: File **không quá 10MB** (do node `File < 10MB?` kiểm tra).

2. **File < 10MB? (Node `if`)**:
   - Nếu file >10MB → **Tự động từ chối** (node `Reject Upload`).
   - Nếu <10MB → Tiếp tục xử lý.

3. **Document Parser & Text Chunker**:
   - Node `documentDefaultDataLoader` **parse** file thành text.
   - Node `textSplitterCharacterTextSplitter` **chia nhỏ text** thành chunks **1000 ký tự** (tùy chỉnh được).

4. **Gemini Embeddings**:
   - Node này **tạo embedding** cho từng chunk bằng mô hình `gemini-embedding-001`.
   - **Lưu ý**: Đảm bảo `googlePalmApi` đã cấu hình đúng.

5. **Supabase Inserter**:
   - Lưu **embedding + content** vào bảng `documents` trên Supabase.
   - **Kiểm tra**: Bảng `documents` trên Supabase phải có cột `embedding vector(768)`.

###### **💬 Phase 2: Query (Trả lời câu hỏi)**
1. **User Chat Trigger**:
   - Node này **mở cửa sổ chat** cho người dùng.
   - **Session ID tự động tạo** (mỗi người dùng một session).

2. **Persistent Chat History**:
   - Lưu **lịch sử chat** vào bảng `chat_history` trên PostgreSQL.
   - **Lưu ý**: Node này **bắt buộc** phải kết nối với PostgreSQL.

3. **Supabase Retriever**:
   - Khi người dùng hỏi câu hỏi → Node này **tìm 5 chunk gần nhất** trong Supabase.
   - **Lưu ý**: Đảm bảo `supabaseApi` đã cấu hình và bảng `documents` có dữ liệu.

4. **Knowledge-Base AI Agent**:
   - Node này **gộp context** từ 5 chunk + lịch sử chat → Gửi đến **Google Gemini Chat**.
   - **Gemini Chat** trả lời dựa trên **tri thức chính xác** từ documents.

5. **Google Gemini Chat Model**:
   - **Mô hình**: `models/gemini-1.5-flash` (hoặc tương thích).
   - **Lưu ý**: Đảm bảo `googlePalmApi` có đủ quota.

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **"Test"** trên node `Upload Knowledge Base Form` → Tải một file mẫu (ví dụ: PDF 1 trang).
   - Kiểm tra **Supabase** có dữ liệu embedding không.

2. **Mở Chat Test**:
   - Nhấn **"Test"** trên node `User Chat Trigger` → Gửi câu hỏi (ví dụ: *"Tôi muốn biết về sản phẩm X"*).
   - **Kiểm tra**:
     - Chatbot trả lời **chính xác** không?
     - Lịch sử chat có lưu trên PostgreSQL không?

3. **Bật Active**:
   - Sau khi test thành công → Nhấn **"Active"** để workflow chạy liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Email để báo lỗi**:
   - Node `Format Error Alert` → Kết nối với **Slack Webhook** hoặc **Email Node** để thông báo khi workflow lỗi.
   - **Cách làm**:
     ```json
     {
       "node": "Format Error Alert",
       "operation": "set",
       "property": "json",
       "value": {
         "text": "🚨 Workflow {{ $node["Error Trigger"].json["error"]["message"] }} đã lỗi!",
         "blocks": [
           {
             "type": "section",
             "text": {
               "type": "mrkdwn",
               "text": "*Lỗi trong workflow:* {{ $node["Error Trigger"].json["error"]["message"] }}"
             }
           }
         ]
       }
     }
     ```
     → Kết nối với **Slack Webhook** để gửi thông báo.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại **tất cả câu hỏi và trả lời**.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.googleSheets` → Kết nối với sheet mới.
     - Sử dụng node `set` để format dữ liệu trước khi lưu.

3. **Cập nhật tri thức định kỳ**:
   - Sử dụng **n8n Scheduler** để **tải tự động** tài liệu mới từ Google Drive/Dropbox vào tri thức cơ sở.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.schedule` → Chọn thời gian (ví dụ: 03:00 hàng ngày).
     - Kết nối với node `Upload Knowledge Base Form`.

4. **Tối ưu hóa mô hình Gemini**:
   - Nếu budget cho phép, thử **mô hình Gemini Pro** (`models/gemini-1.5-pro`) để trả lời **chất lượng cao hơn**.
   - **Lưu ý**: Gemini Pro có **quota cao hơn**, cần kiểm tra ngân sách API.

5. **Duyệt lại tri thức**:
   - Thêm node **Google Forms** để **nhận phản hồi** từ người dùng về câu trả lời của chatbot.
   - Nếu câu trả lời sai → **Cập nhật lại tri thức cơ sở**.

---

### 📌 **Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian & Tăng Trải Nghiệm Khách Hàng**
Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc tra cứu thông tin thủ công, đồng thời **tăng độ chính xác và cá nhân hóa** trong tương tác với khách hàng.

**Các sếp nên:**
✅ **Self-host n8n trên VPS** để tránh giới hạn phiên bản cloud.
✅ **Test workflow với dữ liệu mẫu** trước khi áp dụng toàn diện.
✅ **Kết nối Slack/Email** để theo dõi lỗi.
✅ **Cập nhật tri thức định kỳ** để đảm bảo thông tin mới nhất.

**Bắt đầu ngay!** Import workflow, cấu hình database, và **xem chatbot của bạn hoạt động như thế nào**. Nếu có vấn đề, hãy để lại comment dưới đây, chúng tôi sẽ hỗ trợ!

---
**🚀 Hãy tự động hóa tri thức của doanh nghiệp ngay hôm nay!**