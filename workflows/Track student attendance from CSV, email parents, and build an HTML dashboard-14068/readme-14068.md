---
title: "🚀 Tự động theo dõi điểm danh học sinh, gửi email phụ huynh và xây dựng dashboard HTML"
description: "Giải pháp tự động 100% không cần code giúp nhà trường gửi thông báo tới phụ huynh khi học sinh vắng mặt và cập nhật dashboard điểm danh hàng ngày."
slug: "tu-dong-diem-danh-hoc-sinh-gui-email-phan-huynh-dang-bao-cao-dashboard-html"
tags: [n8n, automation, no-code, education, email, dashboard]
keywords: [n8n workflow, tự động hóa, điểm danh, email phụ huynh, dashboard HTML]
---

# 🚀 Tự động theo dõi điểm danh học sinh, gửi email phụ huynh và xây dựng dashboard HTML

Bạn đang phải mất hàng giờ mỗi buổi học để kiểm tra bảng điểm danh, tìm kiếm thông tin liên lạc của phụ huynh và gửi email thông báo? Workflow này sẽ giúp bạn **điểm danh, gửi email, và cập nhật dashboard** chỉ trong vài phút, hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 2-3 giờ làm việc thủ công xuống còn 5-10 phút.
- **Chính xác**: Dữ liệu được xử lý tự động, giảm thiểu lỗi nhập liệu.
- **Cá nhân hóa**: Email được gửi với màu sắc và nội dung tùy chỉnh theo mức độ rủi ro.
- **Hoạt động liên tục**: Được chạy tự động vào 17:30 mỗi ngày (hoặc tùy chỉnh).
- **Ghi nhận lịch sử**: Tất cả dữ liệu được lưu vào `attendance_report.csv` để phân tích dài hạn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **CSV dữ liệu điểm danh**: `student_attendance.csv` (định dạng: ngày, tên, trạng thái).
- **CSV liên lạc phụ huynh**: `student_contacts.csv` (định dạng: tên, email, điện thoại).
- **File lịch sử**: `attendance_report.csv` (để lưu lịch sử, tạo rỗng nếu chưa có).
- **SMTP Credentials**: Đăng ký tài khoản SMTP (Gmail, SendGrid, v.v.) và lưu `smtp_user` trong **n8n → Settings → Variables**.
- **SMTP Node**: Cấu hình **Send Email** node với host, port, username, password, và SSL/TLS tùy nhà cung cấp.
- **Đường dẫn file**: Đảm bảo các file CSV và HTML được lưu trong thư mục `files` của n8n (đường dẫn tương đối: `files/student_attendance.csv`, `files/student_contacts.csv`, `files/attendance_report.csv`, `files/dashboard.html`).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/14068) hoặc sao chép nội dung JSON.
2. Trong n8n Editor, chọn **Import** → **JSON** → dán nội dung hoặc tải file.
3. Nhấn **Import** để tạo workflow mới.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **Recurring Time Trigger** | Định kỳ chạy workflow | `cron` (default: `30 17 * * 1-5` – 17:30 Mon–Fri). |
| **Student Attendance Data** (`readWriteFile`) | Đọc file CSV điểm danh | `filePath`: `files/student_attendance.csv`. |
| **Extract Attendance CSV** (`spreadsheetFile`) | Phân tích CSV | `sheetName`: `Sheet1` (hoặc tên sheet). |
| **IF: Is Absent?** (`if`) | Chia thành vắng/ có mặt | `condition`: `{{ $json["status"] === "Absent" }}`. |
| **Students Contacts** (`readWriteFile`) | Đọc file CSV liên lạc | `filePath`: `files/student_contacts.csv`. |
| **Extract Contacts CSV** (`spreadsheetFile`) | Phân tích CSV | `sheetName`: `Sheet1`. |
| **Merge Absent + Contacts** (`merge`) | Kết hợp dữ liệu | `mergeMode`: `inner` (có thể tùy chỉnh). |
| **Alert Logic Block** (`code`) | Tính toán rủi ro, tỷ lệ, streak, trend | Không cần cấu hình thêm. |
| **Generate Absence Email** (`code`) | Tạo nội dung email HTML | Không cần cấu hình thêm. |
| **Build Dashboard and Report** (`code`) | Xây dựng dashboard HTML | Không cần cấu hình thêm. |
| **Send Email** (`emailSend`) | Gửi email tới phụ huynh | `SMTP Credentials`: chọn tài khoản đã cấu hình. |
| **Existing Report History** (`readWriteFile`) | Đọc file lịch sử | `filePath`: `files/attendance_report.csv`. |
| **Extract History CSV** (`spreadsheetFile`) | Phân tích CSV | `sheetName`: `Sheet1`. |
| **Combine History + Build Dashboard** (`code`) | Kết hợp lịch sử + dashboard | Không cần cấu hình thêm. |
| **Convert Data** (`convertToFile`) | Chuyển đổi dữ liệu thành text | `operation`: `toText`. |
| **Build Visual Report and Update Attendance File** (`readWriteFile`) | Ghi dashboard và cập nhật lịch sử | `filePath`: `files/dashboard.html` (write) và `files/attendance_report.csv` (append). |
| **Date Filter** (`filter`) | Lọc dữ liệu theo ngày | `expression`: `{{ $json["date"] === $now.format("YYYY-MM-DD") }}`. |

> **Lưu ý**: Đảm bảo các node **code** được copy nguyên vẹn từ workflow gốc. Nếu có thay đổi cấu trúc dữ liệu, cần điều chỉnh logic trong các node code.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công với dữ liệu mẫu để kiểm tra tính đúng đắn.
2. **Bật Active**: Đánh dấu workflow là **Active** để tự động chạy theo lịch.
3. Kiểm tra thư mục `files` xem `dashboard.html` và `attendance_report.csv` đã được cập nhật.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node **Slack** hoặc **Telegram** vào nhánh “No Absences Today” để thông báo nhanh cho giáo viên.
- **Logging**: Sử dụng node **Set** + **Write Binary Data** để ghi log vào file `logs.txt` cho mục đích audit.
- **Báo cáo định kỳ**: Thêm node **Schedule Trigger** vào 08:00 hàng tuần để gửi báo cáo tổng hợp tuần tới phụ huynh.
- **Tùy chỉnh màu sắc**: Sửa đoạn code trong **Generate Absence Email** để thay đổi màu sắc dựa trên mức độ rủi ro.

## 📌 Kết luận
Workflow này giúp nhà trường **điểm danh, gửi email, và cập nhật dashboard** một cách tự động, giảm thiểu công việc thủ công và tăng tính chính xác. Hãy áp dụng ngay để tập trung vào việc dạy học và chăm sóc học sinh!