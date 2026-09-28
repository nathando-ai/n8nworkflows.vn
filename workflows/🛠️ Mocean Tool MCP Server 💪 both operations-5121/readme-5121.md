---
title: "🚀 Tự động hóa SMS & Voice với Mocean Tool MCP Server - Giải pháp hoàn hảo cho AI Agents"
description: "Hướng dẫn chi tiết cách tự động hóa gửi SMS và Voice bằng Mocean Tool MCP Server trong n8n. Tiết kiệm thời gian và nâng cao hiệu suất cho các AI Agents của bạn."
slug: "tu-dong-hoa-sms-voice-mocean-tool-mcp-server"
tags: [n8n, automation, no-code, AI, SMS, Voice]
keywords: [n8n workflow, tự động hóa, Mocean Tool, MCP Server, AI Agents, gửi SMS, gửi Voice]
---

# 🚀 Tự động hóa SMS & Voice với Mocean Tool MCP Server - Giải pháp hoàn hảo cho AI Agents

[Các sếp đang gặp khó khăn khi phải gửi hàng loạt tin nhắn SMS và cuộc gọi Voice thủ công cho khách hàng? Hãy để Mocean Tool MCP Server trong n8n tự động hóa quy trình này một cách hoàn toàn không cần code!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể khi gửi hàng loạt SMS và Voice.
- Tăng hiệu suất làm việc cho các AI Agents của bạn.
- Tự động hóa hoàn toàn quy trình gửi tin nhắn và cuộc gọi.
- Dễ dàng tích hợp với các hệ thống khác trong n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mocean Tool và API Key.
- Các thông tin cần thiết cho SMS và Voice (số điện thoại, nội dung tin nhắn, nội dung cuộc gọi...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào trang [Mocean Tool MCP Server Workflow](https://n8n.io/workflows/5121).
2. Nhấp vào nút "Download" để tải file JSON của workflow.
3. Trong n8n Editor, nhấp vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Mocean Tool MCP Server**:
  - Đảm bảo đường dẫn `path` là `mocean-tool-mcp`.
- **Node Send SMS**:
  - Thêm credentials cho Mocean Tool.
  - Cấu hình các tham số cần thiết cho SMS (số điện thoại, nội dung tin nhắn...).
- **Node Send Voice**:
  - Thêm credentials cho Mocean Tool.
  - Cấu hình các tham số cần thiết cho Voice (số điện thoại, nội dung cuộc gọi...).

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Test Workflow" để kiểm tra hoạt động của workflow.
2. Nhấp vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các node khác trong n8n để tự động hóa quy trình gửi SMS và Voice dựa trên các sự kiện cụ thể.
- Sử dụng các biểu thức `$fromAI()` để tự động điền các tham số từ các AI Agents.
- Lưu trữ lịch sử gửi SMS và Voice để theo dõi và phân tích hiệu suất.

### 📌 Kết luận
Với Mocean Tool MCP Server trong n8n, các sếp có thể tự động hóa hoàn toàn quy trình gửi SMS và Voice một cách dễ dàng và hiệu quả. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu suất làm việc!