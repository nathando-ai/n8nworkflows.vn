---
title: "🌐 Tích hợp LibreTranslate MCP Server cho AI Agent dịch thuật văn bản và tệp tin tự động"
description: "Biến n8n thành MCP Server kết nối AI Agent với LibreTranslate để dịch văn bản, phát hiện ngôn ngữ và xử lý tệp tin tự động không cần code."
slug: "tich-hop-libretranslate-mcp-server-cho-ai-agent"
tags: [n8n, automation, no-code, ai-agent, mcp-server, translation, libretranslate]
keywords: [n8n workflow, libretranslate mcp server, ai agent dịch thuật, n8n mcp trigger, tự động dịch văn bản]
---

# 🌐 Tích hợp LibreTranslate MCP Server cho AI Agent dịch thuật văn bản và tệp tin tự động

Trong quá trình xây dựng các trợ lý AI (AI Agents), việc tích hợp khả năng đa ngôn ngữ là vô cùng quan trọng. Tuy nhiên, việc phải cấu hình các API dịch thuật thủ công hoặc phụ thuộc vào các dịch vụ trả phí đắt đỏ thường gặp nhiều rào cản. Workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách chuyển đổi **LibreTranslate API** thành một **Model Context Protocol (MCP) Server**, cho phép AI Agent gọi trực tiếp 6 tính năng dịch thuật mạnh mẽ một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: AI Agent tự động gọi các công cụ dịch thuật (Detect, Translate Text, Translate File...) mà không cần can thiệp thủ công.
- **Tiết kiệm chi phí**: Sử dụng mã nguồn mở LibreTranslate kết hợp với n8n, loại bỏ hoàn toàn phí thuê bao API dịch thuật đắt đỏ.
- **Linh hoạt & Mở rộng**: Cung cấp sẵn 6 endpoints chuẩn MCP, sẵn sàng kết nối với bất kỳ AI Agent nào hỗ trợ giao thức MCP.
- **Thông minh với AI Expressions**: Các tham số được AI tự động điền thông qua biểu thức `$fromAI()`.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted).
- Một instance **LibreTranslate** đang hoạt động (mặc định trỏ tới `http://libretranslate.local` hoặc địa chỉ server riêng của các sếp).
- AI Agent hỗ trợ cấu hình MCP (Model Context Protocol).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ n8n hoặc tải file, sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **LibreTranslate MCP Server (`mcpTrigger`)**: 
  - Kiểm tra đường dẫn path (mặc định là `libretranslate-mcp`).
  - Copy Webhook URL được tạo ra để cấu hình vào AI Agent của các sếp.
- **Các node HTTP Request (`Detect Text Language`, `List Supported Languages`, `Translate Text`, `Translate File`, `Retrieve Frontend Settings`, `Submit Translation Suggestion`)**:
  - Kiểm tra lại URL của LibreTranslate (`http://libretranslate.local`) và thay đổi thành địa chỉ IP hoặc domain thực tế của server LibreTranslate mà các sếp đang sử dụng.
  - Không cần thiết lập Authentication (trừ khi server LibreTranslate của các sếp có bật bảo mật API Key).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để đưa n8n vào trạng thái chờ kết nối từ MCP client.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Chatbot (Telegram / Slack)**: Kết hợp workflow này với ném lệnh vào Telegram bot để dịch tài liệu tức thì.
- **Tích hợp Error Handling**: Thêm các node xử lý lỗi (Error Trigger) để nhận cảnh báo qua Slack/Email nếu server LibreTranslate gặp sự cố.
- **Lưu lịch sử dịch thuật**: Thêm node Google Sheets hoặc Database để lưu lại các câu lệnh dịch giúp tối ưu hóa prompt sau này.

### 📌 Kết luận
Với workflow n8n này, các sếp đã có thể trao cho AI Agent "siêu năng lực" đa ngôn ngữ một cách mượt mà và chuyên nghiệp. Hãy import ngay vào hệ thống của các sếp và trải nghiệm sức mạnh của MCP Server!