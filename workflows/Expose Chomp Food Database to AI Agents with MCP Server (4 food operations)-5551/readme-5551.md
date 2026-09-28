---
title: "🚀 Kết nối Cơ sở dữ liệu Thực phẩm Chomp với AI Agents sử dụng MCP Server trong n8n"
description: "Hướng dẫn xây dựng MCP Server trên n8n để tích hợp 4 tính năng tra cứu cơ sở dữ liệu thực phẩm Chomp Food Database vào AI Agents một cách tự động."
slug: "ket-noi-chomp-food-database-ai-agents-mcp-server-n8n"
tags: [n8n, automation, ai-agents, mcp-server, rag, api-integration]
keywords: [n8n workflow, chomp food database, mcp server, ai agents, http request tool, tetsup n8n mcp]
---

# 🚀 Kết nối Cơ sở dữ liệu Thực phẩm Chomp với AI Agents qua MCP Server

Các sếp đang phát triển các ứng dụng AI Agent thông minh nhưng lại gặp khó khăn khi muốn tra cứu thông tin dinh dưỡng, mã vạch hoặc thành phần thực phẩm từ các cơ sở dữ liệu lớn? Việc viết code thủ công để tích hợp từng API endpoint vừa tốn thời gian, vừa khó bảo trì.

Giải pháp ở đây chính là workflow n8n sử dụng **Model Context Protocol (MCP)** để biến cơ sở dữ liệu thực phẩm **Chomp Food Database** thành một bộ công cụ (Tools) mạnh mẽ cho AI Agent hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các AI Agents bên ngoài, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 4 thao tác cốt lõi**: Tra cứu thực phẩm theo mã vạch (Barcode), tìm kiếm theo tên, tìm kiếm sản phẩm thương hiệu và tra cứu thành phần thực phẩm.
- **Tích hợp liền mạch với AI**: Sử dụng chuẩn MCP (Model Context Protocol) giúp AI Agent tự động hiểu và gọi các tool một cách chính xác thông qua biểu thức `$fromAI()`.
- **Tiết kiệm thời gian lập trình**: Không cần xây dựng middleware phức tạp, n8n đóng vai trò là một MCP Server hoàn chỉnh sẵn sàng phục vụ.
- **Hoạt động 24/7**: Cung cấp webhook ổn định để AI Agent gọi bất cứ lúc nào cần dữ liệu dinh dưỡng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã bật tính năng LangChain / MCP nodes (phiên bản n8n mới nhất).
- **Chomp This API Key**: Đăng ký tài khoản và lấy API key tại [Chomp This API](https://chompthis.com/api/).
- **AI Agent**: Một hệ thống AI Agent hỗ trợ giao tiếp qua MCP Server (ví dụ: Claude Desktop, Cursor, hoặc custom AI Agent).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào instance n8n của các sếp, hoặc sử dụng tính năng copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính hoạt động nhịp nhàng với nhau:
- **Chomp Food Database API Documentation MCP Server (`mcpTrigger`)**: Đóng vai trò là điểm cuối (endpoint) nhận yêu cầu từ AI Agent. Các sếp cần copy Webhook URL từ node này để cấu hình vào AI Agent.
- **Các HTTP Request Tools**: Bao gồm 4 nodes (`Get Branded Food by Barcode`, `Get Branded Food by Name`, `Search Branded Food Items`, `Search Food Ingredients`) gọi trực tiếp tới API `https://chompthis.com/api/v2`.
  - **Cấu hình Credentials**: Thiết lập API Key dưới dạng **API Key in query** với tên khóa là `api_key` sử dụng key lấy từ Chomp This.
  - **AI Expressions**: Các tham số đầu vào được tự động điền bởi AI thông qua biểu thức `$fromAI()`, đảm bảo linh hoạt theo ngữ cảnh câu hỏi của người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** ở trigger để kiểm tra kết nối MCP Server.
- Bạt công tắc **Active** góc trên bên phải để bật workflow chạy chính thức 24/7.
- Lấy MCP URL dán vào file cấu hình của AI Agent là xong!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ (Tools)**: Các sếp có thể dễ dàng nhân bản các node `httpRequestTool` để tích hợp thêm các endpoint khác từ Chomp API.
- **Thêm tính năng Log**: Gắn thêm node Google Sheets hoặc Telegram vào luồng xử lý để theo dõi lịch sử các câu lệnh mà AI Agent đã gọi.
- **Xử lý lỗi tùy chỉnh**: Thêm các node Error Trigger để nhận thông báo ngay lập tức qua Slack/Telegram nếu API Chomp gặp sự cố gián đoạn.

### 📌 Kết luận
Với workflow n8n này, việc "bơm" dữ liệu thực phẩm khổng lồ vào AI Agent chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay hôm nay để nâng cấp các ứng dụng AI của các sếp lên một tầm cao mới!