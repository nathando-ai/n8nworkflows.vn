---
title: "📊 Tự động theo dõi điểm danh học sinh qua App di động, Google Sheets và cảnh báo Email"
description: "Hướng dẫn tự động hóa quy trình điểm danh học sinh với n8n: Lưu dữ liệu vào Google Sheets, gửi Email cảnh báo và trả về phản hồi xác nhận cho App di động."
slug: "tu-dong-theo-doi-diem-danh-hoc-sinh-voi-n8n"
tags: [n8n, automation, no-code, google-sheets, email]
keywords: [n8n workflow, tự động hóa điểm danh, điểm danh học sinh, google sheets, email cảnh báo]
---

# 📊 Tự động theo dõi điểm danh học sinh với App di động, Google Sheets và Email cảnh báo

[Các sếp giáo viên] có bao giờ phải mất thời gian ghi chép điểm danh học sinh thủ công? Có bao giờ phải mất công gửi Email cảnh báo cho giáo viên khi có học sinh vắng mặt? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình điểm danh học sinh chỉ với vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian ghi chép điểm danh thủ công
- Dữ liệu điểm danh được lưu tự động vào Google Sheets
- Giáo viên nhận được Email cảnh báo khi có học sinh vắng mặt
- App di động nhận được phản hồi xác nhận ngay lập tức
- Quy trình điểm danh được thực hiện liên tục 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản Email (Gmail, Outlook,...) để gửi cảnh báo
- App di động hoặc hệ thống có thể gửi POST request đến n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/7043](https://n8n.io/workflows/7043)
2. Nhấn nút "Import" để tải xuống file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải xuống

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Student Check-in" (Webhook)**
   - Đảm bảo đường dẫn webhook là `student-checkin` và phương thức là POST
   - Nếu cần thay đổi, hãy cập nhật cả ở phía App di động

2. **Node "Append or update row in sheet" (Google Sheets)**
   - Chọn credentials Google API
   - Điền ID của Google Sheet cần lưu dữ liệu
   - Đảm bảo tên các cột trong Google Sheet phù hợp với dữ liệu đầu vào

3. **Node "Email Teacher" (Email Send)**
   - Chọn credentials SMTP
   - Điền địa chỉ Email người nhận (giáo viên)
   - Tùy chỉnh nội dung Email theo nhu cầu

4. **Node "Format Data" (Set)**
   - Kiểm tra và điều chỉnh các biến trong node này để đảm bảo dữ liệu được định dạng đúng

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra:
   - Dữ liệu có được lưu vào Google Sheets không
   - Email cảnh báo có được gửi đến giáo viên không
   - App di động có nhận được phản hồi xác nhận không
3. Sau khi test thành công, nhấn "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo điểm danh
- Thêm node để lưu log các hoạt động điểm danh
- Tạo báo cáo điểm danh hàng ngày/hàng tuần và gửi tự động
- Kết nối với hệ thống học phí để tự động trừ học phí cho học sinh vắng mặt quá số lần quy định

### 📌 Kết luận
Workflow này giúp các sếp giáo viên tự động hóa hoàn toàn quy trình điểm danh học sinh, tiết kiệm thời gian và giảm thiểu sai sót. Hãy áp dụng ngay để nâng cao hiệu quả quản lý lớp học!