---
title: "🚀 Tự động hóa quản lý khách hàng tiềm năng: Gửi thông tin liên hệ từ website đến WhatsApp & Google Sheets"
description: "Hướng dẫn tự động hóa quy trình quản lý khách hàng tiềm năng bằng n8n. Tự động gửi thông tin liên hệ đến WhatsApp và lưu vào Google Sheets để không bỏ lỡ bất kỳ khách hàng nào."
slug: "tu-dong-hoa-quan-ly-khach-hang-tiem-nang-whatsapp-google-sheets"
tags: [n8n, automation, no-code, lead generation, google sheets, whatsapp]
keywords: [n8n workflow, tự động hóa, quản lý khách hàng tiềm năng, google sheets, whatsapp]
---

# 🚀 Tự động hóa quản lý khách hàng tiềm năng: Gửi thông tin liên hệ từ website đến WhatsApp & Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi và quản lý thông tin liên hệ từ website một cách thủ công. Với workflow này, các sếp có thể tự động hóa quy trình này hoàn toàn, không cần viết code. Hệ thống sẽ tự động gửi thông tin liên hệ đến WhatsApp và lưu vào Google Sheets, giúp các sếp không bỏ lỡ bất kỳ khách hàng tiềm năng nào.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công thông tin liên hệ từ website.
- **Chính xác**: Dữ liệu được xử lý và lưu trữ một cách chính xác và đầy đủ.
- **Cá nhân hóa**: Thông tin liên hệ được gửi đến WhatsApp với định dạng dễ đọc và tiện lợi.
- **Hoạt động liên tục**: Hệ thống hoạt động 24/7, không bỏ lỡ bất kỳ thông tin liên hệ nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo một bảng tính với các cột: date, name, email, phone, service, message.
- **WhatsApp API**: Cần có tài khoản WhatsApp Business API và số điện thoại ID.
- **Website Form**: Form liên hệ trên website phải gửi dữ liệu dưới dạng POST với các trường: name, email, phone, service, message.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/7424](https://n8n.io/workflows/7424).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Contact Form Trigger (Webhook)**:
  - Cấu hình path: `/get_data`.
  - Phương thức HTTP: `POST`.
  - Copy webhook URL và thêm vào form liên hệ trên website.

- **Format Lead Data (Code)**:
  - Node này sẽ xử lý dữ liệu đầu vào từ form liên hệ, đảm bảo dữ liệu được sạch và định dạng đúng.
  - Các sếp có thể chỉnh sửa mã JavaScript trong node này để phù hợp với yêu cầu của mình.

- **WhatsApp Alert (WhatsApp)**:
  - Cấu hình credentials: `whatsAppApi`.
  - Thêm số điện thoại của mình vào trường `Phone`.
  - Thêm `Phone Number ID` từ WhatsApp Business API vào trường tương ứng.

- **Log to Database (Google Sheets)**:
  - Cấu hình credentials: `googleSheetsOAuth2Api`.
  - Thêm `Spreadsheet ID` của bảng tính Google Sheets vào trường tương ứng.
  - Đảm bảo bảng tính có các cột: date, name, email, phone, service, message.

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Trước khi kích hoạt workflow, các sếp nên test run với dữ liệu mẫu để đảm bảo hệ thống hoạt động đúng.
- **Bật Active workflow**: Sau khi cấu hình xong, các sếp có thể bật workflow để hệ thống bắt đầu hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm node để gửi thông báo đến Slack hoặc Telegram khi có thông tin liên hệ mới.
- **Lưu log**: Các sếp có thể lưu log các hoạt động của workflow để theo dõi và phân tích hiệu suất.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về số lượng thông tin liên hệ đã nhận được.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình quản lý khách hàng tiềm năng một cách hiệu quả. Với việc gửi thông tin liên hệ đến WhatsApp và lưu vào Google Sheets, các sếp có thể không bỏ lỡ bất kỳ khách hàng nào và quản lý thông tin một cách dễ dàng. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!