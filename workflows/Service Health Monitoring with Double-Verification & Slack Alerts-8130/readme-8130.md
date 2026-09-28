---
title: "🚨 Giám sát tình trạng dịch vụ với xác minh kép & cảnh báo Slack"
description: "Workflow n8n tự động giám sát tình trạng dịch vụ của bạn với xác minh kép, giảm thiểu cảnh báo giả và gửi thông báo Slack khi dịch vụ bị gián đoạn"
slug: "giam-sat-tinh-trang-dich-vu-voi-xac-minh-kep-slack-alerts"
tags: [n8n, automation, devops, monitoring, slack]
keywords: [n8n workflow, giám sát dịch vụ, tự động hóa, cảnh báo Slack, xác minh kép]
---

# 🚨 Giám sát tình trạng dịch vụ với xác minh kép & cảnh báo Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi dịch vụ bị gián đoạn. Giới thiệu workflow như giải pháp tự động hóa giám sát 24/7 với xác minh kép để giảm thiểu cảnh báo giả.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giám sát liên tục dịch vụ của bạn 24/7
- Giảm thiểu cảnh báo giả với xác minh kép
- Nhận thông báo Slack tức thì khi dịch vụ bị gián đoạn
- Tiết kiệm thời gian quản trị hệ thống
- Hoạt động liên tục không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- URL của dịch vụ cần giám sát
- Tài khoản Slack và quyền tạo bot
- Token Slack API (cần cấp quyền `chat:write`)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8130](https://n8n.io/workflows/8130)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "First Check" và "Second Check"**:
   - Thay đổi URL trong phần "URL" của node HTTP Request thành URL của dịch vụ bạn muốn giám sát
   - Có thể thêm nhiều URL bằng cách sao chép node và thay đổi URL

2. **Node "Send Alert to Slack"**:
   - Thêm credentials Slack bằng cách:
     - Click vào biểu tượng bánh răng ở góc trên bên phải
     - Chọn "Credentials"
     - Click "Create" và chọn "Slack"
     - Điền tên credentials (ví dụ: "Slack Alerts")
     - Điền "Bot Token" (bắt đầu bằng "xoxb-")
     - Click "Save"

3. **Node "Check Interval"**:
   - Thay đổi thời gian kiểm tra trong phần "Options" của node Schedule Trigger
   - Ví dụ: Để kiểm tra mỗi 5 phút, chọn "Every 5 minutes"

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" ở góc trên bên phải
2. Để kiểm tra hoạt động, bạn có thể:
   - Tạm thời thay đổi URL trong node HTTP Request thành một URL không tồn tại để kiểm tra cảnh báo
   - Hoặc chờ đến thời gian kiểm tra tiếp theo

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Telegram**: Thêm node Telegram để nhận cảnh báo cùng lúc
2. **Lưu log**: Thêm node Google Sheets hoặc Notion để lưu lịch sử giám sát
3. **Cảnh báo đa kênh**: Kết hợp với node Email để nhận cảnh báo qua email
4. **Giám sát nhiều dịch vụ**: Sao chép toàn bộ workflow và thay đổi URL để giám sát nhiều dịch vụ khác nhau

### 📌 Kết luận
Workflow này cung cấp giải pháp giám sát dịch vụ hiệu quả với xác minh kép, giúp các sếp giảm thiểu cảnh báo giả và nhận thông báo tức thì khi dịch vụ bị gián đoạn. Hãy áp dụng ngay để nâng cao tính sẵn sàng của hệ thống!