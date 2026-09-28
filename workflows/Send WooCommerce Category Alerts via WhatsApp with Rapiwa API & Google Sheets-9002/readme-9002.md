---
title: "🚀 Tự động gửi thông báo danh mục WooCommerce qua WhatsApp với Rapiwa API & Google Sheets"
description: "Hướng dẫn chi tiết cách tự động gửi thông báo danh mục sản phẩm mới từ WooCommerce đến khách hàng qua WhatsApp bằng n8n, kết hợp với Rapiwa API và Google Sheets để quản lý danh sách liên hệ."
slug: "tu-dong-gui-thong-bao-danh-muc-woocommerce-qua-whatsapp-voi-rapiwa-va-google-sheets"
tags: [n8n, automation, no-code, WooCommerce, WhatsApp, Google Sheets]
keywords: [n8n workflow, tự động hóa, WooCommerce, WhatsApp, Google Sheets, Rapiwa API]
---

# 🚀 Tự động gửi thông báo danh mục WooCommerce qua WhatsApp với Rapiwa API & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi thông báo đến hàng nghìn khách hàng mà không cần can thiệp thủ công.
- Tăng độ chính xác: Chỉ gửi thông báo đến những số điện thoại đã xác thực là số WhatsApp hợp lệ.
- Cá nhân hóa: Tùy chỉnh nội dung thông báo theo từng danh mục sản phẩm mới.
- Quản lý hiệu quả: Lưu trữ danh sách khách hàng đã nhận thông báo và trạng thái của họ trong Google Sheets.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản WooCommerce với quyền truy cập API.
- Tài khoản Rapiwa API với số WhatsApp đã được kết nối và ủy quyền.
- Tài khoản Google Sheets với quyền truy cập ghi dữ liệu.
- Tài khoản WhatsApp (Cá nhân hoặc Doanh nghiệp) đã được kết nối với Rapiwa.
- Dịch vụ Rapiwa.com với gói đăng ký (~$5/tháng) bao gồm quyền truy cập các endpoint `verify-whatsapp` và `send-message`.
- Google Sheets đã được định dạng theo mẫu [sample](https://docs.google.com/spreadsheets/d/1SbBOtdqaA9eUmgv2W4MXU0-TODjHix-IrmQmuapiSJA/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán liên kết sau vào ô nhập liệu:
   ```
   https://n8n.io/workflows/9002
   ```
3. Hoặc, các sếp có thể tải xuống file JSON từ liên kết trên và import trực tiếp từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Webhook**:
  - Đảm bảo cấu hình đúng URL webhook: `https://n8.spagreen.net/webhook-test/1c217a0f-503f-49a4-b0c5-1aa431616177`.
  - Phương thức HTTP: `POST`.

- **WooCommerce API Credentials**:
  - Cấu hình đúng thông tin xác thực WooCommerce API trong n8n.

- **Rapiwa Bearer Auth**:
  - Thêm Bearer Token của Rapiwa vào credentials `httpBearerAuth` trong n8n.

- **Google Sheets OAuth2**:
  - Cấu hình đúng thông tin xác thực Google Sheets OAuth2 trong n8n.

- **Google Sheets**:
  - Đảm bảo Google Sheets đã được định dạng đúng với các cột: `name`, `number`, `email`, `address`, `catagoris`, `description`, `status`.
  - Lưu ý: Cột `name` có dấu cách ở cuối, không được xóa.

- **Format Webhook Response Data**:
  - Kiểm tra và điều chỉnh mã JavaScript trong node này nếu cần thiết để phù hợp với cấu trúc dữ liệu của bạn.

- **Clean Number**:
  - Kiểm tra và điều chỉnh mã JavaScript trong node này để đảm bảo số điện thoại được làm sạch và định dạng đúng.

- **Check valid WhatsApp number Using Rapiwa**:
  - Đảm bảo URL endpoint của Rapiwa là chính xác: `https://app.rapiwa.com/api/verify-whatsapp`.

- **Send Message Using Rapiwa**:
  - Đảm bảo URL endpoint của Rapiwa là chính xác: `https://app.rapiwa.com/api/send-message`.
  - Tùy chỉnh nội dung tin nhắn trong node này theo nhu cầu của bạn.

- **Limit**:
  - Điều chỉnh giá trị giới hạn nếu cần thiết (mặc định là 10 khách hàng).

- **Wait**:
  - Điều chỉnh thời gian chờ nếu cần thiết để tránh bị giới hạn API hoặc Sheets.

#### 3. Kích hoạt ⚡️
- Sau khi đã cấu hình đầy đủ các node, các sếp có thể thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Khi đã kiểm tra và đảm bảo hoạt động ổn định, các sếp có thể bật Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh nội dung tin nhắn**: Các sếp có thể tùy chỉnh nội dung tin nhắn trong node `Send Message Using Rapiwa` để phù hợp với từng danh mục sản phẩm.
- **Thêm thông tin cá nhân hóa**: Sử dụng dữ liệu khách hàng từ WooCommerce để cá nhân hóa nội dung tin nhắn.
- **Tạo các sheet riêng biệt**: Tạo các sheet riêng biệt trong Google Sheets cho từng chiến dịch hoặc danh mục sản phẩm.
- **Kết nối với Slack/Telegram**: Kết nối với các kênh thông báo khác để nhận thông báo khi có lỗi hoặc khi workflow hoàn thành.
- **Lưu log hoạt động**: Lưu log hoạt động của workflow để theo dõi và phân tích hiệu suất.

### 📌 Kết luận
Workflow này cung cấp giải pháp tự động hóa hoàn chỉnh để gửi thông báo danh mục sản phẩm mới từ WooCommerce đến khách hàng qua WhatsApp. Với việc kết hợp Rapiwa API và Google Sheets, các sếp có thể quản lý danh sách liên hệ và theo dõi hiệu quả của các chiến dịch marketing. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả kinh doanh!