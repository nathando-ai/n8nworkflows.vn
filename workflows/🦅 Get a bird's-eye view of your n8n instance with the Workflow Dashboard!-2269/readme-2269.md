---
title: "🦅 Tạo bảng điều khiển tổng quan cho n8n của bạn với Workflow Dashboard!"
description: "Hướng dẫn tự động hóa tạo bảng điều khiển tổng quan cho instance n8n của bạn với 28 nodes, bao gồm thống kê workflow, nodes, tags và webhooks. Tiết kiệm thời gian và nâng cao hiệu suất quản lý workflow."
slug: "tao-bang-dieu-khien-tong-quan-n8n"
tags: [n8n, automation, no-code, devops, dashboard]
keywords: [n8n workflow, tự động hóa, bảng điều khiển, thống kê workflow, quản lý n8n]
---

# 🦅 Tạo bảng điều khiển tổng quan cho n8n của bạn với Workflow Dashboard!

[Các sếp đang gặp khó khăn khi quản lý nhiều workflow trên n8n? Workflow này sẽ giúp các sếp có cái nhìn tổng quan về instance n8n của mình với chỉ 1 click. Từ thống kê cơ bản đến chi tiết từng node và webhook, tất cả được tự động hóa hoàn toàn.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Thống kê tổng quan về workflows (số lượng, trạng thái hoạt động)
- Phân tích chi tiết từng node (số lượng workflow sử dụng, danh sách workflow)
- Xem danh sách tags và workflows sử dụng chúng
- Kiểm soát tất cả webhook endpoints của instance
- Tạo dashboard HTML tĩnh có thể chia sẻ
- Dữ liệu JSON sẵn sàng cho các công cụ BI
- Tiết kiệm thời gian quản lý workflow hàng ngày
- Nâng cao hiệu suất làm việc với cái nhìn tổng quan
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n với quyền truy cập API
- Credentials n8n API đã được cấu hình trong n8n
- (Đối với cloud users) URL instance n8n của bạn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/2269)
2. Copy nội dung JSON của workflow
3. Trong n8n Editor, click vào "Import from JSON" và dán nội dung đã copy

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "n8n-get-workflows"**:
   - Chọn credentials n8n API đã cấu hình
   - Đảm bảo tài khoản có quyền truy cập đầy đủ vào instance n8n

2. **Node "get-nodes-via-jmespath"**:
   - Đối với cloud users: Thay đổi biến `instance_url` thành URL instance n8n của bạn
   - Ví dụ: `https://your-n8n-instance.com`

3. **Node "Create HTML"**:
   - Đối với cloud users: Thay thế `{{ $env.WEBHOOK_URL }}` bằng URL instance n8n của bạn
   - Ví dụ: `https://your-n8n-instance.com`

4. **Node "Request HTML dashboard"**:
   - Cấu hình webhook path nếu cần thay đổi
   - Mặc định: `fb550a01-12f2-4709-ba2d-f71197b68340`

5. **Node "Request xsl template"**:
   - Cấu hình webhook path nếu cần thay đổi
   - Mặc định: `73a91e4d-143d-4168-9efb-6c56f2258aec/dashboard.xsl`

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử
2. Kiểm tra kết quả JSON được tạo ra
3. Bật Active workflow để sử dụng liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Tạo báo cáo định kỳ**: Kết hợp với node "Schedule Trigger" để tự động gửi báo cáo hàng ngày qua email
2. **Bảo mật nâng cao**: Thêm node "Basic Auth" trước các webhook để bảo vệ dashboard
3. **Tích hợp Slack**: Kết nối với node "Slack" để thông báo khi có thay đổi quan trọng trong workflows
4. **Lưu trữ lịch sử**: Kết nối với node "Google Sheets" để lưu trữ lịch sử thống kê

### 📌 Kết luận
Workflow này cung cấp cái nhìn toàn diện về instance n8n của bạn với chỉ 1 click. Từ thống kê cơ bản đến chi tiết từng node và webhook, tất cả được tự động hóa hoàn toàn. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất quản lý workflow hàng ngày!