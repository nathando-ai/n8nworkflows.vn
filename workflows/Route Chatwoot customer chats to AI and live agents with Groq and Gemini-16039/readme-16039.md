---
title: "🤖 Tự Động Hóa Chat Của Khách Hàng Từ Chatwoot Sang AI + Nhân Viên Trực Tuyến Với Groq & Gemini (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp phân loại, xử lý và trả lời tin nhắn khách hàng từ Chatwoot thông qua AI (Groq/Gemini) và chuyển tiếp cho nhân viên trực tuyến khi cần thiết. Giảm thiểu thời gian phản hồi, cải thiện trải nghiệm khách hàng và tối ưu hóa công việc hỗ trợ 24/7."
slug: "tieu-dong-hoa-chatwoot-sang-ai-va-nhan-vien-truc-tuyen"
tags: [n8n, automation, chatbot, ai-chatbot, chatwoot, groq, google-gemini, pinecone, postgres, support-automation]
keywords: [tự động hóa chatwoot, ai hỗ trợ khách hàng, groq gemini n8n, phân loại tin nhắn khách hàng, chuyển tiếp cho nhân viên trực tuyến, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Chat Của Khách Hàng Từ Chatwoot Sang AI + Nhân Viên Trực Tuyến Với Groq & Gemini**

## **🔥 Giải Pháu Nỗi Đau Của Các Sếp Hỗ Trợ Khách Hàng**
Hiện nay, các doanh nghiệp thường gặp phải những vấn đề sau khi xử lý chat hỗ trợ khách hàng:
- **Thời gian phản hồi chậm**: Nhân viên phải xử lý hàng loạt tin nhắn, dẫn đến trải nghiệm khách hàng không tốt.
- **Không thể hoạt động 24/7**: Khi nhân viên nghỉ hoặc bận rộn, khách hàng phải chờ lâu.
- **Không phân loại tin nhắn hiệu quả**: Một số tin nhắn đơn giản (ví dụ: hỏi giờ làm việc) lại phải chuyển cho nhân viên, làm tốn thời gian.
- **Không lưu trữ lịch sử chat**: Khách hàng phải giải thích lại vấn đề nhiều lần với nhân viên khác.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Phân loại tự động** tin nhắn khách hàng (hỏi đơn giản, phức tạp, cần chuyển tiếp).
✅ **Sử dụng AI (Groq & Gemini)** để trả lời tin nhắn đơn giản một cách nhanh chóng và chính xác.
✅ **Chuyển tiếp tự động** cho nhân viên trực tuyến khi AI không thể giải quyết.
✅ **Lưu trữ lịch sử chat** trong PostgreSQL để nhân viên tiếp nhận có thể tiếp tục từ điểm dừng.
✅ **Gửi thông báo nội bộ** cho đội ngũ hỗ trợ khi cần hỗ trợ thêm.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI xử lý 80% tin nhắn đơn giản, giảm tải cho nhân viên.
- **Phản hồi nhanh chóng**: Khách hàng được trả lời trong giây phút, không phải chờ đợi.
- **Chuyển tiếp thông minh**: Tin nhắn phức tạp tự động chuyển cho nhân viên phù hợp.
- **Hoạt động liên tục**: Hệ thống hoạt động 24/7, không phụ thuộc vào giờ làm việc của nhân viên.
- **Lịch sử chat đầy đủ**: Nhân viên tiếp nhận có thể tiếp tục hỗ trợ mà không cần khách hàng giải thích lại.
- **Cải thiện trải nghiệm khách hàng**: Trả lời nhanh chóng và chính xác làm tăng độ hài lòng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị các tài khoản và thông tin sau:

#### **1. Tài Khoản & API Keys**
| Dịch vụ/API | Mô tả | Yêu cầu |
|-------------|-------|----------|
| **Chatwoot** | Hệ thống chat hỗ trợ khách hàng | API Key và URL Webhook |
| **Groq API** | Mô hình AI Groq (gpt-oss-120b) | API Key từ [Groq](https://groq.com/) |
| **Google Gemini API** | Mô hình AI Gemini (embeddings & chat) | API Key từ [Google AI Studio](https://makersuite.google.com/) |
| **Pinecone** | Vector Store cho Knowledge Base | API Key và tên Index (đã chứa dữ liệu hỗ trợ) |
| **PostgreSQL** | Lưu trữ lịch sử chat | Credentials (host, port, database, username, password) |
| **Gmail** | Gửi thông báo nội bộ cho đội ngũ | OAuth 2.0 Credentials |

#### **2. Cấu Hình Chatwoot**
- **Tạo Webhook** trong Chatwoot với URL:
  ```
  https://[tên-domain-n8n]/webhook/db587fad-cb47-47a0-9c72-bac02c241a67
  ```
- **Chọn trường dữ liệu** trong Chatwoot phải khớp với workflow (ví dụ: `message`, `conversation_id`, `agent_id`, `type`).

#### **3. Knowledge Base (Pinecone)**
- **Tạo Index** trong Pinecone với dữ liệu hỗ trợ đã được embed bằng **Google Gemini Embeddings**.
- **Cấu hình trong workflow** tên Index và API Key Pinecone.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/16039)).
3. Chọn **Create Workflow** và đặt tên (ví dụ: **"Chatwoot AI Support"**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **17 node**, các sếp cần chú ý cấu hình các node quan trọng sau:

##### **🔹 Node "Incoming Chat Webhook" (webhook)**
- **Không cần thay đổi** vì URL đã được cấu hình sẵn trong workflow.
- **Lưu ý**: Đảm bảo **Chatwoot Webhook** được kích hoạt và gửi dữ liệu đúng định dạng.

##### **🔹 Node "Fetch Live Agent Data" (httpRequest)**
- **Cấu hình URL API Chatwoot**:
  ```
  https://[tên-domain-chatwoot]/api/v1/conversations/{conversation_id}/agents
  ```
- **Headers**:
  ```
  Authorization: Bearer [API_KEY_CHATWOOT]
  ```
- **Tham số động**:
  - `{conversation_id}`: Lấy từ tin nhắn khách hàng.

##### **🔹 Node "Use Groq Chat Model" (lmChatGroq)**
- **Chọn mô hình**: `openai/gpt-oss-120b` (đã cấu hình sẵn).
- **Credentials**: Chọn `groqApi` (đã tạo trước khi import).
- **Prompt mặc định**:
  ```json
  {
    "role": "user",
    "content": "You are a customer support AI. Answer the customer's question based on the conversation history and knowledge base. If you don't know the answer, say 'I don't have the information. Please contact our support team.'"
  }
  ```

##### **🔹 Node "Implement Google Gemini Chat Model" (lmChatGoogleGemini)**
- **Credentials**: Chọn `googlePalmApi`.
- **Prompt tương tự Groq**, nhưng sử dụng API Google Gemini.

##### **🔹 Node "Store Chat Memory in Postgres" (memoryPostgresChat)**
- **Credentials**: Chọn `postgres`.
- **Cấu hình connection**:
  ```
  Host: [host-postgres]
  Port: 5432
  Database: [tên-database]
  Username: [username]
  Password: [password]
  ```

##### **🔹 Node "Utilize Pinecone Vector Store" (vectorStorePinecone)**
- **Credentials**: Chọn `pineconeApi`.
- **Tên Index**: Điền tên Index Pinecone đã tạo (ví dụ: `support-knowledge-base`).
- **Lưu ý**: Đảm bảo Index đã chứa dữ liệu embed bằng **Google Gemini Embeddings**.

##### **🔹 Node "Send Internal Team Email" (gmailTool)**
- **Credentials**: Chọn `gmailOAuth2`.
- **Nội dung email mẫu**:
  ```json
  {
    "to": "[email-nhân-viên-trực-tuyến]",
    "subject": "New Chat Requiring Agent Assistance",
    "text": "A customer chat needs your help. Details: {{ $json["conversation_id"] }}"
  }
  ```

##### **🔹 Node "Split AI Messages" (code)**
- **Mã JavaScript mặc định**:
  ```javascript
  // Chia tin nhắn AI thành nhiều phần nhỏ phù hợp với chat
  const messages = $input.all().json.message.split("\n");
  return messages.map(msg => ({ json: { message: msg.trim() } }));
  ```
- **Lưu ý**: Nếu tin nhắn quá dài, node này sẽ chia thành nhiều phần để gửi cho khách hàng.

##### **🔹 Node "Route by Chat Message Type" (switch)**
- **Cấu hình điều kiện**:
  - **Nếu tin nhắn là "question"**: Chuyển sang AI.
  - **Nếu tin nhắn là "escalation"**: Chuyển tiếp cho nhân viên.
  - **Nếu tin nhắn là "irrelevant"**: Bỏ qua.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một tin nhắn test từ Chatwoot (ví dụ: *"Giờ làm việc của cửa hàng là bao giờ?"*).
   - Kiểm tra AI có trả lời đúng không? Nếu không, điều chỉnh **prompt** hoặc **knowledge base**.
2. **Bật Active Workflow**:
   - Nhấn **Active** trên tab Workflow.
   - Kiểm tra **Logs** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ cho quản lý**:
   - Sử dụng **node `gmailTool`** để gửi báo cáo số lượng tin nhắn được AI xử lý vs. chuyển tiếp cho nhân viên.
   - **Mẫu email**:
     ```json
     {
       "to": "quanly@doanhnghiep.com",
       "subject": "Báo cáo AI Support - Ngày {{ $json["date"] }}",
       "text": "AI xử lý: {{ $json["ai_handled"] }} tin nhắn\nChuyển tiếp: {{ $json["escalated"] }} tin nhắn"
     }
     ```

2. **Kết nối với Slack/Telegram**:
   - Thay thế **node `gmailTool`** bằng **node `slack`** hoặc **`telegram`** để thông báo ngay khi có tin nhắn cần chuyển tiếp.
   - **Mẫu thông báo Slack**:
     ```json
     {
       "text": "🚨 New chat escalation: {{ $json["conversation_id"] }}\nCustomer: {{ $json["customer_name"] }}\nMessage: {{ $json["message"] }}"
     }
     ```

3. **Lưu log chi tiết**:
   - Sử dụng **node `stickyNote`** để ghi lại tất cả hoạt động (AI trả lời, chuyển tiếp, lỗi...).
   - **Mẫu log**:
     ```json
     {
       "timestamp": "{{ $now }}",
       "action": "AI_Response",
       "conversation_id": "{{ $json["conversation_id"] }}",
       "response": "{{ $json["ai_response"] }}"
     }
     ```

4. **Cập nhật Knowledge Base tự động**:
   - Sử dụng **node `httpRequest`** để pull dữ liệu mới từ CMS hoặc CRM vào Pinecone định kỳ.

5. **Tích hợp với CRM (HubSpot, Zoho, Salesforce)**:
   - Sử dụng **node `httpRequest`** để cập nhật thông tin khách hàng từ CRM vào workflow khi có tin nhắn mới.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa hỗ trợ khách hàng trên Chatwoot với sự hỗ trợ của AI (Groq & Gemini) và chuyển tiếp thông minh cho nhân viên khi cần thiết. **Không cần code**, chỉ cần cấu hình vài bước là có thể tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và tối ưu hóa công việc hỗ trợ.

**👉 Hãy áp dụng ngay và trải nghiệm sự khác biệt!**
Nếu có vấn đề trong quá trình setup, các sếp có thể tham khảo [cộng đồng n8n](https://community.n8n.io/) hoặc liên hệ với tác giả Mohan Lal Dhanwani qua email.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng**: Đảm bảo **backup dữ liệu** trong PostgreSQL và Pinecone thường xuyên để tránh mất mát khi có sự cố!