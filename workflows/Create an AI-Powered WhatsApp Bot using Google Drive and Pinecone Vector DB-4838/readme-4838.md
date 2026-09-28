---
title: "🤖 Tạo Bot WhatsApp AI Tự Động Hóa với Google Drive + Pinecone Vector DB (Không Cần Code)"
description: "Tự động hóa bot WhatsApp thông minh dựa trên tri thức từ Google Drive, trả lời chính xác và cá nhân hóa bằng AI GPT-4o-mini. Cập nhật tự động khi tài liệu thay đổi, hỗ trợ cả nhóm chat."
slug: "tai-tao-bot-whatsapp-ai-google-drive-pinecone"
tags: [n8n, automation, ai, whatsapp-bot, pinecone, google-drive, no-code]
keywords: [bot whatsapp tự động hóa, pinecone vector db, ai chatbot google drive, tự động hóa hỗ trợ khách hàng, n8n workflow ai]
---

# 🚀 **Tạo Bot WhatsApp AI Tự Động Hóa với Google Drive + Pinecone Vector DB**

### **Giải pháp cho các sếp:**
Tired of answering the same customer questions repeatedly? Or struggling to keep your team’s knowledge base up-to-date? **This AI-powered WhatsApp bot** automates responses using your **Google Drive documents** as a knowledge base, powered by **Pinecone Vector DB** and **OpenAI’s GPT-4o-mini**. No coding required—just import, configure, and let the bot handle everything.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Bot tự động trả lời các câu hỏi thường gặp từ khách hàng hoặc nội bộ.
- **Chính xác & cá nhân hóa:** Trả lời dựa trên **tài liệu Google Drive** của doanh nghiệp, không sai lệch.
- **Hỗ trợ nhóm chat:** Bot chỉ phản hồi khi được **tag** trong nhóm, không làm rối loạn hội thoại.
- **Cập nhật tự động:** Khi tài liệu trên Google Drive thay đổi, **Pinecone Vector DB** sẽ tự động sync trong vòng **1 phút**.
- **Không cần Meta Account:** Hoạt động với **số WhatsApp thông thường**, không cần API chính thức của Meta.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu tài liệu tri thức).
2. **Tài khoản Pinecone API** (để tạo Vector DB với **dimensions = 1536**).
3. **API Key OpenAI** (để sử dụng **GPT-4o-mini** và Embeddings).
4. **Số WhatsApp** (để kết nối với bot).
5. **Đăng ký Webhook WhatsApp** (xem hướng dẫn [Request Access](#) dưới đây).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4838](https://n8n.io/workflows/4838).
- Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
- **Hoặc** copy toàn bộ JSON và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Google Drive**
- **Node "Every minute check if file is updated"**:
  - Điền **Google Drive credentials** (tạo theo [hướng dẫn](https://docs.n8n.io/integrations/builtin/credentials/google/)).
  - Chọn **file Google Drive** chứa tài liệu tri thức (ví dụ: PDF, DOCX, TXT).
- **Node "Download the file from Google Drive"**:
  - Chọn cùng **credentials Google Drive** như trên.
  - Đảm bảo **file được chia sẻ cho tài khoản n8n**.

##### **B. Cấu hình Pinecone Vector DB**
- **Tạo Index Pinecone**:
  - Đăng nhập [Pinecone Console](https://app.pinecone.io/).
  - Tạo **mới một index** với **dimensions = 1536** (phù hợp với OpenAI Embeddings).
- **Node "Index Pinecone Vector Store"**:
  - Chọn **credentials Pinecone API** (tạo theo [hướng dẫn Pinecone](https://docs.pinecone.io/docs/quickstart)).
  - Điền **index name** vừa tạo.
- **Node "Get top chunks matching query"**:
  - Chọn cùng **credentials Pinecone API**.
  - Đảm bảo **index name** khớp với node trên.

##### **C. Cấu hình OpenAI**
- **Node "Embeddings OpenAI" & "OpenAI Chat Model"**:
  - Điền **OpenAI API Key** (tạo tại [OpenAI Dashboard](https://platform.openai.com/account/api-keys)).
  - Chọn **model = gpt-4o-mini** (đã cấu hình sẵn trong workflow).
- **Node "Embeddings OpenAI2"**:
  - Sử dụng cùng **credentials OpenAI** như trên.

##### **D. Cấu hình WhatsApp Webhook**
- **Node "Listen to Whatsapp webhook"**:
  - Điền **path** là `d1629cd7-6e05-413a-bac0-3c435d4e43b9` (không thay đổi).
  - **HTTP Method** giữ nguyên `POST`.
- **Request Access WhatsApp**:
  - Điền thông tin vào [form này](https://docs.google.com/forms/d/e/1FAIpQLSd-bW5tSJu_rRvJ4NmFrxXSAwaNbO7MbGJtUIS-mBA23B7BWQ/viewform).
  - Sau khi xác nhận, bot sẽ hoạt động trên số WhatsApp của bạn.

##### **E. Cấu hình AI Agent (Optional)**
- **Node "Question & Answer"**:
  - Nếu muốn **tùy chỉnh hệ thống prompt**, mở node này và chỉnh sửa **system message** trong tab **Code**.
  - Ví dụ:
    ```json
    {
      "systemMessage": "You are a helpful assistant for [Tên Doanh Nghiệp]. Use the provided context to answer questions accurately."
    }
    ```

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** và gửi **tài liệu mẫu** vào Google Drive.
  - Kiểm tra **Pinecone Console** để xác nhận dữ liệu đã được index.
- **Bật Active**:
  - Sau khi test thành công, chuyển **Active** sang `ON`.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh hệ thống prompt**:
   - Mở node **"Question & Answer"** → Tab **Code** → Chỉnh sửa `systemMessage` để bot phù hợp với ngành nghề của doanh nghiệp.
   - Ví dụ:
     ```json
     {
       "systemMessage": "You are a customer support agent for [Tên Doanh Nghiệp]. Always respond politely and provide solutions based on our product documentation."
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm **node `n8n-nodes-base.httpRequest`** sau node **"Respond to Whatsapp Webhook"** để gửi log đến **Google Sheets** hoặc **Slack**.
   - Cấu hình như sau:
     ```json
     {
       "method": "POST",
       "url": "https://hooks.slack.com/services/YOUR_WEBHOOK_URL",
       "body": {
         "text": "🤖 Bot WhatsApp đã nhận câu hỏi: {{ $json.body.textBody }}"
       }
     }
     ```

3. **Báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy **tái index** Pinecone mỗi ngày (thay vì mỗi phút).
   - Cấu hình:
     ```json
     {
       "cronTime": "0 0 * * *", // Lúc 0h hàng ngày
       "active": true
     }
     ```

4. **Hỗ trợ nhiều ngôn ngữ**:
   - Thêm **node `n8n-nodes-base.translate`** (nếu có) để dịch câu hỏi từ khách hàng sang tiếng Việt trước khi xử lý.

5. **Kết hợp với Slack**:
   - Thêm **node `n8n-nodes-base.slack`** để bot cũng hoạt động trên Slack cùng lúc.

---

### 📌 **Kết luận**
Với **bot WhatsApp AI tự động hóa này**, các sếp đã có một **công cụ hỗ trợ khách hàng 24/7**, **cập nhật tự động** và **không cần code**. Dùng để:
✅ **Hỗ trợ khách hàng** (FAQ, tư vấn sản phẩm).
✅ **Trợ lý nội bộ** (trả lời câu hỏi về chính sách, thủ tục).
✅ **Quản lý cộng đồng** (trả lời câu hỏi trong nhóm WhatsApp).

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với số WhatsApp khác** để đảm bảo hoạt động.
3. **Tùy chỉnh prompt** để phù hợp với doanh nghiệp.

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/4838) và bắt đầu tự động hóa ngay!