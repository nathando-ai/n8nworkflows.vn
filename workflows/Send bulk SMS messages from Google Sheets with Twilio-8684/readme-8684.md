---
title: "📲 Tự Động Hóa Gửi SMS Bulk Từ Google Sheets Với Twilio - Không Cần Code"
description: "Workflow này tự động gửi SMS cá nhân hóa từ Google Sheets qua Twilio, giúp các sếp tiết kiệm thời gian và quản lý hiệu quả các thông báo bulk như reminder sự kiện, thông báo khuyến mại hoặc thông tin quan trọng cho khách hàng. Hỗ trợ cập nhật trạng thái tự động sau khi gửi."
slug: "tu-dong-hoa-gui-sms-bulk-tu-google-sheets-voi-twilio"
tags: [n8n, automation, no-code, twilio, google-sheets, sms-marketing]
keywords: [n8n workflow gửi sms bulk, tự động hóa sms từ google sheets, twilio n8n, gửi sms bulk không code, tự động hóa marketing sms]
---

# 🚀 **Tự Động Hóa Gửi SMS Bulk Từ Google Sheets Với Twilio - Không Cần Code**

## **🔥 Nỗi Đau Của Các Sếp Khi Gửi SMS Bulk**
Gửi SMS bulk cho khách hàng, nhân viên hoặc đối tác thủ công không chỉ tốn thời gian mà còn dễ gây lỗi như:
- **Quên gửi** hoặc gửi trễ: Làm mất cơ hội chuyển đổi hoặc gây mất tin cậy.
- **Sai thông tin**: Tên, số điện thoại hoặc nội dung không chính xác gây nhầm lẫn.
- **Không theo dõi kết quả**: Không biết SMS đã được gửi thành công hay thất bại, không thể sửa chữa kịp thời.
- **Tốn công sức**: Phải nhập liệu và gửi từng SMS một, đặc biệt khi danh sách lớn.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét và gửi SMS** từ Google Sheets khi trạng thái được cập nhật.
✅ **Cá nhân hóa nội dung** bằng tên (First Name, Last Name).
✅ **Cập nhật trạng thái tự động** (Đang gửi, Thành công, Lỗi).
✅ **Hoạt động 24/7** mà không cần can thiệp của bạn.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu hoặc gửi SMS thủ công.
- **Tăng độ chính xác**: Tránh sai sót trong thông tin khách hàng.
- **Cá nhân hóa tự động**: Chỉnh sửa nội dung SMS theo tên hoặc thông tin trong Sheet.
- **Theo dõi hiệu quả**: Biết ngay SMS nào thành công, nào thất bại và có thể xử lý lại.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có dữ liệu mới trong Sheet.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Twilio**:
   - Đăng ký [miễn phí tại đây](https://www.twilio.com/try-twilio) (có thể dùng thử miễn phí).
   - Lấy **Account SID**, **Auth Token** và **Số điện thoại Twilio** từ Dashboard.
   - [Hướng dẫn cài đặt Twilio cho n8n](https://docs.n8n.io/integrations/n8n-nodes-base.n8nTwilio/#configuration).

2. **Google Sheets**:
   - **Tạo bản sao template** từ [đây](https://docs.google.com/spreadsheets/d/1DGhQ2YLeQ5boLYPMK4nUF8SIOJmDDqvtyleSz5IpJEc/edit?usp=sharing) (File → Make a copy).
   - **Chia sẻ Sheet với n8n**: Cấp quyền "Sửa" cho ứng dụng n8n (n8n sẽ cập nhật trạng thái tự động).
   - [Hướng dẫn kết nối Google Sheets với n8n](https://docs.n8n.io/integrations/n8n-nodes-base.n8nGoogleSheets/#configuration).

3. **Credentials cho n8n**:
   - **Twilio**: Tạo credential mới trong n8n với `Account SID`, `Auth Token` và `From Number`.
   - **Google Sheets**: Tạo credential OAuth2 cho trigger và node update.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8684) và import vào n8n Editor.
- **Copy JSON** từ link trên và dán vào n8n Editor (File → Import Workflow → Paste JSON).

:::note[Lưu ý]
- **Không sử dụng template gốc**: Phải tạo bản sao riêng để workflow có quyền cập nhật trạng thái.
- **Kiểm tra URL Sheet**: Đảm bảo `sheet_url` trong node **Config** trùng với URL của Sheet đã copy.
:::

---

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflows này có **10 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **A. Node "Monitor Google Sheet for SMS Queue" (Trigger)**
- **Credentials**: Chọn `googleSheetsTriggerOAuth2Api` đã tạo trước đó.
- **Sheet URL**: Điền URL của Sheet đã copy (ví dụ: `https://docs.google.com/spreadsheets/d/1ABC123...`).
- **Range**: Đặt là `Sheet1!A:Z` (hoặc tên Sheet cụ thể nếu khác).
- **Watch for changes in column**: Chọn cột **Status** (cột này sẽ theo dõi trạng thái "To send").

##### **B. Node "Config" (Set)**
- **Tham số cần điền**:
  ```json
  {
    "sheet_url": "https://docs.google.com/spreadsheets/d/1ABC123...",
    "from_number": "+1234567890"  // Số Twilio của bạn
  }
  ```
- **Lưu ý**: `sheet_url` phải trùng với URL Sheet đã chia sẻ cho n8n.

##### **C. Node "Prepare SMS Content" (Set)**
- **Tham số mẫu**:
  ```json
  {
    "message": "Xin chào [First Name], [Last Name]! Bạn đã đăng ký sự kiện [Event Name] vào ngày [Date]. Xác nhận lại bằng SMS này. Cảm ơn!"
  }
  ```
- **Placeholder hỗ trợ**:
  - `[First Name]`: Thay thế bằng giá trị trong cột "First Name".
  - `[Last Name]`: Thay thế bằng giá trị trong cột "Last Name".
  - Các placeholder khác có thể thêm tùy chỉnh (ví dụ: `[Event Name]`, `[Date]`).

##### **D. Node "Send SMS via Twilio" (Twilio)**
- **Credentials**: Chọn `twilioApi` đã tạo.
- **Tham số cần điền**:
  - `To`: Số điện thoại của khách hàng (cột "Phone" trong Sheet).
  - `Body`: Nội dung SMS đã chuẩn bị từ node trước (sử dụng `{{ $node["Prepare SMS Content"].json["message"] }}`).
- **Lưu ý**:
  - Đảm bảo số Twilio đã **đăng ký** và có **số dư** (miễn phí cho số lượng nhỏ).
  - Kiểm tra **format số điện thoại**: Nếu số có dấu `+`, Twilio sẽ tự động xử lý.

##### **E. Node "Update Status to Sending" / "Mark as Success" / "Mark as Error" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Range**: Đặt là `Sheet1!A:Z` (hoặc tên Sheet cụ thể).
- **Values**: Sử dụng `{{ $node["Check if Ready to Send"].json["row"] }}` để cập nhật trạng thái.
- **Lưu ý**:
  - Cột **Status** phải có giá trị:
    - `To send` → Workflow sẽ gửi SMS.
    - `Sending` → Trạng thái tạm thời khi SMS đang được xử lý.
    - `Success` → SMS gửi thành công.
    - `Error` → SMS thất bại (ví dụ: số điện thoại không hợp lệ).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Cập nhật một hàng trong Sheet với trạng thái `To send`.
   - Chạy **Manual Trigger** trong node **Monitor Google Sheet for SMS Queue** để kiểm tra.
   - Kiểm tra:
     - SMS có được gửi không? (Kiểm tra trên điện thoại hoặc trong Dashboard Twilio).
     - Trạng thái trong Sheet có được cập nhật không?

2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi SMS gửi thành công/lỗi.
   - Ví dụ: Khi trạng thái `Error`, gửi tin nhắn cảnh báo đến Slack.

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** để ghi lại lịch sử gửi SMS (ngày giờ, trạng thái, nội dung).
   - Cột mới trong Sheet: `Log`, `Sent At`, `Status`.

3. **Gửi SMS Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow vào giờ cố định (ví dụ: 8h sáng để gửi reminder).

4. **Tự Động Xóa Dữ Liệu Sau Gửi**:
   - Thêm node **Google Sheets** để xóa hàng sau khi trạng thái `Success` (nếu không cần lưu lại).

5. **Cá Nhân Hóa Nâng Cao**:
   - Sử dụng **n8n-nodes-base.llm** (nếu có) để tự động tạo nội dung SMS dựa trên dữ liệu trong Sheet.

---

### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần gửi SMS bulk một cách **tự động, chính xác và cá nhân hóa** mà không cần viết code. Bằng cách kết nối Google Sheets và Twilio, các sếp có thể:
✔ **Tiết kiệm hàng giờ** mỗi tuần.
✔ **Tránh sai sót** trong thông tin khách hàng.
✔ **Theo dõi hiệu quả** mọi SMS gửi đi.

**Hành động ngay!**
1. **Tạo bản sao template** và chia sẻ với n8n.
2. **Cấu hình Twilio** và Google Sheets.
3. **Import workflow** và chạy test.
4. **Bật Active** và bắt đầu tự động hóa!

---
**💡 Cần hỗ trợ kỹ thuật?**
- Liên hệ **SmoothWork** qua [đây](https://smoothwork.ai/book-a-call) để được tư vấn chi tiết.
- Hoặc tham gia **community n8n** tại [Discord](https://n8n.io/community).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::