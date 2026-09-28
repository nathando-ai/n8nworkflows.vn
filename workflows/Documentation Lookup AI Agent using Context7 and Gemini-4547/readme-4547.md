---
title: "🚀 Xây dựng Documentation Lookup AI Agent với n8n, Context7 và Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa tra cứu tài liệu lập trình bằng AI Agent, kết nối MCP SSE với Roo Code, Cline qua n8n."
slug: "documentation-lookup-ai-agent-n8n-context7-gemini"
tags: [n8n, automation, ai-agent, google-gemini, mcp, developer-tools]
keywords: [n8n workflow, ai agent mcp, context7 docs, google gemini n8n, roo code mcp, tự động hóa tài liệu]
---

# 🚀 Xây dựng Documentation Lookup AI Agent với n8n, Context7 và Gemini

Các sếp lập trình hay quản lý dự án chắc hẳn đều hiểu cảm giác mệt mỏi khi phải liên tục tra cứu tài liệu (documentation) của các thư viện, framework cập nhật từng ngày. Việc nhảy qua lại giữa IDE và trang chủ tài liệu làm gián đoạn tư duy cực kỳ nhiều. 

Trong bài viết này, chúng ta sẽ khám phá một workflow n8n cực kỳ xịn sò được thiết kế bởi **Jez (Jezweb)**. Workflow này biến n8n thành một **MCP (Multi-Agent Collaboration Protocol) Server**, cho phép các AI coding assistant như **Roo Code** hay **Cline** gọi trực tiếp n8n AI Agent để tra cứu tài liệu chuẩn xác 100% thông qua **Context7** và **Google Gemini** mà không cần tốn nhiều token hay cấu hình phức tạp ở client.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và làm cầu nối MCP Server mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu Token phía Client:** Mọi logic xử lý, system prompt, gọi tool tra cứu đều nằm trong n8n. IDE của các sếp chỉ việc gửi câu hỏi ngắn và nhận kết quả tinh gọn.
- **Tích hợp liền mạch:** Kết nối trực tiếp vào Roo Code, Cline hoặc các hệ thống Agentic khác qua giao thức MCP Server (SSE endpoint).
- **Chính xác tuyệt đối:** Sử dụng Context7 MCP tools (`resolve-library-id` và `get-library-docs`) để kéo đúng phiên bản tài liệu mới nhất của thư viện.
- **Hoạt động tự động 24/7:** Biến n8n thành một "trợ lý tài liệu" trung tâm phục vụ toàn bộ đội ngũ lập trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Hỗ trợ SSE/Webhook public ra ngoài internet).
- Tài khoản và API Key của **Google Gemini (Google Palm API)**.
- Credentials của **Context7 MCP** (`smithery_context7`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy JSON của workflow hoặc import trực tiếp từ kho lưu trữ n8n chính thức với mã ID `4547`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm các thành phần cốt lõi sau cần được cấu hình chính xác:
- **Google Gemini Chat Model**: Kết nối credentials Google AI / Gemini API của các sếp vào node này để cung cấp “bộ não” ngôn ngữ cho AI Agent.
- **Context7 MCP Server Trigger**: Node này đóng vai trò mở cổng SSE công khai. Hãy chú ý đoạn URL được tạo ra (ví dụ: `https://your-n8n-instance.com/mcp/dafdfsdfsdf.../sse`). Đường dẫn ngẫu nhiên dài này giúp bảo mật cơ bản (security by obscurity).
- **call_context7_ai_agent (Tool Workflow Node)**: Node trung gian nhận lệnh từ trigger và chuyển tiếp `query` xuống sub-workflow AI Agent (`Context7 Smithery AI Agent MCP Server`).
- **Context7 AI Agent & Tools (`context7-resolve-library-id`, `context7-get-library-docs`)**: Đảm bảo các tool này đã được gán đúng thông tin xác thực `smithery_context7` để gọi dịch vụ tra cứu ID thư viện và nội dung tài liệu.

#### 3. Cấu hình phía Client (Ví dụ: Roo Code / Cline) 🔌
Để IDE của các sếp gọi được n8n AI Agent này, hãy bổ sung đoạn cấu hình MCP JSON vào file cấu hình của Roo Code/Cline:
```json
"n8n-context7-agent": {
  "url": "https://YOUR_N8N_INSTANCE/mcp/YOUR_LONG_RANDOM_PATH/sse",
  "alwaysAllow": [
    "call_context7_ai_agent"
  ]
}
```
*(Thay `YOUR_N8N_INSTANCE` và `YOUR_LONG_RANDOM_PATH` bằng thông số thực tế từ node `Context7 MCP Server Trigger`)*

#### 4. Kích hoạt ⚡️
- Kiểm tra kết nối API Gemini và Context7 MCP.
- Bật trạng thái **Active** cho workflow trên n8n.
- Thử test câu hỏi trực tiếp từ Roo Code trong VS Code (Ví dụ: *"Cách dùng Flexbox trong Tailwind CSS?"*).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kho công cụ:** Các sếp có thể bổ sung thêm các MCP tool khác vào AI Agent (như GitHub search, StackOverflow search) để trợ lý tài liệu trở nên toàn diện hơn.
- **Lưu lịch sử chat (Logging):** Thêm node Google Sheets hoặc Database ở luồng phụ để lưu lại các câu hỏi phổ biến của team, từ đó biết được dev hay gặp khó khăn ở thư viện nào.
- **Xây dựng hệ thống Multi-Agent:** Biến n8n thành trung tâm điều phối, nơi agent chính phân rã công việc cho nhiều sub-agent chuyên biệt (Agent viết code, Agent test, Agent tra cứu docs).

### 📌 Kết luận
Việc kết hợp n8n, Google Gemini và giao thức MCP mở ra một hướng đi cực kỳ mạnh mẽ để xây dựng các AI Agent tùy chỉnh phục vụ trực tiếp cho quy trình phát triển phần mềm. Hãy triển khai ngay lên VPS của các sếp để tối ưu hóa năng suất lập trình cho cả đội ngũ nhé!