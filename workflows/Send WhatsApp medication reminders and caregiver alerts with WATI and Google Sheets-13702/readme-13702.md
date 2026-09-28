---
title: "💊 [Tự động nhắc nhở thuốc qua WhatsApp + Google Sheets] - Giải pháp chăm sóc sức khỏe thông minh"
description: "Hướng dẫn tự động hóa nhắc nhở thuốc qua WhatsApp và cảnh báo cho người chăm sóc bằng n8n, Google Sheets và WATI. Tiết kiệm thời gian, giảm lỗi và nâng cao hiệu quả chăm sóc sức khỏe."
slug: "tu-dong-nhac-nho-thuoc-qua-whatsapp-google-sheets"
tags: [n8n, automation, no-code, whatsapp, chăm sóc sức khỏe]
keywords: [n8n workflow, tự động hóa nhắc nhở thuốc, google sheets, wati, chăm sóc sức khỏe]
---

# 💊 Tự động nhắc nhở thuốc qua WhatsApp + Google Sheets - Giải pháp chăm sóc sức khỏe thông minh

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các gia đình khi quản lý lịch nhắc nhở thuốc thủ công. Giới thiệu workflow như giải pháp tự động hóa hoàn toàn không cần code, kết hợp sức mạnh của Google Sheets và WhatsApp.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian quản lý lịch nhắc nhở thuốc
- Giảm thiểu lỗi nhắc nhở thủ công
- Tăng cường hiệu quả chăm sóc sức khỏe
- Tự động cảnh báo cho người chăm sóc khi có vấn đề
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ
- Tài khoản WATI (đã tích hợp với WhatsApp Business API)
- Danh sách bệnh nhân và lịch nhắc nhở thuốc trong Google Sheets
- Số điện thoại WhatsApp của bệnh nhân và người chăm sóc
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Google Sheets**: Cấu hình credentials và chỉ định ID của Google Sheet chứa danh sách bệnh nhân và lịch nhắc nhở thuốc.
- **WATI**: Cấu hình credentials và thiết lập template tin nhắn nhắc nhở thuốc.
- **Schedule Trigger**: Thiết lập thời gian chạy workflow (ví dụ: mỗi ngày lúc 8:00 AM).
- **Switch**: Cấu hình điều kiện để gửi cảnh báo cho người chăm sóc khi có vấn đề.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có vấn đề
- Lưu log các tin nhắn đã gửi để theo dõi hiệu quả
- Gửi báo cáo hàng tuần về tình trạng nhắc nhở thuốc
- Tích hợp với hệ thống quản lý bệnh nhân để cập nhật thông tin tự động

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình nhắc nhở thuốc và cảnh báo cho người chăm sóc, nâng cao hiệu quả chăm sóc sức khỏe. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi!