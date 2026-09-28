---
title: "🚀 Tích hợp Brave Search AI Agent vào n8n qua MCP Server và Google Gemini"
description: "Hướng dẫn xây dựng hệ thống tìm kiếm thông minh trên web và địa phương với Brave Search API, Google Gemini và MCP Server trong n8n."
slug: "tich-hop-brave-search-ai-agent-mcp-server-n8n"
tags: [n8n, automation, no-code, ai-agent, mcp-server, google-gemini]
keywords: [n8n workflow, brave search mcp, google gemini n8n, mcp server n8n, ai agent search]
---

# 🚀 Tích hợp Brave Search AI Agent vào n8n qua MCP Server và Google Gemini

Chào các sếp! Việc kết nối các AI coding assistant (như Roo Code, Cline) với các công cụ tìm kiếm bên ngoài thường gặp vấn đề rác data, lãng phí token do nhận quá nhiều thông tin thô từ API. 

Bài toán này sẽ được giải quyết triệt để với workflow n8n sử dụng **Model Context Protocol (MCP)** kết hợp **Google Gemini** và **Brave Search API**. Workflow này đóng vai trò như một Gateway thông minh, giúp AI tự động phân tích ý định người dùng, chọn tìm kiếm web hay tìm kiếm địa phương (local search), sau đó tinh gọn kết quả trước khi trả về cho client.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu Token:** AI tự động lọc và tóm tắt kết quả tìm kiếm từ Brave trước khi gửi về MCP client, tiết kiệm đáng kể chi phí token.
- **Linh hoạt thông minh:** Tự động phân biệt yêu cầu tìm kiếm thông tin chung trên web hay tìm kiếm doanh nghiệp/địa điểm gần đây (Local Search).
- **Tích hợp liền mạch:** Biến n8n thành một MCP Server chuẩn SSE (Server-Sent Events) để kết nối trực tiếp với Roo Code, Cline hoặc các ứng dụng AI khác.
- **Hoạt động độc lập:** Đóng gói toàn bộ logic xử lý phức tạp phía n8n, giúp client code đơn giản hóa tối đa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (Hỗ trợ MCP triggers).
- Tài khoản và API Credentials cho **Google Gemini** (Google Palm/Gemini API).
- Credentials kết nối **Smithery / Brave Search MCP** cho các tool node.
- Các MCP Client hỗ trợ cấu hình qua SSE (ví dụ: Roo Code, Cline).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc tạo mới, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Brave Search MCP Server Trigger**: Node này tạo ra endpoint dạng `/mcp/cc8cc827-3e72-4029-8a9d-76519d1c136d/sse`. Các sếp cần thay thế `YOUR_N8N_INSTANCE` bằng domain thực tế của n8n server.
- **Google Gemini Chat Model**: Chọn đúng model (khuyến nghị `models/gemini-2.5-flash-preview-05-20`) và kết nối thông tin `googlePalmApi` credentials của các sếp.
- **brave_web_search & brave_local_search**: Đảm bảo đã liên kết chính xác với `smithery brave search` credentials để gọi API thành công.
- **Brave Search AI Agent**: Kiểm tra lại System Prompt trong node này để đảm bảo AI hiểu rõ cách thức điều phối giữa Web Search và Local Search.

#### 3. Kích hoạt ⚡️
- Thực hiện test run bằng cách gửi một request POST giả lập đến endpoint SSE hoặc kết nối thử từ Roo Code.
- Sau khi kiểm tra luồng dữ liệu chạy trơn tru, bật công tắc **Active workflow** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn tìm kiếm:** Có thể tích hợp thêm các tool khác như Tavily, SerpAPI hoặc Wikipedia vào Agent để tăng độ phong phú cho nguồn dữ liệu.
- **Caching kết quả:** Thêm node xử lý lưu trữ cache cho các truy vấn phổ biến nhằm giảm thời gian phản hồi và tiết kiệm gọi API.
- **Giám sát và Logging:** Kết nối thêm một nhánh gửi thông báo về Telegram hoặc Slack mỗi khi có lỗi xảy ra trong quá trình gọi MCP tool.

### 📌 Kết luận
Workflow tích hợp Brave Search qua MCP Server và Google Gemini là giải pháp tuyệt vời giúp nâng tầm các AI Coding Agent của các sếp, giúp tiết kiệm token, tăng độ chính xác và kiểm soát hoàn toàn dữ liệu đầu vào. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc với AI!