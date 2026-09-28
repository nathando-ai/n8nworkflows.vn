---
title: "🔐 Tự động xác thực API với Bearer Token và Airtable - Giải pháp bảo mật cho các workflow n8n"
description: "Hướng dẫn chi tiết cách tự động xác thực API bằng Bearer Token và Airtable trong n8n. Giải pháp bảo mật hiệu quả cho các workflow tự động hóa."
slug: "tu-dong-xac-thuc-api-bearer-token-airtable"
tags: [n8n, automation, no-code, api, security]
keywords: [n8n workflow, tự động hóa, xác thực API, Bearer Token, Airtable]
---

# 🔐 Tự động xác thực API với Bearer Token và Airtable - Giải pháp bảo mật cho các workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động xác thực API với Bearer Token một cách an toàn và hiệu quả
- Kiểm soát truy cập vào các endpoint API một cách linh hoạt
- Tích hợp dễ dàng với Airtable để quản lý token và thông tin người dùng
- Giảm thiểu thời gian xử lý các yêu cầu API không hợp lệ
- Tăng cường bảo mật cho các workflow tự động hóa
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Airtable với cơ sở dữ liệu đã được cấu hình
- API key của Airtable để kết nối với n8n
- Các endpoint API cần được bảo vệ bằng xác thực Bearer Token
- Kiến thức cơ bản về cấu hình webhook trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: `https://n8n.io/workflows/6184`
3. Hoặc tải file JSON từ link trên và import trực tiếp vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Other methods" (Webhook)**
   - Cấu hình path: `/test-jobs`
   - Chọn các phương thức HTTP: POST, DELETE, HEAD, PATCH, PUT

2. **Node "GET jobs" (Webhook)**
   - Cấu hình path: `/test-jobs`
   - Chỉ chọn phương thức GET

3. **Node "Get token" (Airtable)**
   - Chọn credentials: `airtableTokenApi`
   - Cấu hình operation: `search`
   - Thiết lập các trường cần tìm kiếm (thường là trường chứa token)

4. **Node "Find job" (Airtable)**
   - Chọn credentials: `airtableTokenApi`
   - Cấu hình operation: `search`
   - Thiết lập các trường cần tìm kiếm (thường là trường chứa thông tin job)

5. **Node "Validator" (Code)**
   - Cập nhật logic xác thực token trong code node này
   - Kiểm tra token tồn tại, chưa hết hạn, và các điều kiện khác

6. **Node "format job" (Code)**
   - Cập nhật logic định dạng dữ liệu job trước khi trả về

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu bằng node "When clicking ‘Execute workflow’" (Manual Trigger)
- Kiểm tra các phản hồi từ các node "respondToWebhook" để đảm bảo logic xử lý đúng
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "Email" để thông báo khi có token không hợp lệ
- Kết hợp với Slack để nhận thông báo thời gian thực về các yêu cầu API
- Thêm node "Schedule Trigger" để kiểm tra và xóa các token hết hạn định kỳ
- Tích hợp với Google Sheets để lưu trữ và phân tích dữ liệu token
- Sử dụng node "Delay" để giới hạn số lượng yêu cầu từ cùng một token trong một khoảng thời gian

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để xác thực API bằng Bearer Token và quản lý token thông qua Airtable. Với cấu hình đơn giản và linh hoạt, các sếp có thể dễ dàng tích hợp vào các hệ thống hiện tại để tăng cường bảo mật và kiểm soát truy cập. Hãy thử ngay để trải nghiệm sự tiện lợi và hiệu quả của workflow này trong việc tự động hóa các quy trình liên quan đến API.