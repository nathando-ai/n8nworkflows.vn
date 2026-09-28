---
title: "🚀 Tự động hóa cập nhật trạng thái đơn hàng qua WhatsApp và lưu log vào Google Sheets"
description: "Hướng dẫn chi tiết cách tự động gửi thông báo trạng thái đơn hàng (đã xác nhận, đang giao, đã giao) cho khách hàng qua WhatsApp và lưu lịch sử vào Google Sheets bằng n8n"
slug: "tu-dong-hoa-cap-nhat-trang-thai-don-hang-qua-whatsapp-va-google-sheets"
tags: [n8n, automation, no-code, e-commerce, logistics]
keywords: [n8n workflow, tự động hóa đơn hàng, WhatsApp API, Google Sheets, quản lý đơn hàng]
---

# 🚀 Tự động hóa cập nhật trạng thái đơn hàng qua WhatsApp và lưu log vào Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi thông báo trạng thái đơn hàng thay vì làm thủ công
- **Chính xác 100%**: Không sót đơn hàng nào nhờ hệ thống tự động hóa hoàn chỉnh
- **Cá nhân hóa**: Gửi thông báo phù hợp với từng trạng thái đơn hàng
- **Hoạt động liên tục**: Không ngừng nghỉ, hoạt động 24/7
- **Lưu trữ an toàn**: Tất cả thông báo được lưu lại trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (đã được phê duyệt)
- Google Sheets (để lưu log)
- Hệ thống quản lý đơn hàng có thể gửi webhook
- Instance n8n (cloud hoặc self-hosted)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15622)
2. Click vào nút "Import" và chọn "Import into n8n"
3. Hoặc copy JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook - Order Event** (Node đầu tiên):
   - Đảm bảo đường dẫn webhook là `order-tracking-inbound`
   - Phương thức HTTP: POST
   - Cấu hình webhook URL trong hệ thống quản lý đơn hàng của bạn

2. **Poll Order System** (Node thứ hai):
   - Thiết lập lịch chạy phù hợp với tần suất đơn hàng của bạn
   - Ví dụ: Mỗi 5 phút cho hệ thống nhỏ, mỗi 15 phút cho hệ thống lớn

3. **Prepare Order Context**:
   - Cấu hình các biến cần thiết cho quá trình xử lý đơn hàng
   - Ví dụ: orderId, customerPhone, orderStatus

4. **JS - Detect Order Event**:
   - Chỉnh sửa logic JavaScript để nhận diện các trạng thái đơn hàng
   - Các trạng thái mặc định: confirmed, shipped, out_for_delivery, delivered

5. **Send WhatsApp Message**:
   - Cấu hình credentials cho WhatsApp Business API
   - Thêm các tham số cần thiết: phone_number_id, access_token
   - Chỉnh sửa các mẫu tin nhắn trong node này

6. **Update Google Sheet Tracker**:
   - Thay thế YOUR_SHEET_ID bằng ID thực của Google Sheet
   - Cấu hình phạm vi và tên sheet phù hợp
   - Đảm bảo tài khoản n8n có quyền truy cập vào Google Sheet

7. **Error Handler**:
   - Thiết lập cách xử lý lỗi (gửi email, thông báo Slack...)
   - Cấu hình các thông báo lỗi phù hợp với từng trường hợp

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một webhook mẫu với các trạng thái đơn hàng khác nhau
   - Kiểm tra cả trường hợp thành công và lỗi
2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node gửi thông báo lỗi đến Slack/Telegram
   - Hoặc gửi báo cáo hàng ngày về số lượng đơn hàng đã xử lý

2. **Tích hợp với hệ thống CRM**:
   - Thêm node cập nhật trạng thái đơn hàng trong hệ thống CRM
   - Hoặc lưu trữ thêm thông tin khách hàng

3. **Báo cáo định kỳ**:
   - Thiết lập node gửi báo cáo hàng ngày về số lượng đơn hàng đã xử lý
   - Hoặc báo cáo tuần/tuần về hiệu suất hệ thống

4. **Xử lý đơn hàng hàng loạt**:
   - Thêm node xử lý các đơn hàng có cùng trạng thái
   - Ví dụ: Gửi thông báo hàng loạt cho các đơn hàng đang giao

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình gửi thông báo trạng thái đơn hàng qua WhatsApp và lưu log vào Google Sheets. Với việc tự động hóa này, các sếp có thể tiết kiệm thời gian, giảm lỗi và cung cấp trải nghiệm khách hàng tốt hơn. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh của bạn!