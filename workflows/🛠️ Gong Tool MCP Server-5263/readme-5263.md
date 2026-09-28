---
title: "🚀 Tự động hóa Gong Tool với n8n - MCP Server đơn giản hóa"
description: "Hướng dẫn chi tiết cách tự động hóa các tác vụ Gong Tool như lấy thông tin cuộc gọi và người dùng chỉ với 5 node n8n. Giải phóng thời gian cho các chuyên gia AI."
slug: "tu-dong-hoa-gong-tool-voi-n8n"
tags: [n8n, automation, no-code, ai, gong]
keywords: [n8n workflow, tự động hóa, Gong Tool, MCP Server, AI agents]
---

# 🚀 Tự động hóa Gong Tool với n8n - MCP Server đơn giản hóa

[Các sếp đang gặp khó khăn khi phải xử lý thủ công các tác vụ liên quan đến Gong Tool như lấy thông tin cuộc gọi và người dùng. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ với 5 node n8n đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý thủ công
- Tự động hóa hoàn toàn các tác vụ Gong Tool
- Tích hợp dễ dàng với các AI agents khác
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gong Tool với quyền truy cập API
- URL webhook từ MCP trigger (sau khi kích hoạt workflow)
- Các thông tin xác thực (credentials) cho Gong Tool
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5263)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link workflow vào
4. Click "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Gong Tool MCP Server"**:
   - Đảm bảo tham số `path` được đặt là "gong-tool-mcp"
   - Kiểm tra URL webhook sau khi kích hoạt workflow

2. **Node "Get call"**:
   - Chọn operation "get" để lấy thông tin cuộc gọi cụ thể
   - Cấu hình các tham số cần thiết cho cuộc gọi

3. **Node "Get many calls"**:
   - Không cần cấu hình operation vì nó đã được thiết lập sẵn
   - Sử dụng để lấy danh sách nhiều cuộc gọi

4. **Node "Get user"**:
   - Chọn resource "user" và operation "get"
   - Cấu hình các tham số cần thiết cho người dùng

5. **Node "Get many users"**:
   - Chọn resource "user" và operation "getAll"
   - Sử dụng để lấy danh sách nhiều người dùng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" ở góc trên bên phải
2. Kiểm tra URL webhook từ MCP trigger (ở bên phải node "Gong Tool MCP Server")
3. Sử dụng URL này trong các cấu hình AI agent của các sếp

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi có cuộc gọi mới
- Lưu log các hoạt động vào Google Sheets để theo dõi
- Tự động gửi báo cáo hàng ngày về các cuộc gọi quan trọng
- Kết nối với các hệ thống CRM khác để cập nhật thông tin người dùng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa các tác vụ Gong Tool chỉ với 5 node n8n đơn giản. Các sếp có thể dễ dàng tích hợp với các AI agents khác và nhận được thông tin cập nhật liên tục. Hãy áp dụng ngay để giải phóng thời gian và tăng hiệu suất làm việc!