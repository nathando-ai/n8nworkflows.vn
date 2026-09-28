---
title: "💰 Tự Động Hóa Quá Trình Yêu Cầu → Phiếu Giá (Request-to-Quote) Với AI, Google Sheets & PDF Tự Động - Không Cần Code"
description: "Giải pháp tự động hóa hoàn toàn cho doanh nghiệp chuyển đổi yêu cầu khách hàng thành phiếu giá chuyên nghiệp, cá nhân hóa và gửi tự động qua email chỉ trong vài giây. Tiết kiệm thời gian lên đến 80% cho bộ phận CRM và marketing."
slug: "tu-dong-hoa-request-to-quote-voi-openai-google-sheets-craftmypdf"
tags: [n8n, automation, crm, ai-chatbot, google-sheets, pdf-automation, openai, no-code]
keywords: [tự động hóa request to quote, n8n workflow crm, tạo phiếu giá tự động, ai chatbot cho doanh nghiệp, craftmypdf n8n, google sheets automation]
---

# 🚀 **Tự Động Hóa Quá Trình Yêu Cầu → Phiếu Giá (Request-to-Quote) Với AI, Google Sheets & PDF Tự Động**

### **📌 Nỗi Đau Của Các Sếp CRM & Marketing**
Hàng ngày, bộ phận CRM của các sếp phải:
- **Nhận hàng chục yêu cầu phiếu giá** qua email, form website hoặc chatbot.
- **Tìm kiếm thủ công** thông tin sản phẩm trên Google Sheets hoặc Excel.
- **Tạo phiếu giá** từ đầu, sao chép nội dung, tính toán giá trị, và đảm bảo tính chuyên nghiệp.
- **Gửi phiếu giá** lại cho khách hàng, đôi khi phải sửa lại nhiều lần vì thiếu thông tin.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại, trong khi khách hàng phải chờ đợi lâu để nhận phản hồi.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong quá trình tạo phiếu giá: AI tự động tra cứu sản phẩm, tính toán giá trị, và tạo phiếu giá chuyên nghiệp.
- **Cá nhân hóa hoàn toàn**: Phiếu giá được tự động điền thông tin khách hàng, yêu cầu cụ thể, và logo doanh nghiệp.
- **Hoạt động 24/7**: Khách hàng có thể yêu cầu phiếu giá bất kỳ lúc nào qua form website, chatbot, hoặc email, và nhận phản hồi ngay lập tức.
- **Chất lượng cao**: Phiếu giá được thiết kế chuyên nghiệp với CraftMyPDF, không còn lo lắng về lỗi định dạng.
- **Dữ liệu thống kê**: Tất cả yêu cầu và phiếu giá được lưu trữ trên Google Sheets, giúp phân tích xu hướng và cải thiện dịch vụ.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets có tên **"Products"** (cấu trúc gồm các cột: `Product Name`, `Description`, `Price`, `SKU`, `Category`).
   - **Chia sẻ quyền truy cập** cho n8n với vai trò "Sửa" (để AI có thể tra cứu sản phẩm).
   - **Mã API Google Sheets**: Tạo tại [Google Cloud Console](https://console.cloud.google.com/) và cấp quyền cho n8n.

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** để sử dụng mô hình AI (ví dụ: `gpt-4` hoặc `gpt-3.5-turbo`).

3. **Tài khoản CraftMyPDF**:
   - Đăng ký tại [CraftMyPDF](https://craftmypdf.com/) và lấy **API Key** để tạo PDF tự động.

4. **Tài khoản Email (SMTP)**:
   - Cấu hình SMTP cho n8n để gửi email phiếu giá (ví dụ: Gmail, SendGrid, hoặc SMTP của nhà cung cấp hosting).

5. **Form Yêu Cầu Phiếu Giá**:
   - Một form trên website (có thể là Typeform, Google Form, hoặc form tùy chỉnh) để khách hàng nhập thông tin yêu cầu.
   - **URL Webhook** của n8n (sẽ được tạo tự động khi import workflow).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/8239](https://n8n.io/workflows/8239) hoặc tải file JSON từ link này.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON đã tải.
- **Bước 3**: Chọn **"Import"** để workflow được tạo thành công.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **7 node** quan trọng, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Form: Request a Quote (n8n-nodes-base.formTrigger)**
- **Cấu hình**:
  - Chọn **"Webhook"** như trigger.
  - **URL Webhook**: Sẽ được tự động tạo khi import. **Chia sẻ URL này với form website** của doanh nghiệp để khách hàng gửi yêu cầu.
  - **Headers**: Đảm bảo form gửi dữ liệu dưới dạng `JSON` (thường là `Content-Type: application/json`).

##### **🔹 Node 2: Google Sheets: Products (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn hoặc tạo mới với **Google Sheets API Key** và **File ID** của bảng `Products`.
  - **Operation**: Chọn **"Read"** để AI có thể tra cứu sản phẩm.
  - **Query**: Điền `SELECT * FROM [Sheet1]` (đảm bảo tên sheet chính xác).

##### **🔹 Node 3: LLM: Select & Quote (JSON only) (@n8n/n8n-nodes-langchain.openAi)**
- **Cấu hình**:
  - **API Key**: Điền **API Key OpenAI** từ tài khoản của bạn.
  - **Model**: Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tùy budget).
  - **Prompt**: Sử dụng **template mặc định** trong workflow (có thể tùy chỉnh để phù hợp với ngành nghề):
     ```json
     {
       "instruction": "Tạo một phiếu giá chi tiết cho yêu cầu sau:\n\nYêu cầu khách hàng: {{$json["request"]}}\n\nDanh sách sản phẩm:\n{{$json["products"]}}\n\nYêu cầu:\n1. Liệt kê sản phẩm phù hợp với yêu cầu.\n2. Tính toán giá trị tổng cộng (bao gồm VAT nếu có).\n3. Đề xuất sản phẩm bổ sung nếu cần.\n4. Trả về kết quả dưới dạng JSON với cấu trúc:\n   {\n     \"products\": [\n       {\n         \"name\": \"\",\n         \"description\": \"\",\n         \"price\": 0,\n         \"quantity\": 1,\n         \"total\": 0\n       }\n     ],\n     \"total_amount\": 0,\n     \"notes\": \"\"\n   }"
     }
     ```
  - **Input**: Chọn `$node["Form: Request a Quote"]["json"]` (dữ liệu từ form).

##### **🔹 Node 4: Code: Map for CraftMyPDF (n8n-nodes-base.code)**
- **Cấu hình**:
  - **Script**: Sử dụng **template mặc định** trong workflow để chuyển đổi JSON từ AI sang định dạng phù hợp cho CraftMyPDF.
  - **Output**: Đảm bảo trả về một đối tượng JSON có cấu trúc:
     ```json
     {
       "title": "Phiếu Giá - {{$json["customer_name"]}}",
       "products": [
         {
           "name": "{{$json["products"][0]["name"]}}",
           "description": "{{$json["products"][0]["description"]}}",
           "price": "{{$json["products"][0]["price"]}}",
           "quantity": "{{$json["products"][0]["quantity"]}}",
           "total": "{{$json["products"][0]["total"]}}"
         }
       ],
       "total_amount": "{{$json["total_amount"]}}",
       "customer_name": "{{$json["customer_name"]}}",
       "customer_email": "{{$json["customer_email"]}}"
     }
     ```

##### **🔹 Node 5: Create a PDF (n8n-nodes-craftmypdf.craftMyPdf)**
- **Cấu hình**:
  - **API Key**: Điền **API Key CraftMyPDF**.
  - **Template**: Chọn hoặc tạo mới một **template PDF** với các phần tử:
    - **Title**: `{{title}}`
    - **Products Table**: Dùng loop để hiển thị danh sách sản phẩm.
    - **Total Amount**: `{{total_amount}}`
    - **Customer Info**: `{{customer_name}}` và `{{customer_email}}`.
  - **Input**: Chọn `$node["Code: Map for CraftMyPDF"]["json"]`.

##### **🔹 Node 6: Get PDF File (n8n-nodes-base.httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: Điền **URL download file PDF** từ CraftMyPDF (sẽ được trả về sau khi tạo PDF).
  - **Headers**: Thêm `Authorization: Bearer {{$node["Create a PDF"]["json"]["token"]}}` (nếu yêu cầu).

##### **🔹 Node 7: Email: Send Quote (n8n-nodes-base.emailSend)**
- **Cấu hình**:
  - **Credentials**: Chọn SMTP đã cấu hình (ví dụ: Gmail).
  - **To**: `{{$json["customer_email"]}}`
  - **Subject**: `Phiếu Giá - {{$json["customer_name"]}}`
  - **Body**: Thêm **đính kèm PDF** từ node trước và nội dung:
     ```html
     <p>Chào {{$json["customer_name"]}},</p>
     <p>Phiếu giá của bạn đã được tạo thành công. Vui lòng xem dưới đây:</p>
     <p><a href="[LINK DOWNLOAD PDF]">Tải phiếu giá</a></p>
     <p>Nếu có thắc mắc, hãy liên hệ với chúng tôi qua email hoặc số điện thoại.</p>
     ```
  - **Attachments**: Chọn file PDF từ node `Get PDF File`.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi phiếu giá được tạo thành công.
   - Ví dụ: Khi workflow hoàn thành, gửi tin nhắn Slack:
     ```json
     {
       "text": "Phiếu giá đã được tạo cho khách hàng: {{$json["customer_name"]}}",
       "attachments": [
         {
           "title": "Phiếu Giá",
           "text": "Tải tại: [LINK PDF]",
           "mrkdwn_in": ["text"]
         }
       ]
     }
     ```

2. **Lưu Log & Dữ Liệu**:
   - Thêm node **Google Sheets (Write)** sau node `Email: Send Quote` để lưu tất cả yêu cầu và phiếu giá vào một sheet mới (ví dụ: `Quotes_Log`).
   - Cấu trúc sheet:
     | Customer Name | Email | Date | Status | PDF Link |
     |---------------|-------|------|--------|----------|

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi báo cáo tổng hợp phiếu giá cho bộ phận quản lý.
   - Ví dụ: Tạo một email tổng hợp tất cả yêu cầu trong tuần và gửi cho CEO.

4. **Tùy Chỉnh Template PDF**:
   - Tạo nhiều **template PDF** khác nhau cho từng ngành nghề (ví dụ: template cho dịch vụ IT khác với template cho sản phẩm vật lý).
   - Sử dụng **dynamic variables** trong CraftMyPDF để thay đổi logo, màu sắc, hoặc nội dung tùy theo khách hàng.

5. **Xử Lý Lỗi & Thông Báo**:
   - Thêm node **Sticky Note** để ghi chú lỗi (ví dụ: nếu AI không trả về kết quả JSON hợp lệ).
   - Kết hợp với **Slack Alert** để thông báo khi workflow gặp vấn đề.

---
### **📌 Kết Luận**
Workflow **Automated Request-to-Quote** này là **giải pháp hoàn hảo** để các sếp CRM và marketing **tự động hóa hoàn toàn** quá trình tạo phiếu giá, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng. Với sự hỗ trợ của **AI (OpenAI)**, **Google Sheets**, và **CraftMyPDF**, mỗi yêu cầu đều được xử lý nhanh chóng, chuyên nghiệp, và cá nhân hóa.

**🚀 Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Kết nối với form website** của doanh nghiệp.
3. **Bật Active workflow** và bắt đầu tự động hóa!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ thêm?** Hãy để lại bình luận hoặc liên hệ với tác giả [Cong Nguyen](https://n8n.io/workflows/8239) để được tư vấn chi tiết!