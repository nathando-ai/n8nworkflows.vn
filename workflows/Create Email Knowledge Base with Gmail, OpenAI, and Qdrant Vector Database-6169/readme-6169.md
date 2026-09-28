---
title: "🤖 Tự Động Tạo Hệ Thống Trợ Lý AI Trả Lời Câu Hỏi Từ Email (Gmail + OpenAI + Qdrant) - Không Cần Code"
description: "Workflow tự động hóa chuyển đổi toàn bộ email vào cơ sở tri thức AI, cho phép các sếp trả lời câu hỏi liên quan đến nội dung email một cách nhanh chóng và chính xác 24/7. Giảm thiểu thời gian tìm kiếm thông tin từ 30 phút xuống dưới 5 giây!"
slug: "tay-dong-tao-he-thong-tro-ly-ai-tu-email-gmail-openai-qdrant"
tags: [n8n, automation, ai-rag, gmail, openai, vector-database, no-code]
keywords: [n8n workflow email ai, tự động hóa cơ sở tri thức, chatbot trả lời câu hỏi từ email, qdrant vector database, openai embeddings, n8n langchain]
---

# 🚀 **Tự Động Tạo Hệ Thống Trợ Lý AI Trả Lời Câu Hỏi Từ Email (Gmail + OpenAI + Qdrant)**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải mất **30 phút** để tìm kiếm thông tin trong hàng trăm email cũ để trả lời một câu hỏi của khách hàng hoặc đồng nghiệp? Hay phải **quay lại lại** những cuộc trò chuyện email cũ để nhắc lại chi tiết một dự án? Với **workflow này**, các sếp có thể:
✅ **Tự động hóa** việc chuyển đổi toàn bộ email thành cơ sở tri thức AI.
✅ **Trả lời câu hỏi** về nội dung email chỉ trong **5 giây** bằng trợ lý AI.
✅ **Giảm thiểu rủi ro** mất thông tin quan trọng khi người dùng thay đổi.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng để bảo mật API keys và dữ liệu nhạy cảm.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (phù hợp cho n8n + Qdrant)
:::

---

## 🎯 **Kết quả các sếp nhận được**
### **Lợi ích cốt lõi:**
1. **Tiết kiệm thời gian** lên đến **90%** khi trả lời câu hỏi liên quan đến email.
2. **Chính xác 100%** nhờ AI RAG (Retrieval-Augmented Generation) kết hợp Qdrant.
3. **Cập nhật tự động** khi có email mới, không cần can thiệp thủ công.
4. **Bảo mật cao** với self-hosted, không phụ thuộc vào cloud công cộng.
5. **Dễ mở rộng** cho nhiều tài khoản Gmail khác nhau.

---
## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã cấp quyền OAuth2 cho n8n).
✔ **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
✔ **Qdrant Vector Database** (cài đặt trên cùng VPS với n8n hoặc cloud riêng).
✔ **n8n Self-hosted** (cài đặt [n8n Community](https://docs.n8n.io/hosting/installation/) hoặc [n8n Cloud](https://n8n.io/)).
✔ **Node LangChain** (cài đặt từ [n8n Marketplace](https://marketplace.n8n.io/)).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ JSON**
1. Tải workflow từ [link gốc](https://n8n.io/workflows/6169) hoặc copy JSON từ đây.
2. Trên **n8n Editor**, nhấn **Import** → **Paste JSON** → Dán và nhấn **Import**.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy từ Canvas**
1. Trên trang workflow gốc, nhấn **Export** → Copy JSON.
2. Trên n8n Editor của các sếp, nhấn **Import** → **Paste JSON** → Dán và import.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Credentials**
Các sếp cần thiết lập **credentials** cho các node quan trọng:

| **Node**               | **Credentials cần thiết**       | **Hướng dẫn cấu hình**                                                                 |
|------------------------|----------------------------------|----------------------------------------------------------------------------------------|
| **Gmail Trigger**      | `gmailOAuth2`                     | 1. Tạo OAuth2 credential tại **Settings → Credentials → Add Credential → Gmail OAuth2**. |
|                        |                                  | 2. Chọn **Gmail API** và đăng nhập tài khoản Gmail.                                    |
| **OpenAI Chat Model**  | `openAiApi`                      | 1. Tạo API Key tại [OpenAI](https://platform.openai.com/), sao chép và thêm vào credential. |
| **Embeddings OpenAI**  | `openAiApi`                      | Cùng với `openAiApi` trên.                                                              |
| **Qdrant Vector Store**| `qdrant` (tự tạo)               | 1. Cài đặt Qdrant trên VPS (hướng dẫn [đây](https://qdrant.tech/documentation/quick-start/)).
|                        |                                  | 2. Thêm credential mới tại **Settings → Credentials → Add Credential → Qdrant**.         |
|                        |                                  | 3. Điền `Url` (ví dụ: `http://localhost:6333`) và `Api Key` (nếu có).                 |

#### **B. Cấu hình Node Qdrant**
1. Trong node **Qdrant Email Vector Store**, **Qdrant Vector Store**, **Qdrant Vector Store1**:
   - **Collection Name**: Đặt tên duy nhất (ví dụ: `email_knowledge_base`).
   - **Vector Size**: Giá trị mặc định (384, phù hợp với embeddings OpenAI).
   - **Distance Metric**: Chọn `cosine` (tối ưu cho RAG).
   - **Url**: Điền URL Qdrant (ví dụ: `http://localhost:6333`).

#### **C. Cấu hình Node RAG Agent**
1. Trong node **RAG Agent**:
   - **Agent Type**: Chọn `langchain.agent`.
   - **Prompt Template**: Sử dụng mặc định hoặc tùy chỉnh để phù hợp với ngữ cảnh email.
   - **Tools**: Đảm bảo các tool như `Qdrant Vector Store` và `OpenAI Chat` được kết nối.

#### **D. Cấu hình Node Chat Trigger (Trả lời câu hỏi)**
1. Trong node **When chat message received**:
   - **Trigger Type**: Chọn **Chat Trigger** (n8n LangChain).
   - **Credentials**: Chọn `openAiApi`.
   - **Model**: Chọn mô hình OpenAI phù hợp (ví dụ: `gpt-3.5-turbo`).

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test Run** với dữ liệu mẫu (ví dụ: một email mẫu).
   - Kiểm tra các node **Embeddings OpenAI** và **Qdrant Vector Store** có lưu trữ embeddings thành công không.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow hoạt động liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Kết hợp với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để nhận câu hỏi từ nhóm.
- Cấu hình **Chat Trigger** để nhận input từ Slack/Telegram và trả lời tự động.

### **2. Lưu log hoạt động**
- Thêm node **StickyNote** hoặc **Google Sheets** để ghi lại lịch sử câu hỏi và trả lời.
- Ví dụ: Lưu vào Google Sheets với cột `Date`, `Question`, `Answer`, `Email ID`.

### **3. Tự động cập nhật cơ sở tri thức**
- Sử dụng **Cron Job** (n8n Schedule Node) để chạy workflow định kỳ (ví dụ: hàng ngày) để cập nhật embeddings từ email mới.

### **4. Tùy chỉnh prompt cho RAG Agent**
- Trong node **RAG Agent**, chỉnh sửa **prompt template** để AI trả lời chính xác hơn:
  ```plaintext
  Context: {context}
  Question: {question}
  Answer the question based on the context. If the context doesn't provide enough information, say "I don't have enough information in the emails."
  ```

### **5. Bảo mật dữ liệu nhạy cảm**
- **Mask email content**: Sử dụng node **Code** để xóa hoặc ẩn thông tin nhạy cảm (ví dụ: số điện thoại, địa chỉ) trước khi lưu vào Qdrant.
- **Chia sẻ Qdrant với quyền hạn**: Cấu hình Qdrant để chỉ cho phép truy cập từ IP VPS của các sếp.

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi việc tìm kiếm thông tin trong email, đồng thời **tăng cường hiệu suất** với AI RAG. Với **self-hosted n8n + Qdrant**, dữ liệu hoàn toàn **an toàn và kiểm soát được**.

**Hành động ngay:**
1. **Import workflow** và cấu hình credentials.
2. **Test Run** với email mẫu.
3. **Bật Active** và bắt đầu sử dụng trợ lý AI trả lời câu hỏi từ email!

---
**🚀 Cần hỗ trợ thêm?**
- Trả lời câu hỏi tại [n8n Community](https://community.n8n.io/).
- Liên hệ với tác giả Zain Ali qua [GitHub](https://github.com/zainali1999).