---
title: "🚀 Tự Động Hóa Thông Báo Hóa Đơn Mới Trên Slack & Gửi Email Tự Động - Giảm 90% Thời Gian Kiểm Tra Email"
description: "Workflow này tự động phát hiện hóa đơn mới trong email IMAP, trích xuất số tiền, và thông báo ngay trên Slack + gửi email cho bộ phận tài chính - hoàn toàn không cần code!"
slug: "tieu-dong-hoa-thong-bao-hoa-don-moi-tren-slack"
tags: [n8n, automation, no-code, finance, email, slack, mindee]
keywords: [n8n workflow hóa đơn, tự động hóa email, thông báo hóa đơn Slack, trích xuất hóa đơn tự động, n8n finance automation]
---

# 🚀 **Tự Động Hóa Thông Báo Hóa Đơn Mới Trên Slack & Gửi Email Tự Động**

### **Nỗi Đau Của Các Sếp: "Tôi phải kiểm tra hàng trăm email hàng ngày để tìm hóa đơn mới và chuyển cho bộ phận tài chính!"**
Hóa đơn là một trong những công việc tốn thời gian nhất trong bộ phận bán hàng và tài chính. Các sếp phải:
- **Lọc thủ công** email trong IMAP/Gmail để tìm hóa đơn mới.
- **Trích xuất số tiền** từ file PDF/đính kèm.
- **Gửi thông báo** cho bộ phận tài chính qua Slack/email.
- **Lo ngại bỏ sót** hóa đơn quan trọng.

**Workflow này giải quyết tất cả!** Nó sẽ:
✅ **Tự động phát hiện** hóa đơn mới trong email IMap.
✅ **Trích xuất số tiền** bằng công nghệ OCR (Mindee).
✅ **Thông báo ngay trên Slack** với thông tin chi tiết.
✅ **Gửi email tự động** cho bộ phận tài chính.
✅ **Lọc hóa đơn lớn (>1000 USD)** để ưu tiên xử lý.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** kiểm tra email hàng ngày.
- **Tránh bỏ sót hóa đơn** nhờ tự động hóa 24/7.
- **Cá nhân hóa thông báo** trên Slack với số tiền và tên khách hàng.
- **Tích hợp hoàn hảo** với bộ phận tài chính bằng email tự động.
- **Không cần code** - chỉ cần cấu hình vài bước đơn giản.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Email IMAP** (để đọc email mới):
   - Thông tin IMAP (server, port, username, password).
   - **Lưu ý**: Nếu dùng Gmail, cần **bật IMAP** và tạo **app password** (nếu 2FA bật).
2. **API Key Mindee** (trích xuất hóa đơn):
   - Đăng ký tại [Mindee](https://mindee.com/) và lấy **API Key**.
3. **Credentials Slack**:
   - **Token Slack API** (tạo từ [Slack API](https://api.slack.com/apps)).
4. **Credentials SMTP** (gửi email tự động):
   - Thông tin SMTP (server, port, username, password).
   - **Gợi ý**: Dùng **Gmail SMTP** hoặc **SendGrid** (miễn phí cho 100 email/ngày).
5. **Email của bộ phận tài chính** (để gửi thông báo).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/1467](https://n8n.io/workflows/1467) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON và paste vào **Create Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Check for new emails (emailReadImap)**
- **Credentials**: Chọn `imap` (đã tạo trước).
- **Folder**: Chọn thư mục email cần theo dõi (ví dụ: "Inbox").
- **Limit**: Đặt `10` (đọc 10 email mới nhất).
- **Test**: Chạy test để đảm bảo kết nối IMAP thành công.

##### **Node 2: If email body contains invoice (if)**
- **Condition**: Đặt `{{ $json.body }}.includes("invoice")` (kiểm tra tiêu đề/nhân vật email có chứa "invoice").
- **Lưu ý**: Nếu email hóa đơn có định dạng khác, cần điều chỉnh regex (ví dụ: `{{ $json.subject.toLowerCase().includes("invoice") }}`).

##### **Node 3: Extract the total amount (mindee)**
- **Credentials**: Chọn `mindeeInvoiceApi`.
- **Resource**: Đặt `invoice` (đã mặc định).
- **File**: Chọn `{{ $node["Check for new emails"].json["attachments"][0]["file"] }}` (trích xuất file đính kèm).
- **Test**: Nếu không trích xuất được, kiểm tra:
  - File đính kèm có phải là PDF?
  - API Key Mindee có đúng không?

##### **Node 4: If Amount > 1000 (if)**
- **Condition**: Đặt `{{ $json.amount > 1000 }}` (lọc hóa đơn >1000 USD).
- **Lưu ý**: Nếu số tiền có đơn vị khác (VND, EUR), cần chuyển đổi (ví dụ: `{{ $json.amount * 23000 }}` cho VND).

##### **Node 5: Send new invoice notification (slack)**
- **Credentials**: Chọn `slackApi`.
- **Channel**: Chọn `#finance` (hoặc channel tương ứng).
- **Message**: Đặt template:
  ```json
  {
    "text": "📄 **New Invoice Detected** 📄",
    "attachments": [
      {
        "title": "Invoice from {{ $json.sender }}",
        "title_link": "https://example.com/invoice/{{ $node["Check for new emails"].json["id"] }}",
        "text": `Amount: **$${{ $json.amount }}**\nDate: {{ $json.date }}`,
        "color": "{{ $json.amount > 1000 ? '#FF0000' : '#00FF00' }}"
      }
    ]
  }
  ```
- **Test**: Gửi thử để kiểm tra Slack thông báo.

##### **Node 6: Send email to finance manager (emailSend)**
- **Credentials**: Chọn `smtp`.
- **To**: Điền email bộ phận tài chính.
- **Subject**: `📄 Invoice Notification: {{ $json.sender }} - ${{ $json.amount }}`
- **Body**: Đặt template:
  ```html
  <p>Xin chào,</p>
  <p>Đã phát hiện hóa đơn mới từ <strong>{{ $json.sender }}</strong> với số tiền <strong>${{ $json.amount }}</strong>.</p>
  <p>Chi tiết:</p>
  <ul>
    <li>Ngày: {{ $json.date }}</li>
    <li>File đính kèm: <a href="{{ $node["Check for new emails"].json["attachments"][0]["url"] }}">Tải xuống</a></li>
  </ul>
  <p>Trân trọng,</p>
  <p>Hệ thống Tự Động Hóa</p>
  ```
- **Test**: Gửi thử email để kiểm tra.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy với email mẫu (đính kèm hóa đơn PDF).
- **Active Workflow**: Bật chế độ **Active** để chạy 24/7.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CẬP NHẬT & MỞ RỘNG]
1. **Thêm Logs**: Sử dụng **node `set`** để lưu lịch sử hóa đơn vào **Google Sheets** hoặc **Airtable**.
   ```json
   {
     "invoiceId": "{{ $node["Check for new emails"].json["id"] }}",
     "amount": "{{ $json.amount }}",
     "date": "{{ $json.date }}",
     "status": "Processed"
   }
   ```
2. **Kết Nối với Trello/Notion**: Sử dụng **node `trello`** để tạo task mới khi hóa đơn >1000 USD.
3. **Gửi Email Định Kỳ**: Sử dụng **node `setInterval`** để gửi báo cáo tổng hợp hóa đơn hàng tháng.
4. **Cảnh Báo Trùng Lặp**: Thêm **node `set`** để kiểm tra hóa đơn đã xử lý trước đó.
5. **Dịch Vụ OCR Tự Do**: Nếu Mindee không phù hợp, thử **node `pytesseract`** (OCR mở nguồn) với **Google Vision API**.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại kiểm tra email hóa đơn. Với **tự động hóa 100% không code**, nó:
✔ **Tiết kiệm 90% thời gian**.
✔ **Tránh bỏ sót hóa đơn**.
✔ **Cung cấp thông báo tức thời** trên Slack.
✔ **Tích hợp hoàn hảo** với bộ phận tài chính.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để chạy 24/7 (đăng ký VPS TinoHost với mã **VPSN8N** để giảm 39%).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với email mẫu** trước khi kích hoạt.

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!**

---
:::note[CHÚ Ý]
- Nếu gặp lỗi **IMAP không kết nối**, kiểm tra **SSL/TLS** và **port** (thường là 993 cho IMAP SSL).
- Đối với **Mindee**, nếu API trả về lỗi, kiểm tra **file đính kèm** có phải là PDF không.
- **Slack Token** phải có quyền `chat:write` và `files:write`.
:::