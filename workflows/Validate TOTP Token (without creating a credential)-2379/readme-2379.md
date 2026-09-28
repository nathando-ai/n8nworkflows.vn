---
title: "🔐 Hướng dẫn tự động hóa xác thực TOTP trong n8n (không cần tạo credentials)"
description: "Học cách tự động xác thực mã TOTP trong n8n mà không cần tạo credentials. Giải pháp hoàn hảo cho hệ thống xác thực hai yếu tố (2FA) trong các ứng dụng doanh nghiệp."
slug: "huong-dan-xac-thuc-totp-trong-n8n"
tags: [n8n, automation, no-code, 2FA, authentication]
keywords: [n8n workflow, tự động hóa, xác thực TOTP, 2FA, hệ thống xác thực]
---

# 🔐 Hướng dẫn tự động hóa xác thực TOTP trong n8n (không cần tạo credentials)

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải tự động hóa quá trình xác thực mã TOTP (Time-based One-Time Password) trong các hệ thống xác thực hai yếu tố (2FA). Thông thường, các sếp phải tự viết code hoặc sử dụng các công cụ phức tạp để thực hiện việc này. Tuy nhiên, với workflow này, các sếp có thể dễ dàng xác thực mã TOTP mà không cần tạo credentials, chỉ với vài bước đơn giản trong n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần viết code để xác thực TOTP.
- Chính xác: Đảm bảo mã TOTP được xác thực chính xác.
- Cá nhân hóa: Dễ dàng tích hợp với các hệ thống xác thực 2FA khác.
- Hoạt động liên tục: Workflow chạy tự động 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản n8n đã được cài đặt và cấu hình.
- Biết cách sử dụng cơ bản của n8n.
- Có sẵn TOTP secret và mã TOTP để kiểm tra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/2379](https://n8n.io/workflows/2379).
3. Nhấn "OK" để hoàn tất quá trình import.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **TOTP VALIDATION**: Node này chứa mã JavaScript để xác thực mã TOTP. Các sếp cần chỉnh sửa dòng 39 và 40 của node này với các giá trị phù hợp cho hệ thống của mình. Ví dụ:
  ```javascript
  const secret = $input.all()[0].json.secret;
  const code = $input.all()[0].json.code;
  ```

- **EXAMPLE FIELDS**: Node này chứa các trường dữ liệu mẫu để kiểm tra workflow. Các sếp có thể chỉnh sửa các giá trị này để phù hợp với hệ thống của mình.

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Các sếp có thể định nghĩa một số giá trị mẫu trong node "EXAMPLE FIELDS" và nhấn "Test Workflow" để kiểm tra xem workflow có hoạt động đúng không.
- **Bật Active workflow**: Sau khi kiểm tra và đảm bảo workflow hoạt động đúng, các sếp có thể bật workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm các node để gửi thông báo qua Slack hoặc Telegram khi mã TOTP được xác thực thành công hoặc thất bại.
- **Lưu log**: Các sếp có thể thêm các node để lưu log các lần xác thực TOTP để theo dõi và phân tích.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về các lần xác thực TOTP thành công hoặc thất bại.

### 📌 Kết luận
Workflow này cung cấp một giải pháp đơn giản và hiệu quả để tự động hóa quá trình xác thực TOTP trong n8n mà không cần tạo credentials. Với các bước cấu hình đơn giản và linh hoạt, các sếp có thể dễ dàng tích hợp workflow này vào các hệ thống xác thực 2FA của mình. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao tính chính xác của hệ thống xác thực của bạn!