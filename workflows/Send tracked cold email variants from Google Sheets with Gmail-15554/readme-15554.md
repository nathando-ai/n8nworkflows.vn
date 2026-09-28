---
title: "📬 Tự động gửi email lạnh đa biến từ Google Sheets với Gmail - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động gửi email lạnh đa biến từ Google Sheets với n8n, theo dõi mở email và tránh gửi trùng lặp. Giải pháp hoàn chỉnh cho các chuyên viên marketing."
slug: "tu-dong-gui-email-lanh-da-bien-tu-google-sheets-voi-gmail"
tags: [n8n, automation, email-marketing, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa email, gửi email lạnh, theo dõi mở email, tránh gửi trùng lặp]
---

# 📬 Tự động gửi email lạnh đa biến từ Google Sheets với Gmail - Workflow n8n hoàn chỉnh

[Các sếp marketing] đang gặp khó khăn khi phải gửi hàng trăm email lạnh thủ công, theo dõi mở email và tránh gửi trùng lặp. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong n8n, tiết kiệm thời gian và tăng hiệu quả tiếp cận khách hàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi email lạnh đa biến từ Google Sheets
- Theo dõi mở email thông qua pixel tracking
- Tránh gửi trùng lặp với cơ chế lọc danh sách
- Tăng hiệu quả tiếp cận khách hàng
- Tiết kiệm thời gian và công sức thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Danh sách liên hệ trong Google Sheets (các cột: email, firstName, companyName)
- Tài khoản n8n đã cài đặt và cấu hình
- Credentials cho Google Sheets và Gmail trong n8n
- Endpoint webhook riêng để theo dõi mở email
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [n8n.io/workflows/15554](https://n8n.io/workflows/15554)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Cấu hình Google Sheets Credential**:
   - Đảm bảo credential có quyền truy cập vào cả hai tab: `Sheet1` (danh sách liên hệ) và `Log Sends` (lịch sử gửi email)
   - Kiểm tra lại tên các cột trong Google Sheets phải khớp với workflow

2. **Cấu hình Gmail Credential**:
   - Đảm bảo tài khoản Gmail đã được "warm up" (không phải tài khoản mới)
   - Cập nhật thông tin người gửi trong các node "Send Variant"

3. **Cập nhật tracking pixel**:
   - Thay thế URL tracking pixel trong các node "Send Variant" bằng endpoint webhook riêng của các sếp
   - URL hiện tại đang trỏ đến endpoint của Voxen: `https://kkks38v7.rpcl.app/webhook/track-open?id=...`

4. **Cập nhật thông tin người gửi**:
   - Tất cả 3 node "Send Variant" đều có chữ ký "Afeez O — Automation Specialist."
   - Các sếp cần thay thế bằng tên và chức danh của mình

5. **Kiểm tra cấu hình Loop node**:
   - Đảm bảo giá trị "Batch Size" được đặt là 1 để tránh gửi email quá nhanh

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Sau khi kiểm tra thành công, kích hoạt workflow bằng cách bật nút "Active" trong n8n Editor

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh các biến thể email**:
   - Các sếp có thể chỉnh sửa nội dung email trong các node "Send Variant" mà không cần thay đổi logic routing

2. **Thay đổi lịch gửi**:
   - Chỉnh sửa biểu thức cron trong node "Schedule Trigger" để thay đổi thời gian gửi email

3. **Điều chỉnh tốc độ gửi**:
   - Thay đổi giá trị thời gian chờ trong node "Wait" để điều chỉnh tốc độ gửi email

4. **Kết hợp với Slack/Telegram**:
   - Thêm node để gửi thông báo khi có email được gửi hoặc mở email

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn chỉnh cho việc tự động gửi email lạnh đa biến từ Google Sheets với n8n. Với các tính năng theo dõi mở email và tránh gửi trùng lặp, các sếp có thể tối ưu hóa chiến dịch tiếp cận khách hàng một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả tiếp cận!