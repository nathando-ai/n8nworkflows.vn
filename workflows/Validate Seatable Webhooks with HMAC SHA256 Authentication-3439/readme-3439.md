---
title: "🔐 Xác thực Webhook Seatable với HMAC SHA256 - Workflow n8n"
description: "Hướng dẫn chi tiết cách xác thực webhook Seatable bằng HMAC SHA256 trong n8n để bảo mật dữ liệu và đảm bảo tính toàn vẹn của thông tin"
slug: "xac-thuc-webhook-seatable-hmac-sha256"
tags: [n8n, automation, no-code, webhook, security]
keywords: [n8n workflow, tự động hóa, xác thực webhook, HMAC SHA256, Seatable]
---

# 🔐 Xác thực Webhook Seatable với HMAC SHA256 - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi xử lý webhook từ Seatable mà không có cơ chế xác thực. Giới thiệu workflow như giải pháp bảo mật toàn diện.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Bảo mật dữ liệu webhook từ Seatable
- Đảm bảo tính toàn vẹn của thông tin
- Tự động hóa quy trình xử lý dữ liệu sau khi xác thực
- Giảm thiểu rủi ro bảo mật
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Seatable với quyền truy cập webhook
- Bí mật chia sẻ (shared secret) từ Seatable
- Quyền truy cập vào n8n để import và cấu hình workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và nhập link: [https://n8n.io/workflows/3439](https://n8n.io/workflows/3439)
3. Hoặc copy JSON từ link trên và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Calculate sha256" (crypto)**:
   - Thay thế giá trị "your-secret-key" bằng bí mật chia sẻ từ Seatable
   - Đảm bảo không chia sẻ bí mật này với bất kỳ ai

2. **Node "Seatable Webhook" (webhook)**:
   - Thay đổi giá trị "path" trong keyParameters thành đường dẫn webhook của bạn
   - Hoặc để "path" là "manual" để sử dụng webhook thủ công

3. **Node "Add nodes for processing" (noOp)**:
   - Đây là nơi các sếp sẽ thêm các node xử lý dữ liệu sau khi xác thực thành công
   - Ví dụ: lưu dữ liệu vào Google Sheets, gửi email thông báo, cập nhật cơ sở dữ liệu...

#### 3. Kích hoạt ⚡️
1. Kiểm tra cấu hình bằng cách gửi một webhook mẫu từ Seatable
2. Kiểm tra log để đảm bảo workflow hoạt động đúng
3. Bật Active workflow khi đã kiểm tra thành công

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node "stickyNote" để lưu lại các thông tin quan trọng về workflow
- Kết hợp với Slack để nhận thông báo khi có webhook không hợp lệ
- Thiết lập lịch gửi báo cáo hàng ngày về các webhook đã xử lý
- Tích hợp với cơ sở dữ liệu để lưu trữ lịch sử các webhook đã xác thực

### 📌 Kết luận
Workflow này cung cấp một giải pháp bảo mật toàn diện cho webhook từ Seatable bằng cách sử dụng HMAC SHA256. Bằng cách xác thực từng webhook trước khi xử lý, các sếp có thể giảm thiểu rủi ro bảo mật và đảm bảo tính toàn vẹn của dữ liệu. Hãy thử ngay và tích hợp với các quy trình xử lý dữ liệu của bạn!