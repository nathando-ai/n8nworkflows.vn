---
title: "🚀 Tự động hóa Affinity Tool với MCP Server - 16 thao tác toàn diện"
description: "Workflow n8n giúp tự động hóa 16 thao tác chính của Affinity Tool qua MCP Server, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-hoa-affinity-tool-mcp-server"
tags: [n8n, automation, no-code, affinity-tool, mcp-server]
keywords: [n8n workflow, tự động hóa, affinity tool, mcp server, quản lý danh sách]
---

# 🚀 Tự động hóa Affinity Tool với MCP Server - 16 thao tác toàn diện

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 16 thao tác chính của Affinity Tool qua MCP Server
- Tiết kiệm thời gian xử lý thủ công
- Tăng tính chính xác và nhất quán trong quản lý dữ liệu
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tích hợp dễ dàng với các hệ thống khác thông qua n8n
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Affinity Tool với quyền truy cập API
- API Key từ Affinity Tool
- MCP Server đã được cấu hình và chạy
- n8n đã được cài đặt và cấu hình sẵn sàng
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và nhập URL: https://n8n.io/workflows/5335
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Affinity Tool MCP Server** (mcpTrigger):
   - Cấu hình credentials với API Key của Affinity Tool
   - Đảm bảo MCP Server đang chạy và có thể truy cập từ n8n

2. **Các node Affinity Tool** (affinityTool):
   - Tất cả các node Affinity Tool đều cần cấu hình credentials với API Key của Affinity Tool
   - Đối với các node tạo mới (Create), cần cấu hình các tham số bắt buộc như tên, mô tả, v.v.
   - Đối với các node cập nhật (Update), cần cung cấp ID của đối tượng cần cập nhật

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu với từng node để đảm bảo kết nối và xử lý đúng
- Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các node khác như Google Sheets, Email, hoặc Slack để tạo báo cáo tự động
- Sử dụng các node điều kiện để lọc và xử lý dữ liệu theo nhu cầu cụ thể
- Tạo các workflow con để quản lý các thao tác phức tạp hơn
- Thiết lập lịch chạy định kỳ cho các thao tác cần xử lý hàng ngày

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa các thao tác chính với Affinity Tool qua MCP Server. Với 16 thao tác được tự động hóa, các sếp có thể tiết kiệm thời gian đáng kể và nâng cao hiệu suất làm việc. Hãy thử ngay và trải nghiệm sự khác biệt mà tự động hóa mang lại!