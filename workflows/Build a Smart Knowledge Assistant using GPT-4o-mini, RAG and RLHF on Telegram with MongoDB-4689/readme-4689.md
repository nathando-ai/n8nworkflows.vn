---
title: "🤖 **Tự Động Hóa Trợ Lý Tri Thức Thông Minh (RAG + RLHF) Trên Telegram Với MongoDB & GPT-4o-mini - Giải Pháp Hỗ Trợ Khách Hàng AI 24/7**"
description: "Workflow này xây dựng một trợ lý AI thông minh tích hợp RAG (Retrieval-Augmented Generation) và RLHF (Reinforcement Learning from Human Feedback) để trả lời câu hỏi khách hàng trên Telegram từ cơ sở tri thức Google Docs, với khả năng học tập liên tục từ phản hồi người dùng. Giúp doanh nghiệp tiết kiệm 80% thời gian hỗ trợ, cải thiện chất lượng phản hồi và tự động hóa quy trình tri thức."
slug: "tay-dong-hoa-tro-ly-tri-thuc-rag-rlhf-telegram-mongodb-gpt-4o-mini"
tags: [n8n, automation, ai, support, telegram, mongodb, gpt-4o-mini, rag, rlhf, no-code]
keywords: [n8n workflow hỗ trợ khách hàng, tự động hóa trợ lý AI Telegram, RAG với MongoDB, RLHF cho AI, tích hợp Google Docs với OpenAI, tự động hóa hỗ trợ 24/7]
---

# 🚀 **Xây Dựng Trợ Lý Tri Thức Thông Minh (RAG + RLHF) Trên Telegram - Giải Pháp Hỗ Trợ Khách Hàng AI Tự Động Hóa 100%**

## **🔥 Nỗi Đau Của Doanh Nghiệp Hiện Nay**
Hiện nay, các doanh nghiệp phải đối mặt với những thách thức lớn trong việc hỗ trợ khách hàng:
- **Tốn thời gian**: Đội ngũ hỗ trợ phải trả lời hàng trăm câu hỏi lặp đi lặp lại hàng ngày.
- **Chất lượng không đồng nhất**: Các nhân viên có kiến thức khác nhau dẫn đến phản hồi không nhất quán.
- **Không học tập được**: Hệ thống không tự động cải thiện dựa trên phản hồi của khách hàng.
- **Không tích hợp tri thức**: Dữ liệu từ Google Docs, FAQ, hoặc tài liệu nội bộ không được sử dụng hiệu quả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 80% công việc hỗ trợ** với trợ lý AI 24/7.
✅ **Trả lời chính xác và cá nhân hóa** nhờ RAG (Retrieval-Augmented Generation).
✅ **Học tập từ phản hồi người dùng** với RLHF (Reinforcement Learning from Human Feedback).
✅ **Tích hợp tri thức từ Google Docs** và lưu trữ trên MongoDB với vector embeddings.
✅ **Hoạt động liên tục** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian hỗ trợ**: Giảm 80% công việc lặp lại cho đội ngũ CSKH.
- **Chất lượng phản hồi cao**: AI trả lời dựa trên tri thức chính xác từ Google Docs.
- **Học tập liên tục**: Trợ lý AI cải thiện dựa trên phản hồi thực tế từ khách hàng.
- **Tích hợp đa kênh**: Hoạt động trên Telegram, có thể mở rộng sang WhatsApp, Email, Slack.
- **Bảo mật dữ liệu**: Dữ liệu khách hàng và tri thức được lưu trữ an toàn trên MongoDB Atlas.
- **Tiết kiệm chi phí**: Không cần thuê thêm nhân viên hỗ trợ, giảm chi phí đào tạo.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **OpenAI API Key** (để sử dụng GPT-4o-mini và Embeddings).
   - **Google Cloud OAuth 2.0 API Key** (để đọc Google Docs).
   - **MongoDB Atlas API Key** (để lưu trữ vector embeddings và phản hồi).
   - **Telegram Bot Token** (để kết nối với Telegram).

2. **Dữ liệu ban đầu**:
   - **Google Docs** chứa tri thức cần tích hợp (ví dụ: FAQ, tài liệu sản phẩm).
   - **MongoDB Atlas Database** đã cấu hình với hai collection:
     - `documentation` (lưu tri thức từ Google Docs).
     - `feedback` (lưu phản hồi từ khách hàng để cải thiện AI).

3. **Cấu hình MongoDB Atlas**:
   - **Collection `documentation`** phải có schema như sau:
     ```json
     {
       "mappings": {
         "dynamic": false,
         "fields": {
           "_id": { "type": "string" },
           "text": { "type": "string" },
           "embedding": { "type": "knnVector", "dimensions": 1536, "similarity": "cosine" },
           "source": { "type": "string" },
           "doc_id": { "type": "string" }
         }
       }
     }
     ```
   - **Collection `feedback`** phải có schema như sau:
     ```json
     {
       "mappings": {
         "dynamic": false,
         "fields": {
           "prompt": { "type": "string" },
           "response": { "type": "string" },
           "text": { "type": "string" },
           "embedding": { "type": "knnVector", "dimensions": 1536, "similarity": "cosine" },
           "feedback": { "type": "token" }
         }
       }
     }
     ```
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/4689](https://n8n.io/workflows/4689) (chọn "Download JSON").
2. **Mở n8n Editor** trên máy chủ tự động hóa của bạn.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo một workflow mới.
2. **Nhấn "Import"** → **"Import from JSON"** → **"Paste JSON"**.
3. **Dán JSON** từ [n8n.io/workflows/4689](https://n8n.io/workflows/4689) (chọn "Copy JSON").
4. **Nhấn "Import"** để workflow xuất hiện.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **23 node** và yêu cầu cấu hình chi tiết. Dưới đây là hướng dẫn cụ thể cho từng phần quan trọng:

#### **🔹 Cấu Hình Credentials (Tham Số API)**
| **Node**                     | **Credentials Cần Thiết**       | **Hướng Dẫn Cấu Hình**                                                                 |
|------------------------------|----------------------------------|-----------------------------------------------------------------------------------------|
| OpenAI Chat Model             | `openAiApi`                      | Điền **API Key** từ OpenAI (mô hình `gpt-4o-mini`).                                      |
| Embeddings OpenAI             | `openAiApi`                      | Sử dụng cùng **API Key** như trên.                                                      |
| Google Docs Importer          | `googleDocsOAuth2Api`            | Cấu hình OAuth 2.0 từ [Google Cloud Console](https://console.cloud.google.com/).         |
| MongoDB Chat Memory           | `mongoDb`                        | Điền **URI MongoDB Atlas** và **Database Name**.                                          |
| Vector Store MongoDB Atlas    | `mongoDb`                        | Sử dụng cùng **URI** và **Database Name** như trên.                                     |
| Telegram Trigger              | `telegramApi`                    | Điền **Bot Token** từ [@BotFather](https://t.me/BotFather) trên Telegram.               |
| Telegram Send Message         | `telegramApi`                    | Sử dụng cùng **Bot Token** như trên.                                                     |

#### **🔹 Cấu Hình Node Quá Trình**
##### **A. Import Tri Thức từ Google Docs**
1. **Node "Google Docs Importer"**:
   - **Operation**: Chọn `get`.
   - **File ID**: Điền ID của Google Docs chứa tri thức (tham khảo [cách lấy ID](https://support.google.com/docs/answer/44859?hl=vi)).
   - **Range**: Chọn toàn bộ sheet (ví dụ: `Sheet1!A:Z`).

2. **Node "Document Section Loader"**:
   - **Source**: Chọn kết quả từ node `Google Docs Importer`.
   - **Format**: Chọn `text`.

3. **Node "Document Chunker"**:
   - **Chunk Size**: Đặt `1000` (tùy chỉnh theo nhu cầu).
   - **Chunk Overlap**: Đặt `200`.

4. **Node "OpenAI Embeddings Generator"**:
   - **Model**: Chọn `text-embedding-ada-002` (hoặc tương tự).
   - **Input**: Kết nối từ node `Document Chunker`.

5. **Node "MongoDB Documentation Inserter"**:
   - **Collection**: Chọn `documentation`.
   - **Fields**:
     - `_id`: `{ "type": "string" }`
     - `text`: `{ "type": "string" }`
     - `embedding`: `{ "type": "knnVector", "dimensions": 1536 }`
     - `source`: `{ "type": "string" }`
     - `doc_id`: `{ "type": "string" }`

##### **B. Xử Lý Câu Hỏi từ Telegram**
1. **Node "Receive Message on Telegram"**:
   - **Chat ID**: Điền ID chat của bot (có thể lấy từ [@userinfobot](https://t.me/userinfobot)).
   - **Trigger**: Chọn `message` và lọc nội dung (ví dụ: `text`).

2. **Node "Knowledge Base Agent"**:
   - **Model**: Chọn `gpt-4o-mini`.
   - **Tools**:
     - **Retrieve from MongoDB**: Chọn `Search Documentation` (từ node `vectorStoreMongoDBAtlas`).
     - **Store feedback**: Chọn `Submit embedded chat feedback` (từ node `vectorStoreMongoDBAtlas`).

3. **Node "Send Message on Telegram, Wait for Feedback"**:
   - **Text**: `{ $json["response"] }` (trả lời AI).
   - **Reply Markup**: Tạo nút phản hồi (ví dụ: `Thích`, `Không thích`, `Cải thiện`).

##### **C. Lưu Phản Hồi và Cải Thiện AI**
1. **Node "Map feedback data"**:
   - **JavaScript Code** (sử dụng trong node `code`):
     ```javascript
     return {
       prompt: $input.all()[0].json.prompt,
       response: $input.all()[0].json.response,
       text: $input.all()[0].json.text,
       embedding: $input.all()[0].json.embedding,
       feedback: $input.all()[0].json.feedback
     };
     ```

2. **Node "Set feedback fields for collection storage"**:
   - **Fields**: Điền theo schema của collection `feedback`.

3. **Node "Submit embedded chat feedback"**:
   - **Collection**: Chọn `feedback`.
   - **Fields**: Điền theo kết quả từ node `Map feedback data`.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **"Execute Workflow"** để chạy thủ công và kiểm tra:
     - AI có trả lời chính xác không?
     - Phản hồi từ Telegram có được lưu vào MongoDB không?
   - **Gợi ý**: Gửi câu hỏi mẫu như:
     - *"Sản phẩm của công ty có tính năng gì?"*
     - *"Làm thế nào để đặt hàng?"*

2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật "Active"** để workflow hoạt động liên tục.
   - **Lưu ý**: Đảm bảo MongoDB và Telegram Bot luôn online.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tích Hợp Với Slack hoặc Email**
- **Sử dụng node `slack` hoặc `email`** để mở rộng kênh hỗ trợ.
- **Cấu hình Webhook** từ Slack/Email vào node `webhook` mới để nhận tin nhắn.

### **2. Lưu Log và Báo Cáo Hàng Ngày**
- **Thêm node `set`** để lưu log hoạt động vào MongoDB.
- **Sử dụng node `googleSheets`** để tạo báo cáo thống kê phản hồi khách hàng.

### **3. Cập Nhật Tri Thức Từ Google Docs**
- **Tạo một workflow riêng** để tự động cập nhật tri thức khi Google Docs thay đổi.
- **Sử dụng node `googleDrive`** để theo dõi thay đổi file.

### **4. Tối Ưu Hóa Mô Hình AI**
- **Thử nghiệm mô hình khác** như `gpt-4` (nếu ngân sách cho phép).
- **Tùy chỉnh prompt** trong node `lmChatOpenAi` để cải thiện chất lượng trả lời.

### **5. Bảo Mật Dữ Liệu**
- **Mật mã hóa API Key** trong n8n bằng node `set`.
- **Sử dụng MongoDB Atlas với TLS** để bảo mật dữ liệu.

---

## **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa hỗ trợ khách hàng với AI thông minh, học tập liên tục và tích hợp tri thức từ Google Docs. Với **RAG + RLHF**, trợ lý AI của bạn sẽ ngày càng thông minh hơn, giúp doanh nghiệp tiết kiệm chi phí và cải thiện trải nghiệm khách hàng.

**🚀 Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản** (OpenAI, Google, MongoDB, Telegram).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật hoạt động** để trải nghiệm sự thay đổi!

---
:::note[**Lưu Ý Cuối Cùng**]
- **N8n Self-Hosted** là lựa chọn tối ưu để workflow hoạt động 24/7 mà không bị giới hạn.
- **Nếu gặp vấn đề**, tham khảo [n8n Community](https://community.n8n.io/) hoặc liên hệ NovaNode (tác giả của workflow).
- **Mở rộng khả năng**: Workflow này có thể tích hợp với **WhatsApp, Email, hoặc CRM** như HubSpot/Zoho.
:::

---
**🎁 Đăng ký VPS TinoHost để tự động hóa 24/7:**
👉 [VPS N8n TinoHost](https://tino.vn/vps-n8n?affid=388) (💰 **Giảm 39%** với mã **VPSN8N**)
👉 [VPS Xeon