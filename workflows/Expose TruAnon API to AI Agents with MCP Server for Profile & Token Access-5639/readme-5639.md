---
title: "🚀 Kết nối TruAnon API với AI Agents qua MCP Server trong n8n"
description: "Hướng dẫn xây dựng MCP Server trên n8n để tích hợp TruAnon API (Lấy thông tin Profile và Token) vào các AI Agent một cách mượt mà và tự động."
slug: "ket-noi-truanon-api-voi-ai-agents-qua-mcp-server-trong-n8n"
tags: [n8n, automation, mcp-server, ai-agents, truanon, api-integration]
keywords: [n8n workflow, mcp server n8n, truanon api, ai agent tools, tự động hóa api]
---

# 🚀 Kết nối TruAnon API với AI Agents qua MCP Server trong n8n

Các sếp có bao giờ gặp khó khăn khi muốn kết nối các hệ thống AI Agent của mình với các API nội bộ như TruAnon mà phải viết code cầu kỳ không? Việc tích hợp thủ công, xử lý tham số và gọi API liên tục làm tốn rất nhiều thời gian và công sức phát triển.

Giải pháp ở đây là sử dụng workflow n8n này để biến n8n thành một **MCP (Model Context Protocol) Server**, cho phép AI Agent tự động gọi TruAnon API (Lấy Profile và tạo Access Token) hoàn toàn tự động mà không cần viết một dòng code backend nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tích hợp AI Agent liền mạch**: Cung cấp trực tiếp 2 công cụ (Tools) mạnh mẽ cho AI Agent thông qua giao thức MCP.
- **Tự động điền tham số**: Sử dụng biểu thức `$fromAI()` để AI tự động nhận diện và điền tham số gọi API chính xác.
- **Tiết kiệm thời gian phát triển**: Không cần dựng server trung gian, n8n đóng vai trò là MCP Server sẵn sàng hoạt động ngay lập tức.
- **Hoạt động 24/7**: Luôn sẵn sàng phản hồi các truy vấn từ AI Agent bất cứ lúc nào.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Khuyên dùng bản tự host hoặc n8n Cloud hỗ trợ MCP).
- TruAnon Service Identifier (thường là tên miền gốc của các sếp) và Member Name.
- Private Token của TruAnon để xác thực các request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON.
- Mở n8n Editor, chọn **Import from JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 3 nodes chính sau đây:
- **TruAnon Private MCP Server (`mcpTrigger`)**: Đóng vai trò là điểm cuối (endpoint) để AI Agent kết nối. Các sếp cần cấu hình đường dẫn `path` (mặc định là `truanon-private-mcp`) để lấy URL webhook cung cấp cho AI Agent.
- **Fetch User Profile (`httpRequestTool`)**: Node gọi API tới `https://staging.truanon.com` để lấy thông tin người dùng. Đảm bảo các tham số đầu vào được cấu hình dùng biểu thức `$fromAI()` để AI tự động điền Service Identifier và Member Name.
- **Generate Access Token (`httpRequestTool`)**: Node thực hiện yêu cầu tạo Access Token từ TruAnon API.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các kết nối giữa các node.
- Copy Webhook URL từ node **TruAnon Private MCP Server** và cấu hình vào phần công cụ (Tools) của AI Agent của các sếp.
- Bật nút **Active** trên góc phải màn hình để kích hoạt workflow chạy nền.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ**: Các sếp có thể bổ sung thêm các node `httpRequestTool` khác nếu TruAnon có thêm các endpoint mới.
- **Thêm tính năng ghi log**: Kết nối thêm node Slack hoặc Telegram để nhận thông báo mỗi khi AI Agent gọi đến các công cụ này.
- **Xử lý lỗi tùy chỉnh**: Thêm Error Trigger để bắt các lỗi phát sinh từ API phía TruAnon nhằm tăng tính ổn định cho hệ thống.

### 📌 Kết luận
Với workflow này, việc "trao quyền" cho AI Agent tương tác với hệ thống TruAnon trở nên dễ dàng và nhanh chóng hơn bao giờ hết. Hãy import ngay vào n8n của các sếp và trải nghiệm sức mạnh của MCP Server ngay hôm nay!