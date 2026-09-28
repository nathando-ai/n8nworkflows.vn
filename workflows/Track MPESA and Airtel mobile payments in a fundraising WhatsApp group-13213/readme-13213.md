---
title: "💰 Theo dõi thanh toán MPESA và Airtel trong nhóm WhatsApp gây quỹ"
description: "Hướng dẫn tự động hóa theo dõi và tổng hợp thanh toán di động trong nhóm WhatsApp gây quỹ bằng n8n. Giảm thiểu công việc thủ công và tránh sai sót trong quá trình ghi nhận."
slug: "theo-doi-thanh-toan-mpesa-airtel-whatsapp"
tags: [n8n, automation, no-code, whatsapp, fundraising]
keywords: [n8n workflow, tự động hóa thanh toán, gây quỹ, mpesa, airtel]
---

# 💰 Theo dõi thanh toán MPESA và Airtel trong nhóm WhatsApp gây quỹ

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các tổ chức gây quỹ khi phải theo dõi thủ công các giao dịch di động trong nhóm WhatsApp. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code để giảm thiểu công việc thủ công và tránh sai sót.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động ghi nhận và phân loại các giao dịch thanh toán từ MPESA và Airtel Money
- Tổng hợp tự động số tiền gây quỹ theo từng nhóm/sender
- Giảm thiểu sai sót trong quá trình ghi nhận thủ công
- Tiết kiệm thời gian quản lý và báo cáo
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Twilio với số điện thoại được kết nối với WhatsApp
- URL webhook có thể truy cập công khai
- Bảng dữ liệu `payment_table` (hoặc sử dụng node SQL cho môi trường sản xuất)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13213](https://n8n.io/workflows/13213)
2. Chọn "Import" và dán JSON vào n8n Editor
3. Hoặc tải file JSON về máy và import từ n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Đảm bảo URL webhook của bạn có dạng: `https://your-domain.com/webhook/mobile-payments`
   - Cấu hình credentials Twilio trong n8n

2. **Node Data Table**:
   - Tạo bảng dữ liệu `payment_table` với các cột: `from`, `to`, `message`, `amount`, `service_provider`
   - Hoặc cấu hình node SQL nếu sử dụng cơ sở dữ liệu thực tế

3. **Node Twilio**:
   - Cấu hình credentials Twilio với Account SID và Auth Token
   - Đảm bảo số điện thoại Twilio đã được kết nối với WhatsApp

4. **Node Code**:
   - Các node `Airtel Money`, `Mpesa` và `Classify Message` chứa logic xử lý tin nhắn
   - Kiểm tra và điều chỉnh regex nếu cần thiết cho các định dạng tin nhắn khác nhau

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu
2. Kiểm tra các node xử lý tin nhắn và tổng hợp
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi có giao dịch mới
- Cấu hình gửi báo cáo định kỳ về tổng số tiền gây quỹ
- Kết hợp với node Google Sheets để lưu trữ dữ liệu
- Thêm chức năng xác nhận giao dịch trước khi ghi nhận

### 📌 Kết luận
Workflow này giúp các tổ chức gây quỹ tự động hóa quy trình theo dõi và tổng hợp thanh toán di động trong nhóm WhatsApp, giảm thiểu công việc thủ công và tránh sai sót. Hãy thử nghiệm ngay và tối ưu hóa theo nhu cầu cụ thể của bạn!