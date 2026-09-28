---
title: "📍 [Tự động hóa] Xác thực địa chỉ và tạo ảnh Street View từ Google Maps & Drive"
description: "Workflow n8n giúp xác thực địa chỉ, lấy ảnh Street View từ Google Maps và lưu vào Google Drive một cách tự động, tiết kiệm thời gian và công sức cho các sếp quản lý bất động sản, du lịch hoặc marketing địa điểm."
slug: "tu-dong-hoa-xac-thuc-dia-chi-tao-anh-street-view-google-maps-drive"
tags: [n8n, automation, no-code, google-maps, google-drive]
keywords: [n8n workflow, tự động hóa địa chỉ, ảnh street view, google maps api, lưu ảnh google drive]
---

# 📍 [Tự động hóa] Xác thực địa chỉ và tạo ảnh Street View từ Google Maps & Drive

[Các sếp quản lý bất động sản, du lịch hoặc marketing địa điểm thường phải làm thủ công việc xác thực địa chỉ, lấy ảnh Street View và lưu trữ chúng. Việc này tốn thời gian, dễ sai sót và không thể thực hiện hàng loạt. Workflow này giúp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng loạt địa chỉ trong vài phút thay vì vài giờ làm thủ công.
- **Chính xác cao**: Sử dụng API chính thức của Google Maps để xác thực và lấy ảnh.
- **Tự động lưu trữ**: Ảnh Street View được tự động lưu vào Google Drive của các sếp.
- **Trải nghiệm người dùng tốt**: Hiển thị kết quả trực quan qua trang web.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Maps API Key**: Có quyền truy cập Geocoding API và Street View API.
- **Google Drive API**: Đã kích hoạt Google Drive API và tạo OAuth 2.0 credentials.
- **Tài khoản n8n**: Đã cài đặt và cấu hình n8n trên VPS hoặc máy chủ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/14568).
2. Sao chép nội dung JSON của workflow.
3. Trong n8n Editor, nhấn vào **Import from JSON** và dán nội dung JSON đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "On form submission"**: Đảm bảo form đã được cấu hình đúng với các trường nhập liệu cần thiết.
- **Node "Geocode address" và "Get street view image"**: Cập nhật Google Maps API Key vào credentials.
- **Node "Upload image"**: Cấu hình Google Drive OAuth 2.0 credentials.
- **Node "Prepare API request data"**: Điều chỉnh kích thước ảnh nếu cần (mặc định: 600x400).

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhập địa chỉ mẫu và kiểm tra kết quả.
2. **Bật Active workflow**: Chuyển workflow sang trạng thái Active để sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
- **Lưu log**: Thêm node lưu log các địa chỉ đã xử lý vào Google Sheets.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo tổng hợp các ảnh đã tạo qua email.

### 📌 Kết luận
Workflow này giúp các sếp quản lý địa điểm tự động hóa quy trình xác thực địa chỉ và tạo ảnh Street View một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả công việc!