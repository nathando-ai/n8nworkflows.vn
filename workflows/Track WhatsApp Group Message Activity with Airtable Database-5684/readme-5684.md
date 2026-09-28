---
title: "🚀 Theo dõi hoạt động tin nhắn WhatsApp và lưu vào Airtable - Workflow n8n"
description: "Tự động hóa việc theo dõi và đếm số lượng tin nhắn trong nhóm WhatsApp, lưu dữ liệu vào Airtable để quản lý và phân tích hoạt động người dùng một cách hiệu quả."
slug: "theo-doi-hoat-dong-whatsapp-airtable"
tags: [n8n, automation, no-code, whatsapp, airtable]
keywords: [n8n workflow, tự động hóa, whatsapp, airtable, quản lý hoạt động]
---

# 🚀 Theo dõi hoạt động tin nhắn WhatsApp và lưu vào Airtable - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa việc theo dõi và đếm số lượng tin nhắn trong nhóm WhatsApp.
- Lưu dữ liệu vào Airtable để quản lý và phân tích hoạt động người dùng một cách hiệu quả.
- Tiết kiệm thời gian và công sức cho việc quản lý hoạt động nhóm.
- Tăng tính minh bạch và công bằng trong việc trao giải thưởng hoặc khuyến khích hoạt động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp và Whapi (WhatsApp API) để nhận webhook tin nhắn.
- Tài khoản Airtable để lưu trữ và quản lý dữ liệu.
- API keys hoặc credentials cho Whapi và Airtable.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Webhook**: Cấu hình webhook từ Whapi để nhận tin nhắn. Đảm bảo đường dẫn và phương thức HTTP là POST.
- **Nachricht? (IF)**: Cấu hình điều kiện để kiểm tra xem tin nhắn có đến từ nhóm WhatsApp mong muốn hay không.
- **Suche nach WA_ID (Airtable)**: Cấu hình để tìm kiếm bản ghi người dùng trong Airtable bằng WhatsApp ID.
- **+1 (Code)**: Viết mã để tăng số lượng tin nhắn lên 1.
- **Airtable Update**: Cấu hình để cập nhật số lượng tin nhắn và thời gian tương tác cuối cùng trong Airtable.
- **Switch**: Cấu hình để kiểm tra loại tin nhắn (text, emoji, voice, image).

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có người dùng mới hoặc khi đạt được số lượng tin nhắn nhất định.
- Lưu log hoạt động để theo dõi và phân tích hiệu suất của nhóm.
- Gửi báo cáo định kỳ về hoạt động của nhóm WhatsApp để quản lý và khuyến khích người dùng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi và quản lý hoạt động trong nhóm WhatsApp một cách hiệu quả. Bằng cách lưu dữ liệu vào Airtable, các sếp có thể dễ dàng quản lý và phân tích hoạt động người dùng, từ đó đưa ra các quyết định và khuyến khích hoạt động một cách minh bạch và công bằng. Hãy áp dụng ngay để tiết kiệm thời gian và công sức cho việc quản lý nhóm WhatsApp của bạn!