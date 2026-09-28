---
title: "🚀 Tự động hóa tin nhắn WhatsApp ra đi với Baserow & WasenderAPI"
description: "Hướng dẫn tự động gửi tin nhắn WhatsApp ra đi từ Baserow và ghi log vào bảng dữ liệu với n8n Workflow"
slug: "tu-dong-hoa-tin-nhan-whatsapp-ra-di-voi-baserow-wasenderapi"
tags: [n8n, automation, no-code, whatsapp, baserow]
keywords: [n8n workflow, tự động hóa, whatsapp marketing, baserow, wasenderapi]
---

# 🚀 Tự động hóa tin nhắn WhatsApp ra đi với Baserow & WasenderAPI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi tin nhắn WhatsApp ra đi từ Baserow
- Ghi log tin nhắn đã gửi vào bảng dữ liệu
- Tiết kiệm thời gian và công sức thủ công
- Đảm bảo tin nhắn được gửi chính xác và kịp thời
- Theo dõi hiệu quả marketing qua dữ liệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Baserow với bảng 'Contacts' và 'Messages' đã cấu hình
- Tài khoản WasenderAPI với API key
- Tài khoản n8n đã cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Webhook: Baserow Outbound Trigger**: Cấu hình webhook với đường dẫn bất kỳ và phương thức POST.
- **WasenderAPI: Send Outbound Message**: Cấu hình API key và các tham số cần thiết để gửi tin nhắn.
- **Filter: Message Status 'Sent'**: Lọc tin nhắn có trạng thái 'Sent'.
- **Baserow: Confirm Outbound Log**: Cập nhật trạng thái tin nhắn trong Baserow.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi tin nhắn được gửi.
- Lưu log chi tiết hơn để phân tích hiệu quả marketing.
- Gửi báo cáo định kỳ về hiệu quả tin nhắn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình gửi tin nhắn WhatsApp ra đi từ Baserow và ghi log vào bảng dữ liệu. Với workflow này, các sếp có thể tiết kiệm thời gian và công sức thủ công, đảm bảo tin nhắn được gửi chính xác và kịp thời, và theo dõi hiệu quả marketing qua dữ liệu.