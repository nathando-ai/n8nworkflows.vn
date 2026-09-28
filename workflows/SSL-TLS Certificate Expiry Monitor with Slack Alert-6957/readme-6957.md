---
title: "🚨 Hệ thống cảnh báo tự động khi chứng chỉ SSL/TLS sắp hết hạn với Slack"
description: "Giải pháp tự động hóa hoàn toàn không cần code để theo dõi và cảnh báo khi chứng chỉ SSL/TLS của các domain sắp hết hạn, giúp ngăn chặn downtime và bảo mật website."
slug: "canh-bao-chung-chi-ssl-tls-sap-het-han-voi-slack"
tags: [n8n, automation, no-code, secops, ssl, tls, security]
keywords: [n8n workflow, tự động hóa, chứng chỉ ssl, cảnh báo ssl, bảo mật website]
---

# 🚨 Hệ thống cảnh báo tự động khi chứng chỉ SSL/TLS sắp hết hạn với Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công chứng chỉ SSL/TLS cho từng domain.
- **Chính xác**: Kiểm tra tự động và chính xác ngày hết hạn của chứng chỉ.
- **Cá nhân hóa**: Cảnh báo kịp thời cho từng domain cụ thể.
- **Hoạt động liên tục**: Theo dõi 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền truy cập vào channel cảnh báo bảo mật.
- Danh sách các domain cần theo dõi chứng chỉ SSL/TLS.
- API để kiểm tra chứng chỉ (có thể sử dụng dịch vụ như Certspotter).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Tạo một workflow mới.
3. Chọn "Import from JSON".
4. Copy và paste nội dung JSON của workflow vào ô nhập liệu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Schedule Trigger**: Cấu hình lịch chạy workflow (ví dụ: mỗi tuần vào thứ Hai lúc 8:00 AM).
- **List Domains to Monitor**: Chỉnh sửa mảng `domainsToMonitor` trong node Code để thêm các domain cần theo dõi.
- **Check Certificate Expiry**: Cập nhật URL của API kiểm tra chứng chỉ SSL/TLS.
- **Is Certificate Expiring?**: Điều chỉnh giá trị `30` trong biểu thức `new Date(Date.now() + 30 * 24 * 60 * 60 * 1000)` để thay đổi thời gian cảnh báo trước khi hết hạn.
- **YOUR_SECURITY_ALERT_CHANNEL_ID**: Chọn credentials Slack và nhập Channel ID của kênh cảnh báo bảo mật.

#### 3. Kích hoạt ⚡️
- **Test run dữ liệu mẫu**: Chạy workflow thủ công để xác nhận nó lấy thông tin chứng chỉ và xử lý đúng.
- **Kiểm tra output**: Kiểm tra kênh Slack để xác nhận cảnh báo được định dạng và gửi đúng.
- **Bật Active workflow**: Sau khi đã kiểm tra và xác nhận mọi thứ hoạt động, kích hoạt workflow để nó chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thêm node Telegram để nhận cảnh báo ngoài Slack.
- **Lưu log**: Thêm node lưu log để theo dõi lịch sử cảnh báo.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về trạng thái chứng chỉ hàng tuần.
- **Kiểm tra nhiều loại chứng chỉ**: Mở rộng workflow để kiểm tra cả chứng chỉ EV và wildcard.

### 📌 Kết luận
Hệ thống cảnh báo tự động chứng chỉ SSL/TLS sắp hết hạn với Slack giúp các sếp bảo mật website một cách hiệu quả và chủ động. Với việc tự động hóa quy trình này, các sếp có thể tập trung vào các nhiệm vụ quan trọng khác mà không phải lo lắng về việc chứng chỉ hết hạn gây downtime. Hãy áp dụng ngay để nâng cao bảo mật và uptime của website!