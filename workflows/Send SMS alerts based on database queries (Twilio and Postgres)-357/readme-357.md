---
title: "📱 Tự động gửi SMS cảnh báo từ cơ sở dữ liệu Postgres qua Twilio"
description: "Hướng dẫn tự động hóa gửi SMS cảnh báo khi có dữ liệu mới trong Postgres, tiết kiệm thời gian và nâng cao hiệu quả hoạt động"
slug: "tu-dong-gui-sms-canh-bao-tu-postgres-qua-twilio"
tags: [n8n, automation, no-code, twilio, postgres]
keywords: [n8n workflow, tự động hóa sms, cảnh báo tự động, twilio sms, postgres query]
---

# 📱 Tự động gửi SMS cảnh báo từ cơ sở dữ liệu Postgres qua Twilio

[Các sếp đang gặp khó khăn khi phải theo dõi cơ sở dữ liệu Postgres và gửi SMS cảnh báo thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, không cần viết code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi SMS cảnh báo khi có dữ liệu mới trong Postgres
- Tiết kiệm thời gian theo dõi thủ công
- Đảm bảo thông tin được cập nhật kịp thời
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Twilio với số điện thoại đã được xác minh
- Thông tin kết nối Postgres (host, port, database, username, password)
- Danh sách số điện thoại nhận cảnh báo
- Truy cập vào n8n Editor để import workflow
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/357](https://n8n.io/workflows/357)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Cron**:
   - Thiết lập lịch chạy phù hợp với nhu cầu (ví dụ: mỗi giờ, mỗi ngày)
   - Ví dụ: `0 * * * *` để chạy mỗi giờ

2. **Node Postgres (Query)**:
   - Thiết lập credentials cho kết nối Postgres
   - Viết truy vấn SQL phù hợp để lấy dữ liệu cảnh báo
   - Ví dụ: `SELECT * FROM alerts WHERE status = 'pending'`

3. **Node Twilio**:
   - Thiết lập credentials cho tài khoản Twilio
   - Cấu hình số điện thoại gửi và nhận
   - Thiết lập nội dung tin nhắn cảnh báo

4. **Node Set**:
   - Thiết lập biến để lưu trữ kết quả từ truy vấn Postgres
   - Ví dụ: `{{ $node["Postgres"].json }}`

5. **Node Postgres1 (Update)**:
   - Thiết lập credentials cho kết nối Postgres
   - Viết truy vấn UPDATE để cập nhật trạng thái dữ liệu sau khi gửi SMS
   - Ví dụ: `UPDATE alerts SET status = 'sent' WHERE id = {{ $node["Postgres"].json[0].id }}`

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra SMS được gửi đến số điện thoại đã cấu hình
3. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập nhiều nhóm nhận cảnh báo khác nhau với nội dung tin nhắn tùy chỉnh
- Kết hợp với Slack hoặc Telegram để nhận cảnh báo đa kênh
- Thêm node để lưu log các tin nhắn đã gửi
- Tự động hóa gửi báo cáo định kỳ về trạng thái hệ thống

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình gửi SMS cảnh báo từ cơ sở dữ liệu Postgres, tiết kiệm thời gian và nâng cao hiệu quả hoạt động. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!