---
title: "🚀 Lịch Học & Nhắc Nhở Tự Động: Đồng Bộ Google Calendar, Email & SMS"
description: "Giải pháp tự động hóa hoàn chỉnh giúp giáo viên và học sinh không bỏ lỡ lớp học, đồng bộ lịch, gửi nhắc nhở qua email hoặc SMS mà không cần viết code."
slug: "lich-hoc-nhac-nho-tuy-dung"
tags: [n8n, automation, no-code, google-calendar, email, sms, excel]
keywords: [n8n workflow, tự động hóa, lịch học, nhắc nhở, Google Calendar, email, SMS]
---

# 🚀 Lịch Học & Nhắc Nhở Tự Động: Đồng Bộ Google Calendar, Email & SMS

Bạn đang phải mất hàng giờ mỗi ngày để kiểm tra bảng lớp, đồng bộ lịch, và gửi nhắc nhở cho học sinh? Đừng lo, workflow này sẽ giúp bạn **đồng bộ lịch học, gửi email/SMS nhắc nhở** chỉ trong vài phút, 24/7, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ làm thủ công xuống chỉ vài phút.
- **Độ chính xác cao**: Không còn lỗi nhập liệu, đồng bộ dữ liệu chính xác 100%.
- **Cá nhân hóa**: Gửi email/SMS riêng cho từng học sinh với nội dung phù hợp.
- **Hoạt động liên tục**: Được chạy tự động 24/7, không phụ thuộc vào con người.
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | Credential | Mô tả |
|---------|------------|-------|
| **Microsoft Excel** | `microsoftExcelOAuth2Api` | Đọc bảng lớp và danh sách học sinh. |
| **Google Calendar** | `googleCalendarOAuth2Api` | Đồng bộ lịch học. |
| **Email** | `smtp` (hoặc dịch vụ email) | Gửi email nhắc nhở. |
| **SMS** | `twilio` (hoặc dịch vụ SMS) | Gửi tin nhắn nhắc nhở. |
| **Environment Variables** | `EMAIL_FROM`, `SMS_FROM` | Định danh người gửi. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ [link workflow](https://n8n.io/workflows/6997) hoặc copy toàn bộ JSON.
2. Mở n8n Editor → **Import** → **Import from JSON** → dán JSON hoặc upload file.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Thông tin cần cấu hình | Ghi chú |
|------|------------------------|---------|
| **Daily Schedule Check** | `Cron` → `Time zone`, `Start date`, `Time` | Đặt thời gian kiểm tra (vd: 08:00 AM). |
| **Read Class Schedule** | `File ID`, `Worksheet` | Chỉ định file Excel chứa lịch học. |
| **Filter Today's Classes** | Code JS | Đảm bảo logic lọc ngày hiện tại. |
| **Has Classes Today?** | `If` → `Condition` | Kiểm tra có lớp hôm nay không. |
| **Read Student Contacts** | `File ID`, `Worksheet` | File Excel danh sách học sinh. |
| **Create Student Reminders** | Code JS | Tạo nội dung nhắc nhở cá nhân. |
| **Split Into Batches** | `Batch size` | Đặt kích thước batch (vd: 10). |
| **Email or SMS?** | `If` → `Condition` | Chọn kênh gửi. |
| **Prepare Email Reminders** | Code JS | Định dạng email (subject, body). |
| **Prepare SMS Reminders** | Code JS | Định dạng SMS. |
| **Sync to Google Calendar** | `Calendar ID`, `Event details` | Đảm bảo quyền truy cập. |
| **Read Reminder Log** | `File ID`, `Worksheet` | File log ghi nhận trạng thái. |
| **Update Reminder Log** | Code JS | Cập nhật trạng thái gửi. |
| **Save Reminder Log** | `Operation: append`, `Worksheet` | Ghi log vào file Excel. |

> **Tip**: Kiểm tra kỹ các trường `File ID` và `Worksheet` trong các node Microsoft Excel, tránh lỗi 404.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Node”).
2. **Xem log**: Kiểm tra console, đảm bảo không có lỗi.
3. **Bật Active**: Bật công tắc “Active” ở góc trên bên phải.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram**: Thêm node Slack/Telegram để gửi thông báo khi workflow chạy thành công.
- **Lưu log vào Google Sheets**: Thay vì Excel, dùng Google Sheets để dễ dàng chia sẻ.
- **Định kỳ gửi báo cáo**: Thêm node `Cron` để gửi báo cáo tuần về số lớp đã đồng bộ.
- **Sử dụng biến môi trường**: Lưu API key, email, SMS credentials trong `.env` để bảo mật.

## 📌 Kết luận
Workflow “Class Scheduling & Reminders” giúp bạn **đồng bộ lịch học, gửi nhắc nhở** một cách tự động, chính xác và tiết kiệm thời gian. Hãy thử ngay, áp dụng cho phòng học, trung tâm đào tạo, hoặc bất kỳ môi trường giáo dục nào. Nếu cần hỗ trợ, liên hệ với Oneclick AI Squad – đội ngũ chuyên gia n8n và AI. 🚀