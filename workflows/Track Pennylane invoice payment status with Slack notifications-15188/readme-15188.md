---
title: "💰 Theo dõi trạng thái thanh toán hóa đơn Pennylane với thông báo Slack"
description: "Tự động hóa theo dõi trạng thái thanh toán hóa đơn Pennylane và nhận thông báo Slack ngay khi có thay đổi. Giảm thiểu công việc thủ công và tăng hiệu suất làm việc."
slug: "theo-doi-trang-thai-thanh-toan-hoa-don-pennylane-voi-slack"
tags: [n8n, automation, no-code, pennylane, slack]
keywords: [n8n workflow, tự động hóa hóa đơn, Pennylane, Slack, thông báo thanh toán]
---

# 💰 Theo dõi trạng thái thanh toán hóa đơn Pennylane với thông báo Slack

[Các sếp đang làm việc với Pennylane và muốn được thông báo tự động khi hóa đơn được thanh toán hoặc quá hạn mà không cần kiểm tra thủ công. Workflow này sẽ giúp các sếp tiết kiệm thời gian và giảm thiểu công việc lặp lại.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Nhận thông báo tức thì khi hóa đơn được thanh toán hoặc quá hạn
- Giảm thiểu công việc thủ công và tăng hiệu suất làm việc
- Theo dõi trạng thái hóa đơn một cách tự động và liên tục
- Nhận báo cáo tổng hợp về các hóa đơn đã thanh toán và quá hạn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Pennylane với quyền truy cập API (gói Essentiel trở lên)
- Token API Pennylane với phạm vi: customer_invoices:all
- (Tùy chọn) Workspace Slack để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/15188](https://n8n.io/workflows/15188)
3. Hoặc tải file JSON từ link trên và import trực tiếp vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Điều chỉnh khoảng thời gian chạy workflow (mặc định là mỗi 15 phút)
- **PL Fetch Invoices**:
  - Tạo một credential mới với loại "HTTP Header Auth"
  - Đặt tên credential là "Authorization"
  - Giá trị là "Bearer <YOUR_PENNYLANE_TOKEN>"
- **Code Filter Status Changes**: Không cần cấu hình thêm, node này tự động phân loại hóa đơn
- **SL Send Notification**:
  - Chọn channel Slack để nhận thông báo
  - (Tùy chọn) Có thể thay đổi node này để gửi thông báo qua Telegram, Email, v.v.

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute Workflow" để kiểm tra workflow với dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấp vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi node "SL Send Notification" để gửi thông báo qua Telegram hoặc Email
- Thêm node để lưu log các thay đổi trạng thái hóa đơn vào Google Sheets hoặc Notion
- Tạo báo cáo định kỳ về trạng thái thanh toán hóa đơn và gửi qua Slack/Email
- Kết hợp với workflow khác để tự động gửi email nhắc nhở khách hàng thanh toán hóa đơn quá hạn

### 📌 Kết luận
Workflow này giúp các sếp theo dõi trạng thái thanh toán hóa đơn Pennylane một cách tự động và nhận thông báo tức thì khi có thay đổi. Với việc giảm thiểu công việc thủ công, các sếp có thể tập trung vào các công việc quan trọng hơn. Hãy áp dụng ngay để tăng hiệu suất làm việc và giảm thiểu rủi ro thất thoát thanh toán!