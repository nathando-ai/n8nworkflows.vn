---
title: "🚀 Tự động gửi tin nhắn từ AI Agents với Mandrill Tool MCP Server"
description: "Hướng dẫn chi tiết cách tự động hóa gửi tin nhắn từ AI Agents thông qua Mandrill Tool MCP Server trên n8n. Tiết kiệm thời gian và nâng cao hiệu quả giao tiếp."
slug: "tu-dong-gui-tin-nhan-tu-ai-agents-voi-mandrill-tool-mcp-server"
tags: [n8n, automation, no-code, AI, email]
keywords: [n8n workflow, tự động hóa, AI agents, Mandrill Tool, MCP Server]
---

# 🚀 Tự động gửi tin nhắn từ AI Agents với Mandrill Tool MCP Server

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian và công sức cho các tác vụ gửi tin nhắn thủ công.
- Tăng cường hiệu quả giao tiếp với khách hàng thông qua các tin nhắn được cá nhân hóa.
- Tự động hóa toàn bộ quá trình gửi tin nhắn từ AI Agents, giảm thiểu lỗi và tăng độ chính xác.
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mandrill Tool đã được cấu hình và có API Key.
- URL webhook từ Mandrill Tool MCP Server.
- Các thông tin cần thiết để cấu hình các node trong workflow.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Mandrill Tool MCP Server**: Cấu hình path là "mandrill-tool-mcp".
- **Send a message based on a template**: Cấu hình các thông tin cần thiết cho việc gửi tin nhắn dựa trên template.
- **Send a message based on HTML**: Cấu hình các thông tin cần thiết cho việc gửi tin nhắn dựa trên HTML.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các công cụ khác như Slack hoặc Telegram để thông báo khi gửi tin nhắn thành công.
- Lưu log các tin nhắn đã gửi để theo dõi và phân tích hiệu quả.
- Gửi báo cáo định kỳ về các tin nhắn đã gửi và phản hồi từ khách hàng.

### 📌 Kết luận
Đoạn đúc kết ngắn gọn, kêu gọi áp dụng ngay.