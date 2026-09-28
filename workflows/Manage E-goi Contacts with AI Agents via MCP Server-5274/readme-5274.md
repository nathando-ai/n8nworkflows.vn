---
title: "🚀 Quản lý danh bạ E-goi bằng AI Agent qua giao thức MCP Server trong n8n"
description: "Tự động hóa toàn diện việc quản lý contact E-goi (tạo, đọc, cập nhật) thông qua AI Agents sử dụng mô hình MCP Server trong n8n."
slug: "quan-ly-danh-ba-e-goi-ai-agents-mcp-server"
tags: [n8n, automation, ai-agents, mcp-server, e-goi, crm]
keywords: [n8n workflow, e-goi mcp server, ai agents e-goi, tu dong hoa crm, mcp trigger n8n]
---

# 🚀 Quản lý danh bạ E-goi thông minh với AI Agents qua MCP Server

Việc quản lý danh sách khách hàng (contacts) trên các nền tảng email marketing như E-goi thường tiêu tốn nhiều thời gian thao tác thủ công qua giao diện hoặc qua lại giữa các ứng dụng. Các sếp có bao giờ nghĩ đến việc chỉ cần "ra lệnh" cho AI thông qua chat (như Claude, ChatGPT hoặc các AI Agent khác) và hệ thống sẽ tự động thêm, sửa, tra cứu thông tin khách hàng trên E-goi ngay lập tức không?

Workflow n8n này do tác giả David Ashby xây dựng chính là giải pháp "tất cả trong một", biến n8n thành một **MCP (Model Context Protocol) Server** chuyên dụng để AI Agents giao tiếp trực tiếp với tài khoản E-goi của các sếp một cách mượt mà và tự động 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và kết nối liên tục với AI Agents, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cho phép các AI Agent thực hiện các thao tác CRUD (Tạo, Đọc, Cập nhật) danh bạ E-goi thông qua câu lệnh tự nhiên.
- **Tiết kiệm thời gian:** Không cần phải thao tác thủ công trên giao diện E-goi, mọi yêu cầu tra cứu hay cập nhật contact được xử lý trong tích tắc.
- **Tích hợp linh hoạt:** Dễ dàng kết nối với bất kỳ AI Agent nào hỗ trợ giao thức MCP (Model Context Protocol).
- **Hoạt động 24/7:** Biến n8n thành một trợ lý trung gian trực tuyến luôn sẵn sàng nhận lệnh từ AI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (phiên bản hỗ trợ LangChain và MCP nodes).
- Tài khoản và API Key của nền tảng **E-goi**.
- AI Agent (ví dụ: Claude Desktop hoặc ứng dụng AI hỗ trợ MCP Client) để kết nối tới MCP Server của n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, trong đó các sếp cần chú ý cấu hình kỹ lưỡng sau:
- **E-goi Tool MCP Server (`mcpTrigger`):** Node này đóng vai trò là điểm kết nối (endpoint) cho MCP. Các sếp cần kiểm tra đường dẫn (`path` được thiết lập mặc định là `e-goi-tool-mcp`) và lấy URL webhook sau khi activate để trỏ AI Agent vào đây.
- **Các tool nodes quản lý contact (`Create a member`, `Get a member`, `Get many members`, `Update a member`):**
  - Sử dụng chung loại node `egoiTool`.
  - **🔑 Add Credentials:** Các sếp chỉ cần cấu hình thông tin xác thực E-goi API (`egoiApi`) ở một node bất kỳ, sau đó mở và lưu lại các node còn lại để hệ thống tự nhận diện credentials.
  - Các tham số bên trong được thiết lập sẵn sàng với biểu thức `$fromAI()`, cho phép AI Agent tự động điền thông số dựa trên ngữ cảnh trò chuyện của người dùng.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại toàn bộ kết nối và thông tin API của E-goi.
- Bật công tắc **Active workflow** ở góc trên cùng bên phải.
- Copy URL webhook từ MCP Trigger để cấu hình vào MCP Client/AI Agent của các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ:** Các sếp có thể nhân bản thêm các node E-goi khác để mở rộng tính năng (ví dụ: xóa contact, quản lý chiến dịch, thống kê...) tùy theo nhu cầu kinh doanh.
- **Tích hợp Slack/Telegram:** Kết hợp thêm node thông báo để mỗi khi AI thực hiện một hành động tạo/sửa contact quan trọng, hệ thống sẽ gửi log báo cáo về nhóm chat nội bộ.
- **Bảo mật MCP Server:** Đảm bảo instance n8n của các sếp sử dụng HTTPS và được bảo vệ bằng các phương thức xác thực phù hợp khi kết nối với AI Agent bên ngoài.

### 📌 Kết luận
Với workflow MCP Server tích hợp E-goi này, các sếp đã có thể nâng tầm hệ thống tự động hóa của mình lên một nấc thang mới nhờ sự trợ giúp của AI. Hãy import ngay vào n8n và trải nghiệm sự tiện lợi này nhé!