---
title: "🤖 Tự Động Hóa Chat AI với Dữ Liệu HubSpot: Tìm Hiểu Khách Hàng & Giao Dịch Mới Nhất (Không Cần Code)"
description: "Workflow này tự động hóa việc chat AI với dữ liệu HubSpot để tổng hợp thông tin khách hàng và giao dịch mới nhất, giúp các sếp tiết kiệm thời gian lên đến 80% trong việc phân tích và tương tác với khách hàng."
slug: "tieu-dong-hoa-chat-ai-hubspot"
tags: [n8n, automation, crm, ai-summarization, hubspot, google-gemini]
keywords: [n8n workflow hubspot, tự động hóa chat ai, tổng hợp dữ liệu hubspot, chatbot crm, gemini api, tự động hóa bán hàng]
---

# 🤖 **Tự Động Hóa Chat AI với Dữ Liệu HubSpot: Tìm Hiểu Khách Hàng & Giao Dịch Mới Nhất**

### **🚨 Nỗi Đau Của Các Sếp Trong CRM**
Các sếp thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm thủ công** thông tin khách hàng và giao dịch trong HubSpot.
- **Tổng hợp dữ liệu** từ nhiều nguồn khác nhau để đưa ra quyết định bán hàng.
- **Trả lời khách hàng** một cách không đồng bộ, dẫn đến mất thời gian và cơ hội.

Workflow này **giải quyết tất cả** bằng cách **tự động hóa chat AI** với dữ liệu HubSpot, giúp các sếp:
✅ **Tìm kiếm khách hàng và giao dịch** chỉ bằng một câu lệnh.
✅ **Tổng hợp thông tin chi tiết** từ AI (Google Gemini) một cách nhanh chóng.
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công trong HubSpot.
- **Tương tác AI 24/7**: AI trả lời nhanh chóng với dữ liệu chính xác từ HubSpot.
- **Tổng hợp thông tin chi tiết**: AI tổng hợp thông tin khách hàng và giao dịch một cách logic.
- **Cải thiện quyết định bán hàng**: Dữ liệu được tổng hợp tự động, giúp các sếp đưa ra quyết định nhanh chóng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản HubSpot** (đã cấu hình OAuth2 API).
2. **API Key của Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
3. **n8n Self-hosted** (để chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8971](https://n8n.io/workflows/8971).
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** và chọn file JSON đã tải.
  - Hoặc **copy/paste** JSON từ file vào **Import Workflow** và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: When chat message received (chatTrigger)**
- **Chức năng**: Khởi động workflow khi nhận được tin nhắn từ người dùng.
- **Lưu ý**:
  - Đảm bảo **credentials** của `chatTrigger` được cấu hình đúng (nếu sử dụng API Webhook).
  - Nếu muốn test, các sếp có thể **gửi tin nhắn qua Slack/Telegram** (cần kết nối thêm node tương ứng).

##### **🔹 Node 2: AI Agent (agent)**
- **Chức năng**: Quản lý logic chat với AI.
- **Lưu ý**:
  - Node này **không cần cấu hình thêm**, chỉ cần kết nối với node `Google Gemini Chat Model`.

##### **🔹 Node 3: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Chức năng**: Sử dụng AI Gemini để trả lời tin nhắn.
- **Lưu ý**:
  - **Cần cấu hình credentials**:
    - Tạo **Google Palm API** trong n8n:
      - **API Key**: Điền từ [Google AI Studio](https://makersuite.google.com/).
      - **Model**: Chọn `gemini-pro` (hoặc phiên bản khác nếu có).
    - **Prompt mặc định**:
      ```plaintext
      You are an AI assistant that can search and summarize data from HubSpot CRM.
      When a user asks about a contact or deal, search HubSpot for the latest information and provide a summary.
      ```
  - **Test API Key**:
    - Để đảm bảo API hoạt động, các sếp có thể **gửi một tin nhắn test** như:
      ```plaintext
      "Tìm thông tin về khách hàng tên John Doe"
      ```

##### **🔹 Node 4 & 5: Search contacts & deals in HubSpot (hubspotTool)**
- **Chức năng**: Tìm kiếm khách hàng và giao dịch trong HubSpot.
- **Lưu ý**:
  - **Cần cấu hình credentials HubSpot OAuth2**:
    - Tạo **HubSpot OAuth2 API** trong n8n:
      - **Client ID & Secret**: Lấy từ [HubSpot Developer Portal](https://developers.hubspot.com/).
      - **Scopes**: Chọn `contacts`, `deals`, `crm.objects`.
    - **Test kết nối**:
      - Node này sẽ tự động lấy dữ liệu khi AI yêu cầu.
      - Nếu gặp lỗi, kiểm tra **permissions** của OAuth2.

##### **🔹 Node 6: Simple Memory (memoryBufferWindow)**
- **Chức năng**: Lưu trữ lịch sử chat để AI nhớ các thông tin trước đó.
- **Lưu ý**:
  - **Không cần cấu hình**, node này tự động lưu trữ dữ liệu trong **10 tin nhắn gần nhất**.
  - Nếu muốn lưu lâu hơn, các sếp có thể **cấu hình lại window size** (ví dụ: 20 tin nhắn).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một tin nhắn test như:
    ```plaintext
    "Hãy tìm thông tin về giao dịch mới nhất của khách hàng tên Alice Smith"
    ```
  - Kiểm tra **output** của AI có trả lời chính xác không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và **đặt chế độ Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để chat với AI qua kênh công việc.
2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử chat và dữ liệu tìm kiếm.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp dữ liệu HubSpot hàng tuần.
4. **Tối Ưu Prompt AI**:
   - Cập nhật **prompt** của Gemini để AI trả lời **cụ thể hơn** (ví dụ: yêu cầu AI liệt kê các giao dịch đang mở).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **quyết định chiến lược** thay vì làm việc thủ công trong CRM. **Chỉ cần một lần setup**, AI sẽ tự động **tìm kiếm, tổng hợp và trả lời** mọi câu hỏi về khách hàng và giao dịch.

👉 **Hãy thử ngay** và **tự động hóa CRM của mình** với n8n!

---
:::note[CHÚ Ý]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow hoạt động **24/7** mà không bị giới hạn.
- **Nếu gặp lỗi API**, kiểm tra lại **credentials** và **permissions** của HubSpot & Google.
:::