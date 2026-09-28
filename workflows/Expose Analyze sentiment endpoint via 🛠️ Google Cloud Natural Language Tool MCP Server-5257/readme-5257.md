---
title: "🚀 Tích hợp Google Cloud Natural Language Phân tích Cảm Xúc qua MCP Server trong n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp expose Google Cloud Natural Language API làm MCP Server, cho phép các AI Agent phân tích cảm xúc văn bản tự động."
slug: "expose-analyze-sentiment-mcp-server-n8n"
tags: [n8n, automation, no-code, mcp-server, google-cloud, ai-agent]
keywords: [n8n workflow, mcp server n8n, google cloud natural language, phân tích cảm xúc ai, ai agent tools]
---

# 🚀 Xây dựng MCP Server Phân tích Cảm Xúc với Google Cloud Natural Language trong n8n

Các sếp có bao giờ gặp khó khăn khi muốn kết nối các công cụ AI bên ngoài (như Claude Desktop, Cursor, hay custom AI Agent) với sức mạnh phân tích ngôn ngữ tự nhiên của Google Cloud không? Việc code các API Gateway thủ công vừa tốn thời gian, vừa dễ phát sinh lỗi bảo mật.

Với workflow n8n này, các sếp sẽ biến n8n thành một **Model Context Protocol (MCP) Server** chuyên nghiệp chỉ trong vài nốt nhạc. Workflow này expose trực tiếp tính năng phân tích cảm xúc (*Analyze sentiment*) từ Google Cloud Natural Language, giúp các AI Agent tự động gọi công cụ này để thấu hiểu cảm xúc khách hàng từ văn bản một cách mượt mà và hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và làm MCP Server kết nối liên tục với AI Agents, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: AI Agent tự động gọi API phân tích cảm xúc thông qua chuẩn MCP mà không cần viết code cầu kỳ.
- **Tích hợp linh hoạt**: Dễ dàng kết nối với Claude, Cursor hoặc bất kỳ AI Client nào hỗ trợ giao thức MCP.
- **Chính xác cao**: Sử dụng mô hình NLP mạnh mẽ từ Google Cloud để đánh giá sắc thái (tích cực, tiêu cực, trung tính) của văn bản.
- **Hoạt động 24/7**: Biến n8n thành một trạm trung chuyển (tool hub) sẵn sàng phục vụ các hệ thống AI bất cứ lúc nào.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n (Phiên bản hỗ trợ LangChain và MCP nodes).
- Tài khoản Google Cloud Platform (GCP) đã bật dịch vụ **Cloud Natural Language API**.
- Credentials: OAuth2 hoặc Service Account để kết nối Google Cloud trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tải file JSON của workflow từ n8n hoặc copy trực tiếp mã JSON và paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow cực kỳ tinh gọn với chỉ 2 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node `Google Cloud Natural Language Tool MCP Server` (Trigger):**
  - Node này đóng vai trò là điểm tiếp nhận yêu cầu theo chuẩn MCP. 
  - Hãy kiểm tra đường dẫn `path` (mặc định là `google-cloud-natural-language-tool-mcp`) để định danh endpoint của MCP Server.
  - Sau khi kích hoạt, copy lại Webhook URL của node này để cấu hình vào AI Agent Client của các sếp.

- **Node `Analyze sentiment` (Google Cloud Natural Language):**
  - **Credentials**: Kết nối tài khoản Google Cloud của các sếp tại đây (chọn `googleCloudNaturalLanguageOAuth2Api`).
  - Các tham số đầu vào sẽ được các AI Agent tự động điền thông qua biểu thức `$fromAI()`, các sếp không cần cấu hình phức tạp thủ công cho phần truyền dữ liệu văn bản.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** ở node MCP Trigger để kiểm tra kết nối.
- Bạt công tắc **Active** góc trên cùng bên phải để chính thức vận hành MCP Server 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kho công cụ (Tool Hub)**: Các sếp có thể gắn thêm các node MCP khác (như dịch thuật, phân tích thực thể - Entity Analysis) vào cùng một workflow hoặc các workflow độc lập để tạo thành một "vũ khí tối thượng" cho AI Agent.
- **Kết hợp Telegram/Slack Bot**: Nhận feedback khách hàng qua chat, tự động gọi MCP Server này để phân tích cảm xúc, nếu điểm tiêu cực quá thấp thì tự động bắn cảnh báo vào nhóm xử lý sự cố.
- **Log dữ liệu**: Lưu trữ kết quả phân tích cảm xúc vào Google Sheets hoặc Database để làm báo cáo thống kê hàng tuần.

### 📌 Kết luận
Việc tích hợp MCP Server với Google Cloud Natural Language trong n8n mở ra khả năng vô tận trong việc xây dựng các AI Agent thông minh, thấu hiểu cảm xúc người dùng thực tế. Hãy triển khai ngay hôm nay để nâng cấp hệ thống automation của các sếp lên một tầm cao mới!