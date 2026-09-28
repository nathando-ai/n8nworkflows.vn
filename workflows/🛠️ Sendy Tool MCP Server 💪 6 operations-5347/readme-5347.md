---
title: "🚀 Tự động hóa Sendy Tool với n8n: Quản lý Campaign & Subscriber 100% Không Code"
description: "Hướng dẫn chi tiết cách tự động hóa các thao tác với Sendy Tool (tạo campaign, quản lý subscriber) bằng n8n - giải pháp tiết kiệm thời gian và giảm lỗi thủ công cho các sếp marketing."
slug: "tu-dong-hoa-sendy-tool-voi-n8n"
tags: [n8n, automation, no-code, email-marketing, sendy-tool]
keywords: [n8n workflow, tự động hóa email, sendy tool, quản lý subscriber, marketing automation]
---

# 🚀 Tự động hóa Sendy Tool với n8n: Quản lý Campaign & Subscriber 100% Không Code

[Các sếp marketing] đang gặp khó khăn khi phải thực hiện nhiều thao tác thủ công với Sendy Tool như tạo campaign, thêm/xóa subscriber, kiểm tra trạng thái... Điều này tốn thời gian, dễ gây lỗi và không thể mở rộng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ với vài bước cấu hình đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa 6 thao tác quan trọng với Sendy Tool
- Giảm lỗi: Loại bỏ các thao tác thủ công dễ sai sót
- Tích hợp dễ dàng: Kết nối với các hệ thống khác trong workflow
- Hoạt động liên tục: Chạy tự động 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Sendy Tool và API Key (cần cấp quyền đầy đủ)
- n8n đã được cài đặt và cấu hình (tự host hoặc sử dụng dịch vụ cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5347](https://n8n.io/workflows/5347)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên
4. Hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Sendy Tool MCP Server"**: Cần cấu hình credentials với API Key của Sendy Tool
- **Node "Create a campaign"**: Điền các thông tin bắt buộc như tên campaign, danh sách email...
- **Node "Add a subscriber"**: Cấu hình email và thông tin subscriber cần thêm
- **Node "Count a subscriber"**: Chỉnh sửa điều kiện đếm nếu cần
- **Node "Delete a subscriber"**: Cập nhật email của subscriber cần xóa
- **Node "Remove a subscriber"**: Cấu hình email và campaign cần loại bỏ
- **Node "Get subscriber's status"**: Điền email cần kiểm tra trạng thái

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Kiểm tra kết quả ở mỗi node
3. Nếu mọi thứ ổn, click vào nút "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có lỗi xảy ra
- Lưu log các thao tác quan trọng vào Google Sheets
- Tự động gửi báo cáo hàng tuần về hoạt động của campaign
- Kết nối với các hệ thống CRM khác để đồng bộ dữ liệu

### 📌 Kết luận
Workflow này giúp các sếp marketing tự động hóa toàn bộ quy trình quản lý Sendy Tool chỉ với vài bước cấu hình đơn giản. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu lỗi trong các thao tác thủ công!