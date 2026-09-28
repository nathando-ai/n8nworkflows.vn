---
title: "🚀 Theo dõi chấm công nhân viên với báo cáo email & cảnh báo Slack từ Google Sheets"
description: "Tự động hóa chấm công nhân viên 24/7 với báo cáo email hàng ngày và cảnh báo Slack khi có sự cố. Giảm thiểu công việc thủ công và tăng tính chính xác."
slug: "theo-doi-cham-cong-nhan-vien-voi-bao-cao-email-slack-google-sheets"
tags: [n8n, automation, no-code, hr, google-sheets, email, slack]
keywords: [n8n workflow, tự động hóa chấm công, báo cáo nhân sự, cảnh báo Slack, Google Sheets]
---

# 🚀 Theo dõi chấm công nhân viên với báo cáo email & cảnh báo Slack từ Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chấm công thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quá trình theo dõi chấm công hàng giờ
- Nhận báo cáo email hàng ngày với dữ liệu chấm công chi tiết
- Cảnh báo Slack tức thì khi phát hiện nhân viên nghỉ quá nhiều
- Giảm thiểu công việc thủ công lên tới 90%
- Tăng tính chính xác và minh bạch trong quản lý nhân sự
- Lưu trữ lịch sử chấm công để phân tích xu hướng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để truy cập Google Sheets API)
- Tài khoản SMTP (để gửi email báo cáo)
- Tài khoản Slack (để nhận cảnh báo)
- Google Sheets với 2 bảng dữ liệu:
  1. Bảng chấm công (Attendance Records)
  2. Bảng thông tin nhân viên (Employee Master Data)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/10106)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Attendance Records"**:
   - Chọn credentials Google API
   - Điền Spreadsheet ID của bảng chấm công
   - Đặt tên Range là "A:Z" để lấy toàn bộ dữ liệu

2. **Node "Fetch Employee Master Data"**:
   - Chọn credentials Google API
   - Điền Spreadsheet ID của bảng thông tin nhân viên
   - Đặt tên Range là "A:Z" để lấy toàn bộ dữ liệu

3. **Node "Analytics Engine"**:
   - Kiểm tra và điều chỉnh logic phân tích nếu cần
   - Đảm bảo các biến như `attendanceData` và `employeeData` được định nghĩa đúng

4. **Node "Send Email"**:
   - Cấu hình credentials SMTP
   - Điền địa chỉ email người nhận
   - Đặt tiêu đề email: "Báo cáo chấm công hàng ngày - [Ngày tháng]"

5. **Node "Post to Slack"**:
   - Cấu hình credentials Slack API
   - Điền Channel ID để gửi cảnh báo
   - Kiểm tra định dạng tin nhắn trong node "Format Slack"

6. **Node "Log Summary"**:
   - Điền Spreadsheet ID của bảng lưu trữ lịch sử
   - Đảm bảo bảng này có cột phù hợp với dữ liệu summary

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ luồng
2. Kích hoạt workflow bằng cách bật nút Active
3. Đặt lịch chạy hàng giờ (hoặc theo nhu cầu) trong node "Schedule Trigger"

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Google Calendar**: Thêm node để tự động tạo sự kiện lịch cho nhân viên nghỉ quá nhiều
2. **Báo cáo tuần/tháng**: Sửa đổi node "Schedule Trigger" để chạy hàng tuần/tháng
3. **Dashboard trực quan**: Kết nối với Google Data Studio để tạo bảng điều khiển trực quan
4. **Cảnh báo đa kênh**: Thêm node để gửi SMS hoặc tin nhắn Teams khi có sự cố

### 📌 Kết luận
Workflow này giúp các sếp HR tự động hóa hoàn toàn quá trình theo dõi chấm công, giảm thiểu công việc thủ công và tăng tính minh bạch trong quản lý nhân sự. Bằng cách áp dụng ngay, các sếp có thể tiết kiệm thời gian quý giá và tập trung vào các nhiệm vụ chiến lược quan trọng hơn.