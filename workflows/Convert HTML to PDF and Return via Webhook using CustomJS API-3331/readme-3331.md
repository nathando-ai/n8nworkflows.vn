---
title: "🚀 Chuyển HTML sang PDF Tự Động & Trả Về qua Webhook - Giải Pháp Tự Động Hóa Không Code"
description: "Workflow này tự động chuyển đổi nội dung HTML thành PDF và trả kết quả qua Webhook, giúp các sếp tiết kiệm thời gian và tự động hóa quy trình tạo tài liệu. Phù hợp cho hệ thống CRM, email marketing, hoặc báo cáo tự động."
slug: "chuyen-html-sang-pdf-va-tra-ve-qua-webhook"
tags: [n8n, automation, no-code, pdf-generator, webhook, custom-js]
keywords: [n8n workflow chuyển html sang pdf, tự động hóa tạo pdf, webhook trả kết quả pdf, tự động hóa không code, node custom-js]
---

# 🚀 Chuyển HTML sang PDF Tự Động & Trả Về qua Webhook

### **Giải Pháp Tự Động Hóa Không Code cho Các Sếp**
Bạn có bao giờ phải chuyển đổi HTML thành PDF để gửi cho khách hàng, gửi báo cáo định kỳ, hoặc tích hợp vào hệ thống CRM? Thì việc làm thủ công này không chỉ tốn thời gian mà còn dễ gây lỗi và không nhất quán. **Workflow này sẽ tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chuyển đổi thủ công từ HTML sang PDF.
- **Chính xác & nhất quán**: Kết quả PDF luôn đồng nhất với nội dung HTML đầu vào.
- **Tích hợp dễ dàng**: Trả kết quả qua Webhook để sử dụng trong hệ thống tự động hóa khác (Slack, Email, CRM...).
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản CustomJS API**:
   - Đăng ký tại [CustomJS](https://customjs.com/) và lấy **API Key** từ Dashboard.
   - Cấu hình **credentials** trong n8n với tên `customJsApi` và gắn API Key vào.
2. **Webhook URL**:
   - Workflow sẽ sử dụng Webhook với **path**: `060dbacf-0feb-43d4-b4ac-44011a7dd1a4`.
   - Các sếp có thể thay đổi path này trong node **Webhook** nếu cần.
3. **Nội dung HTML đầu vào**:
   - Khi gọi Webhook, phải gửi dữ liệu JSON chứa thẻ `html` với nội dung HTML cần chuyển đổi.
   - Ví dụ:
     ```json
     {
       "html": "<h1>Hello World</h1><p>This is a test PDF.</p>"
     }
     ```

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3331) hoặc copy/paste JSON vào **n8n Editor**.
- Trong n8n Dashboard, chọn **Create Workflow** → **Import from JSON** và dán nội dung JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
##### **Node 1: Webhook**
- **Path**: Giá trị mặc định là `060dbacf-0feb-43d4-b4ac-44011a7dd1a4`. Các sếp có thể thay đổi nếu muốn.
- **Method**: Đặt thành `POST` (phù hợp cho dữ liệu HTML).
- **Response Format**: Chọn `JSON`.

##### **Node 2: HTML to PDF (CustomJS)**
- **Credentials**: Chọn `customJsApi` (đã cấu hình trước ở bước **Yêu cầu cần thiết**).
- **Input Data**: Node này tự động nhận dữ liệu từ **Webhook** và chuyển đổi sang PDF.
- **Output**: Kết quả PDF sẽ được trả về dưới dạng **base64** hoặc **file PDF** tùy thuộc vào cấu hình CustomJS.

##### **Node 3: Respond to Webhook**
- **Response Format**: Chọn `JSON` hoặc `Text` tùy thuộc vào cách bạn muốn trả kết quả.
- **Example Response**:
  ```json
  {
    "status": "success",
    "pdf_url": "data:application/pdf;base64,JVBERi0xLjQK..."
  }
  ```
  - Các sếp có thể tùy chỉnh nội dung trả về để phù hợp với hệ thống của mình.

#### 3. Kích hoạt ⚡️
- **Test Run**:
  - Gửi một request POST đến Webhook với dữ liệu mẫu (ví dụ như trong phần **Yêu cầu cần thiết**).
  - Kiểm tra kết quả trả về trong **Response to Webhook**.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang trạng thái **Active**.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**:
   - Sau khi tạo PDF thành công, gửi thông báo qua Slack/Telegram để các sếp biết kết quả.
   - Sử dụng node **Slack** hoặc **Telegram Bot** để gửi tin nhắn tự động.

2. **Lưu PDF vào Google Drive/Dropbox**:
   - Sử dụng node **Google Drive** hoặc **Dropbox** để lưu PDF vào cloud thay vì chỉ trả về qua Webhook.

3. **Gửi PDF qua Email**:
   - Kết hợp với node **Email** (ví dụ: Gmail, SendGrid) để gửi PDF trực tiếp đến khách hàng hoặc đồng nghiệp.

4. **Log & Monitoring**:
   - Sử dụng node **HTTP Request** để gửi log đến một hệ thống theo dõi (ví dụ: Datadog, Logflare) để theo dõi quá trình chuyển đổi.

5. **Tùy chỉnh Template HTML**:
   - Nếu nội dung HTML là động (ví dụ: lấy từ database), các sếp có thể sử dụng node **Database** (MySQL, PostgreSQL) để lấy dữ liệu trước khi chuyển đổi.

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình chuyển đổi HTML sang PDF mà không cần viết code. Bằng cách tích hợp với Webhook, các sếp có thể dễ dàng kết nối với hệ thống tự động hóa khác (CRM, Email Marketing, Slack...) và tiết kiệm thời gian đáng kể.

**Hãy áp dụng ngay và tự động hóa quy trình của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúng tôi sẽ hỗ trợ các sếp một cách chi tiết nhất!