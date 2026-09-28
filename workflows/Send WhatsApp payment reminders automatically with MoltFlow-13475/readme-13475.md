---
title: "💰 Tự động nhắc nhở thanh toán qua WhatsApp hàng ngày với MoltFlow"
description: "Hướng dẫn tự động hóa gửi nhắc nhở thanh toán qua WhatsApp hàng ngày vào lúc 9 AM với n8n và MoltFlow API"
slug: "tu-dong-nhac-nho-thanh-toan-qua-whatsapp-hang-ngay"
tags: [n8n, automation, no-code, whatsapp, payment-reminder]
keywords: [n8n workflow, tự động hóa thanh toán, nhắc nhở qua WhatsApp, MoltFlow API]
---

# 💰 Tự động nhắc nhở thanh toán qua WhatsApp hàng ngày với MoltFlow

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải nhắc nhở khách hàng thanh toán bằng cách thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi nhắc nhở hàng ngày vào lúc 9 AM mà không cần can thiệp thủ công.
- Cá nhân hóa: Mỗi khách hàng nhận được thông báo thanh toán riêng biệt với thông tin chi tiết.
- Chất lượng: Giảm thiểu sai sót do việc nhập tay thông tin.
- Tính nhất quán: Đảm bảo tất cả khách hàng đều nhận được nhắc nhở đúng thời gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản MoltFlow đã kết nối WhatsApp (quét mã QR để xác thực).
- API Key từ MoltFlow (tạo mới trong phần Sessions > API Keys).
- Danh sách khách hàng với thông tin thanh toán (số điện thoại, số tiền, hạn thanh toán...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/13475)
2. Chọn "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Daily 9 AM Trigger"**:
   - Kiểm tra lịch trình đã được đặt đúng vào lúc 9 AM hàng ngày.

2. **Node "Prepare Contacts"**:
   - Chỉnh sửa code để phù hợp với cấu trúc dữ liệu của các sếp.
   - Đảm bảo dữ liệu đầu vào chứa các trường: số điện thoại, số tiền, hạn thanh toán.

3. **Node "Send WhatsApp Reminder"**:
   - Thêm credentials "httpHeaderAuth" với:
     - Name: `X-API-Key`
     - Value: API Key của MoltFlow
   - Kiểm tra URL API đã đúng với endpoint của MoltFlow.

4. **Nodes "Log Success" và "Log Failure"**:
   - Tùy chỉnh code để phù hợp với hệ thống ghi log của các sếp.

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết nối và nội dung tin nhắn.
2. Sau khi xác nhận hoạt động bình thường, bật "Active" cho workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi báo cáo hàng tuần về tỷ lệ nhắc nhở thành công.
- Kết hợp với hệ thống CRM để tự động cập nhật trạng thái thanh toán.
- Tạo phiên bản workflow cho các kênh nhắn tin khác như Telegram hoặc SMS.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình nhắc nhở thanh toán qua WhatsApp, tiết kiệm thời gian và đảm bảo thông tin được gửi đi đúng lúc. Hãy thử ngay để nâng cao trải nghiệm khách hàng và tối ưu hóa quy trình kinh doanh!