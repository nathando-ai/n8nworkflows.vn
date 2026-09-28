---
title: "🚀 Tự động hóa WhatsApp: Tóm tắt nhóm tự động với AI và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc tóm tắt nội dung nhóm WhatsApp hàng ngày bằng n8n, AI và Google Sheets - tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-hoa-tom-tat-nhom-whatsapp-voi-n8n-ai-google-sheets"
tags: [n8n, automation, no-code, whatsapp, google-sheets, ai, langchain]
keywords: [n8n workflow, tự động hóa, whatsapp, google sheets, ai, langchain, tóm tắt nhóm]
---

# 🚀 Tự động hóa WhatsApp: Tóm tắt nhóm tự động với AI và Google Sheets

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải tóm tắt nội dung nhóm WhatsApp hàng ngày? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ việc thu thập tin nhắn đến tạo bản tóm tắt bằng AI và gửi kết quả trực tiếp vào nhóm - mà không cần phải can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và xử lý tin nhắn hàng ngày
- **Tăng hiệu suất**: AI tạo bản tóm tắt chất lượng cao một cách nhanh chóng
- **Cá nhân hóa**: Bản tóm tắt được gửi trực tiếp vào nhóm phù hợp
- **Hoạt động liên tục**: Workflow chạy tự động vào giờ cố định hàng ngày
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WhatsApp Business API (hoặc sử dụng các dịch vụ trung gian như Twilio, 360dialog...)
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key từ OpenAI (hoặc các dịch vụ AI tương tự)
- Google Sheets với 3 tab: `Mensagens`, `Grupos` và `Filtro de Grupos`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/7141
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Webhook**:
   - Cấu hình path: `/resumir_grupos`
   - Phương thức: POST
   - Thêm header `Authorization` với token bảo mật

2. **Node Google Sheets**:
   - Tạo 3 credentials cho Google Sheets API
   - Cấu hình các tham số:
     - Spreadsheet ID: ID của Google Sheet chứa dữ liệu
     - Sheet Name: `Mensagens`, `Grupos` hoặc `Filtro de Grupos` (tùy node)

3. **Node OpenAI**:
   - Cấu hình credentials cho OpenAI API
   - Chọn model: `gpt-4o-mini` (hoặc model khác phù hợp)

4. **Node HTTP Request (WhatsApp)**:
   - Cấu hình credentials cho WhatsApp API
   - Đảm bảo có quyền gửi tin nhắn vào các nhóm

5. **Node Schedule Trigger**:
   - Thiết lập thời gian chạy: 08:00 hàng ngày

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một tin nhắn thử vào nhóm
   - Kiểm tra dữ liệu được lưu vào Google Sheets
   - Xác nhận bản tóm tắt được tạo và gửi đúng thời gian

2. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo khi workflow chạy
- Lưu log hoạt động vào Google Sheets để theo dõi hiệu suất
- Tạo báo cáo hàng tuần từ dữ liệu tóm tắt
- Kết hợp với các công cụ phân tích dữ liệu để đánh giá hiệu suất nhóm

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình tóm tắt nội dung nhóm WhatsApp hàng ngày, từ việc thu thập dữ liệu đến tạo bản tóm tắt và gửi kết quả. Với sự kết hợp của n8n, AI và Google Sheets, các sếp có thể tiết kiệm thời gian quý giá và tập trung vào các nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của nhóm!