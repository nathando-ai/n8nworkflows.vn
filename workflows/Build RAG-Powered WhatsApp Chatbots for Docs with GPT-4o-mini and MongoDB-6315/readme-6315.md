---
title: "🤖 **Tự Động Hóa Chatbot WhatsApp Cường Độ AI RAG với GPT-4o-mini & MongoDB – Hỗ Trợ Khách Hàng Siêu Nhanh**"
description: "Xây dựng chatbot WhatsApp thông minh dựa trên công nghệ RAG (Retrieval-Augmented Generation) để trả lời khách hàng từ tài liệu Google Docs, với trí nhớ hội thoại và khả năng xử lý âm thanh, hình ảnh, tài liệu. Giảm thời gian hỗ trợ từ 5 phút xuống 30 giây!"
slug: "tay-dong-hoa-chatbot-whatsapp-rag-gpt-4o-mini-mongodb"
tags: [n8n, automation, ai-rag, chatbot-whatsapp, mongodb, gpt-4o-mini, no-code]
keywords: [n8n workflow chatbot, tự động hóa hỗ trợ khách hàng, RAG với MongoDB, GPT-4o-mini WhatsApp, xử lý âm thanh hình ảnh tài liệu]
---

# 🚀 **Chatbot WhatsApp Cường Độ AI RAG: Hỗ Trợ Khách Hàng Siêu Nhanh với GPT-4o-mini & MongoDB**

### **Nỗi Đau Của Các Sếp**
Hiện nay, các doanh nghiệp thường phải:
- **Tốn thời gian** để tìm kiếm thông tin trong tài liệu hỗ trợ khách hàng (Google Docs, PDF, Excel).
- **Không nhớ lịch sử hội thoại** → Khách hàng phải lặp lại thông tin nhiều lần.
- **Không xử lý được nhiều loại file** (âm thanh, hình ảnh, tài liệu) → Trải nghiệm tệ.
- **Cần nhân viên 24/7** để phản hồi nhanh → Chi phí cao.

**Giải pháp?** Một **chatbot WhatsApp tự động hóa 100%** với trí nhớ AI và khả năng tra cứu thông tin từ tài liệu **siêu nhanh**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** với tài nguyên tối thiểu:
- **CPU:** 2 vCore
- **RAM:** 4GB
- **Đĩa:** 50GB SSD

👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
✅ **Trả lời khách hàng trong 30 giây** (thay vì 5 phút tìm kiếm thủ công).
✅ **Trí nhớ hội thoại** → Khách hàng không cần lặp lại thông tin.
✅ **Xử lý tất cả loại file** (âm thanh, hình ảnh, PDF, Excel, Google Docs).
✅ **Tự động cập nhật tài liệu mới** → Không cần cập nhật thủ công.
✅ **Giảm chi phí nhân sự** (giảm 30-50% thời gian hỗ trợ).

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
| **Tài Nguyên**               | **Mô Tả**                                                                 | **Lưu Ý**                                                                 |
|------------------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **API Key OpenAI**           | API Key từ [OpenAI](https://platform.openai.com/account/api-keys) (để sử dụng GPT-4o-mini). | **Không** dùng API Key miễn phí (nếu quá tải, workflow sẽ bị treo).       |
| **MongoDB Atlas**            | Database trên [MongoDB Atlas](https://www.mongodb.com/atlas/database) với **Vector Search**. | Cần tạo **collection** với schema như trong **Search Index Example** dưới đây. |
| **Tài khoản WhatsApp Business** | API WhatsApp Business (đăng ký tại [Meta Developer](https://developers.facebook.com/)). | Cần **Phone Number** và **API Credentials**.                              |
| **Tài liệu Google Docs**      | File Google Docs chứa tài liệu hỗ trợ khách hàng (ví dụ: Sản phẩm, Chính sách). | Workflow sẽ tự động **import** và **chuyển đổi thành vector embeddings**. |
| **VPS n8n (Self-hosted)**    | Máy chủ để chạy workflow 24/7 (không dùng n8n.cloud).                     | **Không** dùng phiên bản miễn phí (n8n.cloud có giới hạn).                  |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6315](https://n8n.io/workflows/6315) (ấn **Export**).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste JSON** vào **Import Workflow** (nếu file quá lớn).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình MongoDB Vector Store**
1. **Tạo Collection** trong MongoDB Atlas với **schema** như sau:
   ```json
   {
     "mappings": {
       "dynamic": false,
       "fields": {
         "_id": { "type": "string" },
         "text": { "type": "string" },
         "embedding": {
           "type": "knnVector",
           "dimensions": 1536,
           "similarity": "cosine"
         },
         "source": { "type": "string" },
         "doc_id": { "type": "string" }
       }
     }
   }
   ```
2. **Điền vào node `MongoDB Vector Store Inserter`**:
   - **Connection Name**: Tên kết nối MongoDB của bạn.
   - **Database Name**: Tên database (ví dụ: `n8n_rag_db`).
   - **Collection Name**: Tên collection (ví dụ: `product_docs`).
   - **Vector Search Index Name**: Tên index vector (ví dụ: `product_docs_index`).

##### **B. Cấu Hình OpenAI**
1. **Tạo API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/account/api-keys).
   - **Chọn model**: `gpt-4o-mini` (rẻ và nhanh).
2. **Thêm Credentials trong n8n**:
   - **Settings** → **Credentials** → **Add Credential** → **OpenAI API**.
   - Điền **API Key** và tên (ví dụ: `openAiApi`).

##### **C. Cấu Hình WhatsApp**
1. **Đăng ký API WhatsApp Business**:
   - Tạo tài khoản tại [Meta Developer](https://developers.facebook.com/).
   - Nhận **Phone Number** và **API Credentials**.
2. **Thêm Credentials trong n8n**:
   - **Settings** → **Credentials** → **Add Credential** → **WhatsApp API**.
   - Điền **Phone Number**, **API Key**, và **App ID**.

##### **D. Cấu Hình Google Docs**
1. **Chia sẻ file Google Docs**:
   - Mở file Google Docs → **Chia sẻ** → Thêm email của **Google OAuth Client ID** (tạo trong **Settings → Credentials → Add Credential → Google OAuth**).
2. **Thêm Credentials trong n8n**:
   - **Settings** → **Credentials** → **Add Credential → Google OAuth**.
   - Điền **Client ID**, **Client Secret**, và **Refresh Token**.

##### **E. Cấu Hình File Extensions & Prompts**
- **Node `Map file extensions`**: Đảm bảo **tất cả file** (PDF, XLSX, DOCX, PNG, MP3) được xử lý.
- **Node `Map document prompt`**: Điền **câu hỏi mẫu** để AI trả lời (ví dụ: *"Tôi cần hỗ trợ về sản phẩm X, hãy tìm thông tin từ tài liệu."*).
- **Node `Map image prompt`**: Điền **câu hỏi mẫu** cho hình ảnh (ví dụ: *"Mô tả chi tiết sản phẩm trong hình này."*).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** để **import tài liệu** từ Google Docs vào MongoDB.
   - Gửi **tin nhắn mẫu** qua WhatsApp để kiểm tra AI trả lời.
2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** và **đặt WhatsApp Trigger** để hoạt động 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
🔹 **Tự động cập nhật tài liệu mới**:
   - Sử dụng **Google Drive Webhook** để khi có file mới, workflow tự động **import và update MongoDB**.

🔹 **Gửi báo cáo định kỳ**:
   - Thêm **node `Set`** sau `Send Response` để **lưu lịch sử hội thoại** vào MongoDB.
   - Sử dụng **node `HTTP Request`** để gửi báo cáo qua **Email/Slack** hàng ngày.

🔹 **Cải thiện trải nghiệm với AI**:
   - **Tăng độ dài context** trong `Simple Memory` để AI nhớ nhiều hơn.
   - **Sử dụng model khác** (nếu `gpt-4o-mini` không đủ) như `gpt-4` (tốn kém hơn).

🔹 **Xử lý lỗi tự động**:
   - Thêm **node `Code`** để **lọc tin nhắn rác** (nếu khách hàng gửi "Xin chào" nhiều lần).
   - **Node `Send Unsupported Response`** để trả lời khi AI không tìm thấy thông tin.

---

### 📌 **Kết Luận**
**Workflow này không chỉ tự động hóa hỗ trợ khách hàng mà còn làm cho AI "thông minh hơn" bằng cách:**
✔ **Tra cứu từ tài liệu thực tế** (không phải từ internet).
✔ **Nhớ lịch sử hội thoại** → Trải nghiệm tốt hơn.
✔ **Xử lý tất cả loại file** (âm thanh, hình ảnh, tài liệu).
✔ **Hoạt động 24/7** trên VPS riêng.

**Hành động ngay!**
1. **Chuẩn bị tài nguyên** (OpenAI, MongoDB, WhatsApp API).
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Test và bật hoạt động** để **giảm thời gian hỗ trợ xuống 30 giây!**

**🚀 Cần hỗ trợ?** Đăng ký **VPS n8n** với **TinoHost** hoặc **BNIX** để workflow chạy ổn định! 👇
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Giảm 39%**)
👉 [Đăng ký VPS Xeon 4GB](https://my.bnix.one/aff.php?aff=172)