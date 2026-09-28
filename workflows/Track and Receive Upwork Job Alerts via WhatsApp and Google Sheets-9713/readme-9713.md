---
title: "🚀 Tự động theo dõi và nhận thông báo công việc Upwork qua WhatsApp và Google Sheets"
description: "Hướng dẫn tự động hóa việc theo dõi công việc Upwork, lưu dữ liệu vào Google Sheets và nhận thông báo qua WhatsApp - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-theo-doi-cong-viec-upwork-qua-whatsapp-va-google-sheets"
tags: [n8n, automation, no-code, upwork, google-sheets, whatsapp]
keywords: [n8n workflow, tự động hóa, upwork, google sheets, whatsapp]
---

# 🚀 Tự động theo dõi và nhận thông báo công việc Upwork qua WhatsApp và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động theo dõi và lọc thông tin công việc Upwork mà không cần can thiệp thủ công.
- Dữ liệu được lưu trữ: Tất cả thông tin công việc được lưu vào Google Sheets để theo dõi và quản lý.
- Thông báo tức thì: Nhận thông báo qua WhatsApp ngay khi có công việc mới phù hợp với tiêu chí của bạn.
- Tự động hóa hoàn toàn: Không cần viết code, chỉ cần cấu hình một lần và hệ thống sẽ chạy tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập Google Sheets.
- Tài khoản WhatsApp Business API (hoặc số điện thoại được đăng ký với WhatsApp Business API).
- API Key từ RapidAPI để truy cập dữ liệu công việc Upwork.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/9713](https://n8n.io/workflows/9713).
3. Nhấp vào "Import" để tải workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Append or update row in sheet"**:
   - Chọn credentials "googleSheetsOAuth2Api".
   - Điền thông tin Sheet ID và tên Sheet cần lưu dữ liệu.

2. **Node "Send message"**:
   - Chọn credentials "whatsAppApi".
   - Điền số điện thoại nhận thông báo và cấu hình nội dung tin nhắn.

3. **Node "HTTP Request"**:
   - Cấu hình URL và phương thức HTTP để truy cập dữ liệu từ RapidAPI.
   - Điền API Key từ RapidAPI vào phần Headers.

4. **Node "HTTP Request1"**:
   - Cấu hình URL và phương thức HTTP để truy cập dữ liệu từ Upwork.

5. **Node "Edit Fields" và "Edit Fields2"**:
   - Cấu hình các trường dữ liệu cần chỉnh sửa để lọc thông tin công việc.

6. **Node "If"**:
   - Cấu hình điều kiện để lọc thông tin công việc phù hợp với tiêu chí của bạn.

7. **Node "Webhook"**:
   - Cấu hình đường dẫn và phương thức HTTP cho webhook.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút "Execute workflow" để kiểm tra dữ liệu mẫu.
- Sau khi kiểm tra thành công, nhấp vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack hoặc Telegram để nhận thông báo.
- Lưu log các công việc đã được theo dõi.
- Gửi báo cáo định kỳ về các công việc mới được theo dõi.

### 📌 Kết luận
Workflow này giúp các sếp tự động theo dõi và nhận thông báo về các công việc Upwork mới một cách nhanh chóng và hiệu quả. Với việc lưu trữ dữ liệu vào Google Sheets và nhận thông báo qua WhatsApp, các sếp có thể quản lý và theo dõi thông tin công việc một cách dễ dàng và tiện lợi. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu suất làm việc!