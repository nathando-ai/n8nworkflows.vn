---
title: "🤖 **Tự Động Hóa Trợ Lý AI WhatsApp Siêu Thông Minh Với Gemini AI + Bộ Nhớ Pinecone (Không Cần Code!)**"
description: "Workflow này giúp doanh nghiệp xây dựng một trợ lý AI tự động hóa hỗ trợ khách hàng trên WhatsApp với khả năng nhớ lại lịch sử trò chuyện, trả lời tự nhiên bằng Gemini AI và truy cập bộ kiến thức chuyên ngành. Giảm thiểu thời gian phản hồi từ 5 phút xuống 0 giây!"
slug: "tay-dong-hoa-tro-ly-ai-whatsapp-gemini-pinecone"
tags: [n8n, automation, no-code, chatbot-ai, whatsapp-automation, gemini-ai, pinecone-vector-db]
keywords: [n8n workflow whatsapp, tự động hóa trợ lý ai, gemini ai chatbot, pinecone bộ nhớ ai, hỗ trợ khách hàng tự động, whatsapp automation no-code]
---

# 🚀 **Trợ Lý AI WhatsApp Siêu Thông Minh: Gemini AI + Bộ Nhớ Pinecone (Không Cần Code!)**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hiện nay, hầu hết doanh nghiệp phải mất **5-10 phút** để trả lời một câu hỏi khách hàng trên WhatsApp, đặc biệt khi:
- Khách hàng gọi lại để nhắc lại lịch sử trước đó.
- Câu hỏi liên quan đến nhiều chủ đề khác nhau (đơn hàng, chính sách, sản phẩm).
- Đội ngũ support quá tải, phản hồi chậm.

**Workflow này giúp:**
✅ **Tự động trả lời khách hàng trong giây lát** với khả năng hiểu ngữ cảnh.
✅ **Nhớ lại toàn bộ lịch sử trò chuyện** cho mỗi khách hàng (không cần nhắc lại).
✅ **Truy cập bộ kiến thức chuyên ngành** để trả lời chính xác, không sai sót.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 80% thời gian phản hồi** (giảm từ 5 phút xuống 0 giây).
- **Trải nghiệm khách hàng siêu cá nhân hóa** (AI nhớ tên, sở thích, lịch sử).
- **Chính xác 100%** nhờ bộ nhớ Pinecone và Gemini AI.
- **Hoạt động liên tục** mà không cần giám sát.
- **Dễ dàng mở rộng** cho nhiều khách hàng đồng thời.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản WAMM.pro** (miễn phí 50 tin nhắn/tháng):
   - [Đăng ký WAMM.pro](https://wamm.pro) (sử dụng mã giảm giá **N8NWHATSAPP** để có 10 tin nhắn miễn phí thêm).
   - **Lấy 2 thông tin sau:**
     - **Instance ID** (tìm trong **Account Manager**).
     - **Access Token** (tạo trong **API Keys**).
   - **Cấu hình Webhook** trong WAMM:
     - URL Webhook từ n8n (sau khi import workflow).
     - Chọn **Relevant messages** (loại bỏ tin nhắn không có nội dung).

2. **Tài khoản Pinecone** (miễn phí cho 2 index):
   - Tạo **2 index** với cấu hình:
     - **Tên index 1:** `historywa` (bộ nhớ lịch sử trò chuyện).
     - **Tên index 2:** `knowledge` (bộ kiến thức chuyên ngành).
     - **Dimensions:** `3072` (phù hợp với model `text-embedding-3-large`).
     - **Metric:** `cosine`.
   - **Lưu ý:** Cần **API Key** của Pinecone để kết nối với n8n.

3. **Tài khoản Google AI (Gemini)**:
   - [Đăng ký API Key Gemini](https://makersuite.google.com/) (miễn phí cho 1 triệu request/tháng).
   - **Model sử dụng:** `gemini-pro`.

4. **Tài khoản OpenAI** (miễn phí cho embeddings):
   - [Đăng ký API Key OpenAI](https://platform.openai.com/) (miễn phí cho 5 triệu token/tháng).
   - **Model sử dụng:** `text-embedding-3-large`.

5. **n8n Self-hosted** (không dùng n8n.cloud):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6170) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Cách import:**
  1. Mở **n8n Editor** (trang `workflows`).
  2. Nhấn **Import** → **Paste JSON** → Dán toàn bộ mã JSON.
  3. Nhấn **Import**.

:::note[**Lưu ý quan trọng**]
- **Không thay đổi tên node** (n8n sẽ tự động liên kết).
- **Không xóa node** nào trong workflow (trừ khi biết rõ tác dụng).
:::

### **2. Cấu Hình Cần Thiết (BẮT BUỘC CHỈNH) 📌**
Sau khi import, các sếp phải cấu hình **5 node quan trọng** sau:

#### **A. Node `Webhook` (Nhận tin nhắn từ WhatsApp)**
- **Không cần chỉnh gì** (n8n tự động lấy URL từ WAMM).
- **Kiểm tra:**
  - Webhook đã được **Active** trong WAMM (trong **Integrations → Webhooks**).
  - **HTTP Method:** `POST`.
  - **Path:** `1c9432a6-f982-4102-ad0e-39ec15876b0a` (không đổi).

#### **B. Node `WAMM: Send Message` (Gửi tin nhắn trả lời)**
- **Credentials:**
  - Chọn **`wammApi`** (tạo mới trong **Credentials** của n8n).
  - Điền:
    - **Instance ID:** (từ WAMM).
    - **Access Token:** (từ WAMM).
- **Test:**
  - Gửi tin nhắn test từ WhatsApp → AI nên trả lời tự động.

#### **C. Node `Google Gemini Chat Model` (Trả lời tự nhiên)**
- **Credentials:**
  - Chọn **`googlePalmApi`** (tạo mới).
  - Điền **API Key** từ Google AI.
- **Cấu hình:**
  - **Model:** `gemini-pro` (không đổi).
  - **Temperature:** `0.7` (để AI trả lời tự nhiên).

#### **D. Node `Embeddings OpenAI` (Tạo vector cho bộ nhớ)**
- **Credentials:**
  - Chọn **`openAiApi`** (tạo mới).
  - Điền **API Key** từ OpenAI.
- **Cấu hình:**
  - **Model:** `text-embedding-3-large` (không đổi).

#### **E. Node `Pinecone Vector Store` (Bộ nhớ AI)**
- **Credentials:**
  - Chọn **`pineconeApi`** (tạo mới).
  - Điền:
    - **API Key:** (từ Pinecone).
    - **Environment:** (chọn môi trường của bạn, ví dụ: `us-west1-gcp`).
  - **Index Settings:**
    - **Index 1 (`historywa`):** Dùng để lưu lịch sử trò chuyện.
    - **Index 2 (`knowledge`):** Dùng để lưu bộ kiến thức.
- **Test:**
  - Gửi tin nhắn test → Kiểm tra AI có nhớ lại lịch sử không.

#### **F. Node `AI Agent` (Quản lý logic)**
- **Không cần chỉnh** (n8n tự động kết nối các node khác).
- **Cấu hình mặc định:**
  - **Memory Tool:** Tìm kiếm lịch sử trong `historywa`.
  - **Knowledge Tool:** Tìm kiếm trong `knowledge`.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run:**
   - Nhấn **Run Workflow** với dữ liệu mẫu (ví dụ: tin nhắn "Xin chào").
   - Kiểm tra AI có trả lời tự nhiên không.
2. **Active Workflow:**
   - Nhấn **Active** (đỏ → xanh).
   - **Không quên bật Webhook** trong WAMM.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Cách Tối Ưu Hiệu Suất**]
1. **Populate Knowledge Base (Bộ Kiến Thức):**
   - Sử dụng node `Default Data Loader` để tải lên **FAQ, hướng dẫn sản phẩm, chính sách**.
   - Ví dụ: Tải file PDF/Word về **n8n File System** → Kết nối với node này.

2. **Tự Động Lưu Lịch Sử Trò Chuyện:**
   - Node `Processing data for Pinecone` tự động lưu tin nhắn vào `historywa`.
   - **Không cần chỉnh** (n8n tự động xử lý).

3. **Gửi Báo Cáo Hàng Ngày:**
   - Thêm node **Slack/Telegram** sau `WAMM: Send Message` để báo cáo tin nhắn mới.
   - Ví dụ:
     ```json
     {
       "node": "slack",
       "type": "n8n-nodes-base.slack",
       "credentials": "slackApi",
       "parameters": {
         "channel": "#chatbot-reports",
         "text": "📊 New WhatsApp message from {{ $node["WAMM: Send Message"].json()["phone"] }}: {{ $node["WAMM: Send Message"].json()["message"] }}"
       }
     }
     ```

4. **Hỗ Trợ Nhiều Ngôn Ngữ:**
   - Thêm node **Google Translate** trước khi gửi tin nhắn trả lời.
   - Ví dụ:
     ```json
     {
       "node": "translate",
       "type": "n8n-nodes-base.googleTranslate",
       "credentials": "googleTranslateApi",
       "parameters": {
         "text": "{{ $node["Google Gemini Chat Model"].json()["response"] }}",
         "targetLanguage": "vi"
       }
     }
     ```

5. **Xóa Dữ Liệu Cũ (Cleanup):**
   - Thêm node **Code** sau `Pinecone Vector Store` để xóa tin nhắn cũ hơn 30 ngày.
   - Ví dụ:
     ```javascript
     // Node Code (xóa tin nhắn cũ)
     const { $node } = context;
     const now = new Date();
     const thirtyDaysAgo = new Date(now.getTime() - 30 * 24 * 60 * 60 * 1000);

     if ($node.input[0].timestamp && new Date($node.input[0].timestamp) < thirtyDaysAgo) {
       $node.output[0].data = { delete: true };
     } else {
       $node.output[0].data = $node.input[0].data;
     }
     ```
:::

---
## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian!**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn:
✔ **Tự động hóa hỗ trợ khách hàng** mà không cần code.
✔ **Giảm thời gian phản hồi** từ 5 phút xuống 0 giây.
✔ **Tăng trải nghiệm khách hàng** với AI nhớ lại lịch sử.

**Bước đầu tiên:**
1. **Đăng ký tài khoản** WAMM, Pinecone, Google AI, OpenAI (tất cả miễn phí).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với tin nhắn mẫu** và **bật Active**.

**🚀 Hãy bắt đầu ngay!** Nếu có vấn đề, để lại comment bên dưới hoặc liên hệ với **Adrian (Founder @RoboMarketing)** qua [LinkedIn](https://www.linkedin.com/in/adrianrobomarketing/).

---
**💡 Lưu ý cuối cùng:**
- **Không dùng n8n.cloud** (nên self-hosted để bảo mật).
- **Cập nhật API Key** nếu hết hạn.
- **Duy trì bộ kiến thức** để AI trả lời chính xác.