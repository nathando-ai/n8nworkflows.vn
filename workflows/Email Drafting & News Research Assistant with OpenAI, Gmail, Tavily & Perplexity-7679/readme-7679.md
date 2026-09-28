---
title: "🚀 Xây dựng Trợ lý AI Nghiên cứu Tin tức & Soạn thảo Email tự động với OpenAI, Gmail, Tavily & Perplexity (MCP)"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình nghiên cứu thị trường và soạn thảo email thông minh từ một khung chat duy nhất trong n8n sử dụng công nghệ Model Context Protocol (MCP)."
slug: "tro-ly-ai-nghien-cuu-tin-tuc-soan-thao-email-n8n-mcp"
tags: [n8n, automation, ai-agent, mcp, openai, gmail, tavily, perplexity]
keywords: [n8n workflow, ai agent mcp, tu dong hoa email, nghien cuu tin tuc ai, openai gpt-4, tavily perplexity n8n]
---

# 🚀 Trợ lý AI Nghiên cứu Tin tức & Soạn thảo Email tự động với n8n & MCP

Các sếp có bao giờ cảm thấy mệt mỏi khi mỗi ngày phải mất hàng giờ mở hàng tá tab trình duyệt để đọc báo cáo, tổng hợp tin tức thị trường, sau đó lại lọ mọ viết từng bức email outreach cho khách hàng hay đội ngũ? Việc làm thủ công này cực kỳ tốn thời gian, dễ bỏ sót thông tin và làm giảm năng suất sáng tạo.

Giải pháp ở đây là gì? Bài viết này sẽ hướng dẫn các sếp triển khai một **AI Agent** toàn diện trong **n8n** sử dụng công nghệ **Model Context Protocol (MCP)** tiên tiến. Workflow này giúp các sếp chỉ cần nhập một câu lệnh (prompt) tự nhiên duy nhất qua khung chat, AI sẽ tự động đi sâu vào internet nghiên cứu tin tức mới nhất (qua Tavily và Perplexity), sau đó trực tiếp soạn thảo hoặc gửi email cho người nhận (qua Gmail).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tích hợp 2 trong 1 (Research + Outreach):** Từ một prompt duy nhất, hệ thống vừa tìm kiếm thông tin nóng hổi, vừa tự động lên ý tưởng và gửi email mà không cần chuyển đổi qua lại giữa nhiều tab.
- **Dữ liệu thời gian thực cực chuẩn:** Kết hợp sức mạnh tìm kiếm của Tavily và khả năng tổng hợp trả lời thông minh của Perplexity.
- **Tự động hóa Email thông minh:** Tích hợp trực tiếp Gmail để gửi email hoặc tạo bản nháp (draft) dựa trên dữ liệu đã nghiên cứu.
- **Bộ nhớ ngữ cảnh linh hoạt:** Ghi nhớ nội dung hội thoại nhiều lượt (multi-turn) giúp các sếp dễ dàng yêu cầu chỉnh sửa, bổ sung thông tin cho email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Nền tảng **n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (cho Chat Model).
- **Tavily API Key** & tài khoản **Perplexity**.
- Tài khoản **Google/Gmail** (để cấu hình Gmail Tool).
- Endpoint của **News MCP Server** và **Email MCP Server** công khai để các MCP Client kết nối.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của template workflow này từ n8n.io (Link gốc: [Workflow #7679](https://n8n.io/workflows/7679)) và tiến hành Import trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes, trong đó có các cấu hình cốt lõi cần lưu ý sau:
- **When chat message received & AI Agent:** Node khởi chạy chat và trung tâm điều phối. Các sếp có thể tùy chỉnh System Prompt trong AI Agent (ví dụ: *"helpful email assistant"*) để định hình văn phong và tính cách cho trợ lý ảo của mình.
- **OpenAI Chat Model:** Chọn model `gpt-4.1-mini` (hoặc model OpenAI tương đương) và kết nối **OpenAI API Credentials**.
- **Simple Memory:** Giữ nguyên cấu hình bộ nhớ đệm (Memory Buffer Window) để AI hiểu ngữ cảnh các câu lệnh trước đó.
- **News MCP Server & Email MCP Server (mcpTrigger):** Cấu hình đường dẫn endpoint (`path`) cho các server MCP chuyên biệt.
- **News MCP Client & Email MCP Client:** Kết nối các tool nghiên cứu tin tức (Tavily, Perplexity) và công cụ gửi email (Gmail) thông qua giao thức MCP, đảm bảo transport được đặt ở chế độ `httpStreamable` (trừ khi có yêu cầu đặc biệt khác).
- **Tool Nodes (Search in Tavily, Message a model in Perplexity, Send a message in Gmail):** Đăng nhập và xác thực các tài khoản tương ứng tại từng node tool để cấp quyền cho AI tương tác.

#### 3. Kích hoạt ⚡️
- Nhấn **Chat with node** hoặc mở khung chat test để thử nghiệm câu lệnh đầu vào.
- Thử nghiệm các prompt mẫu thực tế:
  - *"Find today’s top stories on Kubernetes security and draft an intro email to Acme."*
  - *"Summarize the latest AI infra trends and email a 3‑bullet update to my team."*
- Sau khi test thành công, gạt công tắc **Active** góc trên cùng bên phải để bật workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Sử dụng câu lệnh có động từ rõ ràng:** Hãy cấu trúc prompt theo dạng: *"Nghiên cứu chủ đề X, sau đó gửi email cho Y với các ý chính Z"*.
- **An toàn là trên hết:** Khi mới bắt đầu với Gmail Tool, hãy cấu hình bot chỉ tạo bản nháp (**Draft**) thay vì gửi trực tiếp (**Send**) để kiểm tra nội dung trước khi xuất xưởng.
- **Mở rộng kênh thông báo:** Các sếp có thể bổ sung thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo mỗi khi AI hoàn tất một bản nghiên cứu hoặc gửi email thành công.
- **Tùy chỉnh giọng văn:** Thêm các quy tắc cụ thể về văn phong (trang trọng, thân thiện, chuyên nghiệp) vào system prompt của AI Agent để email tạo ra phù hợp hoàn toàn với thương hiệu cá nhân hoặc doanh nghiệp.

### 📌 Kết luận
Workflow tích hợp AI Agent và MCP này là bước tiến vượt bậc giúp tự động hóa hoàn toàn quy trình nghiên cứu thông tin và chăm sóc khách hàng qua email. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!