---
title: "🚀 Tự động hóa Gotify với MCP Server - Giải pháp thông báo AI toàn diện"
description: "Hướng dẫn chi tiết cách tự động hóa các thao tác với Gotify (tạo, xóa, lấy tin nhắn) thông qua MCP Server trong n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-gotify-voi-mcp-server"
tags: [n8n, automation, no-code, gotify, ai]
keywords: [n8n workflow, tự động hóa, gotify, mcp server, thông báo ai]
---

# 🚀 Tự động hóa Gotify với MCP Server - Giải pháp thông báo AI toàn diện

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn các thao tác với Gotify (tạo, xóa, lấy tin nhắn)
- Tiết kiệm thời gian và công sức cho các tác vụ thủ công
- Tích hợp dễ dàng với các hệ thống AI khác thông qua MCP Server
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gotify đã hoạt động
- API Key của Gotify
- MCP Server đã được cấu hình (nếu sử dụng)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: [https://n8n.io/workflows/5246](https://n8n.io/workflows/5246)
3. Hoặc tải file JSON về máy và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Gotify Tool MCP Server"**:
  - Đảm bảo đường dẫn "path" là duy nhất và phù hợp với cấu hình của bạn
  - Ví dụ: `gotify-tool-mcp`

- **Node "Create a message"**:
  - Cấu hình credentials "gotifyApi" với API Key của bạn
  - Điền các tham số cần thiết như tiêu đề, nội dung tin nhắn

- **Node "Delete a message"**:
  - Cấu hình credentials "gotifyApi" với API Key của bạn
  - Điền ID của tin nhắn cần xóa

- **Node "Get many messages"**:
  - Cấu hình credentials "gotifyApi" với API Key của bạn
  - Có thể tùy chỉnh các tham số lọc nếu cần

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, hãy test run với dữ liệu mẫu
2. Kiểm tra kết quả trên Gotify để đảm bảo các thao tác hoạt động đúng
3. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các hệ thống thông báo khác như Slack, Telegram để nhận thông báo tức thời
- Tạo các báo cáo định kỳ từ dữ liệu tin nhắn
- Sử dụng các biểu thức `$fromAI()` để tự động điền các tham số từ các hệ thống AI khác
- Tích hợp với các hệ thống quản lý công việc để tự động hóa các quy trình làm việc

### 📌 Kết luận
Workflow này cung cấp một giải pháp toàn diện để tự động hóa các thao tác với Gotify thông qua MCP Server. Với các tính năng sẵn có và khả năng tùy chỉnh, các sếp có thể dễ dàng tích hợp và mở rộng để phù hợp với nhu cầu cụ thể của mình. Hãy thử ngay và tiết kiệm thời gian cho các tác vụ thủ công!