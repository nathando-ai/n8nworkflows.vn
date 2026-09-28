```yaml
---
title: "🚀 Tự động hóa Iterable với n8n: MCP Server 6 Operations"
description: "Hướng dẫn tự động hóa 6 thao tác chính của Iterable (Track Event, User Management, List Management) hoàn toàn không cần code bằng n8n"
slug: "tu-dong-hoa-iterable-voi-n8n-mcp-server-6-operations"
tags: [n8n, automation, no-code, iterable, email-marketing]
keywords: [n8n workflow, tự động hóa Iterable, MCP Server, email marketing, no-code]
---

# 🚀 Tự động hóa Iterable với n8n: MCP Server 6 Operations

[Các sếp đang làm việc với Iterable nhưng mệt mỏi với việc phải thực hiện thủ công 6 thao tác quan trọng này: Track Event, User Management và List Management. Workflow này sẽ giúp các sếp tự động hóa hoàn toàn 6 thao tác này chỉ với vài bước cấu hình đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 6 thao tác quan trọng của Iterable: Track Event, User Management và List Management
- Tiết kiệm thời gian đáng kể cho các tác vụ lặp đi lặp lại
- Đảm bảo dữ liệu luôn được cập nhật mới nhất
- Tích hợp dễ dàng với các hệ thống khác trong công ty
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Iterable với API Key (để tạo credentials trong n8n)
- Dữ liệu mẫu để test workflow (nếu cần)
- Kiến thức cơ bản về n8n (không bắt buộc)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/5239)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Iterable Tool MCP Server"**:
   - Tạo credentials mới trong n8n:
     - API Key: Nhập API Key của Iterable
     - Base URL: Để mặc định hoặc thay đổi nếu cần
   - Chọn credentials vừa tạo cho node này

2. **Node "Track an event"**:
   - Thiết lập các tham số:
     - Event Name: Tên sự kiện cần track
     - User ID: ID người dùng (có thể để trống nếu sử dụng email)
     - Email: Email người dùng (có thể để trống nếu sử dụng User ID)
     - Data Fields: Các trường dữ liệu bổ sung nếu cần

3. **Node "Create or update a user"**:
   - Thiết lập các tham số:
     - Email: Email người dùng (bắt buộc)
     - Data Fields: Các trường dữ liệu người dùng (tùy chọn)

4. **Node "Delete a user"**:
   - Thiết lập các tham số:
     - Email: Email người dùng cần xóa (bắt buộc)

5. **Node "Get a user"**:
   - Thiết lập các tham số:
     - Email: Email người dùng cần lấy thông tin (bắt buộc)

6. **Node "Add a user to a list"**:
   - Thiết lập các tham số:
     - Email: Email người dùng (bắt buộc)
     - List ID: ID danh sách cần thêm người dùng vào (bắt buộc)

7. **Node "Remove a user from a list"**:
   - Thiết lập các tham số:
     - Email: Email người dùng (bắt buộc)
     - List ID: ID danh sách cần xóa người dùng khỏi (bắt buộc)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên Iterable
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với các node khác để tạo chuỗi tự động hóa phức tạp hơn
2. Thiết lập webhook để kích hoạt workflow từ các hệ thống khác
3. Sử dụng node "Delay" để tạo chuỗi các thao tác theo thời gian
4. Kết nối với Slack/Telegram để nhận thông báo khi workflow chạy

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn 6 thao tác quan trọng của Iterable chỉ với vài bước cấu hình đơn giản. Với việc tích hợp dễ dàng và hoạt động liên tục 24/7, các sếp có thể tiết kiệm thời gian đáng kể và tập trung vào các nhiệm vụ quan trọng hơn. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại!```