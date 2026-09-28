---
title: "🔗 Tạo URL rút gọn với TinyURL qua Webhook - Tự động hóa 100% không code"
description: "Hướng dẫn chi tiết cách tự động rút gọn URL với TinyURL qua webhook trong n8n. Giải phóng thời gian và nâng cao hiệu quả marketing với workflow đơn giản, dễ triển khai."
slug: "tao-url-rut-gon-tinyurl-qua-webhook"
tags: [n8n, automation, no-code, marketing, api]
keywords: [n8n workflow, tự động hóa marketing, rút gọn URL, TinyURL, webhook]
---

# 🔗 Tạo URL rút gọn với TinyURL qua Webhook - Tự động hóa 100% không code

[Các sếp marketing] chắc hẳn đã từng gặp tình trạng này: phải liên tục rút gọn các URL dài, đặc biệt là khi làm việc với nhiều liên kết khác nhau. Việc này không chỉ tốn thời gian mà còn dễ gây lỗi khi phải làm thủ công. Với workflow này, các sếp có thể tự động rút gọn bất kỳ URL nào chỉ với một webhook đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động rút gọn URL chỉ với một webhook, không cần can thiệp thủ công.
- **Chính xác cao**: Loại bỏ lỗi do nhập liệu thủ công.
- **Tích hợp dễ dàng**: Kết nối với các hệ thống khác thông qua webhook.
- **Hoạt động liên tục**: Workflow chạy 24/7, không bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản TinyURL**: Đăng ký và lấy API token từ [TinyURL](https://tinyurl.com/app).
- **n8n Editor**: Đã cài đặt và cấu hình sẵn n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào **Import from URL** và dán link sau: [https://n8n.io/workflows/4595](https://n8n.io/workflows/4595).
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/4595) và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Receive Link Webhook"**:
  - Đảm bảo đường dẫn `path` là `shorten-link` và phương thức `httpMethod` là `POST`.
  - Ví dụ: `http://your-n8n-instance.com/webhook/shorten-link`.

- **Node "Create TinyURL"**:
  - Thêm credentials cho TinyURL API.
  - Cấu hình các tham số bắt buộc:
    - `api_token`: API token của bạn từ TinyURL.
    - `url`: URL cần rút gọn (được truyền từ webhook).
  - Các tham số tùy chọn:
    - `domain`: Domain tùy chỉnh (nếu có).
    - `alias`: Alias tùy chỉnh cho URL rút gọn.
    - `description`: Mô tả cho URL rút gọn.

- **Node "Respond with Shortened URL"**:
  - Đảm bảo node này được kết nối với node "Create TinyURL".
  - Node này sẽ trả về URL rút gọn cho người gọi webhook.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Gửi một yêu cầu POST đến webhook với body JSON như sau:
     ```json
     {
       "api_token": "your_api_token",
       "url": "https://example.com/very-long-url"
     }
     ```
   - Kiểm tra kết quả trả về từ webhook.

2. **Bật Active workflow**:
   - Sau khi kiểm tra thành công, nhấn vào nút **Activate** để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu log**: Thêm node để lưu log các URL đã rút gọn vào Google Sheets hoặc cơ sở dữ liệu.
- **Gửi thông báo**: Kết nối với Slack hoặc Telegram để thông báo khi có URL mới được rút gọn.
- **Tích hợp với các công cụ khác**: Kết nối với các công cụ khác như Mailchimp, HubSpot để tự động gửi URL rút gọn trong email marketing.

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động rút gọn URL với TinyURL chỉ với một webhook đơn giản. Với việc tích hợp dễ dàng và hoạt động liên tục, các sếp có thể tiết kiệm thời gian và nâng cao hiệu quả marketing một cách đáng kể. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!