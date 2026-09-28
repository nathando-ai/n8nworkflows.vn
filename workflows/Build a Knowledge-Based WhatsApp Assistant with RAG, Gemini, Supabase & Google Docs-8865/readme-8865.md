---
title: "🤖 **Tự Động Hóa Trợ Lý WhatsApp Căn Bản Với AI Gemini, RAG & Supabase – Không Cần Code!**"
description: "Xây dựng một trợ lý WhatsApp thông minh dựa trên trí tuệ nhân tạo (AI) với công nghệ RAG (Retrieval-Augmented Generation), mô hình Gemini của Google và cơ sở dữ liệu Supabase. Workflow này tự động hóa việc trả lời tin nhắn, phân tích nội dung và cung cấp thông tin chính xác từ tài liệu Google Docs – hoàn toàn tự động, 24/7, không cần can thiệp thủ công."
slug: "tay-dong-hoa-tro-ly-whatsapp-ai-gemini-rag-supabase"
tags: [n8n, automation, no-code, ai-gemini, supabase, whatsapp-bot, content-creation, rag, google-docs]
keywords: [tự động hóa whatsapp với ai, workflow n8n gemini, trợ lý ảo whatsapp, rag ai google docs, supabase n8n, tự động trả lời tin nhắn whatsapp]
---

# 🚀 **Tự Động Hóa Trợ Lý WhatsApp Căn Bản Với AI Gemini, RAG & Supabase**

## **💡 Giải Pháp Cho Những Ai?**
Các sếp đang gặp khó khăn trong việc:
- **Trả lời tin nhắn WhatsApp một cách nhanh chóng và chính xác** mà không phải ngồi thủ công 24/7?
- **Tận dụng tài liệu Google Docs** (ví dụ: FAQ, hướng dẫn sản phẩm, kiến thức nội bộ) để tự động trả lời khách hàng?
- **Cần một trợ lý AI thông minh** có thể phân tích yêu cầu của người dùng và trả lời dựa trên kiến thức hiện có, thay vì phải nhớ tất cả mọi thứ?

**Workflow này giải quyết tất cả!** Nó kết hợp **AI Gemini (Google)**, **công nghệ RAG (Retrieval-Augmented Generation)** và **Supabase** để tạo ra một **trợ lý WhatsApp tự động hóa 100%**, trả lời tin nhắn dựa trên kiến thức từ tài liệu của bạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Không phải trả lời tin nhắn WhatsApp thủ công anymore.
✅ **Trả lời chính xác**: Dựa trên kiến thức từ Google Docs, tránh sai sót của con người.
✅ **Hoạt động 24/7**: Không cần người dùng phải chờ đợi, hệ thống hoạt động liên tục.
✅ **Cá nhân hóa**: AI hiểu yêu cầu của người dùng và trả lời phù hợp.
✅ **Dễ dàng mở rộng**: Thêm tài liệu mới vào Google Docs, hệ thống tự động cập nhật kiến thức.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản WhatsApp Business API** (để kết nối với n8n).
2. **Tài khoản Google Cloud** (để sử dụng mô hình Gemini).
3. **Tài khoản Supabase** (để lưu trữ embedding và dữ liệu).
4. **Tài liệu Google Docs** (chứa kiến thức cần sử dụng, ví dụ: FAQ, hướng dẫn sản phẩm).
5. **API Keys**:
   - **Google Cloud API Key** (để sử dụng Gemini).
   - **Supabase URL & Key** (để kết nối với cơ sở dữ liệu).
   - **WhatsApp Business API Credentials** (để gửi/nhận tin nhắn).
6. **n8n Self-hosted** (để chạy workflow 24/7, không phụ thuộc vào phiên bản miễn phí).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/8865) (hoặc sao chép từ link trên).
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **13 node**, mỗi node đều cần cấu hình chính xác. Dưới đây là **các bước quan trọng**:

##### **🔹 Node 1: WhatsApp Trigger (n8n-nodes-base.whatsAppTrigger)**
- **Cấu hình**:
  - Chọn **WhatsApp Business API** đã đăng ký.
  - **Webhook URL** phải trỏ đến n8n (cần mở port 5678 trên VPS).
  - **Phone Number** (số điện thoại WhatsApp của bạn).

##### **🔹 Node 2: Content for the Training (n8n-nodes-base.googleDocs)**
- **Cấu hình**:
  - **Google Docs ID** (tìm trong URL của file Google Docs).
  - **Sheet Name** (nếu là Google Sheet) hoặc **Document Name**.
  - **Credentials**: Sử dụng **Google OAuth 2.0** (cần tạo **Service Account** và cấp quyền cho Google Docs).

##### **🔹 Node 3: Splitting into Chunks (n8n-nodes-base.code)**
- **Lưu ý**:
  - Node này **chia tài liệu thành các mảnh nhỏ** (chunk) để dễ xử lý.
  - **Không cần chỉnh sửa** nếu đã import file JSON chính xác.

##### **🔹 Node 4 & 5: Embedding Uploaded Document (n8n-nodes-base.httpRequest) + Save the Embedding in DB (n8n-nodes-base.supabase)**
- **Cấu hình Supabase**:
  - **URL Supabase** (ví dụ: `https://abc123.supabase.co`).
  - **API Key** (tìm trong **Project Settings** của Supabase).
  - **Table Name**: Cần tạo **bảng mới** (ví dụ: `document_embeddings`) với các cột:
    - `id` (UUID)
    - `chunk` (nội dung chunk)
    - `embedding` (vector embedding)
    - `document_id` (ID của tài liệu gốc)
  - **Node HTTP Request**:
    - **Endpoint**: API của **Gemini Embeddings** (Google Cloud).
    - **Headers**: `Content-Type: application/json`.
    - **Body**:
      ```json
      {
        "model": "models/embedding-gecko@001",
        "content": "{{$node["Splitting into Chunks"].json["chunk"]}}"
      }
      ```

##### **🔹 Node 6: Aggregate (n8n-nodes-base.aggregate)**
- **Lưu ý**:
  - Node này **gộp các embedding** từ tài liệu thành một danh sách.
  - **Không cần chỉnh sửa** nếu import file JSON chính xác.

##### **🔹 Node 7 & 8: Search Embeddings + Embed User Message (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Endpoint**: API của **Gemini** (để tìm kiếm embedding gần nhất).
  - **Headers**: `Content-Type: application/json`.
  - **Body**:
    - **Search Embeddings**:
      ```json
      {
        "model": "models/embedding-gecko@001",
        "content": "{{$node["Splitting into Chunks"].json["chunk"]}}",
        "task_type": "retrieval_query"
      }
      ```
    - **Embed User Message**:
      ```json
      {
        "model": "models/embedding-gecko@001",
        "content": "{{$json["message"]}}"
      }
      ```

##### **🔹 Node 9: Manual Trigger (n8n-nodes-base.manualTrigger)**
- **Lưu ý**:
  - Node này **không bắt buộc** nếu muốn tự động hóa hoàn toàn.
  - Nếu muốn **test trước**, các sếp có thể kích hoạt thủ công.

##### **🔹 Node 10: Google Gemini Chat Model (n8n-nodes-base.lmChatGoogleGemini)**
- **Cấu hình**:
  - **API Key Google Cloud** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
  - **Model**: Chọn `gemini-pro` (hoặc `gemini-1.5-flash` nếu muốn tiết kiệm chi phí).
  - **Prompt**:
    ```plaintext
    You are a helpful assistant. Use the following context to answer the user's question:
    {{$json["context"]}}

    User question: {{$json["question"]}}
    Answer:
    ```

##### **🔹 Node 11: AI Agent (n8n-nodes-langchain.agent)**
- **Lưu ý**:
  - Node này **tự động hóa logic** của AI dựa trên kết quả từ Gemini.
  - **Không cần chỉnh sửa** nếu import file JSON chính xác.

##### **🔹 Node 12: If (n8n-nodes-base.if)**
- **Cấu hình**:
  - **Condition**: Kiểm tra nếu AI trả lời có ý nghĩa hay không.
  - **Example**:
    ```json
    {{ $json["response"].length > 0 }}
    ```

##### **🔹 Node 13: Send Message (n8n-nodes-base.whatsApp)**
- **Cấu hình**:
  - **Phone Number**: Số điện thoại người dùng gửi tin nhắn.
  - **Message**: Nội dung trả lời từ AI (`{{$json["response"]}}`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi tin nhắn WhatsApp đến số đã cấu hình.
  - Kiểm tra nếu AI trả lời chính xác dựa trên kiến thức từ Google Docs.
- **Bật Active Workflow**:
  - Sau khi test thành công, **bật workflow** để hoạt động 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁC Ý TƯỞNG MỞ RỘNG**]
🔹 **Kết nối với Slack/Telegram**:
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để gửi thông báo khi có tin nhắn mới.

🔹 **Lưu Log & Analytics**:
   - Sử dụng **n8n-nodes-base.googleSheets** hoặc **Supabase** để ghi lại lịch sử tin nhắn và phân tích hiệu suất.

🔹 **Cập Nhật Tài Liệu Tự Động**:
   - Sử dụng **n8n-nodes-base.googleDrive** để tự động tải xuống và cập nhật tài liệu mới từ Google Drive.

🔹 **Thêm Nhiều Mô Hình AI**:
   - Thay thế Gemini bằng **Mistral AI** hoặc **LLama 3** nếu muốn đa dạng hóa.

🔹 **Tạo Báo Cáo Định Kỳ**:
   - Sử dụng **n8n-nodes-base.email** để gửi báo cáo tổng hợp về hoạt động của trợ lý.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách tự động hóa **trả lời tin nhắn WhatsApp** dựa trên kiến thức từ Google Docs, với sự hỗ trợ của **AI Gemini** và **Supabase**. Không cần code, không cần chuyên gia AI – chỉ cần **cấu hình đúng và chạy**!

**🚀 Hãy áp dụng ngay và trải nghiệm sự tự động hóa hoàn toàn!**

---
:::info[**GỢI Ý HẠN CHẾ N8N**]
Để workflow **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS** thay vì dùng phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ?** Hãy để lại bình luận hoặc liên hệ với tác giả [@iamvaar](https://n8n.io/workflows/8865) để được tư vấn chi tiết!