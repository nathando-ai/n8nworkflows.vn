---
title: "🚀 Tự động chuyển tin nhắn WhatsApp sang Chatwoot với hỗ trợ media"
description: "Hướng dẫn tự động hóa chuyển tin nhắn WhatsApp sang Chatwoot với hỗ trợ media (ảnh, video, âm thanh) bằng n8n. Giải pháp tiết kiệm thời gian và nâng cao trải nghiệm khách hàng."
slug: "tu-dong-chuyen-tin-nhan-whatsapp-sang-chatwoot-voi-ho-tro-media"
tags: [n8n, automation, no-code, whatsapp, chatwoot, customer support]
keywords: [n8n workflow, tự động hóa, chatwoot, whatsapp, customer support]
---

# 🚀 Tự động chuyển tin nhắn WhatsApp sang Chatwoot với hỗ trợ media

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý tin nhắn WhatsApp và Chatwoot thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển tin nhắn WhatsApp sang Chatwoot với đầy đủ nội dung và media (ảnh, video, âm thanh)
- Tiết kiệm thời gian xử lý thủ công lên tới 90%
- Nâng cao trải nghiệm khách hàng với phản hồi nhanh chóng
- Hỗ trợ quản lý cuộc trò chuyện một cách hiệu quả
- Tự động tạo liên hệ và cuộc trò chuyện mới trong Chatwoot khi nhận tin nhắn mới
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (Evolution API)
- Tài khoản Chatwoot
- Redis server để lưu trữ trạng thái tin nhắn
- PostgreSQL database để lưu trữ thông tin cuộc trò chuyện
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/6988](https://n8n.io/workflows/6988)
2. Click vào nút "Download" để tải file JSON workflow
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When Executed by Another Workflow"**:
   - Cấu hình để nhận dữ liệu từ Evolution API webhook
   - Đảm bảo workflow này được kích hoạt khi có tin nhắn mới từ WhatsApp

2. **Node "REDIS - EVOLUTION MSG - GET/SET"**:
   - Cấu hình credentials Redis
   - Đặt tên key phù hợp với môi trường của bạn (ví dụ: `evolution_msg_<your_prefix>`)

3. **Node "EVOLUTION - GET FILE"**:
   - Cấu hình credentials Evolution API
   - Đảm bảo API key có quyền truy cập vào media của tin nhắn

4. **Node "SEND CHATWOOT FILE"**:
   - Cấu hình credentials Chatwoot API
   - Đặt URL endpoint đúng với phiên bản Chatwoot của bạn

5. **Node "LOAD CONTACT"**:
   - Cấu hình credentials Chatwoot API
   - Đảm bảo API key có quyền truy cập vào tài nguyên Contacts

6. **Node "CREATE CONTACT"**:
   - Cấu hình credentials Chatwoot API
   - Đảm bảo API key có quyền tạo mới liên hệ

7. **Node "CREATE CONVERSATION"**:
   - Cấu hình credentials Chatwoot API
   - Đảm bảo API key có quyền tạo mới cuộc trò chuyện

8. **Node "SEND INCOMING/OUTGOING MESSAGE"**:
   - Cấu hình credentials Chatwoot API
   - Đảm bảo API key có quyền gửi tin nhắn

9. **Node "Get Conversations"**:
   - Cấu hình credentials PostgreSQL
   - Tạo bảng `conversations` với cấu trúc phù hợp (id, contact_id, conversation_id, etc.)

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu từ Evolution API webhook
2. Kiểm tra các node quan trọng để đảm bảo dữ liệu được xử lý đúng
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node gửi thông báo đến Slack/Telegram khi có tin nhắn mới
2. Tích hợp với Google Sheets để lưu trữ log các tin nhắn
3. Thêm node xử lý tin nhắn tự động với LLM (Language Model)
4. Tạo báo cáo hàng ngày về số lượng tin nhắn được xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình chuyển tin nhắn WhatsApp sang Chatwoot một cách hiệu quả. Bằng cách áp dụng workflow này, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao trải nghiệm khách hàng với phản hồi nhanh chóng và chính xác. Hãy thử ngay và trải nghiệm sự khác biệt!