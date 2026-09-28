---
title: "🚀 Theo dõi điểm danh học sinh bằng iOS, Google Sheets & Thông báo Email"
description: "Tự động hóa điểm danh học sinh thông qua iOS Shortcut, Google Sheets và thông báo email tự động. Giảm thiểu công việc thủ công và tăng độ chính xác."
slug: "theo-doi-diem-danh-hoc-sinh-ios-google-sheets-email"
tags: [n8n, automation, no-code, ios, google-sheets, email]
keywords: [n8n workflow, tự động hóa điểm danh, iOS Shortcut, Google Sheets, email thông báo]
---

# 🚀 Theo dõi điểm danh học sinh bằng iOS, Google Sheets & Thông báo Email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các trường học khi quản lý điểm danh thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 30% thời gian quản lý điểm danh thủ công
- Giảm thiểu lỗi điểm danh do con người
- Theo dõi thời gian đến trường của học sinh
- Nhận thông báo email tự động khi học sinh đến trường
- Lưu trữ dữ liệu điểm danh trên Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (để sử dụng Google Sheets API)
- Tài khoản email SMTP (để gửi thông báo)
- Ứng dụng iOS Shortcut được cấu hình để gửi dữ liệu vị trí
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7044](https://n8n.io/workflows/7044)
2. Click vào nút "Import" trên trang workflow
3. Trong n8n Editor, chọn "Import from URL" và dán link workflow
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Location Update Webhook** (Node webhook):
   - Đảm bảo đường dẫn "student-location" là duy nhất và không bị trùng lặp
   - Giữ phương thức HTTP là POST

2. **Log School Arrival** (Node httpRequest):
   - Cấu hình Google Sheets OAuth2 API credentials
   - Thay đổi ID của Google Sheet đích
   - Đảm bảo tài khoản có quyền ghi dữ liệu vào sheet

3. **Notify Teacher** và **Notify Parent** (Node emailSend):
   - Cấu hình SMTP credentials
   - Thay đổi địa chỉ email người nhận
   - Tùy chỉnh nội dung email theo nhu cầu

4. **Student Arrived?** và **At School?** (Node if):
   - Điều chỉnh điều kiện kiểm tra vị trí học sinh
   - Có thể thay đổi tọa độ hoặc bán kính kiểm tra

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một yêu cầu POST đến webhook với dữ liệu mẫu
   - Kiểm tra kết quả trên Google Sheets và hộp thư email

2. Bật Active workflow:
   - Chọn workflow trong danh sách
   - Click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo tức thì
- Thêm node để lưu log hoạt động của workflow
- Tạo báo cáo hàng ngày về tình trạng điểm danh
- Kết nối với hệ thống quản lý học sinh khác

### 📌 Kết luận
Workflow này giúp các trường học tự động hóa quy trình điểm danh học sinh, giảm thiểu công việc thủ công và tăng độ chính xác. Hãy áp dụng ngay để nâng cao hiệu quả quản lý trường học của bạn!