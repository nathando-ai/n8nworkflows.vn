---
title: "🚀 Tự động hóa Marketing WhatsApp với Google Sheets và Meta Templates"
description: "Hướng dẫn chi tiết cách tự động gửi tin nhắn WhatsApp hàng loạt từ Google Sheets sử dụng Meta Templates với n8n. Tiết kiệm thời gian và cá nhân hóa nội dung marketing."
slug: "tu-dong-hoa-marketing-whatsapp-google-sheets-meta-templates"
tags: [n8n, automation, no-code, whatsapp, marketing]
keywords: [n8n workflow, tự động hóa marketing, whatsapp marketing, google sheets, meta templates]
---

# 🚀 Tự động hóa Marketing WhatsApp với Google Sheets và Meta Templates

[Các sếp đang gặp khó khăn khi phải gửi hàng loạt tin nhắn WhatsApp thủ công cho khách hàng. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ lấy dữ liệu đến gửi tin nhắn cá nhân hóa một cách nhanh chóng và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi gửi hàng loạt tin nhắn
- Cá nhân hóa nội dung tin nhắn cho từng khách hàng
- Tự động hóa toàn bộ quy trình marketing WhatsApp
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tăng độ chính xác và giảm lỗi khi gửi tin nhắn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Meta Developer (với WhatsApp Business API đã cấu hình)
- Tài khoản Google Sheets với danh sách liên hệ (số điện thoại, tên đầy đủ, URL hình ảnh)
- Tài khoản n8n Data Table với cấu trúc cột: template_name, language_code, components_structure, template_id, status, category
- Token truy cập WhatsApp vĩnh viễn
- ID WABA (WhatsApp Business Account)
- ID số điện thoại WhatsApp
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập URL: https://n8n.io/workflows/9553
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Templates from Meta"**:
   - Thêm ID WABA của bạn vào URL trong node này
   - Kết nối credential "whatsAppApi" và "httpHeaderAuth"

2. **Node "Get Contacts from Google Sheet"**:
   - Kết nối credential "googleSheetsOAuth2Api"
   - Cập nhật ID Google Sheet của bạn
   - Đảm bảo Google Sheet có cấu trúc: Phone Number, Full Name, Marketing Image URL

3. **Node "Send WhatsApp Message"**:
   - Thêm ID số điện thoại WhatsApp của bạn vào URL
   - Kết nối credential "httpHeaderAuth"

4. **Node "Get Template Structure from Table"**:
   - Cập nhật ID Data Table của bạn
   - Đảm bảo Data Table có cấu trúc cột như đã nêu

5. **Node "API: Get Templates for Frontend"**:
   - Lưu ý URL webhook này sẽ được sử dụng trong dashboard frontend

#### 3. Kích hoạt ⚡️
1. Chạy Flow 2 (bắt đầu từ "Sync Daily") một lần để đồng bộ tất cả các template đã được phê duyệt từ Meta vào Data Table
2. Kiểm tra API endpoint bằng cách truy cập URL từ node "API: Get Templates for Frontend"
3. Gửi yêu cầu test đến webhook "Trigger: Send Broadcast" với body JSON: {"templateName": "your_template_name"}
4. Kiểm tra WhatsApp để xác nhận tin nhắn đã được gửi thành công
5. Kích hoạt tất cả các phần của workflow

### ✍️ Mẹo & gợi ý nâng cao
1. Tích hợp với Slack/Telegram để nhận thông báo khi gửi tin nhắn thành công/lỗi
2. Thêm node để lưu log các tin nhắn đã gửi vào Google Sheets
3. Tự động gửi báo cáo hàng ngày về số lượng tin nhắn đã gửi
4. Thêm chức năng kiểm tra trạng thái tin nhắn (đã đọc/chưa đọc) từ Meta API

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa marketing WhatsApp. Bằng cách kết hợp Google Sheets và Meta Templates, các sếp có thể gửi hàng loạt tin nhắn cá nhân hóa một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tối ưu hóa chiến dịch marketing của bạn!