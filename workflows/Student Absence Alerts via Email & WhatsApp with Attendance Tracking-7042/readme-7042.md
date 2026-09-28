---
title: "🚨 Hệ thống cảnh báo vắng mặt học sinh qua Email & WhatsApp với theo dõi điểm danh"
description: "Tự động hóa cảnh báo vắng mặt học sinh qua email và WhatsApp với theo dõi điểm danh 30 ngày, giúp giáo viên quản lý hiệu quả tình trạng vắng mặt và nâng cao chất lượng giáo dục."
slug: "he-thong-canh-bao-vang-mat-hoc-sinh"
tags: [n8n, automation, no-code, education, attendance]
keywords: [n8n workflow, tự động hóa giáo dục, theo dõi điểm danh, cảnh báo vắng mặt]
---

# 🚨 Hệ thống cảnh báo vắng mặt học sinh qua Email & WhatsApp với theo dõi điểm danh

[Các sếp giáo viên] có biết không? Việc quản lý điểm danh thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những học sinh vắng mặt thường xuyên. Hãy thử workflow này để tự động hóa cảnh báo vắng mặt qua email và WhatsApp, cùng với theo dõi điểm danh 30 ngày để nâng cao hiệu quả quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý điểm danh thủ công
- Cảnh báo kịp thời về tình trạng vắng mặt
- Theo dõi điểm danh 30 ngày để phân tích xu hướng
- Tăng cường tương tác với phụ huynh qua email và WhatsApp
- Tạo báo cáo điểm danh tự động hàng ngày
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Microsoft Excel (để lưu trữ dữ liệu điểm danh và thông tin liên hệ học sinh)
- Tài khoản email SMTP (để gửi cảnh báo qua email)
- API WhatsApp (để gửi cảnh báo qua WhatsApp)
- Dữ liệu điểm danh hàng ngày được cập nhật vào Excel
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link gốc workflow](https://n8n.io/workflows/7042)
2. Nhấn nút "Download" để tải file JSON về máy
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Daily Attendance Check - 10:30 AM"**: Cấu hình lịch chạy hàng ngày lúc 10:30 AM
- **Node "Read Today's Attendance"**: Cập nhật ID của file Excel chứa dữ liệu điểm danh hàng ngày và tên sheet tương ứng
- **Node "Read Student Contacts"**: Cập nhật ID của file Excel chứa thông tin liên hệ học sinh và tên sheet tương ứng
- **Node "Send Absence Email"**: Cấu hình tài khoản SMTP để gửi email cảnh báo
- **Node "Send Absence WhatsApp"**: Cập nhật API WhatsApp và cấu hình thông số gửi tin nhắn
- **Node "Save Attendance Report"**: Cập nhật ID của file Excel để lưu báo cáo điểm danh hàng ngày và tên sheet tương ứng

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo vắng mặt ngay lập tức
- Lưu log cảnh báo để theo dõi lịch sử vắng mặt
- Gửi báo cáo điểm danh hàng tuần qua email cho các cấp quản lý
- Tích hợp với hệ thống quản lý học sinh khác để cập nhật thông tin tự động

### 📌 Kết luận
Workflow này giúp các sếp giáo viên tự động hóa cảnh báo vắng mặt học sinh, theo dõi điểm danh 30 ngày và tạo báo cáo hàng ngày một cách hiệu quả. Hãy áp dụng ngay để nâng cao chất lượng quản lý và tương tác với phụ huynh!