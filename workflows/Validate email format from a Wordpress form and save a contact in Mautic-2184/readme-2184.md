---
title: "🚀 Tự động hóa: Kiểm tra định dạng email từ Wordpress và lưu liên hệ vào Mautic"
description: "Hướng dẫn tự động hóa kiểm tra định dạng email từ form Wordpress và lưu liên hệ vào Mautic bằng n8n. Tiết kiệm thời gian và tránh lỗi nhập liệu."
slug: "tu-dong-hoa-kiem-tra-email-wordpress-mautic"
tags: [n8n, automation, no-code, wordpress, mautic]
keywords: [n8n workflow, tự động hóa, kiểm tra email, wordpress, mautic]
---

# 🚀 Tự động hóa: Kiểm tra định dạng email từ Wordpress và lưu liên hệ vào Mautic

[Các sếp đang gặp khó khăn khi xử lý thủ công hàng nghìn liên hệ từ form Wordpress. Với workflow này, các sếp có thể tự động kiểm tra định dạng email và lưu liên hệ vào Mautic một cách chính xác và nhanh chóng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý hàng nghìn liên hệ từ form Wordpress.
- Giảm thiểu lỗi nhập liệu nhờ kiểm tra định dạng email tự động.
- Tích hợp liền mạch với Mautic để quản lý danh sách liên hệ hiệu quả.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Wordpress với form cần xử lý.
- Tài khoản Mautic với API key.
- Kiến thức cơ bản về n8n và cấu hình webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Click vào "Import from URL" và nhập link: [https://n8n.io/workflows/2184](https://n8n.io/workflows/2184)
3. Hoặc copy/paste JSON từ file workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node WordpressForm**:
   - Cấu hình webhook để nhận dữ liệu từ form Wordpress.
   - Đảm bảo đường dẫn (path) là duy nhất và bảo mật.
   - Ví dụ: `path: "917366ee-14a8-4fef-9f0b-6638cdc35fad"`

2. **Node LeadData**:
   - Chỉnh sửa biểu thức để chuẩn hóa dữ liệu từ form Wordpress.
   - Ví dụ: `{{ $json["email"] }}` để lấy email từ dữ liệu đầu vào.

3. **Node CheckEmailValid**:
   - Cấu hình điều kiện kiểm tra định dạng email.
   - Ví dụ: `{{ $node["WordpressForm"].json["email"] }}` phải là một địa chỉ email hợp lệ.

4. **Node CreateContactMautic**:
   - Cấu hình credentials cho Mautic API.
   - Ánh xạ các trường dữ liệu từ Wordpress sang Mautic.
   - Ví dụ: `email: {{ $node["WordpressForm"].json["email"] }}`

5. **Node LeadMauticDNC**:
   - Cấu hình để thêm liên hệ vào danh sách Do Not Contact (DNC) nếu cần.
   - Chọn operation là `editDoNotContactList`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow sau khi đã kiểm tra kỹ.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có liên hệ mới.
- Lưu log các liên hệ đã xử lý để theo dõi hiệu suất.
- Tự động gửi email cảm ơn đến các liên hệ hợp lệ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình kiểm tra và lưu liên hệ từ Wordpress vào Mautic một cách hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao chất lượng quản lý danh sách liên hệ!