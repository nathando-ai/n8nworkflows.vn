---
title: "📅 [Tự động hóa Bảo trì Định kỳ] Gửi Lịch Bảo trì từ Google Sheets qua Email với File ICS"
description: "Hướng dẫn tự động hóa gửi lịch bảo trì định kỳ từ Google Sheets đến email với file ICS, tiết kiệm thời gian và đảm bảo thông tin chính xác cho đội ngũ kỹ thuật."
slug: "tu-dong-hoa-bao-tri-dinh-ky-google-sheets-gmail-ics"
tags: [n8n, automation, no-code, google-sheets, gmail, calendar]
keywords: [n8n workflow, tự động hóa bảo trì, google sheets, gmail ics, lịch bảo trì]
---

# 📅 [Tự động hóa Bảo trì Định kỳ] Gửi Lịch Bảo trì từ Google Sheets qua Email với File ICS

[Các sếp đang gặp khó khăn khi quản lý lịch bảo trì định kỳ cho các thiết bị quan trọng. Việc thủ công nhập thông tin vào Google Sheets và gửi email với file ICS (iCalendar) cho từng kỹ thuật viên tốn thời gian và dễ gây lỗi. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình gửi lịch bảo trì hàng ngày.
- **Chính xác cao**: Dữ liệu được lấy trực tiếp từ Google Sheets, đảm bảo thông tin luôn cập nhật.
- **Tiện ích cho kỹ thuật viên**: File ICS được đính kèm trong email giúp dễ dàng thêm vào lịch Google hoặc Outlook.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Một bảng tính chứa danh sách các công việc bảo trì định kỳ.
- **Google Workspace**: Tài khoản Google Workspace để truy cập Google Sheets và Gmail.
- **n8n**: Đã cài đặt và cấu hình n8n trên máy chủ hoặc VPS.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút **"Import from URL"** và nhập URL sau: [https://n8n.io/workflows/7700](https://n8n.io/workflows/7700).
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/7700) và chọn **"Import from File"**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger**:
   - Cấu hình thời gian chạy hàng ngày (ví dụ: 8:00 AM).
   - Đảm bảo múi giờ được đặt chính xác.

2. **Read Maintenance Tasks**:
   - Cấu hình **Google Sheets OAuth2 API** trong n8n.
   - Nhập **Spreadsheet ID** và **Sheet Name** chứa danh sách công việc bảo trì.
   - Đảm bảo cột dữ liệu trong Google Sheets có cấu trúc như sau:
     - `Task Name`: Tên công việc bảo trì.
     - `Assignee Email`: Email của kỹ thuật viên phụ trách.
     - `Start Time`: Thời gian bắt đầu (định dạng: `YYYY-MM-DD HH:MM`).
     - `End Time`: Thời gian kết thúc (định dạng: `YYYY-MM-DD HH:MM`).
     - `Details`: Mô tả chi tiết công việc.

3. **Generate ICS Data**:
   - Node này tự động tạo dữ liệu ICS từ thông tin lấy từ Google Sheets.
   - Không cần cấu hình thêm.

4. **Create ICS File**:
   - Node này chuyển đổi dữ liệu ICS thành file .ics.
   - Không cần cấu hình thêm.

5. **Send Calendar Invite Email**:
   - Cấu hình **Gmail OAuth2** trong n8n.
   - Đảm bảo email gửi đi có cấu trúc như sau:
     - **Subject**: `Bảo trì định kỳ: [Task Name]`.
     - **Body**: `Xin chào [Assignee Name],\n\nVui lòng xem thông tin bảo trì định kỳ trong file đính kèm.\n\nTrân trọng,\nĐội ngũ kỹ thuật`.
     - **Attachments**: File .ics được tạo từ node trước đó.

#### 3. Kích hoạt ⚡️
1. Nhấn **"Execute Workflow"** để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấn **"Activate"** để workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Teams**: Thêm node gửi thông báo đến Slack hoặc Microsoft Teams khi gửi email thành công.
- **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets để theo dõi lịch sử gửi email.
- **Gửi báo cáo định kỳ**: Mở rộng workflow để gửi báo cáo tổng hợp các công việc bảo trì đã thực hiện trong tuần.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình gửi lịch bảo trì định kỳ, tiết kiệm thời gian và đảm bảo thông tin chính xác. Hãy áp dụng ngay để nâng cao hiệu quả quản lý bảo trì trong doanh nghiệp!