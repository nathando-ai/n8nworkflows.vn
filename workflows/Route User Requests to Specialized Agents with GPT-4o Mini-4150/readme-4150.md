---
title: "🤖 **Tự Động Hướng Yêu Cầu Khách Hàng Đến Các Nhà Cung Cấp Chuyên Môn Với GPT-4o Mini (N8n + AI)**"
description: "Giải pháp tự động hóa hoàn toàn không-code để phân loại và chuyển tiếp yêu cầu khách hàng đến các chuyên gia phù hợp, sử dụng GPT-4o Mini và n8n. Tiết kiệm 80% thời gian hỗ trợ, giảm sai sót và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoi-dong-yeu-cau-khach-hang-den-chuyen-gia-gpt-4o-mini"
tags: [n8n, automation, ai, support, marketing, no-code, gpt-4o-mini, langchain, openrouter]
keywords: [tự động hóa hỗ trợ khách hàng, n8n workflow, GPT-4o Mini, phân loại yêu cầu, AI chatbot, tự động chuyển tiếp yêu cầu, hỗ trợ khách hàng 24/7]
---

# 🚀 **Tự Động Hướng Yêu Cầu Khách Hàng Đến Các Nhà Cung Cấp Chuyên Môn Với GPT-4o Mini**

### **Giải pháp cho các sếp đang mệt mỏi với công việc hỗ trợ khách hàng thủ công**
Hiện nay, đội ngũ hỗ trợ khách hàng của các doanh nghiệp thường phải mất **giờ đồng hồ** mỗi ngày để phân loại và chuyển tiếp yêu cầu đến các chuyên gia phù hợp. Điều này không chỉ tốn thời gian mà còn dễ gây **sai sót, trễ nải và mất trải nghiệm khách hàng**.

Với **workflow này**, các sếp có thể:
✅ **Tự động phân loại yêu cầu** dựa trên nội dung (ví dụ: yêu cầu lịch hẹn, hỗ trợ tài liệu, nhắc nhở).
✅ **Chuyển tiếp tự động** đến các **nhà cung cấp chuyên môn** (Email Agent, Meeting Agent, Document Agent) mà **không cần can thiệp thủ công**.
✅ **Sử dụng GPT-4o Mini** để xử lý logic phức tạp, tự động hóa lưu trữ lịch sử hội thoại trong **PostgreSQL**, và **sửa lỗi output** tự động.
✅ **Hoạt động 24/7** mà không cần nhân viên trực ca.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **ổn định và hoạt động liên tục**, các sếp nên **self-host n8n** trên VPS riêng để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho AI + PostgreSQL)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** của đội ngũ hỗ trợ (không cần phân loại thủ công).
- **Chuyển tiếp chính xác** yêu cầu đến chuyên gia phù hợp (Email, Lịch hẹn, Tài liệu).
- **Lưu trữ lịch sử hội thoại** trong PostgreSQL để theo dõi và phân tích.
- **Sử dụng GPT-4o Mini** với chi phí thấp hơn so với GPT-4, nhưng hiệu suất vẫn cao.
- **Hoạt động tự động** 24/7, không cần nhân viên trực ca.
- **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng và chuyên nghiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản OpenRouter API** (để kết nối với GPT-4o Mini).
✔ **Tài khoản PostgreSQL** (để lưu trữ lịch sử hội thoại).
✔ **Credentials cho n8n** (để kết nối với các node như `openRouterApi` và `postgres`).
✔ **Webhook URL** (để nhận yêu cầu từ khách hàng).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow này **không cần API key của OpenAI** (sử dụng OpenRouter thay thế).
- **GPT-4o Mini** có chi phí thấp hơn so với GPT-4, nhưng hiệu suất vẫn ổn định cho việc phân loại và xử lý yêu cầu.
- **PostgreSQL** được sử dụng để lưu trữ **bộ nhớ hội thoại** (memory), giúp AI nhớ lại lịch sử trong các cuộc hội thoại sau.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải file JSON** từ [n8n.io/workflows/4150](https://n8n.io/workflows/4150).
2. Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON.
3. **Hoặc**, copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **16 node**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Node Webhook (Nhận yêu cầu từ khách hàng)**
- **Key Parameters**:
  - `path`: `3576c6b9-11a2-4375-b7cb-f58e36557a7b` (không cần thay đổi).
  - `httpMethod`: `POST` (không cần thay đổi).
- **Lưu ý**:
  - Các sếp cần **cấu hình Webhook URL** trong hệ thống của mình (ví dụ: trong Slack, Telegram, hoặc hệ thống CRM).
  - **Test Webhook** bằng cách gửi một yêu cầu mẫu (ví dụ: `{"text": "Tôi muốn hẹn lịch họp với team kỹ thuật"}`).

##### **🔹 Node Switch (Phân loại yêu cầu)**
- **Conditions**:
  - Workflow sẽ **so sánh nội dung yêu cầu** và chuyển đến **nhà cung cấp phù hợp** (Email, Meeting, Document).
  - Các sếp **không cần chỉnh sửa logic** này, nhưng có thể **thêm/loại điều kiện** nếu cần.

##### **🔹 Node GPT-4o Mini (Xử lý logic AI)**
- **Credentials**: `openRouterApi` (cần thiết).
- **Prompt**:
  ```json
  {
    "role": "user",
    "content": "Analyze the user request and categorize it into one of the following: 'email', 'meeting', 'document', or 'reminder'. Return the result in JSON format: {'category': 'email|meeting|document|reminder'}."
  }
  ```
- **Lưu ý**:
  - Nếu **OpenRouter API không hoạt động**, workflow sẽ **ngừng hoạt động**.
  - Các sếp cần **kiểm tra API key** và **cấu hình rate limit** để tránh bị chặn.

##### **🔹 Node PostgreSQL (Lưu trữ lịch sử hội thoại)**
- **Credentials**: `postgres` (cần thiết).
- **Cấu hình**:
  - **Host**: `your-postgres-host`
  - **Port**: `5432`
  - **Database**: `your-database-name`
  - **User**: `your-username`
  - **Password**: `your-password`
- **Lưu ý**:
  - Nếu **PostgreSQL không hoạt động**, AI sẽ **không nhớ lịch sử** và có thể trả lời sai.
  - Các sếp nên **tạo bảng `chat_memory`** trước khi chạy workflow (cấu trúc sẽ tự động tạo nếu chưa có).

##### **🔹 Node Auto-fixing Output Parser & Structured Output Parser**
- **Chức năng**:
  - **Auto-fixing** sẽ **sửa lỗi output** từ AI (ví dụ: nếu AI trả về JSON sai định dạng).
  - **Structured Output Parser** sẽ **chuyển đổi output thành định dạng chuẩn** (JSON).
- **Lưu ý**:
  - Các sếp **không cần chỉnh sửa** node này, nhưng có thể **thêm logic kiểm tra** nếu cần.

##### **🔹 Node ExecuteWorkflow (Chuyển tiếp yêu cầu)**
- **Các node này** sẽ **gọi workflow riêng** cho từng loại yêu cầu:
  - **Email Agent** (xử lý yêu cầu liên quan email).
  - **Meeting Agent** (xử lý yêu cầu lịch hẹn).
  - **Document Agent** (xử lý yêu cầu tài liệu).
  - **Reminder Agent** (nhắc nhở khách hàng).
- **Lưu ý**:
  - Các sếp cần **cấu hình các workflow con** này (nếu chưa có, có thể bỏ qua và chỉ sử dụng **respondToWebhook**).

##### **🔹 Node RespondToWebhook (Trả lời khách hàng)**
- **Chức năng**: Trả lời khách hàng qua Webhook (Slack, Telegram, CRM...).
- **Lưu ý**:
  - Các sếp cần **cấu hình URL trả lời** trong hệ thống của mình.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu mẫu qua Webhook (ví dụ: `{"text": "Tôi cần hỗ trợ về tài liệu hợp đồng"}`).
   - Kiểm tra **output** của workflow (nếu có lỗi, chỉnh sửa node tương ứng).
2. **Bật Active workflow**:
   - Chọn **Active** trong n8n Editor.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì sử dụng Webhook, các sếp có thể **nối workflow với Slack/Telegram** để nhận yêu cầu từ đó.
   - **Cách làm**:
     - Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** để nhận tin nhắn.
     - Chuyển tin nhắn thành **JSON** và gửi qua Webhook.

2. **Lưu log hoạt động**:
   - Sử dụng **node `n8n-nodes-base.httpRequest`** để gửi log hoạt động đến **Google Sheets** hoặc **Notion**.
   - **Cách làm**:
     - Thêm node **HTTP Request** sau **Switch** để lưu dữ liệu phân loại.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow hàng ngày và gửi **báo cáo tổng hợp** về số lượng yêu cầu, loại yêu cầu phổ biến nhất.
   - **Cách làm**:
     - Tạo một **workflow mới** với **Schedule** và **Email Node** để gửi báo cáo.

4. **Cải thiện Prompt cho GPT-4o Mini**:
   - Nếu workflow **phân loại sai**, các sếp có thể **cập nhật Prompt** trong node **`lmChatOpenRouter`** để rõ ràng hơn.
   - **Ví dụ Prompt cải tiến**:
     ```json
     {
       "role": "user",
       "content": "Categorize the following user request into one of these categories: 'email', 'meeting', 'document', or 'reminder'. If the request is about support, use 'email'. If it's about scheduling, use 'meeting'. If it's about documents, use 'document'. If it's a reminder, use 'reminder'. Return ONLY in JSON format: {'category': 'email|meeting|document|reminder'}. Do not add any extra text."
     }
     ```

5. **Sử dụng nhiều mô hình AI**:
   - Nếu **GPT-4o Mini không phù hợp**, các sếp có thể **thay thế bằng mô hình khác** trong OpenRouter (ví dụ: **Mistral, Llama 2**).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn **tự động hóa hỗ trợ khách hàng** mà **không cần code**. Với **GPT-4o Mini** và **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** của đội ngũ hỗ trợ.
✔ **Chuyển tiếp yêu cầu chính xác** đến chuyên gia phù hợp.
✔ **Hoạt động 24/7** mà không cần nhân viên trực ca.
✔ **Cải thiện trải nghiệm khách hàng** với phản hồi nhanh chóng.

**🚀 Hãy áp dụng ngay và tự động hóa đội ngũ hỗ trợ của mình!**
Nếu có **vấn đề khi chạy workflow**, các sếp có thể liên hệ với tác giả **Dhrumil Patel** qua [website](https://sentiimenta-ai.com) hoặc email [founder@sentiimenta-ai.com](mailto:founder@sentiimenta-ai.com).

---
**💡 Bạn có ý tưởng nào khác về cách tối ưu workflow này? Hãy chia sẻ trong phần comment dưới đây!**