---
title: "🤖 Trợ lý AI RAG Thực thời với Gmail + OpenAI GPT: Tự động hóa tìm kiếm email thông minh 100% tự động"
description: "Workflow này tự động hóa việc lưu trữ và truy vấn thông tin từ email Gmail bằng công nghệ RAG (Retrieval-Augmented Generation), giúp các sếp tìm kiếm thông tin nhanh chóng và chính xác thông qua AI Chatbot. Giảm thời gian tìm kiếm email từ 5 phút xuống 5 giây!"
slug: "tro-ly-ai-rag-thuc-thoi-gmail-openai"
tags: [n8n, automation, ai-rag, gmail, openai, vector-database]
keywords: [n8n workflow gmail, tự động hóa email, ai chatbot tìm kiếm email, vector database pgvector, openai gpt, rag technology]
---

# 🚀 Trợ lý AI RAG Thực thời với Gmail + OpenAI GPT: Tìm kiếm thông tin email như "thần thông"

## 📌 Nỗi đau thực tế của các sếp khi tìm kiếm email thủ công
Các sếp đã bao giờ phải:
- **Tìm kiếm email trong hàng trăm tin nhắn** để tìm một thông tin cụ thể?
- **Mất thời gian** copy-paste nội dung email vào chatbot để AI phân tích?
- **Không chắc chắn** rằng đã tìm được tất cả các tin nhắn liên quan?
- **Không có hệ thống lưu trữ thông minh** để truy vấn lại thông tin cũ?

Workflow này **giải quyết tất cả** bằng cách tự động hóa việc:
✅ **Lưu trữ toàn bộ nội dung email** vào vector database (PGVector)
✅ **Tạo chatbot AI thông minh** trả lời câu hỏi về email bằng RAG
✅ **Tìm kiếm thông tin trong email chỉ bằng cách chat** (không cần mở Gmail)

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị giới hạn tài nguyên, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với cấu hình tối thiểu:
- **CPU:** 2 nhân
- **RAM:** 4GB+
- **Disk:** 20GB+

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tìm kiếm thông tin trong email chỉ trong **5 giây** thay vì 5 phút.
- **Truy vấn thông minh:** AI trả lời **câu hỏi phức tạp** về email (ví dụ: "Email nào liên quan đến dự án X trong tháng 12?").
- **Lưu trữ vĩnh cửu:** Tất cả email được **chuyển đổi thành vector** và lưu trữ trong PGVector, không bao giờ mất.
- **Hoạt động liên tục:** Workflow chạy **24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa:** AI hiểu **ngôn ngữ tự nhiên** và trả lời chính xác theo ngữ cảnh email.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (và **API Key Gmail**):
   - Bật **Gmail API** trong [Google Cloud Console](https://console.cloud.google.com/).
   - Tạo **OAuth Client ID** và cấp quyền cho email.
2. **Tài khoản OpenAI** (và **API Key OpenAI**):
   - Tạo **API Key** tại [OpenAI Platform](https://platform.openai.com/).
3. **Cấu hình PostgreSQL + PGVector**:
   - Cài đặt **PostgreSQL 14+** và **PGVector extension**.
   - Tạo **bảng vector** để lưu trữ embeddings.
4. **N8n Self-hosted** (không dùng n8n.cloud):
   - Cài đặt **n8n Community Edition** hoặc **n8n Enterprise**.
   - Cài đặt **nodes LangChain** (bằng cách cài đặt `@n8n/n8n-nodes-langchain`).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/5908](https://n8n.io/workflows/5908) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Create Workflow** trong n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### **A. Cấu hình Gmail Trigger & Get Mail Data**
- **Node "Gmail Trigger"**:
  - Chọn **credentials** là tài khoản Gmail đã cấp quyền OAuth.
  - Chọn **event**: `newEmail` (để workflow kích hoạt khi có email mới).
- **Node "Get Mail Data"**:
  - Chọn **operation**: `get`.
  - Thêm **filter** để chỉ lấy email từ **những thư mục cụ thể** (ví dụ: "Inbox", "Dự án X").

##### **B. Cấu hình PGVector (Vector Database)**
- **Node "Postgres PGVector Store"**:
  - **Host**: Địa chỉ IP của PostgreSQL.
  - **Port**: 5432 (mặc định).
  - **Database**: Tên cơ sở dữ liệu.
  - **Table**: Tên bảng lưu trữ vector (ví dụ: `email_vectors`).
  - **Collection**: Tên collection (ví dụ: `email_embeddings`).
  - **PGVector Extension**: `vector` (đã cài đặt).
  - **Embedding Dimension**: **512** (do OpenAI GPT-3.5 sử dụng).
  - **Credentials**: Tạo **credentials mới** trong n8n với thông tin PostgreSQL.

##### **C. Cấu hình OpenAI API**
- **Node "Embeddings OpenAI" & "OpenAI Chat Model"**:
  - Chọn **credentials**: `openAiApi` (đã tạo trước).
  - **Model**:
    - **Embeddings**: `text-embedding-ada-002` (mặc định).
    - **Chat**: `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).
  - **API Key**: Điền **API Key OpenAI** vào credentials.

##### **D. Cấu hình RAG Agent**
- **Node "New RAG Agent"**:
  - **Agent Type**: `langchain.agent.AgentExecutor`.
  - **Tools**:
    - Chọn **vector store** là `Postgres PGVector Store`.
    - Chọn **chat model** là `OpenAI Chat Model`.
  - **Prompt**: Sử dụng **prompt mặc định** của LangChain (không cần chỉnh sửa).
  - **Credentials**: Chọn `openAiApi`.

##### **E. Cấu hình Chat Trigger (Chatbot AI)**
- **Node "When chat message received"**:
  - Chọn **credentials**: Tạo **credentials mới** với URL của **Slack/Telegram/Discord** (ví dụ: Slack Webhook).
  - **Event**: `message` (để AI phản hồi khi có tin nhắn mới).

---

#### 3. Kích hoạt ⚡️
1. **Test Run** với **email mẫu**:
   - Gửi **email test** vào Gmail.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Chuyển **switch Active** sang **ON**.
   - **Monitor** trong **Execution Log** để theo dõi hoạt động.

---

### ✍️ Mẹo & gợi ý nâng cao
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì sử dụng **Chat Trigger**, các sếp có thể **gửi tin nhắn vào Slack/Telegram** để AI trả lời.
   - Ví dụ: "AI, email nào liên quan đến hợp đồng với khách hàng ABC?"

2. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để lưu **lịch sử truy vấn** của AI.
   - Ví dụ: "AI đã trả lời câu hỏi 'Email nào về dự án Y?' vào lúc 10:00 AM."

3. **Tạo báo cáo định kỳ**:
   - Sử dụng **node `googleSheets`** để **lưu trữ thống kê** về:
     - Số lượng email được xử lý.
     - Thời gian phản hồi trung bình của AI.
     - Top 5 câu hỏi thường gặp.

4. **Cập nhật dữ liệu tự động**:
   - Thêm **node `setInterval`** để **lấy email mới định kỳ** (ví dụ: mỗi 1 giờ).
   - Ít nhất **1 lần/ngày** để đảm bảo dữ liệu mới nhất.

5. **Tối ưu hóa PGVector**:
   - **Tạo index** cho các trường quan trọng (ví dụ: `subject`, `sender`).
   - **Xóa email cũ** sau 6 tháng để tiết kiệm dung lượng.
:::

---

### 📌 Kết luận
Workflow **Real-time Email RAG Assistant** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tìm kiếm email nhanh chóng** mà không cần mở Gmail.
✔ **Truy vấn thông tin thông minh** bằng AI Chatbot.
✔ **Tự động hóa lưu trữ** và truy vấn email một cách **mạnh mẽ và chính xác**.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với email mẫu** để đảm bảo hoạt động.
3. **Kết nối với Slack/Telegram** để sử dụng AI mọi lúc mọi nơi.

🚀 **Từ nay, tìm kiếm email không còn là nỗi đau!** AI sẽ làm tất cả cho các sếp.

---