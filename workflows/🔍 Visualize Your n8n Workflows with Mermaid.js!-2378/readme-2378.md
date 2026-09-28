---
title: "🔍 Hiển thị Workflow n8n bằng Mermaid.js - Tự động hóa trực quan"
description: "Hướng dẫn chi tiết cách tạo workflow n8n để trực quan hóa các workflow khác bằng Mermaid.js, tiết kiệm thời gian và nâng cao hiệu quả quản lý quy trình."
slug: "hien-thi-workflow-n8n-bang-mermaid-js"
tags: [n8n, automation, no-code, visualization, mermaid]
keywords: [n8n workflow, tự động hóa, trực quan hóa quy trình, mermaid.js, quản lý workflow]
---

# 🔍 Hiển thị Workflow n8n bằng Mermaid.js - Tự động hóa trực quan

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi quản lý nhiều workflow n8n, đặc biệt là khi cần hiểu cấu trúc và mối quan hệ giữa các quy trình. Việc phải mở từng workflow để xem chi tiết tốn thời gian và dễ gây nhầm lẫn. Workflow này sẽ giúp các sếp trực quan hóa toàn bộ hệ thống workflow bằng Mermaid.js, một công cụ vẽ biểu đồ mã nguồn mở phổ biến.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần mở từng workflow để xem chi tiết.
- **Trực quan hóa**: Hiển thị toàn bộ hệ thống workflow dưới dạng biểu đồ.
- **Dễ quản lý**: Xem mối quan hệ giữa các quy trình một cách rõ ràng.
- **Tự động hóa**: Cập nhật biểu đồ tự động khi có thay đổi trong workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với quyền truy cập API.
- Kiến thức cơ bản về Mermaid.js (không bắt buộc).
- Nếu sử dụng phiên bản cloud, cần thay đổi các biến môi trường như hướng dẫn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào nút "Import" ở góc trên bên phải.
3. Chọn file JSON của workflow này hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "List workflows" và "Single workflow"**:
   - Cần cấu hình credentials cho n8n API.
   - Đối với phiên bản cloud, thay đổi `{{$env["N8N_PROTOCOL"]}}://{{$env["N8N_HOST"]}}` thành URL của instance cloud của bạn.

2. **Node "Webhook"**:
   - Thay đổi `{{$env["N8N_ENDPOINT_WEBHOOK"] || "webhook"}}` thành `webhook` để đảm bảo webhook hoạt động đúng trên môi trường production.

3. **Node "CONFIG"**:
   - Cấu hình các tham số như `instance_url` và `webhook_path` theo hướng dẫn.

#### 3. Kích hoạt ⚡️
- Nhấn "Test workflow" để kiểm tra dữ liệu mẫu.
- Sau khi kiểm tra thành công, bật "Active workflow" để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi biểu đồ Mermaid qua Slack hoặc Telegram mỗi khi có thay đổi.
- **Lưu log**: Thêm node để lưu lịch sử các thay đổi trong workflow.
- **Tự động hóa báo cáo**: Tạo workflow con để gửi báo cáo định kỳ về trạng thái của hệ thống workflow.

### 📌 Kết luận
Workflow này sẽ giúp các sếp quản lý hệ thống workflow n8n một cách hiệu quả hơn. Bằng cách trực quan hóa toàn bộ hệ thống, các sếp có thể dễ dàng theo dõi và quản lý các quy trình một cách chuyên nghiệp. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của bạn!