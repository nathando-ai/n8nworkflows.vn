---
title: "🚀 Tích hợp Internet Archive Wayback Machine API cho AI Assistant với n8n"
description: "Hướng dẫn cấu hình workflow n8n biến Wayback Machine API thành MCP Server cho AI Agent, giúp trợ lý AI dễ dàng tra cứu và lưu trữ trang web lịch sử."
slug: "tich-hop-internet-archive-wayback-machine-api-cho-ai-assistant"
tags: [n8n, automation, ai-agents, mcp, rag, internet-archive]
keywords: [n8n workflow, wayback machine api, mcp server, ai assistants, rag automation, tự động hóa n8n]
languages: [vi]
---

# 🚀 Tích hợp Internet Archive Wayback Machine API cho AI Assistant với n8n

Các sếp đang phát triển trợ lý ảo (AI Agent) nhưng gặp khó khăn khi AI không thể truy cập vào các phiên bản lưu trữ lịch sử của trang web trên Internet Archive (Wayback Machine)? Việc tra cứu thủ công hoặc viết code tích hợp phức tạp thường tốn rất nhiều thời gian và công sức.

Giải pháp ở đây là gì? Workflow n8n này sẽ biến **Internet Archive Wayback Machine API** thành một **MCP Server (Model Context Protocol)** hoàn chỉnh, cho phép trợ lý AI của các sếp gọi trực tiếp các công cụ (tools) này một cách mượt mà mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với các AI Agent bên ngoài, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Mở rộng năng lực cho AI**: Giúp AI Agent tự động tra cứu dữ liệu lưu trữ lịch sử (Get Wayback) và lưu trữ trang web mới (Create Wayback) một cách chính xác.
- **Tự động hóa 100%**: Sử dụng chuẩn MCP (Model Context Protocol) hiện đại, không cần cấu hình API phức tạp.
- **Tiết kiệm thời gian**: Triển khai nhanh chóng chỉ trong vài phút, sẵn sàng kết nối với các AI client hỗ trợ MCP.
- **Hoạt động 24/7**: Phục vụ mọi truy vấn từ trợ lý ảo bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted hỗ trợ MCP Trigger).
- Trợ lý AI hoặc AI client có hỗ trợ cấu hình MCP Server.
- **Không cần tài khoản API Key**: Internet Archive Wayback Machine API mở và hoàn toàn miễn phí!
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow từ n8n.
- Dán (Paste) vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes chính, cấu trúc rất gọn gàng:
- **Wayback MCP Server (Node `mcpTrigger`)**: 
  - Đảm nhận vai trò endpoint để nhận yêu cầu từ AI Agent.
  - Các sếp cần kiểm tra đường dẫn path (mặc định là `wayback-mcp`) và lấy URL webhook sau khi Active workflow để cấu hình cho AI Agent.
- **Get wayback (Node `httpRequestTool`)**: 
  - Gửi request đến API của Internet Archive để lấy dữ liệu trang web đã lưu trữ.
  - Các tham số được AI tự động điền thông qua biểu thức `$fromAI()`.
- **Create wayback (Node `httpRequestTool`)**: 
  - Gửi request để lưu trữ (snapshot) một URL mới lên Wayback Machine.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các node để đảm bảo không có lỗi cấu hình.
- Nhấn nút **Active** để bật workflow và khởi động MCP Server.
- Copy URL MCP từ trigger và dán vào phần cấu hình MCP của AI Agent.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node thông báo mỗi khi AI Agent thực hiện một lệnh tạo snapshot (Create wayback) thành công.
- **Lưu Log vào Google Sheets**: Theo dõi các URL mà trợ lý AI thường xuyên tra cứu để tối ưu hóa dữ liệu RAG.
- **Bảo mật Endpoint**: Cấu hình xác thực nếu cần thiết để giới hạn quyền truy cập vào MCP Server của các sếp.

### 📌 Kết luận
Với workflow n8n này, các sếp đã dễ dàng nâng cấp trợ lý AI của mình với khả năng "du hành thời gian" trên internet thông qua Wayback Machine API. Hãy import ngay vào hệ thống và trải nghiệm sức mạnh của AI kết hợp No-Code automation nhé!