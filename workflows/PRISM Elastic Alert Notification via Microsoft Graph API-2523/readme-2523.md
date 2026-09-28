---
title: "🚨 **Tự Động Hóa Thông Báo Cảnh Báo Elastic PRISM qua Microsoft Graph API – Giúp IT/DevOps Không Bị "Chìm" trong Lũ Cảnh Báo"**
description: "Workflow tự động hóa nhận cảnh báo từ Elastic PRISM (Elastic Security) và gửi thông báo ngay lập tức qua email, giúp IT/DevOps phản ứng kịp thời với các sự cố an ninh mà không cần phải kiểm tra thủ công. Giảm thiểu thời gian phản ứng từ giờ xuống phút!"
slug: "tu-dong-hoa-thong-bao-elastic-prism-microsoft-graph-api"
tags: [n8n, automation, it-ops, secops, elastic-prism, microsoft-graph-api, email-notification]
keywords: [n8n workflow elastic security, tự động hóa cảnh báo an ninh, Microsoft Graph API email alert, giảm thời gian phản ứng IT, cảnh báo Elastic PRISM tự động]
---

# 🚨 **Tự Động Hóa Thông Báo Cảnh Báo Elastic PRISM qua Microsoft Graph API – Không Bị "Chìm" trong Lũ Cảnh Báo An Ninh**

### **Nỗi Đau Của Các Sếp IT/DevOps**
Hàng ngày, các sếp IT/DevOps phải đối mặt với **lũ cảnh báo từ Elastic PRISM** (Elastic Security) – từ các sự cố an ninh nhỏ đến các mối đe dọa nghiêm trọng. Nếu không được xử lý kịp thời, những cảnh báo này có thể dẫn đến:
- **Thời gian phản ứng chậm**: Các sếp phải thủ công kiểm tra email, Slack hay dashboard Elastic, mất nhiều giờ để phát hiện và xử lý.
- **Rủi ro an ninh tăng cao**: Các sự cố nhỏ có thể leo thang thành tai nạn lớn nếu không được cảnh báo ngay lập tức.
- **Sự mệt mỏi và sai sót**: Kiểm tra thủ công dễ dẫn đến bỏ sót cảnh báo quan trọng hoặc phản ứng quá muộn.

**Workflow này giải quyết tất cả đó bằng cách:**
✅ **Tự động nhận cảnh báo từ Elastic PRISM** và chuyển đổi thành thông báo email **ngay lập tức**.
✅ **Gửi thông báo qua Microsoft Graph API** (không cần phụ thuộc vào SMTP truyền thống), đảm bảo tính nhất quán và an toàn.
✅ **Chia nhỏ và xử lý từng cảnh báo** để tránh quá tải và đảm bảo không bỏ sót bất kỳ sự kiện nào.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công, giảm thiểu thời gian phản ứng từ **giờ xuống phút**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không phải kiểm tra thủ công hàng ngày, tự động nhận cảnh báo ngay khi xảy ra.
- **Phản ứng nhanh chóng**: Các sự cố an ninh được thông báo ngay lập tức, giảm thiểu rủi ro.
- **Tính nhất quán cao**: Dữ liệu cảnh báo được xử lý theo quy trình tự động, không bị ảnh hưởng bởi sự mệt mỏi của con người.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào giờ làm việc.
- **Tích hợp Microsoft 365**: Sử dụng Microsoft Graph API để gửi email, phù hợp với môi trường doanh nghiệp hiện đại.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Elastic PRISM**:
   - **URL API của Elastic PRISM** (ví dụ: `https://your-elastic-domain.com/api/v1/alerts`).
   - **Token API** hoặc **API Key** để truy cập Elastic PRISM (thường được tạo trong **Elastic Security > API Keys**).
   - **Endpoint cụ thể** để lấy cảnh báo (thường là `/api/v1/alerts` hoặc `/api/v1/incidents`).

2. **Tài khoản Microsoft 365**:
   - **Microsoft Graph API Access Token** (được tạo từ **Azure AD App Registration**).
     - **Client ID** và **Client Secret** (hoặc **Certificate**).
     - **Permissions** cần thiết:
       - `Mail.Send` (để gửi email).
       - `User.Read` (để xác thực người dùng).
   - **Email của người nhận cảnh báo** (có thể là email cá nhân hoặc nhóm).

3. **VPS cho n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo hiệu suất cao).

4. **n8n Workflow Editor**:
   - Tài khoản n8n (cả **n8n.cloud** hay **self-hosted** đều được).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/2523) (nếu có).
- **Hoặc copy toàn bộ JSON** từ [đây](https://n8n.io/workflows/2523) và dán vào **n8n Editor** (trong tab **Import/Export**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **7 node**, nhưng các node quan trọng nhất cần cấu hình cẩn thận:

##### **A. Node "Schedule Trigger" (Động cơ lịch)**
- **Cấu hình**:
  - **Schedule**: Chọn **`*` `*` `*` `*` `*`** (hoặc tùy chỉnh theo nhu cầu, ví dụ: **`0 * * * *`** để chạy mỗi giờ).
  - **Time Zone**: Đặt theo múi giờ của doanh nghiệp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý**:
  - Nếu muốn **gửi cảnh báo ngay khi có sự kiện mới** (không phải theo lịch), thay thế bằng **Webhook** từ Elastic PRISM (xem phần **Mẹo & Gợi Ý Nâng Cao**).

##### **B. Node "Get Elastic Alert" (Lấy Cảnh Báo từ Elastic PRISM)**
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: Điền **endpoint API của Elastic PRISM** (ví dụ: `https://your-elastic-domain.com/api/v1/alerts`).
  - **Headers**:
    - `Authorization`: `Bearer YOUR_ELASTIC_API_TOKEN`.
    - `Content-Type`: `application/json`.
  - **Body**: Trống (nếu không cần tham số).
- **Lưu ý**:
  - Nếu Elastic PRISM yêu cầu **query parameters**, thêm vào **URL** hoặc **Body**.
  - **Test API** trước để đảm bảo trả về dữ liệu cảnh báo.

##### **C. Node "Response is not empty" (Kiểm Tra Dữ Liệu)**
- **Cấu hình**:
  - **Condition**: `$.length > 0` (kiểm tra nếu có cảnh báo mới).
- **Lưu ý**:
  - Nếu Elastic không trả về cảnh báo, workflow sẽ **bỏ qua** và không gửi email (tránh spam).

##### **D. Node "Loop Over Each Alert Items" (Chia Nhóm Cảnh Báo)**
- **Cấu hình**:
  - **Batch Size**: Đặt **1** (để xử lý từng cảnh báo một).
- **Lưu ý**:
  - Nếu Elastic trả về nhiều cảnh báo cùng lúc, node này sẽ **chia nhỏ** và xử lý từng cảnh báo riêng biệt.

##### **E. Node "Send Email Notification" (Gửi Email qua Microsoft Graph API)**
- **Cấu hình**:
  - **Method**: `POST`.
  - **URL**: `https://graph.microsoft.com/v1.0/users/{user-id}/sendMail`.
    - Thay `{user-id}` bằng **ID người dùng** hoặc **group ID** (xem [Microsoft Graph API docs](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0)).
  - **Headers**:
    - `Authorization`: `Bearer YOUR_MICROSOFT_GRAPH_TOKEN`.
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "message": {
        "subject": "🚨 Cảnh Báo An Ninh từ Elastic PRISM",
        "body": {
          "contentType": "HTML",
          "content": "<h2>Cảnh Báo Mới:</h2><p><strong>Tên:</strong> {{ $json["name"] }}</p><p><strong>Mô Tả:</strong> {{ $json["description"] }}</p><p><strong>Thời Gian:</strong> {{ $json["timestamp"] }}</p>"
        },
        "toRecipients": [
          {
            "emailAddress": {
              "address": "email-nhan@doanhnghiep.com"
            }
          }
        ]
      },
      "saveToSentItems": "false"
    }
    ```
    - **Thay `{{ $json["name"] }}`, `{{ $json["description"] }}`, `{{ $json["timestamp"] }}`** bằng các trường dữ liệu thực tế từ Elastic PRISM (xem **Output** của node `Get Elastic Alert`).
- **Lưu ý**:
  - **Lấy `user-id`** từ [Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer).
  - **Test token Microsoft Graph** trước để đảm bảo gửi email thành công.

##### **F. Node "No Operation" (Dừng Vòng Lặp)**
- **Cấu hình**: Không cần thay đổi gì.
- **Lưu ý**:
  - Node này **dừng vòng lặp** sau khi xử lý xong cảnh báo cuối cùng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual test** trên node `Get Elastic Alert` để kiểm tra API trả về dữ liệu như mong đợi.
   - Sau đó, **test email** bằng cách gửi một cảnh báo mẫu.
2. **Bật Active**:
   - Sau khi cấu hình xong, **bật workflow** và **monitor** qua **n8n Dashboard**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**CẬP NHẬT & TỰ ĐỘNG HÓA HƠN**]
1. **Thay thế Schedule Trigger bằng Webhook (Real-time Alerts)**
   - Thay vì chạy theo lịch, các sếp có thể **cấu hình Webhook** từ Elastic PRISM để gửi cảnh báo ngay khi có sự kiện mới.
   - **Cách làm**:
     - Tạo một **Webhook node** trong n8n với URL: `https://your-n8n-domain.com/webhook/your-webhook-id`.
     - Trong Elastic PRISM, cấu hình **Webhook Integration** để gửi cảnh báo đến URL trên.
     - Xóa node `Schedule Trigger` và **kết nối Webhook node** vào node `Get Elastic Alert`.

2. **Lưu Log Cảnh Báo vào Google Sheets/Notion**
   - Thêm node **Google Sheets** hoặc **Notion** sau node `Send Email Notification` để **lưu lịch sử cảnh báo**.
   - **Cấu hình**:
     - **Google Sheets**: Chọn sheet và sheet name, cấu hình headers như `name`, `description`, `timestamp`.
     - **Notion**: Tạo một **database** và cấu hình API Notion.

3. **Gửi Cảnh Báo qua Slack/Telegram**
   - Thêm node **Slack** hoặc **Telegram Bot** để **gửi thông báo ngay lập tức** khi có cảnh báo mới.
   - **Cấu hình**:
     - **Slack**: Thêm node `Slack`, chọn channel và cấu hình message template.
     - **Telegram**: Thêm node `Telegram Bot`, gửi tin nhắn với thông tin cảnh báo.

4. **Phân Loại Cảnh Báo theo Độ Nghiêm Trọng**
   - Sử dụng node **`if`** để **phân loại cảnh báo** (ví dụ: `critical`, `warning`, `info`).
   - **Cấu hình**:
     - Thêm node `if` sau `Loop Over Each Alert Items`.
     - Kiểm tra trường `severity` trong dữ liệu Elastic PRISM.
     - Gửi email khác nhau cho từng mức độ nghiêm trọng (ví dụ: email `critical` có tiêu đề **🚨 CRITICAL ALERT**).

5. **Gửi Email với Attachment (Log File)**
   - Nếu Elastic PRISM có **log file** hoặc **screenshots**, các sếp có thể **gửi kèm** trong email.
   - **Cách làm**:
     - Thêm node **`httpRequest`** để tải log file từ Elastic PRISM.
     - Thêm vào **body email** dưới dạng **attachment**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng các sếp IT/DevOps** khỏi việc phải **kiểm tra thủ công hàng ngày** các cảnh báo từ Elastic PRISM. Bằng cách **tự động hóa gửi email thông báo** qua Microsoft Graph API, các sếp sẽ:
✔ **Phản ứng nhanh chóng** với các sự cố an ninh.
✔ **Giảm thiểu rủi ro** do bỏ sót cảnh báo.
✔ **Tiết kiệm thời gian** để tập trung vào công việc chiến lược.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản Elastic PRISM và Microsoft 365**.
2. **Cài đặt n8n trên VPS** (nếu chưa có).
3. **Import workflow** và **cấu hình** theo hướng dẫn.
4. **Bật workflow** và **monitor** kết quả!

**Nếu có vấn đề**, các sếp có thể tham khảo:
- [Tài liệu Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0).
- [Tài liệu Elastic PRISM API](https://www.elastic.co/guide/en/security/current/api-alerts.html).
- [Community n8n](https://community.n8n.io/).

**Chúc các sếp thành công với tự động hóa an ninh!** 🚀