---
title: "🤖 Tự Động Hóa Chatbot AI Query Dữ Liệu Doanh Nghiệp Với RAG + Text-to-SQL (N8n + OpenAI + Peliqan)"
description: "Workflow tự động hóa chatbot AI sử dụng công nghệ RAG (Retrieval-Augmented Generation) kết hợp Text-to-SQL để truy vấn dữ liệu doanh nghiệp từ nhiều nguồn (CRM, ERP, Notion...) chỉ với câu hỏi tiếng Việt. Giúp các sếp tiết kiệm 10+ giờ/tuần trong việc phân tích báo cáo thủ công."
slug: "tự-dộng-hoa-chatbot-ai-query-dữ-liệu-doanh-nghiệp"
tags: [n8n, automation, ai-chatbot, rag, text-to-sql, peliqan, openai, no-code]
keywords: [n8n workflow chatbot ai, tự động hóa truy vấn sql bằng ai, chatbot doanh nghiệp, rag với openai, peliqan n8n, tự động hóa báo cáo doanh nghiệp]
---

# 🚀 Chatbot AI Query Dữ Liệu Doanh Nghiệp: Từ Câu Hỏi → Kết Quả Trực Tiếp (Không Cần Code)

## 💡 Giới Thiệu: Giải Pháp "Thủ Công → Tự Động" Cho Các Sếp
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Lọc dữ liệu từ CRM (Hubspot, Pipedrive), ERP (QuickBooks), hoặc hệ thống nội bộ (Notion, Google Sheets) để trả lời câu hỏi như:
  *"Doanh thu tháng 12/2023 của khách hàng ở khu vực Bắc Bộ là bao nhiêu?"*
  *"Số lượng đơn hàng bị trì hoãn trên 7 ngày trong tháng này là bao nhiêu?"*
- Tạo báo cáo thủ công từ nhiều nguồn dữ liệu phân tán.
- Đối mặt với **rủi ro sai sót** khi phân tích dữ liệu thủ công.

**Workflow này giải quyết tất cả đó** bằng cách xây dựng một **chatbot AI thông minh** có thể:
✅ **Hiểu câu hỏi tiếng Việt tự nhiên** (ví dụ: *"Hãy cho tôi danh sách khách hàng mới trong tháng này"*).
✅ **Truy vấn SQL chính xác** trên dữ liệu doanh nghiệp (không cần viết code).
✅ **Trả lời chính xác** với dữ liệu từ nhiều nguồn (CRM, ERP, kho lưu trữ đám mây...).
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**. Đây là giải pháp tối ưu nhất để:
- **Bảo mật dữ liệu doanh nghiệp** (không phụ thuộc vào cloud công cộng).
- **Tiết kiệm chi phí** (so với các dịch vụ cloud như AWS Lambda).
- **Tối ưu tốc độ** (không bị giới hạn request như phiên bản cloud).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tuần** trong việc phân tích báo cáo thủ công.
- **Giảm sai sót** do con người (AI truy vấn SQL chính xác 100%).
- **Cập nhật dữ liệu thời gian thực** từ CRM/ERP (không cần sync thủ công).
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa** cho từng bộ phận (HR, Marketing, Finance...).
- **Bảo mật cao** (dữ liệu lưu trữ trên VPS riêng hoặc Supabase).
:::

---

### 🔧 Yêu cầu cần thiết
Trước khi import workflow, các sếp cần chuẩn bị:
#### 1. **Tài khoản & API Keys**
| Dịch vụ               | Yêu cầu                                                                 | Làm thế nào để lấy?                                                                 |
|-----------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **OpenAI**            | API Key (để sử dụng ChatGPT và Embeddings)                             | [Tạo API Key tại OpenAI](https://platform.openai.com/account/api-keys)               |
| **Peliqan**           | API Key (để truy cập dữ liệu doanh nghiệp)                              | [Đăng ký Peliqan](https://peliqan.io/) → Cài đặt → Copy API Key                     |
| **Supabase**          | URL Database & API Key (để lưu trữ vector cho RAG)                     | [Tạo Supabase miễn phí](https://supabase.com/) → Project Settings → Copy URL & Key    |
| **N8n (Self-hosted)**| Cài đặt n8n trên VPS (không dùng phiên bản cloud)                       | [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/installation/installation-on-linux/) |

#### 2. **Dữ liệu doanh nghiệp**
- Các sếp cần **kết nối Peliqan với các nguồn dữ liệu** như:
  - CRM: Hubspot, Pipedrive, Salesforce
  - ERP: QuickBooks, Xero
  - Kho lưu trữ: Notion, Google Sheets, Airtable
- **Hướng dẫn kết nối**:
  1. Đăng ký [Peliqan](https://peliqan.io/) và thêm các nguồn dữ liệu.
  2. Chạy workflow **"RAG"** (nếu có) để sync dữ liệu vào Peliqan.
  3. Chỉnh sửa **tên bảng (table name)** trong node **"Get table data"** để phù hợp với dữ liệu của mình.

#### 3. **Môi trường kỹ thuật**
- **N8n Community Packages**: Cần bật cho phép sử dụng **Peliqan Tool**.
  - Mở terminal và chạy:
    ```bash
    export N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=True
    ```
  - (Nếu dùng Docker, thêm vào `docker-compose.yml`)

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. **Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
##### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/6706](https://n8n.io/workflows/6706).
2. Trên **n8n Editor**, nhấn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

##### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
2. Copy toàn bộ nội dung JSON từ [n8n.io/workflows/6706](https://n8n.io/workflows/6706) và dán vào.
3. Nhấn **"Import"** để hoàn tất.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **13 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **A. Cấu hình OpenAI (2 node)**
- **Node**: `OpenAI Chat Model` và `Embeddings OpenAI for RAG retrieval`
  - **Credentials**: Chọn `"openAiApi"` (đã tạo khi đăng ký OpenAI).
  - **Model**:
    - Chat Model: Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tùy budget).
    - Embeddings: Chọn `text-embedding-ada-002` (mặc định).

##### **B. Cấu hình Peliqan (2 node)**
- **Node**: `Get table data` và `Execute an SQL query via Peliqan`
  - **Credentials**: Chọn `"peliqanApi"` (API Key từ Peliqan).
  - **Node "Get table data"**:
    - **Table Name**: Điền tên **bảng dữ liệu** trong Peliqan (ví dụ: `customers`, `orders`).
    - **Columns**: Nếu cần, chỉ định các cột muốn lấy (ví dụ: `id, name, email`).
  - **Node "Execute SQL query"**:
    - **Operation**: Đã mặc định là `exec`.
    - **Resource**: Đã mặc định là `query`.

##### **C. Cấu hình Supabase (2 node)**
- **Node**: `Supabase Vector Store to store vectors` và `Supabase Vector Store for search`
  - **Credentials**: Chọn `"supabaseApi"` (URL và API Key từ Supabase).
  - **Table Name**: Điền tên **bảng vector** (ví dụ: `rag_vectors`).
  - **Collection Name**: Điền tên **collection** (ví dụ: `documents`).

##### **D. Cấu hình AI Agent (1 node)**
- **Node**: `AI Agent`
  - **System Message**: Đây là **câu lệnh hướng dẫn AI** khi trả lời.
    - Các sếp **cần chỉnh sửa** phần này để phù hợp với dữ liệu của mình.
    - Ví dụ:
      ```json
      "You are a business data assistant. You can query SQL on the following tables: customers, orders, products. Use the following format for SQL queries:
      SELECT column1, column2 FROM table_name WHERE condition.
      Only use the data from the tables mentioned above. If you don't know the answer, say 'I don't have enough information to answer that question.'"
      ```
  - **Tools**: Đã mặc định là `SQL` và `RAG` (không cần chỉnh).

##### **E. Cấu hình Manual Trigger (1 node)**
- **Node**: `When clicking ‘Execute workflow’`
  - Đây là **điểm kích hoạt thủ công** để test workflow.
  - Sau khi cấu hình xong, các sếp có thể **bỏ qua node này** và sử dụng **Webhook** hoặc **Chat Trigger** (node `When chat message received`).

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** trên node `When clicking ‘Execute workflow’` để chạy test.
   - Gửi một **câu hỏi mẫu** như:
     *"Hãy cho tôi danh sách khách hàng mới trong tháng 12/2023"*.
   - Kiểm tra kết quả trả về có chính xác không.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **status workflow** từ **"Inactive"** sang **"Active"**.
   - **Lưu ý**: Nếu dùng **Chat Trigger**, các sếp cần kết nối với **Slack/Telegram/Email** để chatbot hoạt động.

---

### ✍️ Mẹo & gợi ý nâng cao
#### 1. **Kết nối với Slack/Telegram để chatbot hoạt động 24/7**
- Thêm **node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.telegram` sau node `When chat message received`.
- Cấu hình **webhook** từ Slack/Telegram để nhận tin nhắn và trả lời tự động.

#### 2. **Lưu log hoạt động để theo dõi**
- Thêm **node `n8n-nodes-base.stickyNote`** sau node `AI Agent` để ghi lại:
  - Câu hỏi của người dùng.
  - Query SQL được generate.
  - Kết quả trả về.
- **Lợi ích**: Giúp các sếp **debug** và **optimize** chatbot sau này.

#### 3. **Tạo báo cáo định kỳ tự động**
- Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow hàng ngày/lần tuần.
- Ví dụ: **"Tạo báo cáo doanh thu hàng tháng tự động"** bằng cách:
  1. Chạy workflow vào ngày 1 hàng tháng.
  2. AI tự động **truy vấn dữ liệu** và **export ra Google Sheets/Excel**.

#### 4. **Cập nhật dữ liệu thường xuyên**
- **Sync dữ liệu từ Peliqan** vào Supabase mỗi ngày bằng cách:
  - Sử dụng **node `n8n-nodes-base.httpRequest`** để gọi API Peliqan.
  - Chạy workflow **hàng ngày** bằng **node `n8n-nodes-base.schedule`**.

#### 5. **Optimize performance**
- **Chọn model OpenAI tiết kiệm chi phí**: Thay `gpt-4` bằng `gpt-3.5-turbo` nếu budget hạn chế.
- **Tối ưu vector store**: Nếu dữ liệu lớn, chia nhỏ thành **nhiều collection** trong Supabase.

---

### 📌 Kết luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Sản Xuất
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa truy vấn dữ liệu** từ CRM/ERP mà không cần viết code.
✔ **Giảm thời gian phân tích báo cáo** từ **giờ đồng hồ** xuống **giây phút**.
✔ **Bảo mật dữ liệu** bằng cách tự host trên VPS riêng.

**Bước đầu tiên**: Import workflow và **chỉnh sửa System Message** trong AI Agent để phù hợp với dữ liệu của mình. Sau đó, **test với câu hỏi mẫu** và **bật Active** để chatbot hoạt động 24/7!

---
**🚀 Hãy thử ngay và chia sẻ kết quả với chúng tôi!** Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ qua [Peliqan](https://peliqan.io/) để hỗ trợ.