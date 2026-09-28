---
title: "🚀 Tự động hóa lịch trình du lịch với Google Calendar, Excel và nhắc nhở SMS-Email"
description: "Tự động hóa hoàn toàn quá trình quản lý lịch trình du lịch, đồng bộ với Google Calendar, gửi nhắc nhở qua email/SMS và theo dõi hoạt động với Excel - giải pháp tiết kiệm thời gian 100% không cần code."
slug: "tu-dong-hoa-lich-trinh-du-lich-google-calendar-excel-sms-email"
tags: [n8n, automation, no-code, travel, google-calendar, excel, sms, email]
keywords: [n8n workflow, tự động hóa du lịch, quản lý lịch trình, nhắc nhở du lịch, google calendar, excel, sms, email]
---

# 🚀 Tự động hóa lịch trình du lịch với Google Calendar, Excel và nhắc nhở SMS-Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải tự tay quản lý lịch trình du lịch, gửi nhắc nhở cho từng người, đồng bộ với lịch Google và theo dõi hoạt động không? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý lịch trình du lịch hàng ngày
- Đồng bộ tự động với Google Calendar của từng người
- Gửi nhắc nhở qua email/SMS theo lựa chọn của từng người
- Theo dõi hoạt động và trạng thái nhắc nhở qua Excel
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar với quyền truy cập API
- Tài khoản Microsoft 365 với quyền truy cập Excel Online
- File Excel chứa dữ liệu lịch trình du lịch (trip_itinerary.xlsx)
- File Excel chứa thông tin liên lạc của người đi du lịch (traveler_contacts.xlsx)
- File Excel để lưu log nhắc nhở (reminder_log.xlsx)
- Tài khoản SMTP để gửi email (nếu sử dụng nhắc nhở qua email)
- Tài khoản dịch vụ SMS (như Twilio, Nexmo) (nếu sử dụng nhắc nhở qua SMS)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9846](https://n8n.io/workflows/9846)
2. Click vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Daily Travel Check",
      "type": "n8n-nodes-base.cron",
      "parameters": {
        "options": {
          "scheduleOptions": {
            "every": {
              "unit": "day",
              "value": 1
            }
          }
        }
      }
    },
    // Các node khác...
  ],
  "connections": [
    // Các kết nối giữa các node...
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **Node "Daily Travel Check"**:
   - Cấu hình lịch chạy hàng ngày (mặc định đã được thiết lập)

2. **Node "Read Travel Itinerary"**:
   - Chọn credentials "microsoftExcelOAuth2Api"
   - Cấu hình tham số:
     - File Location: Đường dẫn đến file trip_itinerary.xlsx
     - Sheet Name: Tên sheet chứa dữ liệu lịch trình
     - Range: Phạm vi dữ liệu (ví dụ: A1:L100)

3. **Node "Filter Today's Trips"**:
   - Code JavaScript để lọc các chuyến đi hôm nay (đã được thiết lập sẵn)

4. **Node "Read Traveler Contacts"**:
   - Chọn credentials "microsoftExcelOAuth2Api"
   - Cấu hình tham số:
     - File Location: Đường dẫn đến file traveler_contacts.xlsx
     - Sheet Name: Tên sheet chứa thông tin liên lạc
     - Range: Phạm vi dữ liệu

5. **Node "Sync to Google Calendar"**:
   - Chọn credentials "googleCalendarOAuth2Api"
   - Cấu hình tham số:
     - Operation: Create
     - Calendar ID: ID lịch Google cần đồng bộ
     - Title: Tên sự kiện (sử dụng biến từ dữ liệu chuyến đi)
     - Description: Mô tả sự kiện (sử dụng biến từ dữ liệu chuyến đi)
     - Start Date: Ngày bắt đầu (sử dụng biến từ dữ liệu chuyến đi)
     - End Date: Ngày kết thúc (sử dụng biến từ dữ liệu chuyến đi)

6. **Node "Read Reminder Log"**:
   - Chọn credentials "microsoftExcelOAuth2Api"
   - Cấu hình tham số:
     - File Location: Đường dẫn đến file reminder_log.xlsx
     - Sheet Name: Tên sheet chứa log nhắc nhở
     - Range: Phạm vi dữ liệu

7. **Node "Save Reminder Log"**:
   - Chọn credentials "microsoftExcelOAuth2Api"
   - Cấu hình tham số:
     - File Location: Đường dẫn đến file reminder_log.xlsx
     - Sheet Name: Tên sheet chứa log nhắc nhở
     - Range: Phạm vi dữ liệu
     - Operation: Append
     - Resource: Worksheet

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Test workflow bằng cách chạy thử với dữ liệu mẫu
3. Kiểm tra Google Calendar, email/SMS và file Excel để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi thông báo đến kênh Slack/Teams khi có chuyến đi mới
2. **Báo cáo định kỳ**: Thêm node để tạo báo cáo tổng hợp các chuyến đi và nhắc nhở đã gửi
3. **Xử lý lỗi**: Thêm node để gửi email thông báo khi workflow gặp lỗi
4. **Tích hợp với các dịch vụ khác**: Kết nối với các dịch vụ khác như Airbnb, Booking.com để tự động cập nhật thông tin đặt phòng

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình quản lý lịch trình du lịch, đồng bộ với Google Calendar, gửi nhắc nhở qua email/SMS và theo dõi hoạt động với Excel. Với việc triển khai workflow này, các sếp có thể tiết kiệm thời gian đáng kể và đảm bảo không bỏ lỡ bất kỳ chuyến đi nào. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của mình!