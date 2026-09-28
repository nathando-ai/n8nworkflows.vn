---
title: "🚀 Tự động nhắc nhở hóa đơn quá hạn từ Pennylane lên Slack hàng ngày"
description: "Hướng dẫn tự động hóa gửi thông báo hóa đơn quá hạn từ Pennylane lên Slack hàng ngày, tiết kiệm thời gian và tăng hiệu quả theo dõi công nợ."
slug: "tu-dong-nhac-nho-hoa-don-qua-han-pennylane-slack"
tags: [n8n, automation, no-code, pennylane, slack]
keywords: [n8n workflow, tự động hóa hóa đơn, Pennylane, Slack, quản lý công nợ]
---

# 🚀 Tự động nhắc nhở hóa đơn quá hạn từ Pennylane lên Slack hàng ngày

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải theo dõi và nhắc nhở hóa đơn quá hạn thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình theo dõi hóa đơn quá hạn hàng ngày.
- Tăng hiệu quả: Nhận thông báo chi tiết về hóa đơn quá hạn ngay trên Slack.
- Cá nhân hóa: Điều chỉnh ngưỡng ngày quá hạn và kênh thông báo theo nhu cầu.
- Hoạt động liên tục: Workflow chạy tự động mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Pennylane với quyền truy cập API (gói Essentiel trở lên).
- API token Pennylane với scope: `customer_invoices:all`.
- Tài khoản Slack (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15189](https://n8n.io/workflows/15189).
2. Click vào nút "Import" để tải workflow về máy.
3. Mở n8n Editor và chọn "Import from File" để tải workflow lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Điều chỉnh thời gian chạy hàng ngày (mặc định là 9:00 AM).
- **PL Fetch Invoices**: Tạo credential `httpHeaderAuth` với tên `Authorization` và giá trị `Bearer <YOUR_PENNYLANE_TOKEN>`.
- **Code Filter Overdue**: Thay đổi giá trị `THRESHOLD_DAYS` để điều chỉnh ngưỡng ngày quá hạn (mặc định: 7 ngày).
- **SL Send Notification**: Chọn kênh Slack để nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để chạy tự động hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Telegram hoặc Email để nhận thông báo thay vì Slack.
- Lưu log các hóa đơn đã xử lý để theo dõi lịch sử.
- Gửi báo cáo tổng hợp hàng tuần về tình trạng công nợ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi và nhắc nhở hóa đơn quá hạn hàng ngày, tiết kiệm thời gian và tăng hiệu quả quản lý công nợ. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!