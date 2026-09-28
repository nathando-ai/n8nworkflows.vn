---
title: "🚀 Tự Động Hóa Thông Báo Khách Hàng Đến Viếng: Từ Google Calendar → Slack & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp doanh nghiệp gửi thông báo khách hàng đến viếng đến các thành viên liên quan qua Slack và ghi chép chi tiết vào Google Sheets, tiết kiệm thời gian và tránh bỏ sót thông tin quan trọng. Hoạt động 24/7, cá nhân hóa và chính xác 100%."
slug: "tieu-dong-hoa-thong-bao-khach-hang-den-vieng"
tags: [n8n, automation, google-calendar, google-sheets, slack-integration, no-code, business-automation]
keywords: [tự động hóa n8n, thông báo khách hàng đến viếng, google calendar slack, tự động hóa doanh nghiệp, lưu trữ lịch sử khách hàng, giảm thời gian thủ công]
---

# 🚀 **Tự Động Hóa Thông Báo Khách Hàng Đến Viếng: Từ Google Calendar → Slack & Google Sheets**

### **Giải pháp hoàn hảo cho các doanh nghiệp muốn:**
- **Không còn quên thông báo khách hàng đến viếng** (tự động gửi 24h trước và 1h trước).
- **Tiết kiệm thời gian** của bộ phận reception, sales và quản lý (không cần copy-paste thủ công).
- **Cải thiện trải nghiệm khách hàng** với chuẩn bị sẵn sàng từ phòng họp, tài liệu đến nhân viên tiếp đón.
- **Ghi chép toàn bộ lịch sử** vào Google Sheets để theo dõi và báo cáo định kỳ.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần can thiệp thủ công, hoạt động 24/7 từ 6h sáng đến 6h chiều.
- **Cá nhân hóa thông báo**: Gửi thông tin chi tiết (thời gian, khách hàng, người liên hệ) đến từng thành viên liên quan.
- **Ghi chép trung thực**: Tất cả thông báo được lưu vào Google Sheets với thời gian và trạng thái (đã gửi/đã chuẩn bị).
- **Tăng cường chuyên nghiệp**: Khách hàng nhận được sự chuẩn bị chu đáo, nâng cao hình ảnh doanh nghiệp.
- **Dễ dàng mở rộng**: Thêm Slack, Email, hoặc QR check-in sau này chỉ với vài bước cấu hình.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google**:
   - **Google Calendar OAuth2 API**: Client ID và Client Secret (cài đặt tại [Google Cloud Console](https://console.cloud.google.com/)).
   - **Google Sheets OAuth2 API**: Client ID và Client Secret (dùng để ghi chép lịch sử).
   - **Google Drive OAuth2 API**: Client ID và Client Secret (nếu có file ảnh liên quan đến khách hàng).
   - **Google Sheet mẫu**: Tạo 2 sheet:
     - `Odoo Calendar Event notifications` (để lưu thông tin đã gửi).
     - `Member Slack` (để lưu danh sách thành viên liên quan và email của họ).

2. **Slack App**:
   - Tạo **Slack App** và lấy **Bot User OAuth Token** (cài đặt tại [Slack API](https://api.slack.com/apps)).
   - Chọn **Permissions**: `chat:write`, `files:write`, `users:read.email`.

3. **n8n Self-hosted**:
   - Cài đặt n8n trên **VPS** để workflow hoạt động liên tục (không phụ thuộc vào phiên làm việc).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

4. **Thời gian hoạt động**:
   - Workflow chạy tự động **mỗi giờ từ 6h sáng đến 6h chiều** (thời gian Việt Nam).
   - **Lưu ý**: Nếu khách hàng đến vào buổi tối, workflow sẽ gửi thông báo vào ngày hôm sau.
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải file JSON của workflow từ [n8n.io/workflows/13111](https://n8n.io/workflows/13111).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create new workflow**.
2. Chọn **Import from JSON** → Dán toàn bộ nội dung JSON từ [đây](https://n8n.io/workflows/13111) (hoặc file tải xuống).
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **phức tạp** với 55 node, nhưng chỉ cần chú ý đến các bước sau:

#### **🔹 Cấu hình Credentials (Bắt buộc)**
| Node Type               | Credentials cần thiết                          | Hướng dẫn cấu hình                          |
|-------------------------|-----------------------------------------------|---------------------------------------------|
| **Google Calendar**     | `googleCalendarOAuth2Api`                      | Thêm OAuth2 Credential trong n8n → Chọn **Google Calendar API**. |
| **Google Sheets**       | `googleSheetsOAuth2Api`                       | Thêm OAuth2 Credential → Chọn **Google Sheets API**. |
| **Google Drive**        | `googleDriveOAuth2Api`                        | Thêm OAuth2 Credential → Chọn **Google Drive API**. |
| **HTTP Request (Slack)**| `httpQueryAuth` và `httpBearerAuth`           | Thêm **Custom Auth** trong n8n → Điền `Bearer <Slack Token>`. |

#### **🔹 Cấu hình Google Sheets**
1. **Sheet `Odoo Calendar Event notifications`**:
   - Cột cần có: `Event ID`, `Customer Name`, `Customer Company`, `Time`, `Status` (đã gửi/đã chuẩn bị).
   - **Lưu ý**: Node `Step 8`, `Step 24`, `Step 42` sẽ đọc từ sheet này để tránh gửi lại thông báo.

2. **Sheet `Member Slack`**:
   - Cột cần có: `Member Name`, `Slack ID`, `Email`, `Role` (vd: Reception, Sales, IT).
   - **Lưu ý**: Node `Step 9` sẽ đọc danh sách này để gửi thông báo đến đúng người.

#### **🔹 Cấu hình Slack**
1. Trong **Step 31, Step 49, Step 52** (gọi API Slack):
   - Thay đổi `channel_id` thành **public channel** của doanh nghiệp (vd: `#customer-visits`).
   - Thay đổi `username` thành tên bot (vd: `CustomerVisitBot`).
   - **Lưu ý**: Node `Step 33`, `Step 51` sẽ gửi file ảnh (nếu có) lên Slack.

#### **🔹 Cấu hình thời gian**
- Workflow chạy **mỗi giờ từ 6h sáng đến 6h chiều** (node `Step 1`).
- **Lưu ý**:
  - Nếu khách hàng đến **buổi tối**, workflow sẽ gửi thông báo vào **ngày hôm sau**.
  - Node `Step 27` và `Step 45` kiểm tra thời gian hiện tại để quyết định gửi thông báo công khai (>= 8h sáng).

#### **🔹 Cấu hình nội dung thông báo**
- **Thông báo 24h trước** (Step 16):
  ```json
  {
    "text": "🚨 **Khách hàng đến viếng sắp đến!** 🚨",
    "attachments": [
      {
        "title": "Thông tin khách hàng",
        "title_link": "https://calendar.google.com/...",
        "text": `*Khách hàng*: {{ $node["Step 4"].json["summary"] }}\n*Công ty*: {{ $node["Step 4"].json["description"] }}\n*Thời gian*: {{ $node["Step 4"].json["start"].dateTime }}`,
        "fields": [
          { "title": "Người liên hệ", "value": "{{ $node["Step 13"].json["partner_email"] }}", "short": true }
        ]
      }
    ]
  }
  ```
- **Thông báo 1h trước** (Step 33/51):
  - Gửi **file ảnh** (nếu có) của khách hàng (tải từ Google Drive).
  - Nội dung: `*Xin chào! Khách hàng {{ $node["Step 4"].json["summary"] }} sẽ đến trong 1h. Vui lòng chuẩn bị phòng họp và tài liệu.*`

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Chọn **Step 1** (scheduleTrigger) → Nhấn **Run**.
   - Kiểm tra **Google Sheets** và **Slack** để xác nhận thông báo được gửi đúng.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CẬP NHẬT & MỞ RỘNG]
1. **Thêm Email Notification**:
   - Thay thế node `Step 16` bằng **n8n-nodes-base.email** để gửi email thay vì Slack.
   - Cấu hình SMTP hoặc sử dụng dịch vụ như SendGrid.

2. **QR Code Check-in**:
   - Thêm node **Google Drive** để tạo QR code cho khách hàng scan khi đến.
   - Gửi QR code cùng thông báo 24h trước.

3. **Báo cáo định kỳ**:
   - Thêm node **Google Sheets** để tạo **báo cáo hàng tháng** về số lượng khách hàng đến viếng.
   - Sử dụng **n8n-nodes-base.pivot** để tổng hợp dữ liệu.

4. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** mới để ghi **log hoạt động** (vd: thời gian gửi, trạng thái thành công/thất bại).

5. **Tích hợp với Odoo**:
   - Nếu doanh nghiệp sử dụng Odoo, thay thế Google Calendar bằng **Odoo Calendar API** để đồng bộ hóa tự động.

6. **Thông báo nhắc nhở**:
   - Thêm node **n8n-nodes-base.if** để gửi **thông báo nhắc nhở** 30 phút trước khi khách hàng đến.
:::

---
## 📌 **Kết luận**
Workflow này **giải quyết triệt để** vấn đề quên thông báo khách hàng đến viếng, giúp doanh nghiệp:
✅ **Tiết kiệm thời gian** của bộ phận hành chính và sales.
✅ **Cải thiện trải nghiệm khách hàng** với chuẩn bị chu đáo.
✅ **Ghi chép toàn bộ lịch sử** để báo cáo và phân tích sau này.

**Bắt đầu ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình **Google Calendar, Sheets, Slack** theo hướng dẫn.
3. **Bật Active** và để workflow làm việc tự động!

**Cần hỗ trợ thêm?**
- Liên hệ **BHSoft** qua [LinkedIn](https://www.linkedin.com/company/bac-ha-software/) hoặc [Website](https://bachasoftware.com/bhsoft-contacts).
- **Không cần code**, chỉ cần n8n và một chút cấu hình!

---
:::note[CHÚ Ý]
- Workflow **không hỗ trợ gửi thông báo sau 6h chiều** (do cấu hình scheduleTrigger).
- Nếu cần gửi thông báo vào buổi tối, hãy mở rộng **scheduleTrigger** để chạy cả ban đêm.
- **Backup Google Sheets** định kỳ để tránh mất dữ liệu.
:::

---
**💡 Mẹo cuối**: Nếu doanh nghiệp có nhiều khách hàng quốc tế, hãy thêm **node `n8n-nodes-base.dateTime`** để chuyển đổi thời gian theo múi giờ của khách hàng!