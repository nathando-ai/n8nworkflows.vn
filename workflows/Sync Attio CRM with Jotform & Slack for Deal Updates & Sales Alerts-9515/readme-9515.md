---
title: "🚀 Tự động hóa CRM Attio với Jotform & Slack: Cập nhật giao dịch & cảnh báo bán hàng"
description: "Hướng dẫn tự động hóa quy trình quản lý khách hàng tiềm năng từ Jotform đến Attio CRM và thông báo qua Slack, tiết kiệm thời gian và tăng hiệu quả bán hàng."
slug: "tu-dong-hoa-crm-attio-jotform-slack"
tags: [n8n, automation, no-code, crm, sales]
keywords: [n8n workflow, tự động hóa, crm, sales automation, lead management]
---

# 🚀 Tự động hóa CRM Attio với Jotform & Slack: Cập nhật giao dịch & cảnh báo bán hàng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý khách hàng tiềm năng từ 80%.
- Tăng hiệu quả bán hàng nhờ thông báo tức thời qua Slack.
- Giảm lỗi thủ công trong quản lý CRM.
- Hoạt động liên tục 24/7 mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Attio CRM với quyền truy cập API.
- Tài khoản Jotform để nhận form submissions.
- Tài khoản Slack để nhận thông báo.
- API keys cho các dịch vụ trên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9515](https://n8n.io/workflows/9515)
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Receive form submissions" (Webhook)**:
  - Đảm bảo đường dẫn webhook là `events` và phương thức HTTP là `POST`.
  - Cấu hình credentials cho webhook (nếu cần).

- **Node "Get the deals id (CRM)" và các node HTTP Request khác**:
  - Cấu hình credentials cho HTTP Bearer Auth.
  - Đảm bảo URL API của Attio CRM được điền chính xác.

- **Node "Send slack message"**:
  - Cấu hình webhook URL của Slack.
  - Tùy chỉnh nội dung thông báo theo nhu cầu.

- **Node "If pending status does not exist" và "If urgent status does not exist"**:
  - Đảm bảo tên các stage trong Attio CRM được đặt đúng (`Pending` và `Urgent`).

- **Node "If message column does not exist"**:
  - Đảm bảo tên cột `Message` trong Attio CRM được đặt đúng.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Telegram để nhận thông báo thay vì Slack.
- Lưu log các hoạt động vào Google Sheets để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về hiệu quả bán hàng qua email.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình quản lý khách hàng tiềm năng từ Jotform đến Attio CRM và thông báo tức thời qua Slack. Với việc triển khai, các sếp sẽ tiết kiệm thời gian, giảm lỗi và tăng hiệu quả bán hàng một cách đáng kể. Hãy áp dụng ngay để nâng cao hiệu suất kinh doanh!