---
title: "🚀 Tự động theo dõi đơn hàng DHL/Delhivery và thông báo khách hàng qua WhatsApp/Email"
description: "Workflow n8n tự động theo dõi trạng thái đơn hàng từ DHL và Delhivery, cập nhật Google Sheets và thông báo khách hàng qua WhatsApp và email. Giảm thiểu công việc thủ công và tăng cường trải nghiệm khách hàng."
slug: "tu-dong-theo-doi-don-hang-dhl-delhivery-whatsapp-email"
tags: [n8n, automation, logistics, google-sheets, whatsapp]
keywords: [n8n workflow, tự động hóa vận chuyển, theo dõi đơn hàng, thông báo khách hàng]
---

# 🚀 Tự động theo dõi đơn hàng DHL/Delhivery và thông báo khách hàng qua WhatsApp/Email

[Các sếp đang làm việc thủ công theo dõi hàng trăm đơn hàng mỗi ngày? Bị mắc kẹt trong công việc lặp đi lặp lại? Workflow này sẽ giải phóng thời gian của các sếp bằng cách tự động hóa toàn bộ quy trình theo dõi vận chuyển và thông báo khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm thiểu công việc thủ công lên tới 90%
- **Chính xác 100%**: Theo dõi trạng thái đơn hàng theo thời gian thực
- **Trải nghiệm khách hàng**: Cập nhật thông tin vận chuyển kịp thời
- **Hiệu quả hoạt động**: Tự động hóa toàn bộ quy trình vận chuyển
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- API Key từ DHL và Delhivery
- Tài khoản SMTP để gửi email
- Số điện thoại WhatsApp Business API (nếu sử dụng WhatsApp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6650](https://n8n.io/workflows/6650)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Daily Trigger**:
   - Thay đổi thời gian chạy (mặc định 9 AM) trong node Cron
   - Ví dụ: `0 9 * * *` để chạy mỗi ngày lúc 9:00 AM

2. **Get Shipments List**:
   - Cấu hình Google Sheets credentials
   - Điền ID của Google Sheet chứa danh sách đơn hàng
   - Đảm bảo Sheet có các cột: `trackingNumber`, `courier`, `status`, `customerEmail`, `customerPhone`

3. **Track via Delhivery & Track via DHL**:
   - Cấu hình HTTP Header Auth credentials cho cả 2 node
   - Thêm API Key của Delhivery và DHL vào headers
   - Kiểm tra endpoint API của từng dịch vụ vận chuyển

4. **Send WhatsApp Update**:
   - Cấu hình endpoint của WhatsApp Business API
   - Thêm template message ID đã được phê duyệt
   - Đảm bảo số điện thoại khách hàng đã được đăng ký với WhatsApp

5. **Send Email Update**:
   - Cấu hình SMTP credentials
   - Thiết lập email gửi và chủ đề email
   - Tùy chỉnh nội dung email trong node

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở các node cuối cùng (Update Google Sheet, Send WhatsApp Update, Send Email Update)
3. Sau khi test thành công, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack**: Thêm node Slack để nhận thông báo lỗi hoặc trạng thái workflow
2. **Lưu log hoạt động**: Thêm node Database để lưu lịch sử các đơn hàng đã xử lý
3. **Báo cáo định kỳ**: Tạo workflow phụ để tổng hợp báo cáo hàng tuần/tháng
4. **Xử lý lỗi tự động**: Thêm node Error Handling để xử lý các trường hợp ngoại lệ

### 📌 Kết luận
Workflow này đã tự động hóa hoàn toàn quy trình theo dõi vận chuyển và thông báo khách hàng, giúp các sếp tiết kiệm thời gian và tập trung vào các công việc chiến lược hơn. Hãy thử ngay và trải nghiệm sự khác biệt của tự động hóa!