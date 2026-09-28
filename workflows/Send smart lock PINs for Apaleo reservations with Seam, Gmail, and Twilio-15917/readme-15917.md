---
title: "🔑 Tự động hóa PIN khóa thông minh cho đặt phòng Apaleo với Seam, Gmail và Twilio"
description: "Hướng dẫn tự động hóa hoàn toàn quá trình tạo và phân phối PIN khóa thông minh cho khách hàng khi đặt phòng qua Apaleo, tiết kiệm thời gian và nâng cao trải nghiệm khách hàng"
slug: "tu-dong-hoa-pin-khoa-thong-minh-apaleo-seam-gmail-twilio"
tags: [n8n, automation, no-code, smart lock, hotel management]
keywords: [n8n workflow, tự động hóa đặt phòng, smart lock PIN, Apaleo, Seam, Gmail, Twilio]
---

# 🔑 Tự động hóa PIN khóa thông minh cho đặt phòng Apaleo với Seam, Gmail và Twilio

[Các sếp khách sạn đang gặp khó khăn khi phải tạo và phân phối PIN khóa thông minh cho từng khách hàng một cách thủ công. Quá trình này tốn thời gian, dễ gây lỗi và không đồng bộ với hệ thống đặt phòng. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình này, từ tạo PIN đến gửi thông báo qua email và SMS.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tạo PIN khóa thông minh cho từng đặt phòng
- Gửi thông báo PIN qua email và SMS đồng thời
- Cập nhật thông tin PIN vào hệ thống Apaleo
- Hoạt động liên tục 24/7 với token tự động refresh
- Tiết kiệm 80% thời gian thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Apaleo với quyền truy cập API
- API key từ Seam cho quản lý khóa thông minh
- Tài khoản Gmail với quyền gửi email
- Tài khoản Twilio với số điện thoại đã xác minh
- Danh sách ánh xạ giữa phòng trong Apaleo và ID khóa trong Seam
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/15917)
2. Click nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On Reservation Unit Assignment"**:
   - Cấu hình credentials Apaleo OAuth2
   - Đảm bảo đã đăng ký sự kiện "reservation unit assignment" trong Apaleo

2. **Node "Retrieve Reservation Details"**:
   - Cấu hình credentials Apaleo OAuth2
   - Kiểm tra operation là "BookingReservationsByIdGet"

3. **Node "Create Access Code on Seam"**:
   - Thêm header Authorization với Bearer token từ Seam
   - Cập nhật URL endpoint của Seam API
   - Kiểm tra payload JSON chứa device_id và các tham số khác

4. **Node "Link Room to Lock Code"**:
   - Chỉnh sửa danh sách ánh xạ giữa phòng Apaleo và ID khóa Seam
   - Đảm bảo logic ánh xạ chính xác

5. **Node "Add PIN to Reservation Note"**:
   - Cấu hình credentials Apaleo OAuth2
   - Kiểm tra operation là "BookingReservationsByIdPatch"
   - Cập nhật format ghi chú PIN trong payload

6. **Node "Retrieve Customer Contact Info"**:
   - Thêm header Authorization với Bearer token từ Apaleo
   - Cập nhật URL endpoint để lấy thông tin liên hệ khách hàng

7. **Node "Deliver PIN via Gmail"**:
   - Cấu hình credentials Gmail OAuth2
   - Chỉnh sửa template email với thông tin PIN và hướng dẫn sử dụng

8. **Node "Send PIN using Twilio"**:
   - Cấu hình credentials Twilio API
   - Chỉnh sửa template tin nhắn với thông tin PIN

9. **Node "When Triggered Every 58 Minutes"**:
   - Đặt thời gian chạy phù hợp (58 phút là giá trị mặc định)

10. **Node "Obtain Apaleo Access Token"**:
    - Cập nhật URL endpoint và payload để lấy token mới
    - Thêm header Authorization với Basic Auth từ Apaleo

11. **Node "Update API Credential Information"**:
    - Cấu hình credentials n8n API và httpBearerAuth
    - Cập nhật URL của n8n instance
    - Kiểm tra ID của credential cần cập nhật

#### 3. Kích hoạt ⚡️
1. Chạy test với một đặt phòng mẫu để kiểm tra toàn bộ chuỗi hoạt động
2. Kiểm tra email và SMS được gửi đến khách hàng
3. Xác nhận thông tin PIN đã được cập nhật trong hệ thống Apaleo
4. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node Slack để thông báo khi có lỗi xảy ra trong quá trình tự động hóa
2. Tích hợp với hệ thống CRM để lưu trữ lịch sử giao dịch PIN
3. Thêm chức năng xác thực hai yếu tố cho quá trình nhận PIN
4. Tự động hóa báo cáo hàng ngày về số lượng PIN đã tạo và phân phối

### 📌 Kết luận
Workflow này sẽ giúp các sếp khách sạn tự động hóa hoàn toàn quá trình quản lý PIN khóa thông minh, nâng cao trải nghiệm khách hàng và giảm thiểu rủi ro lỗi. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả kinh doanh!