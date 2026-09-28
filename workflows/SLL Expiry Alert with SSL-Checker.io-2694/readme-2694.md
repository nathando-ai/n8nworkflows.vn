---
title: "🚨 [Hướng dẫn tự động hóa cảnh báo hết hạn SSL với n8n]"
description: "Tự động giám sát và cảnh báo khi chứng chỉ SSL sắp hết hạn với workflow n8n đơn giản, tiết kiệm thời gian và tránh gián đoạn dịch vụ"
slug: "huong-dan-tu-dong-hoa-canh-bao-het-han-ssl-voi-n8n"
tags: [n8n, automation, no-code, ssl, security]
keywords: [n8n workflow, tự động hóa, cảnh báo ssl, ssl checker, bảo mật web]
---

# 🚨 Tự động hóa cảnh báo hết hạn SSL với n8n - Giám sát dễ dàng, cảnh báo kịp thời

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý chứng chỉ SSL thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giám sát tự động chứng chỉ SSL hàng tuần
- Nhận cảnh báo kịp thời khi còn 7 ngày hết hạn
- Dữ liệu được cập nhật tự động lên Google Sheets
- Tiết kiệm thời gian quản trị hệ thống
- Giảm rủi ro gián đoạn dịch vụ do hết hạn SSL
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Workspace (cho Google Sheets và Gmail)
- Danh sách URL cần giám sát (đã lưu trong Google Sheets)
- API Key từ SSL-Checker.io (miễn phí)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "URLs to Monitor" (Google Sheets)**
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Cấu hình:
     - Spreadsheet URL: Địa chỉ Google Sheet chứa danh sách URL
     - Sheet Name: Tên sheet chứa dữ liệu
     - Range: Vùng dữ liệu (ví dụ: A2:A100)
     - Operation: `update`

2. **Node "Weekly Trigger" (Schedule Trigger)**
   - Cấu hình lịch chạy hàng tuần (ví dụ: mỗi thứ Hai lúc 8:00 AM)

3. **Node "Fetch URLs" (Google Sheets)**
   - Chọn credentials: `googleSheetsOAuth2Api`
   - Cấu hình tương tự node "URLs to Monitor"

4. **Node "Check SSL" (HTTP Request)**
   - URL: `https://api.ssl-checker.io/v1/check`
   - Method: GET
   - Query Parameters:
     - `host`: `={{$node["Fetch URLs"].json[0].url}}`
     - `days`: `7`

5. **Node "Expiry Alert" (If)**
   - Điều kiện: `{{$node["Check SSL"].json.days_remaining}} <= 7`

6. **Node "Send Alert Email" (Gmail)**
   - Chọn credentials: `gmailOAuth2`
   - Cấu hình:
     - To: Địa chỉ email nhận cảnh báo
     - Subject: `SSL Certificate Expiry Alert for {{$node["Check SSL"].json.host}}`
     - Body: `The SSL certificate for {{$node["Check SSL"].json.host}} will expire in {{$node["Check SSL"].json.days_remaining}} days.`

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Teams để nhận cảnh báo qua chat
- Cấu hình cảnh báo cho nhiều mức thời gian khác nhau (30 ngày, 15 ngày, 7 ngày)
- Tích hợp với hệ thống giám sát khác như Zabbix/Prometheus
- Tự động gia hạn chứng chỉ SSL khi sắp hết hạn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quá trình giám sát chứng chỉ SSL, giảm thiểu rủi ro gián đoạn dịch vụ và tiết kiệm thời gian quản trị hệ thống. Hãy áp dụng ngay để bảo vệ hệ thống của bạn khỏi những rủi ro bảo mật tiềm ẩn!