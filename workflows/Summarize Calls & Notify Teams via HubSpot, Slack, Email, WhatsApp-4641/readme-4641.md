---
title: "🚀 Tự động hóa tổng kết cuộc gọi và thông báo cho đội ngũ qua HubSpot, Slack, Email, WhatsApp"
description: "Workflow n8n tự động tổng kết nội dung cuộc gọi, phân loại thông tin và gửi thông báo đến các kênh khác nhau để tăng hiệu quả làm việc cho đội ngũ bán hàng và IT Ops."
slug: "tu-dong-hoa-tong-ket-cuoc-goi-va-thong-bao-doi-ngu"
tags: [n8n, automation, no-code, sales, ai, it-ops]
keywords: [n8n workflow, tự động hóa, tổng kết cuộc gọi, thông báo đội ngũ, ai, sales]
---

# 🚀 Tự động hóa tổng kết cuộc gọi và thông báo cho đội ngũ qua HubSpot, Slack, Email, WhatsApp

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian tổng kết cuộc gọi từ 50% đến 80%.
- Tự động phân loại thông tin quan trọng cho từng bộ phận.
- Tăng tính chính xác và nhất quán trong việc ghi chú cuộc họp.
- Thông báo tức thì đến các kênh khác nhau (Slack, WhatsApp, Email).
- Tích hợp liền mạch với HubSpot để quản lý khách hàng hiệu quả hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để sử dụng LLM cho tổng kết và phân loại).
- Tài khoản Gmail (để gửi email thông báo).
- Tài khoản Slack (để gửi thông báo vào kênh).
- Tài khoản WhatsApp Business Cloud (để gửi thông báo qua WhatsApp).
- Tài khoản HubSpot (để lưu trữ và quản lý thông tin khách hàng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook**: Cấu hình đường dẫn và phương thức HTTP để nhận dữ liệu cuộc gọi.
  - Đường dẫn: `1ffeacc2-1dbd-4a9e-bf3f-6811ddd31642`
  - Phương thức: `POST`

- **OpenAI Chat Model**: Cấu hình API key và chọn mô hình để sử dụng.
  - Mô hình: `gpt-4o-mini`

- **Gmail**: Cấu hình tài khoản Gmail để gửi email thông báo.
  - Đảm bảo đã kích hoạt OAuth2 và cấp quyền cho n8n.

- **Slack**: Cấu hình tài khoản Slack để gửi thông báo vào kênh.
  - Đảm bảo đã kích hoạt OAuth2 và cấp quyền cho n8n.

- **WhatsApp Business Cloud**: Cấu hình tài khoản WhatsApp để gửi thông báo.
  - Đảm bảo đã kích hoạt API và cấp quyền cho n8n.

- **HubSpot Search Client**: Cấu hình tài khoản HubSpot để tìm kiếm thông tin khách hàng.
  - Đảm bảo đã kích hoạt OAuth2 và cấp quyền cho n8n.

- **HubSpot Save Notes**: Cấu hình tài khoản HubSpot để lưu trữ ghi chú cuộc họp.
  - Đảm bảo đã kích hoạt OAuth2 và cấp quyền cho n8n.

- **Define routing emails**: Cấu hình danh sách email của các nhân viên phụ trách để gửi thông báo.
  - Ví dụ: `sales@company.com`, `support@company.com`, `marketing@company.com`

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Google Calendar để tự động tạo lịch hẹn sau cuộc gọi.
- Sử dụng node "Sticky Note" để lưu trữ các ghi chú quan trọng từ cuộc gọi.
- Tích hợp với các công cụ phân tích dữ liệu để theo dõi hiệu suất của đội ngũ bán hàng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình tổng kết cuộc gọi, phân loại thông tin và gửi thông báo đến các kênh khác nhau. Điều này giúp tăng hiệu quả làm việc cho đội ngũ bán hàng và IT Ops. Hãy áp dụng ngay để tiết kiệm thời gian và tăng tính chính xác trong công việc hàng ngày.