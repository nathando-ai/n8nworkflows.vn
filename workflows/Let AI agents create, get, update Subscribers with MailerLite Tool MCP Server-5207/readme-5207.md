---
title: "🚀 Tích hợp AI Agent quản lý danh sách Subscriber trên MailerLite qua MCP Server trong n8n"
description: "Hướng dẫn sử dụng workflow n8n tích hợp Model Context Protocol (MCP) để AI Agents tự động tạo, lấy, cập nhật subscriber trên MailerLite hoàn toàn không cần code."
slug: "ai-agent-quan-ly-subscriber-mailerlite-mcp-server"
tags: [n8n, automation, no-code, ai-agent, mailerlite, mcp]
keywords: [n8n workflow, mcp server, mailerlite automation, ai agent mailerlite, tự động hóa email marketing]
---

# 🚀 Tích hợp AI Agent quản lý danh sách Subscriber trên MailerLite qua MCP Server

Quản lý danh sách người đăng ký (subscriber) thủ công trên các nền tảng Email Marketing như MailerLite luôn tốn nhiều thời gian và dễ xảy ra sai sót khi cần tra cứu hoặc cập nhật thông tin liên tục cho các chiến dịch. 

Đừng lo, workflow n8n này sẽ biến n8n thành một **MCP Server (Model Context Protocol)** chuyên nghiệp. Giờ đây, các trợ lý AI (AI Agents) của các sếp có thể trực tiếp tương tác, tạo mới, tìm kiếm và cập nhật subscriber trên MailerLite thông qua ngôn ngữ tự nhiên một cách mượt mà và tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa thông minh**: Cho phép AI Agent tự gọi các công cụ MailerLite thông qua giao thức MCP chuẩn hóa.
- **Thao tác toàn diện**: Hỗ trợ 4 tác vụ cốt lõi: Tạo mới (Create), Lấy thông tin 1 subscriber (Get), Lấy danh sách (Get All) và Cập nhật (Update).
- **Không cần code phức tạp**: Sử dụng biểu thức `$fromAI()` giúp AI tự động điền các tham số chính xác từ câu lệnh của người dùng.
- **Vận hành liên tục 24/7**: Biến n8n thành một server trung gian kết nối linh hoạt giữa các AI Client và MailerLite.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted hỗ trợ LangChain và MCP).
- Tài khoản **MailerLite** và API Key/Credentials tương ứng.
- AI Agent platform hoặc ứng dụng hỗ trợ tích hợp MCP (như Claude Desktop, Cursor, hoặc các custom AI Agent xây dựng trên n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây cần được cấu hình chuẩn xác:
- **MailerLite Tool MCP Server (`mcpTrigger`)**: Node đóng vai trò trigger nhận yêu cầu từ MCP Client. Các sếp cần đặt đường dẫn `path` (mặc định là `mailerlite-tool-mcp`).
- **Các node MailerLite Tool (`Create a subscriber`, `Get a subscriber`, `Get many subscribers`, `Update a subscriber`)**: 
  - Cấu hình thông tin xác thực (Credentials) tài khoản MailerLite của các sếp tại một node bất kỳ, các node còn lại sẽ tự động nhận diện.
  - Kiểm tra các tham số thao tác (`operation`: `get`, `getAll`, `update`, v.v.) đảm bảo đã được thiết lập đúng như thiết kế sẵn.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại các kết nối và thực hiện test run cơ bản.
- Copy đường dẫn Webhook URL từ node MCP Trigger ở phía bên phải.
- Đưa URL này vào cấu hình MCP Client/AI Agent của các sếp và bật **Active workflow** để đưa hệ thống vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ**: Các sếp có thể bổ sung thêm các tool node khác của MailerLite (như quản lý chiến dịch, nhóm người dùng) vào cùng một MCP Server này.
- **Tích hợp Slack/Telegram**: Thêm node thông báo mỗi khi AI Agent thực hiện thành công một thao tác tạo hoặc cập nhật subscriber quan trọng.
- **Lưu log hoạt động**: Kết nối thêm Google Sheets hoặc cơ sở dữ liệu để ghi lại lịch sử các yêu cầu mà AI Agent đã xử lý qua MCP.

### 📌 Kết luận
Với workflow tích hợp **MailerLite Tool MCP Server** này, việc quản lý email marketing giờ đây trở nên hiện đại và tự động hóa tối đa thông qua sức mạnh của AI. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc nhé!