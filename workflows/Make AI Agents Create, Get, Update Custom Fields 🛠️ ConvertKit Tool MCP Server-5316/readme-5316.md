---
title: "🛠️ Tích hợp AI Agent với ConvertKit qua MCP Server: Tự động quản lý Custom Fields & Subscriptions"
description: "Hướng dẫn cài đặt workflow n8n sử dụng MCP Server để trao quyền cho AI Agents tạo, lấy, cập nhật Custom Fields và quản lý Subscriptions trong ConvertKit hoàn toàn tự động."
slug: "ai-agent-convertKit-mcp-server-custom-fields"
tags: [n8n, automation, ai-agents, convertKit, mcp-server, no-code]
keywords: [n8n workflow, convertkit mcp server, ai agents convertkit, tu dong hoa marketing, custom fields convertkit]
---

# 🛠️ Tích hợp AI Agent với ConvertKit qua MCP Server: Tự động quản lý Custom Fields & Subscriptions

Trong vận hành hệ thống Email Marketing với ConvertKit (nay là Kit), việc quản lý thủ công danh sách người đăng ký, tùy chỉnh trường dữ liệu (Custom Fields), thẻ (Tags) hay chuỗi chiến dịch (Sequences) thường ngốn rất nhiều thời gian của đội ngũ Marketing. Khi hệ thống lớn dần, các thao tác này càng trở nên nhàm chán và dễ sai sót.

Đã đến lúc các sếp nâng cấp quy trình với sự trợ giúp của Trí tuệ Nhân tạo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực mạnh, đóng vai trò như một **MCP Server (Model Context Protocol)** để trao toàn quyền cho AI Agents tương tác trực tiếp với tài khoản ConvertKit của các sếp. Giờ đây, AI có thể tự động tạo, đọc, cập nhật custom fields, quản lý subscriber, tags và forms chỉ bằng các câu lệnh ngôn ngữ tự nhiên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cho phép AI Agent tự động gọi các công cụ (tools) trong ConvertKit mà không cần viết code tích hợp phức tạp.
- **Quản lý linh hoạt:** AI có thể tạo mới, cập nhật hoặc truy xuất Custom Fields, Subscriptions, Tags, Forms, Sequences trực tiếp qua chat.
- **Tăng tốc vận hành:** Giảm thiểu 90% thời gian thao tác thủ công trên giao diện quản trị ConvertKit.
- **Mở rộng dễ dàng:** Dễ dàng kết nối với các AI Clients hỗ trợ MCP (như Claude Desktop, Cursor hoặc custom AI agents) để giao việc tự động.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted phiên bản hỗ trợ LangChain và MCP nodes).
- Tài khoản ConvertKit (Kit) và thông tin API Key / Credentials kết nối với n8n.
- Kiến thức cơ bản về cách hoạt động của MCP (Model Context Protocol).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy đoạn mã JSON được cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` để dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 16 nodes chủ yếu tập trung vào giao tiếp MCP và các công cụ ConvertKit. Các sếp cần chú ý cấu hình các phần sau:
- **ConvertKit Tool MCP Server (`mcpTrigger`):** Node cốt lõi khởi tạo giao thức MCP. Các sếp cần đảm bảo đường dẫn endpoint hoặc cấu hình kết nối chuẩn xác để AI Client có thể gọi tới server này.
- **Các node công cụ ConvertKit (`convertKitTool`):** 
  - Bao gồm các thao tác: *Create a custom field, Delete a custom field, Get many custom fields, Update a custom field, Add a subscriber, Get many forms, Create a tag, Add a tag to a subscriber*, v.v.
  - Các sếp phải cấu hình **ConvertKit API Credentials** cho các node này để n8n có quyền truy cập vào tài khoản ConvertKit của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc thực hiện câu lệnh thử nghiệm từ AI Client kết nối với MCP Server để kiểm tra xem các tool có phản hồi chính xác không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram:** Thêm các node thông báo để mỗi khi AI thực hiện một thay đổi quan trọng (như tạo Custom Field mới hoặc thêm Subcriber hàng loạt), hệ thống sẽ báo cáo về group chat của team.
- **Ghi log hoạt động:** Lưu lại lịch sử các câu lệnh và kết quả xử lý của AI vào Google Sheets hoặc Notion để dễ dàng audit sau này.
- **Mở rộng MCP Tools:** Các sếp có thể bổ sung thêm các tool khác ngoài ConvertKit để AI Agent trở thành một trợ lý Marketing toàn năng hơn.

### 📌 Kết luận
Việc tích hợp AI Agent thông qua MCP Server mở ra một kỷ nguyên mới trong tự động hóa No-Code. Với workflow n8n này, các sếp đã sẵn sàng biến AI thành một "nhân sự" thực thụ, tự động hóa toàn bộ quy trình quản-lý-dữ-liệu-khách-hàng trên ConvertKit. Hãy cài đặt ngay và trải nghiệm sự tiện lợi này nhé!