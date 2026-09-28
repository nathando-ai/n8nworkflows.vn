---
title: "🚀 Xây dựng Mobility API MCP Server với n8n và AI Agent"
description: "Hướng dẫn tích hợp Mobility API (Cộng hòa Séc) thành MCP Server trên n8n, giúp AI Agent tự động truy vấn dữ liệu di chuyển và lộ trình giao thông một cách thông minh."
slug: "mobility-api-mcp-server-n8n"
tags: [n8n, automation, ai-agent, mcp-server, api-integration]
keywords: [n8n workflow, mcp trigger, mobility api, ai agent tool, http request tool]
---

# 🚀 Tự động hóa truy vấn dữ liệu di chuyển với Mobility API MCP Server trên n8n

Các sếp có bao giờ gặp khó khăn khi muốn kết nối các API dữ liệu phức tạp trực tiếp với AI Chatbot hay AI Agent của mình? Việc cấu hình thủ công từng endpoint, xử lý tham số hay viết code trung gian thường rất mất thời gian và dễ phát sinh lỗi. 

Với workflow **Mobility API MCP Server** này, các sếp sẽ biến n8n thành một Model Context Protocol (MCP) Server chính hiệu. Workflow sẽ đóng gói Mobility API (dữ liệu di chuyển dựa trên mạng di động O2 tại Cộng hòa Séc) thành các công cụ (tools) mà AI Agent có thể tự động gọi và sử dụng một cách mượt mà, hoàn toàn không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối liên tục với AI Agent, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: AI Agent tự hiểu và điền các tham số API thông qua biểu thức `$fromAI()`.
- **Mở rộng năng lực AI**: Biến bất kỳ API nào thành MCP Tool để AI tương tác trực tiếp.
- **Tiết kiệm thời gian lập trình**: Không cần xây dựng backend trung gian, chỉ cần import và cấu hình trực tiếp trên n8n.
- **Hoạt động 24/7**: Cung cấp endpoint ổn định để kết nối với các ứng dụng AI như Claude, Cursor, hoặc các AI Agent tự phát triển.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted phiên bản hỗ trợ MCP nodes).
- Không cần tài khoản xác thực phức tạp (API sandbox không yêu cầu authentication).
- AI Agent hoặc ứng dụng hỗ trợ giao thức MCP (Model Context Protocol).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n của các sếp, hoặc sử dụng tính năng copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 3 nodes chính cấu thành một MCP Server hoàn chỉnh:
- **Mobility MCP Server (`mcpTrigger`)**: 
  - Node này đóng vai trò là điểm cuối (endpoint) để AI Agent gửi yêu cầu.
  - Hãy kiểm tra thông số `path` (mặc định là `mobility-mcp`) và copy URL webhook được tạo ra để cấu hình vào AI Agent của các sếp.
- **Retrieve Application Info (`httpRequestTool`)**: 
  - Node gọi API (`https://developer.o2.cz/mobility/sandbox/api`) để lấy thông tin ứng dụng. Không yêu cầu xác thực rườm rà.
- **Calculate Transit Route (`httpRequestTool`)**: 
  - Node tính toán lộ trình di chuyển và số liệu người dùng di chuyển giữa các điểm A và B.
  - Các tham số trong request được tự động điền bởi AI thông qua cú pháp `$fromAI()`. Các sếp có thể tùy chỉnh lại giá trị mặc định hoặc cấu hình thêm xử lý dữ liệu nếu cần.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các endpoint trong HTTP Request nodes.
- Bật công tắc **Active** ở góc trên bên phải để kích hoạt workflow và khởi chạy MCP server.
- Sử dụng MCP URL cung cấp từ Trigger node cấu hình vào cấu hình AI Agent của các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng Tool**: Các sếp có thể bổ sung thêm các HTTP Request Tool khác để tích hợp thêm nhiều endpoint API mới vào MCP Server.
- **Ghi log & Giám sát**: Thêm các node lưu log (như Google Sheets hoặc cơ sở dữ liệu) sau các HTTP Request để theo dõi các câu lệnh và dữ liệu mà AI Agent đang truy vấn.
- **Xử lý lỗi tùy chỉnh**: Thêm Error Trigger để nhận thông báo qua Telegram/Slack ngay lập tức nếu API gặp sự cố phản hồi.

### 📌 Kết luận
Mobility API MCP Server là một giải pháp cực kỳ mạnh mẽ giúp thu hẹp khoảng cách giữa các REST API truyền thống và thế giới AI Agent hiện đại. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc với AI!