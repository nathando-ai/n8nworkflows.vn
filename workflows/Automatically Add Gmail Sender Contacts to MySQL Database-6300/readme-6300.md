---
title: "🚀 Tự Động Hóa Thêm Liên Hệ Khách Hàng Từ Gmail Vào Cơ Sở Dữ Liệu MySQL (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp tự động lưu trữ tên và email của người gửi email vào cơ sở dữ liệu MySQL, tiết kiệm thời gian quản lý leads và bảo vệ dữ liệu quan trọng."
slug: "tu-dong-hoa-luu-tru-lien-he-khach-hang-tu-gmail-vao-mysql"
tags: [n8n, automation, lead-generation, mysql, gmail, no-code]
keywords: [n8n workflow gmail mysql, tự động hóa lưu email, lưu trữ leads từ gmail, bảo vệ dữ liệu gmail, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Thêm Liên Hệ Khách Hàng Từ Gmail Vào MySQL (Không Cần Code)**

### **Giải Pháp Cho Các Sếp Bán Hàng, Marketing Và Quản Lý Dữ Liệu**
Có bao giờ các sếp phải mất thời gian thủ công ghi chép tên và email của khách hàng từ hàng trăm email hàng ngày? Hoặc sợ mất dữ liệu quan trọng khi Gmail bị xóa hoặc mất quyền truy cập? **Workflow này sẽ tự động hóa toàn bộ quá trình**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/tuần** ghi chép liên hệ thủ công.
✅ **Bảo vệ dữ liệu** bằng cách sao lưu tự động vào cơ sở dữ liệu MySQL.
✅ **Xây dựng danh sách leads** để gửi email marketing hoặc theo dõi sau.
✅ **Tránh mất dữ liệu** khi Gmail bị xóa hoặc bị khóa.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần ghi chép thủ công, hệ thống làm việc 24/7.
- **Dữ liệu chính xác**: Trích xuất tên và email từ người gửi một cách tự động.
- **Bảo mật cao**: Dữ liệu được lưu trữ trong MySQL, không phụ thuộc vào Gmail.
- **Tích hợp dễ dàng**: Hoàn toàn miễn phí và chỉ cần 3 node cơ bản.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (đã cấp quyền OAuth 2.0 cho n8n).
2. **Cơ sở dữ liệu MySQL** (có thể là MySQL Server, MariaDB hoặc cơ sở dữ liệu cloud như AWS RDS).
3. **Bảng dữ liệu (Table)** trong MySQL với cấu trúc sau:
   - **Cột `name`** (kiểu `VARCHAR`, cho phép giá trị `NULL`).
   - **Cột `email`** (kiểu `VARCHAR`, **đơn nhất - UNIQUE** để tránh trùng lặp).
   - *(Tùy chọn)* Các cột khác như `subject`, `messageId`, `threadId` (nếu muốn lưu thêm thông tin email).
4. **API Key hoặc Credentials** cho:
   - **Gmail OAuth 2.0** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **MySQL** (tên host, tên database, username, password).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste mã JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor** tại [n8n.io](https://n8n.io/).
2. Nhấn **Import Workflow** và chọn file JSON (hoặc paste mã JSON dưới đây).
3. **Mã JSON của workflow**:
   ```json
   {
     "nodes": [
       {
         "parameters": {},
         "name": "Receive Email",
         "type": "n8n-nodes-base.gmailTrigger",
         "credentials": {
           "gmailOAuth2": "gmail-credentials"
         }
       },
       {
         "parameters": {
           "code": "// Extract sender name and email\nconst sender = $input.all()[0].payload.payload.from;\n\n// Split email to get name and address\nconst emailParts = sender.split('<');\nconst name = emailParts[0].trim();\nconst email = emailParts[1].replace('>', '').trim();\n\n// Return data for MySQL node\nreturn {\n  name: name,\n  email: email\n};"
         },
         "name": "Extract Client Name and Email",
         "type": "n8n-nodes-base.code"
       },
       {
         "parameters": {
           "operation": "upsert",
           "table": "contacts", // Thay đổi thành tên bảng của bạn
           "matchColumn": "email", // Cột để so sánh (phải là UNIQUE)
           "valueColumn": "name", // Cột để lưu tên
           "values": {
             "name": "{{$node[\"Extract Client Name and Email\"].json.name}}",
             "email": "{{$node[\"Extract Client Name and Email\"].json.email}}"
           }
         },
         "name": "Insert New Client in MySQL",
         "type": "n8n-nodes-base.mySql",
         "credentials": {
           "mySql": "mysql-credentials"
         }
       }
     ],
     "connections": {
       "gmailTrigger": ["Extract Client Name and Email"],
       "Extract Client Name and Email": ["Insert New Client in MySQL"]
     }
   }
   ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Node Gmail Trigger**
- **Credentials**: Chọn `gmailOAuth2` (đã đăng ký trước đó).
- **Label Filter (tùy chọn)**: Nếu muốn chỉ lấy email có nhãn cụ thể (ví dụ: `label="leads"`), thêm vào `parameters`:
  ```json
  "parameters": {
    "labelIds": ["leads"] // Thay "leads" bằng nhãn của bạn
  }
  ```

##### **B. Cấu Hình Node Code (Trích Xuất Tên & Email)**
- **Mã JavaScript** đã được tối ưu để trích xuất:
  - **Tên người gửi**: Phần trước `<` trong địa chỉ email (ví dụ: `John Doe <john@example.com>` → `John Doe`).
  - **Email**: Phần sau `<` và trước `>`.
- **Lưu ý**: Nếu email không có tên (ví dụ: `noreply@example.com`), node sẽ trả về `null` cho cột `name`.

##### **C. Cấu Hình Node MySQL (Upsert)**
- **Table**: Chọn bảng chứa dữ liệu liên hệ (ví dụ: `contacts`).
- **Match Column**: Chọn cột `email` (phải là `UNIQUE`).
- **Value Column**: Chọn cột `name` để lưu tên người gửi.
- **Test Connection**: Kiểm tra kết nối trước khi kích hoạt workflow.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một email mẫu đến tài khoản Gmail đã kết nối.
   - Kiểm tra bảng MySQL để xác nhận dữ liệu đã được lưu.
2. **Bật Workflow**:
   - Đánh dấu workflow thành **Active**.
   - **Lưu ý**: Workflow sẽ chạy **mỗi phút** để kiểm tra email mới.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐI ƯU TIẾP THỪA]
1. **Lưu Thông Tin Email Chi Tiết**:
   - Mở rộng node MySQL để lưu thêm:
     - **Tiêu đề email** (`subject`).
     - **ID Thread** (`threadId`) để theo dõi cuộc trò chuyện.
     - **Snippet** (nội dung tóm tắt email).
   - Cách làm: Trong node MySQL, nhấn **Add Value** và chọn trường từ node Gmail.

2. **Lọc Email Theo Nhãn (Label)**:
   - Thêm bộ lọc để chỉ lưu email có nhãn cụ thể (ví dụ: `label="potential-client"`).
   - Cấu hình trong node Gmail Trigger:
     ```json
     "parameters": {
       "labelIds": ["potential-client"]
     }
     ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **n8n-nodes-base.email** hoặc **Slack** để báo cáo số lượng leads mới được lưu hàng ngày.
   - Ví dụ: Gửi email tự động vào mỗi sáng với thống kê:
     ```json
     "parameters": {
       "to": ["team@example.com"],
       "subject": "Báo cáo leads mới từ Gmail",
       "html": "Hôm nay đã lưu {{$node[\"Insert New Client in MySQL\"].executions.length}} liên hệ mới!"
     }
     ```

4. **Lưu Log Lịch Sử**:
   - Sử dụng **n8n-nodes-base.telegram** hoặc **n8n-nodes-base.slack** để ghi log mỗi khi có email mới được xử lý.
   - Cách làm: Thêm node Telegram/Slack sau node MySQL với nội dung:
     ```
     Email mới được lưu: {{$node["Extract Client Name and Email"].json.email}}
     Tên: {{$node["Extract Client Name and Email"].json.name}}
     ```

5. **Tích Hợp CRM**:
   - Nếu sử dụng **HubSpot**, **Salesforce** hoặc **Zoho CRM**, thay thế node MySQL bằng node tương ứng (ví dụ: `n8n-nodes-base.hubspot`) để tự động thêm leads vào CRM.
:::

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng, marketing hoặc quản lý dữ liệu muốn tự động hóa việc lưu trữ liên hệ từ Gmail. **Không cần code**, không cần chi phí cao, và **hoạt động 24/7** để bảo vệ dữ liệu của bạn.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy ổn định (👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật workflow** và bắt đầu tự động hóa việc quản lý leads!

---
:::note[CHÚ Ý]
- **Không xóa email** trong Gmail sau khi đã được lưu vào MySQL, vì workflow dựa vào ID email để tránh trùng lặp.
- **Kiểm tra định kỳ** bảng MySQL để đảm bảo dữ liệu không bị lỗi.
- **Nếu gặp lỗi**, kiểm tra log trong node MySQL và node Code.
:::

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Nếu có thắc mắc, hãy để lại bình luận hoặc liên hệ qua [community n8n](https://community.n8n.io/). Chúc các sếp thành công với việc tự động hóa! 💪