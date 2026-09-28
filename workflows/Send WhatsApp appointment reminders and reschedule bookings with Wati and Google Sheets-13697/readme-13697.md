---
title: "📅 [Tự động hóa lịch hẹn WhatsApp] Gửi nhắc lịch hẹn và điều chỉnh lịch hẹn qua Wati + Google Sheets"
description: "Hướng dẫn tự động hóa gửi nhắc lịch hẹn WhatsApp, xác nhận và điều chỉnh lịch hẹn thông qua Wati và Google Sheets với n8n. Tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-hoa-lich-hen-whatsapp-wati-google-sheets"
tags: [n8n, automation, no-code, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa lịch hẹn, nhắc lịch hẹn, wati, google sheets]
---

# 📅 [Tự động hóa lịch hẹn WhatsApp] Gửi nhắc lịch hẹn và điều chỉnh lịch hẹn qua Wati + Google Sheets

[Các sếp đang gặp khó khăn khi quản lý lịch hẹn thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình nhắc lịch hẹn, xác nhận và điều chỉnh lịch hẹn thông qua WhatsApp và Google Sheets với n8n. Tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và giảm thiểu lỗi nhân viên.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi nhắc lịch hẹn hàng ngày mà không cần can thiệp thủ công.
- **Nâng cao trải nghiệm khách hàng**: Khách hàng có thể xác nhận, hủy hoặc điều chỉnh lịch hẹn trực tiếp qua WhatsApp.
- **Giảm thiểu lỗi**: Dữ liệu được đồng bộ tự động giữa Google Sheets và hệ thống nhắn tin.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi sáng lúc 9 giờ mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Wati với API key.
- Tài khoản Google với quyền truy cập vào Google Sheets và Google Calendar.
- Google Sheets đã được cấu hình với các tab: Appointments, AvailableSlots, RescheduleSessions.
- Số điện thoại WhatsApp đã được kết nối với Wati.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13697](https://n8n.io/workflows/13697).
2. Nhấn nút **Download** để tải file JSON của workflow.
3. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger – 9AM Daily**:
   - Đảm bảo thời gian chạy là 9:00 sáng hàng ngày.

2. **Google Sheets – Read Appointments**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Điền **Spreadsheet ID** của Google Sheets chứa dữ liệu lịch hẹn.
   - Điền **Range Name** là tên tab chứa dữ liệu lịch hẹn (ví dụ: Appointments).

3. **Filter Upcoming Appointments**:
   - Kiểm tra và điều chỉnh mã JavaScript để lọc các lịch hẹn trong vòng 24 giờ.

4. **Build Reminder Message**:
   - Điều chỉnh mã JavaScript để tạo nội dung nhắc lịch hẹn phù hợp với nhu cầu của các sếp.

5. **Route Message**:
   - Cấu hình các điều kiện để phân loại các phản hồi từ khách hàng (confirm, cancel, reschedule, myappointment).

6. **Google Sheets – Read for Confirm**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Điền **Spreadsheet ID** và **Range Name** tương ứng.

7. **Process Confirmation**:
   - Kiểm tra và điều chỉnh mã JavaScript để xử lý xác nhận lịch hẹn.

8. **Google Sheets – Update Status Confirmed**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Điền **Spreadsheet ID** và **Range Name** tương ứng.
   - Đảm bảo **operation** được đặt là **update**.

9. **Google Sheets – Read for Cancel**:
   - Chọn credentials **googleSheetsOAuth2Api**.
   - Điền **Spreadsheet ID** và **Range Name** tương ứng.

10. **Process Cancellation**:
    - Kiểm tra và điều chỉnh mã JavaScript để xử lý hủy lịch hẹn.

11. **Google Sheets – Update Status Cancelled**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.
    - Đảm bảo **operation** được đặt là **update**.

12. **Google Sheets – Read Available Slots**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.

13. **Build Available Slots**:
    - Kiểm tra và điều chỉnh mã JavaScript để tạo danh sách các khung giờ trống.

14. **Google Sheets – Save Reschedule Session**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.
    - Đảm bảo **operation** được đặt là **append**.

15. **Google Sheets – Read Reschedule Session**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.

16. **Process Slot Selection**:
    - Kiểm tra và điều chỉnh mã JavaScript để xử lý chọn khung giờ mới.

17. **Google Sheets – Update Rescheduled**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.
    - Đảm bảo **operation** được đặt là **update**.

18. **Google Sheets – Read My Appointment**:
    - Chọn credentials **googleSheetsOAuth2Api**.
    - Điền **Spreadsheet ID** và **Range Name** tương ứng.

19. **Build My Appointment Card**:
    - Kiểm tra và điều chỉnh mã JavaScript để tạo thẻ thông tin lịch hẹn.

20. **Send a text message**:
    - Chọn credentials **watiApi**.
    - Điền **Phone Number** của người nhận.
    - Điền **Message** chứa nội dung nhắc lịch hẹn.

21. **Wati Trigger**:
    - Chọn credentials **watiApi**.
    - Đảm bảo webhook đã được cấu hình đúng để nhận phản hồi từ khách hàng.

22. **Send a text message5**:
    - Chọn credentials **watiApi**.
    - Điền **Phone Number** của người nhận.
    - Điền **Message** chứa thông tin lịch hẹn.

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, nhấn vào nút **Execute Node** để kiểm tra workflow.
2. Đảm bảo workflow chạy thành công với dữ liệu mẫu.
3. Bật **Active workflow** để workflow chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo đến Slack hoặc Telegram khi có lịch hẹn mới hoặc thay đổi.
- **Lưu log**: Thêm node để lưu log các hoạt động của workflow để theo dõi và phân tích.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp hàng tuần hoặc hàng tháng về các lịch hẹn.
- **Tích hợp với Google Calendar**: Thêm node để đồng bộ dữ liệu lịch hẹn với Google Calendar để quản lý lịch trình một cách hiệu quả.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình nhắc lịch hẹn, xác nhận và điều chỉnh lịch hẹn thông qua WhatsApp và Google Sheets với n8n. Tiết kiệm thời gian, nâng cao trải nghiệm khách hàng và giảm thiểu lỗi nhân viên. Hãy áp dụng ngay để tối ưu hóa quy trình quản lý lịch hẹn của các sếp!