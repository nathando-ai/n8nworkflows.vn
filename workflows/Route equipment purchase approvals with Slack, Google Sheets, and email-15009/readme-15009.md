---
title: "🚀 Tự Động Hóa Xác Nhận Mua Sắm Thiết Bị - Từ Slack Đến Email & Google Sheets (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho việc xử lý đơn xin mua thiết bị nội bộ, với tự động xác nhận cho đơn dưới ngưỡng và gửi yêu cầu xác nhận qua Slack cho đơn trên ngưỡng. Tiết kiệm thời gian quản lý lên đến 80% cho các sếp HR/Operations."
slug: "tu-dong-hoa-xac-nhan-mua-sam-thiet-bi-slack-google-sheets"
tags: [n8n, automation, no-code, google-sheets, slack, gmail, purchase-approval]
keywords: [n8n workflow mua sắm, tự động hóa đơn xin mua thiết bị, Slack + Google Sheets, tự động xác nhận đơn hàng, quản lý mua sắm nội bộ]
---

# 🚀 **Tự Động Hóa Xác Nhận Mua Sắm Thiết Bị - Từ Slack Đến Email & Google Sheets**

## **Nỗi Đau Của Các Sếp: Quản Lý Đơn Xin Mua Thiết Bị Làm Thủ Công**
Hàng ngày, các sếp HR, Operations hoặc IT phải:
- **Làm thủ công** xử lý hàng chục đơn xin mua thiết bị, giấy tờ, văn phòng phẩm.
- **Trao đổi qua email** với nhiều người, dễ bị quên hoặc trễ hạn.
- **Không theo dõi được** tình trạng của từng đơn (chờ duyệt, đã duyệt, bị từ chối).
- **Phải nhớ** ngưỡng giá tự động duyệt (ví dụ: dưới 1 triệu đồng tự duyệt, trên phải báo cấp trên).

Kết quả? **Thời gian quản lý tăng gấp 3-5 lần**, hiệu suất làm việc giảm, và dễ xảy ra lỗi nhân sự.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** quản lý đơn xin mua (không cần tra cứu, nhắc nhở, gửi email thủ công).
✅ **Tự động duyệt đơn dưới ngưỡng** (ví dụ: dưới 1 triệu đồng) và thông báo ngay cho bộ phận mua sắm.
✅ **Gửi yêu cầu duyệt tự động** qua Slack DM cho cấp trên đối với đơn trên ngưỡng, **với form phản hồi nhanh** (chấp thuận/từ chối + ghi chú).
✅ **Lưu toàn bộ lịch sử** trong Google Sheets, dễ theo dõi và báo cáo.
✅ **Cá nhân hóa thông báo** (email + Slack) cho từng người dùng, giảm rủi ro nhầm lẫn.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài Khoản & API Keys**:
- **Google Sheets OAuth2** (để đọc/ghi dữ liệu đơn xin mua và thông tin quản lý).
- **Slack OAuth2** (để gửi thông báo và form duyệt qua DM).
- **Gmail OAuth2** (để gửi email thông báo kết quả duyệt/từ chối).
- **Slack App** có quyền `chat:write`, `im:write`, `users:read` (để gửi DM và nhận phản hồi).

📌 **Google Sheets Template**:
- Copy từ [đây](https://docs.google.com/spreadsheets/d/1n9gRUOrz_oLC0S5fq9NQXJFodfT50JL8mTyS6XuVVKc/copy).
- Cập nhật **ID của Sheet** vào các node `Get Manager Info`, `Log Request`, và `Update Status`.

📌 **Thông Tin Cần Điền**:
- **Ngưỡng tự động duyệt** (mặc định: 10,000 JPY → các sếp thay bằng số tiền phù hợp, ví dụ: 1,000,000 VND).
- **Slack Channel ID** của nhóm mua sắm (để thông báo tự động).
- **Email gửi thông báo** (ví dụ: `purchasing@company.com`).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/15009) (ấn "Export" để download file `.json`).
2. Trên **n8n Editor**, click **"Import"** → Chọn file JSON vừa tải.
3. Click **"Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io](https://n8n.io/workflows/15009) (ấn "Export" → "Copy JSON").
2. Trên **n8n Editor**, click **"Import"** → Chọn **"Paste JSON"** → Dán mã và click **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Credentials (Tài Khoản)**
| **Node**               | **Thao Tác**                          | **Tham Số Cần Điền**                          |
|------------------------|---------------------------------------|-----------------------------------------------|
| `Get Manager Info`     | Google Sheets OAuth2                  | Chọn credential đã thiết lập trước (ví dụ: `googleSheetsOAuth2Api`). |
| `Log Request`          | Google Sheets OAuth2                  | Cùng credential như trên.                     |
| `Update Status (×3)`   | Google Sheets OAuth2                  | Cùng credential.                             |
| `Notify Purchasing`    | Slack OAuth2                          | Chọn credential Slack (ví dụ: `slackOAuth2Api`). |
| `Send Approval Request`| Slack OAuth2                          | Cùng credential Slack.                       |
| `Send Auto/Approval/Rejection Email` | Gmail OAuth2 | Chọn credential Gmail (ví dụ: `gmailOAuth2`). |

#### **B. Cập Nhật Thông Tin Cụ Thể**
1. **Google Sheets ID**:
   - Mở Sheet đã copy, sao chép **ID** từ URL (ví dụ: `https://docs.google.com/spreadsheets/d/1ABC123.../edit` → `1ABC123...`).
   - Điền vào các node:
     - `Get Manager Info` → Tham số `Spreadsheet ID`.
     - `Log Request` → Tham số `Spreadsheet ID`.
     - `Update Status (Auto/Approved/Rejected)` → Tham số `Spreadsheet ID`.

2. **Ngưỡng tự động duyệt**:
   - Mở node `Check Amount Threshold` → Thay đổi giá trị trong `Value 2` (ví dụ: từ `10000` thành `1000000` để tự động duyệt đơn dưới 1 triệu).

3. **Slack Channel ID**:
   - Mở Slack, copy **ID của channel** (ví dụ: `#purchasing`) từ URL (ví dụ: `https://your-slack-team.slack.com/archives/C123456789` → `C123456789`).
   - Điền vào node `Notify Purchasing (Auto)` và `Notify Purchasing (Approved)` → Tham số `channel`.

4. **Email gửi thông báo**:
   - Trong các node `Send Auto/Approval/Rejection Email`, thay đổi `sendTo` thành email của người nhận (ví dụ: `purchasing@company.com`).

#### **C. Cấu Hình Slack App**
1. **Bật Interactivity**:
   - Trên Slack App Dashboard → **Features** → **Interactivity & Shortcuts** → Bật **Interactivity**.
   - Đặt **Request URL** thành:
     ```
     https://TEN-MIEN-N8N-CỦA-BẠN.app.n8n.cloud/rest/waiting-webhook/
     ```
     (Ví dụ: `https://my-n8n-instance.app.n8n.cloud/rest/waiting-webhook/`).

2. **Cấp quyền cho App**:
   - Trong **OAuth & Permissions**, thêm scopes:
     - `chat:write` (gửi tin nhắn).
     - `im:write` (gửi DM).
     - `users:read` (đọc thông tin người dùng).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Click **"Run Workflow"** và nhập dữ liệu mẫu vào form `Purchase Request Form`.
   - Kiểm tra các node:
     - `Log Request` (đã ghi vào Sheets chưa?).
     - `Notify Purchasing` (đã gửi Slack chưa?).
     - Email (đã gửi chưa?).

2. **Bật Active**:
   - Sau khi test thành công, click **"Active"** để workflow chạy tự động khi có đơn xin mới.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp với Trello/Notion**
- Sử dụng node **Trello** hoặc **Notion** để tự động tạo card/note mới khi đơn được duyệt/từ chối.
- Ví dụ: Khi đơn được duyệt, tạo card mới trong Trello với thông tin chi tiết.

### **2. Gửi Báo Cáo Định Kỳ**
- Sử dụng **n8n Scheduler** để chạy workflow hàng tuần, gửi báo cáo tổng hợp đơn xin mua qua email.
- Ví dụ: Báo cáo số đơn duyệt/từ chối, tổng giá trị, và danh sách đơn chờ duyệt.

### **3. Cập Nhật Ngưỡng Duyệt Tự Động**
- Thay vì hardcode ngưỡng trong node `Check Amount Threshold`, đọc ngưỡng từ **Google Sheets** (sheet riêng để quản lý ngưỡng).
- Cách làm:
  1. Tạo sheet mới với cột `approval_threshold`.
  2. Sử dụng node **Google Sheets** để đọc giá trị này trước khi kiểm tra ngưỡng.

### **4. Thêm Log Lịch Sử**
- Sử dụng node **StickyNote** để lưu log chi tiết của từng đơn (ví dụ: thời gian duyệt, người duyệt, lý do từ chối).
- Ví dụ:
  ```json
  {
    "timestamp": "2024-05-20T10:00:00",
    "approved_by": "U012345678",
    "reason": "Duyệt - Đã có ngân sách"
  }
  ```

### **5. Kết Nối với ERP/CRM**
- Nếu công ty sử dụng **SAP**, **Odoo**, hoặc **Zoho CRM**, có thể tích hợp để tự động tạo đơn hàng khi đơn được duyệt.
- Ví dụ: Khi đơn được duyệt, node **HTTP Request** gửi dữ liệu đến API của ERP để tạo đơn mua.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR/Operations để tập trung vào công việc chiến lược hơn, thay vì mắc kẹt trong việc quản lý đơn xin mua thủ công. Với **tự động hóa 100%**, các sếp sẽ:
✔ **Không quên** gửi email nhắc nhở.
✔ **Không bị trễ hạn** trong xử lý đơn.
✔ **Dễ dàng theo dõi** toàn bộ lịch sử duyệt.
✔ **Tiết kiệm chi phí** do giảm thời gian làm việc không cần thiết.

---
### **🛠️ Hạ Tầng N8n 24/7 (Không Phải Self-Host)**
Nếu các sếp muốn workflow **chạy liên tục** mà không lo downtime, có thể đăng ký **VPS n8n** từ các nhà cung cấp uy tín:
:::info[Gợi ý hạ tầng cho n8n]
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### **🚀 Bắt Đầu Ngay!**
1. **Import workflow** từ [n8n.io](https://n8n.io/workflows/15009).
2. **Cập nhật credentials** và thông tin cụ thể.
3. **Test run** và bật **Active**.
4. **Tích hợp với Slack/Email** để bắt đầu tự động hóa!

**Chia sẻ workflow này với đồng nghiệp của bạn để cùng tiết kiệm thời gian!** 🚀