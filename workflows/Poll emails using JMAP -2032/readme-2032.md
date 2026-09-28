---
title: "📧 **Tự Động Lấy Tất Cả Email Mới (Unread) Với JMAP – Không Cần Code!**"
description: "Workflow tự động hóa lấy tất cả email chưa đọc từ tài khoản JMAP (Fastmail, ProtonMail,...) chỉ với một nút bấm. Giúp các sếp tiết kiệm thời gian kiểm tra email thủ công, đồng thời giảm tải API bằng cách lưu trữ ID tài khoản và hộp thư."
slug: "tieu-dong-hoa-lay-email-unread-jmap"
tags: [n8n, automation, email, jmap, fastmail, protonmail, no-code]
keywords: [n8n workflow lấy email, tự động hóa email JMAP, lấy email chưa đọc tự động, Fastmail API, ProtonMail tự động hóa]
---

# 🚀 **Lấy Tất Cả Email Mới (Unread) Tự Động Với JMAP – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Khi Kiểm Tra Email Thủ Công**
Hàng ngày, các sếp phải mất **từ 30 phút đến 1 giờ** để:
- Đăng nhập vào email (Fastmail, ProtonMail,...) và kiểm tra hộp thư.
- Lọc email chưa đọc (unread) trong số hàng trăm tin nhắn.
- Xử lý email quan trọng trước khi quên hoặc bị chìm trong luồng thông báo.

**Workflow này giải quyết tất cả!** Với **JMAP** (giao thức email hiện đại của Fastmail), các sếp có thể **lấy tất cả email chưa đọc chỉ với một nút bấm**, đồng thời **tối ưu hiệu suất** bằng cách lưu trữ ID tài khoản và hộp thư để tránh gọi API liên tục.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần đăng nhập thủ công vào email hàng ngày.
✅ **Chính xác 100%**: Lấy tất cả email chưa đọc (unread) mà không bỏ sót.
✅ **Tối ưu API**: Lưu trữ ID tài khoản và hộp thư để giảm tải cho Fastmail/ProtonMail.
✅ **Hoạt động 24/7**: Sử dụng n8n **Self-hosted** để workflow chạy liên tục mà không cần can thiệp.
✅ **Dễ mở rộng**: Kết hợp với **Slack/Telegram** để thông báo email mới hoặc **lưu vào Google Sheets/Notion**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản JMAP hỗ trợ**:
   - Fastmail (khuyến nghị)
   - ProtonMail (cần cấu hình OAuth2 hoặc Bearer Token)
   - Các dịch vụ khác hỗ trợ JMAP (xem [danh sách dịch vụ JMAP](https://jmap.io/implementors/)).

2. **API Token**:
   - **Fastmail**: Tạo token tại [Fastmail Security Tokens](https://www.fastmail.com/settings/security/tokens).
   - **ProtonMail**: Sử dụng OAuth2 hoặc token Bearer (nếu hỗ trợ).

3. **n8n Self-hosted**:
   - Để workflow chạy 24/7 ổn định, các sếp nên **cài n8n trên VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

4. **Credentials trong n8n**:
   - **Header Auth** (để truyền token Bearer):
     - Tên: `Authorization`
     - Giá trị: `Bearer <your_api_token>` (thay `<your_api_token>` bằng token thực tế).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Workflow này có **5 node** và được thiết kế để lấy email chưa đọc từ JMAP. Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/2032](https://n8n.io/workflows/2032) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào **Import Workflow** trong n8n.

:::note[Lưu ý]
Nếu muốn **tối ưu hiệu suất**, các sếp nên **lưu trữ ID tài khoản và hộp thư** (mailbox) sau lần đầu chạy để tránh gọi API mỗi lần.
:::

---

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này có **3 node `httpRequest`** để gọi API JMAP. Các sếp cần **cấu hình chính xác** như sau:

##### **A. Node "Get mailboxes"**
- **Method**: `GET`
- **URL**: `https://mail.yourdomain.com/jmap/mailboxes`
  *(Thay `yourdomain.com` bằng tên miền của tài khoản Fastmail/ProtonMail)*
- **Headers**:
  - `Authorization: Bearer <your_api_token>`
  - `Content-Type: application/json`
- **Lưu ý**:
  - Sau khi chạy lần đầu, **lưu trữ `id` của mailbox** (ví dụ: `inbox`, `sent`) vào **Sticky Note** hoặc **Variable** để sử dụng trong lần chạy sau.

##### **B. Node "Fetch API details"**
- **Method**: `GET`
- **URL**: `https://mail.yourdomain.com/jmap/mailboxes/<mailbox_id>/list`
  *(Thay `<mailbox_id>` bằng ID mailbox từ bước trước, ví dụ: `inbox`)*
- **Headers**: Giống như trên.
- **Lưu ý**:
  - Nếu muốn **tối ưu**, các sếp nên **lưu trữ `id` của mailbox** để không gọi API mỗi lần.

##### **C. Node "Get unread messages"**
- **Method**: `GET`
- **URL**: `https://mail.yourdomain.com/jmap/mail/<mailbox_id>/list`
  *(Thay `<mailbox_id>` bằng ID mailbox từ bước trước)*
- **Headers**: Giống như trên.
- **Query Parameters**:
  - `properties`: `name,unread`
  - `limit`: `100` (hoặc số lượng email muốn lấy)
- **Lưu ý**:
  - Kết quả sẽ là danh sách email **chưa đọc (unread)**.
  - Các sếp có thể **lọc email** bằng `$.json.unread === true`.

##### **D. Node "Format results" (n8n-nodes-base.set)**
- **Function**:
  ```javascript
  return {
    json: {
      emails: $.json.map(email => ({
        id: email.id,
        subject: email.name,
        unread: email.unread,
        // Thêm các trường khác cần thiết
      }))
    }
  };
  ```
- **Lưu ý**:
  - Format lại dữ liệu để dễ đọc và xử lý sau này.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và kiểm tra kết quả trong **Node "Format results"**.
   - Nếu có lỗi, kiểm tra **Headers** và **URL** trong các node `httpRequest`.

2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH MỞ RỘNG THÊM]
1. **Gửi Email Mới Vào Slack/Telegram**:
   - Sử dụng **node `slack`** hoặc **`telegram`** để thông báo khi có email mới.
   - Ví dụ:
     ```json
     {
       "text": `📧 Email mới từ ${$.json.subject} (ID: ${$.json.id})`,
       "attachments": [
         {
           "title": "Chi tiết email",
           "text": `Người gửi: ${$.json.from}`,
           "color": "#36a64f"
         }
       ]
     }
     ```

2. **Lưu Email Vào Google Sheets/Notion**:
   - Sử dụng **node `google-sheets`** hoặc **`notion`** để tự động ghi email mới vào bảng tính hoặc trang Notion.
   - Ví dụ:
     ```json
     {
       "range": "Sheet1!A1:D1",
       "values": [
         ["ID", "Tiêu đề", "Người gửi", "Trạng thái"],
         [$.json.id, $.json.subject, $.json.from, $.json.unread ? "Chưa đọc" : "Đã đọc"]
       ]
     }
     ```

3. **Xóa Email Sau Khi Đọc**:
   - Sử dụng **node `httpRequest`** với method `PATCH` để đánh dấu email là đã đọc (`unread: false`).
   - URL:
     ```
     https://mail.yourdomain.com/jmap/mail/<mailbox_id>/set
     ```
   - Body:
     ```json
     {
       "update": {
         "<email_id>": {
           "unread": false
         }
       }
     }
     ```

4. **Lưu Log Cho Theo Dõi**:
   - Sử dụng **node `stickyNote`** hoặc **`database`** để lưu lịch sử email đã lấy.
   - Ví dụ:
     ```json
     {
       "key": "last_email_id",
       "value": $.json[0].id
     }
     ```
   - Sau đó, trong node `Get unread messages`, thêm điều kiện:
     ```javascript
     if ($.json.length > 0 && $.json[0].id !== $inputLastEmailId) {
       // Lấy email mới
     }
     ```

---

### 📌 **Kết Luận**
Workflow này giúp **các sếp tự động hóa việc lấy email chưa đọc từ JMAP chỉ với một nút bấm**, đồng thời **tối ưu hiệu suất** bằng cách lưu trữ ID tài khoản và hộp thư. **Không cần code**, chỉ cần **cấu hình đúng credentials** và **cài n8n trên VPS** để workflow chạy 24/7.

**Hành động ngay!**
1. **Cài n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình credentials**.
3. **Test run** và **bật Active** để bắt đầu tự động hóa email!

👉 **Bạn có thể mở rộng workflow này thêm nhiều tính năng khác như gửi báo cáo email hàng ngày, tích hợp với CRM, hoặc tự động trả lời email!** Hãy thử và chia sẻ kết quả với chúng tôi. 🚀