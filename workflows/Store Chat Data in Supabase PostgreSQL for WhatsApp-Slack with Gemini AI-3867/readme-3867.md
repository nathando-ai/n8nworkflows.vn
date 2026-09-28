```yaml
---
title: "🚀 Tự động lưu trữ dữ liệu chat WhatsApp-Slack vào Supabase PostgreSQL với AI Gemini"
description: "Hướng dẫn tự động hóa lưu trữ và xử lý dữ liệu chat giữa WhatsApp và Slack vào cơ sở dữ liệu Supabase PostgreSQL với AI Gemini của Google"
slug: "tu-dong-luu-tru-du-lieu-chat-whatsapp-slack-supabase-gemini"
tags: [n8n, automation, no-code, supabase, postgresql, ai, gemini]
keywords: [n8n workflow, tự động hóa, supabase, postgresql, ai, gemini, chatbot]
---
```

# 🚀 Tự động lưu trữ dữ liệu chat WhatsApp-Slack vào Supabase PostgreSQL với AI Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý dữ liệu chat giữa các nền tảng khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động lưu trữ dữ liệu chat giữa WhatsApp và Slack vào cơ sở dữ liệu Supabase PostgreSQL
- Sử dụng AI Gemini của Google để phân tích và xử lý dữ liệu chat
- Tiết kiệm thời gian và công sức cho việc quản lý dữ liệu chat
- Tăng cường khả năng xử lý và phản hồi với dữ liệu chat
- Dễ dàng mở rộng và tích hợp với các hệ thống khác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API key cho Google Gemini
- Tài khoản Supabase với thông tin kết nối PostgreSQL
- Dữ liệu mẫu để test workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **When clicking ‘Test workflow’**: Node này dùng để test workflow. Các sếp có thể bỏ qua nếu không cần test.
- **Set sample Input Variables**: Node này dùng để thiết lập các biến đầu vào mẫu. Các sếp cần chỉnh sửa các biến này theo dữ liệu thực tế.
- **GeminiFlash2.0**: Node này dùng để kết nối với AI Gemini của Google. Các sếp cần cung cấp API key của Google Cloud.
- **Supabase Postgres Database**: Node này dùng để kết nối với cơ sở dữ liệu Supabase PostgreSQL. Các sếp cần cung cấp thông tin kết nối của Supabase.
- **Update additonal Values e.g. Name, Address ...**: Node này dùng để cập nhật các giá trị bổ sung vào cơ sở dữ liệu. Các sếp cần chỉnh sửa các giá trị này theo dữ liệu thực tế.
- **Sample Agent**: Node này dùng để xử lý dữ liệu chat. Các sếp có thể bỏ qua nếu không cần xử lý dữ liệu chat.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các hệ thống khác như Slack, Telegram để nhận thông báo khi có dữ liệu mới.
- Lưu log dữ liệu chat để theo dõi và phân tích.
- Gửi báo cáo định kỳ về dữ liệu chat.

### 📌 Kết luận
Workflow này giúp các sếp tự động lưu trữ và xử lý dữ liệu chat giữa WhatsApp và Slack vào cơ sở dữ liệu Supabase PostgreSQL với AI Gemini của Google. Các sếp có thể dễ dàng mở rộng và tích hợp với các hệ thống khác để tăng cường khả năng xử lý và phản hồi với dữ liệu chat.