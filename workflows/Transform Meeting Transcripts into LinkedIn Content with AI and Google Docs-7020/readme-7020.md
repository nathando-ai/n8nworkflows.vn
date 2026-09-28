---
title: "🚀 Tự động hóa chuyển đổi bản ghi cuộc họp thành nội dung LinkedIn bằng AI và Google Docs"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi bản ghi cuộc họp thành nội dung LinkedIn chuyên nghiệp bằng AI và Google Docs, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-chuyen-doi-ban-ghi-cuoc-hop-thanh-noi-dung-linkedin"
tags: [n8n, automation, no-code, LinkedIn, Google Docs]
keywords: [n8n workflow, tự động hóa, LinkedIn, Google Docs, AI]
---

# 🚀 Tự động hóa chuyển đổi bản ghi cuộc họp thành nội dung LinkedIn bằng AI và Google Docs

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải chuyển đổi bản ghi cuộc họp thành nội dung LinkedIn chuyên nghiệp. Quy trình thủ công này tốn thời gian, dễ bị lỗi và không nhất quán. Workflow này giúp tự động hóa toàn bộ quy trình từ phát hiện cuộc họp đến tạo nội dung LinkedIn hoàn chỉnh, giúp các sếp tiết kiệm thời gian và nâng cao hiệu suất làm việc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình từ phát hiện cuộc họp đến tạo nội dung LinkedIn.
- Chính xác: AI phân tích bản ghi cuộc họp và tạo nội dung chuyên nghiệp.
- Cá nhân hóa: Nội dung được tạo phù hợp với giọng điệu và thương hiệu của các sếp.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Calendar để phát hiện cuộc họp.
- Tài khoản Gmail để gửi và nhận email.
- Tài khoản Google Drive để lưu trữ nội dung.
- Tài khoản AI (OpenAI, Anthropic, etc.) để tạo nội dung.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **New Event Started**: Cấu hình Google Calendar Trigger để phát hiện cuộc họp.
- **Wait till Even End**: Cấu hình thời gian chờ sau khi cuộc họp kết thúc.
- **Need Transcript to be Provided**: Cấu hình Gmail để gửi email yêu cầu bản ghi cuộc họp.
- **Personal LinkedIn Generator** và **Company LinkedIn Generator**: Cấu hình AI Agent để tạo nội dung LinkedIn.
- **Create New Folder**: Cấu hình Google Drive để tạo thư mục mới.
- **Create Transcript Doc** và **Create Content Doc**: Cấu hình Google Docs để tạo tài liệu mới.
- **Update Transcript Doc** và **Update Content Doc**: Cấu hình Google Docs để cập nhật tài liệu.
- **Content Results**: Cấu hình Gmail để gửi kết quả nội dung.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có nội dung mới.
- Lưu log các nội dung đã tạo để theo dõi và quản lý.
- Gửi báo cáo định kỳ về số lượng nội dung đã tạo và thời gian tiết kiệm.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình chuyển đổi bản ghi cuộc họp thành nội dung LinkedIn chuyên nghiệp, tiết kiệm thời gian và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để trải nghiệm lợi ích của tự động hóa!