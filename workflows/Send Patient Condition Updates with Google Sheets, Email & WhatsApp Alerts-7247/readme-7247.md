---
title: "🚀 Tự động hóa theo dõi tình trạng bệnh nhân qua Email & WhatsApp với Google Sheets"
description: "Hướng dẫn tự động hóa gửi báo cáo tình trạng bệnh nhân hàng ngày qua email và WhatsApp, với cảnh báo tự động cho các trường hợp nguy kịch"
slug: "tu-dong-hoa-theo-doi-tinh-trang-benh-nhan-google-sheets-email-whatsapp"
tags: [n8n, automation, no-code, google-sheets, email, whatsapp]
keywords: [n8n workflow, tự động hóa bệnh viện, báo cáo bệnh nhân, cảnh báo sức khỏe, google sheets]
---

# 🚀 Tự động hóa theo dõi tình trạng bệnh nhân qua Email & WhatsApp với Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của bệnh viện khi phải theo dõi tình trạng bệnh nhân hàng ngày và gửi báo cáo thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi báo cáo hàng ngày mà không cần can thiệp thủ công.
- Tăng tính chính xác: Dữ liệu được xử lý tự động, giảm thiểu lỗi con người.
- Cảnh báo kịp thời: Nhận thông báo ngay khi có bệnh nhân trong tình trạng nguy kịch.
- Theo dõi hiệu quả: Dễ dàng xem lại lịch sử báo cáo trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã được kích hoạt.
- Tài khoản email (Gmail) để gửi báo cáo.
- API key từ Twilio hoặc dịch vụ gửi tin nhắn khác để gửi WhatsApp.
- Google Sheet với hai bảng:
  - "Patients" chứa dữ liệu bệnh nhân (bắt buộc có cột "Status" để xác định bệnh nhân hoạt động)
  - "Reports_Log" để lưu trữ lịch sử báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7247](https://n8n.io/workflows/7247)
2. Click vào nút "Download" để tải file JSON workflow.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger (8 AM)**:
   - Không cần cấu hình gì thêm, node này sẽ kích hoạt workflow hàng ngày lúc 8 AM.

2. **Read Patient Data**:
   - Chọn credentials Google API đã được cấu hình.
   - Điền thông tin:
     - Spreadsheet ID: ID của Google Sheet chứa dữ liệu bệnh nhân.
     - Sheet Name: "Patients" (hoặc tên bảng bạn đã đặt).
     - Range: "A:Z" để lấy toàn bộ dữ liệu.

3. **Filter Active Patients**:
   - Thiết lập điều kiện lọc: `{{$node["Read Patient Data"].json["Status"]}} === "Active"`

4. **Process Patient Data**:
   - Node này xử lý dữ liệu và tạo nội dung báo cáo. Bạn có thể chỉnh sửa code JavaScript nếu cần thay đổi định dạng báo cáo.

5. **Send Email Report**:
   - Chọn credentials SMTP đã được cấu hình.
   - Điền thông tin:
     - To: Địa chỉ email của bác sĩ hoặc nhân viên y tế.
     - Subject: "Daily Patient Report - {{ $executionId }}"
     - Body: Sử dụng biểu thức `{{ $node["Process Patient Data"].json["reportContent"] }}` để lấy nội dung báo cáo.

6. **Send WhatsApp Message**:
   - Cấu hình HTTP Request:
     - Method: POST
     - URL: Endpoint của dịch vụ gửi tin nhắn (ví dụ: Twilio)
     - Headers: Thêm các header cần thiết (Content-Type: application/json, Authorization: Bearer YOUR_API_KEY)
     - Body: JSON chứa nội dung tin nhắn và số điện thoại nhận.

7. **Filter Critical Patients**:
   - Thiết lập điều kiện lọc: `{{$node["Process Patient Data"].json["isCritical"]}} === true`

8. **Send Critical Alert**:
   - Tương tự như node "Send Email Report", nhưng gửi đến email của nhân viên y tế hoặc quản lý bệnh viện.

9. **Log Report to Sheet**:
   - Chọn credentials Google API đã được cấu hình.
   - Điền thông tin:
     - Spreadsheet ID: ID của Google Sheet chứa dữ liệu bệnh nhân.
     - Sheet Name: "Reports_Log" (hoặc tên bảng bạn đã đặt).
     - Range: "A1" (hoặc ô bắt đầu bạn muốn ghi dữ liệu).
     - Data: Sử dụng biểu thức `{{ $node["Process Patient Data"].json["reportData"] }}` để lấy dữ liệu báo cáo.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow.
2. Để kiểm tra workflow hoạt động đúng, bạn có thể:
   - Chạy thử với dữ liệu mẫu bằng cách click vào nút "Execute Workflow".
   - Kiểm tra email và WhatsApp để xác nhận báo cáo được gửi đúng.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi thông báo đến Slack hoặc Telegram để nhận cảnh báo ngay lập tức.
- Tạo báo cáo định kỳ hàng tuần/tháng bằng cách thêm node Cron Trigger mới.
- Tích hợp với hệ thống quản lý bệnh viện (EHR) để lấy dữ liệu bệnh nhân tự động.
- Thêm chức năng gửi SMS thay vì WhatsApp nếu cần độ phủ sóng rộng hơn.

### 📌 Kết luận
Workflow này giúp các bệnh viện tự động hóa quy trình theo dõi tình trạng bệnh nhân, giảm thiểu công việc thủ công và tăng tính chính xác của báo cáo. Bằng cách áp dụng workflow này, các sếp có thể tập trung vào việc chăm sóc bệnh nhân thay vì phải tốn thời gian gửi báo cáo hàng ngày. Hãy thử ngay và trải nghiệm sự khác biệt mà tự động hóa mang lại!