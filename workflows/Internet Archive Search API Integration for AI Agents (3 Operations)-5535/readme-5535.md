---
title: "🚀 Tích hợp Internet Archive Search API vào AI Agents với n8n MCP"
description: "Hướng dẫn cài đặt workflow n8n biến Internet Archive Search API thành MCP Server, giúp AI Agent tra cứu kho tàng tri thức khổng lồ một cách tự động."
slug: "internet-archive-search-mcp-n8n"
tags: [n8n, automation, ai-agents, mcp, internet-archive, rag]
keywords: [n8n workflow, internet archive api, mcp server n8n, ai agent tools, tim kiếm internet archive]
---

# 🚀 Tích hợp Internet Archive Search API vào AI Agents với n8n MCP

Các sếp có bao giờ gặp khó khăn khi muốn AI Agent của mình tiếp cận và khai thác kho tàng tài liệu, sách báo, và dữ liệu lịch sử khổng lồ từ **Internet Archive** chưa? Việc viết code thủ công để kết nối các API phức tạp này vừa tốn thời gian, vừa dễ phát sinh lỗi khi cấu hình tham số.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp biến **Internet Archive Search API** thành một **MCP (Model Context Protocol) Server** hoàn chỉnh chỉ trong vài phút. AI Agent của các sếp có thể trực tiếp gọi 3 thao tác (Fields, Return, Scrape) để tìm kiếm và trích xuất dữ liệu dựa trên độ liên quan một cách mượt mà, hoàn toàn tự động và không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối mượt mà với AI Agents, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến n8n thành MCP Server cung cấp công cụ (tools) trực tiếp cho AI Agent.
- **Truy cập kho dữ liệu khổng lồ**: Khai thác 3 operations quan trọng từ Internet Archive (Xem trường dữ liệu, Tìm kiếm theo độ liên quan, và Scrape dữ liệu).
- **AI-Driven Parameters**: Các tham số tự động được điền bởi AI thông qua biểu thức `$fromAI()`, tối ưu hóa trải nghiệm hỏi đáp.
- **Hoạt động 24/7**: Sẵn sàng phục vụ các tác vụ RAG (Retrieval-Augmented Generation) bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted phiên bản hỗ trợ LangChain/MCP).
- AI Agent hỗ trợ giao thức MCP (Model Context Protocol) để kết nối tới webhook của n8n.
- Không cần tài khoản hay API Key phức tạp từ Internet Archive vì đây là API mở công khai.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON của workflow.
- Mở giao diện n8n của các sếp, chọn **Add workflow** -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 4 nodes chính được cấu hình sẵn:
- **Search Services MCP Server (`mcpTrigger`)**: Node cốt lõi đóng vai trò MCP Server. Các sếp cần chú ý cấu hình đường dẫn `path` (mặc định là `search-services-mcp`). Sau khi kích hoạt, hãy copy Webhook URL này để cấu hình vào AI Agent.
- **Fields that can be requested (`httpRequestTool`)**: Xử lý việc lấy danh sách các trường dữ liệu có thể yêu cầu từ Internet Archive API (`https://api.archive.org`). Sử dụng xác thực `httpHeaderAuth` nếu cần thiết.
- **Return relevance-based results from search queries (`httpRequestTool`)**: Truy vấn và trả về kết quả tìm kiếm dựa trên độ liên quan. Các tham số được tự động điền bởi AI qua `$fromAI()`.
- **Scrape search results from Internet Archive... (`httpRequestTool`)**: Cho phép cào dữ liệu kết quả tìm kiếm từ Internet Archive với khả năng cuộn trang (scroll).

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các thông số kết nối API tới `https://api.archive.org`.
- Bật công tắc **Active** ở góc trên bên phải để khởi chạy MCP Server.
- Lấy URL endpoint từ `mcpTrigger` và trỏ AI Agent của các sếp vào đó để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ (Tools)**: Các sếp có thể bổ sung thêm các HTTP Request Tool khác để truy xuất metadata chi tiết hơn từ Internet Archive.
- **Thêm node ghi log**: Đặt thêm một node lưu trữ lịch sử các câu lệnh gọi từ AI Agent vào Google Sheets hoặc Database để phân tích nhu cầu tìm kiếm của người dùng.
- **Kết hợp Slack/Telegram**: Tạo thêm thông báo mỗi khi AI Agent thực hiện một chuỗi tìm kiếm lớn, giúp giám sát hoạt động hệ thống dễ dàng hơn.

### 📌 Kết luận
Việc tích hợp Internet Archive Search API vào AI Agents qua n8n MCP chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để nâng cấp trợ lý AI của các sếp với khả năng tra cứu kho tàng tri thức nhân loại một cách thông minh nhất! 

Nếu cần hỗ trợ thêm, các sếp có thể ping tác giả David Ashby qua [Discord](https://discord.me/cfomodz) nhé!