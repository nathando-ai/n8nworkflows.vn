---
title: "🚀 Tích hợp YOURLS MCP Server với n8n để Rút gọn và Quản lý URL tự động"
description: "Hướng dẫn xây dựng MCP Server trên n8n để kết nối với YOURLS, giúp AI tự động rút gọn link, mở rộng URL và lấy thống kê click ngay lập tức."
slug: "tich-hop-yourls-mcp-server-n8n"
tags: [n8n, automation, no-code, mcp, yourls, ai-tools]
keywords: [n8n workflow, yourls mcp server, rut gon link ai, mcp trigger n8n, quan ly url tu dong]
keywords: [n8n workflow, yourls mcp server, rut gon link ai, mcp trigger n8n, quan ly url tu dong]
---

# 🚀 Tích hợp YOURLS MCP Server với n8n để Rút gọn và Quản lý URL tự động

Trong quá trình làm việc với AI agents hoặc chatbot, việc yêu cầu AI thực hiện các tác vụ quản trị hệ thống như rút gọn link, kiểm tra thống kê click từ một dịch vụ Self-hosted (như YOURLS) thường gặp nhiều khó khăn do thiếu kết nối tiêu chuẩn. Việc làm thủ công qua bảng điều khiển vừa mất thời gian vừa không thể tối ưu hóa quy trình làm việc tự động.

Workflow này giải quyết triệt để vấn đề đó bằng cách thiết lập một **Model Context Protocol (MCP) Server** trực tiếp trên n8n. Nó trao cho AI khả năng gọi trực tiếp 3 thao tác cốt lõi của YOURLS: Rút gọn URL, Mở rộng URL và Lấy thống kê click một cách hoàn toàn tự động, không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Cho phép AI (Claude, ChatGPT qua MCP client) tự động tạo link rút gọn ngay trong đoạn chat.
- **Tích hợp liền mạch:** Kết nối trực tiếp công cụ quản lý link cá nhân (YOURLS) vào hệ sinh thái AI Agent mà không cần lập trình backend phức tạp.
- **Truy xuất dữ liệu nhanh chóng:** Dễ dàng kiểm tra hiệu suất click (stats) và mở rộng link (expand) chỉ bằng câu lệnh tự nhiên.
- **Hoạt động 24/7:** Vận hành ổn định trên nền tảng n8n với độ bảo mật cao từ giao thức MCP.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đã được cấu hình hỗ trợ `@n8n/n8n-nodes-langchain` (n8n phiên bản mới tích hợp AI).
- Dịch vụ rút gọn link **YOURLS** đang hoạt động (cần có API Signature/Token và URL của trang YOURLS).
- Ứng dụng/AI Client hỗ trợ **MCP (Model Context Protocol)** để kết nối tới n8n MCP Server.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n (hoặc copy toàn bộ JSON workflow) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần chú ý cấu hình kỹ phần thông tin kết nối YOURLS:
- **Yourls Tool MCP Server (`mcpTrigger`):** Node gốc đóng vai trò lắng nghe và cung cấp các công cụ cho AI Agent thông qua giao thức MCP. Không cần chỉnh sửa nhiều ngoài việc bật Trigger.
- **Shorten a URL (`yourlsTool`):** Cấu hình Credentials kết nối đến YOURLS của các sếp (bao gồm API URL và Signature). Node này chịu trách nhiệm nhận URL dài từ AI và trả về link đã rút gọn.
- **Expand a URL (`yourlsTool`):** Cấu hình tương tự để cho phép giải mã/mở rộng một link rút gọn YOURLS ngược trở lại URL gốc.
- **Get stats for a URL (`yourlsTool`):** Cấu hình để truy vấn số liệu thống kê lượt truy cập của một Short URL cụ thể.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại phần xác thực thông tin YOURLS trong các tool nodes.
- Kết nối n8n MCP Server với AI Client của các sếp (như Claude Desktop hoặc ứng dụng AI nội bộ).
- Bật công tắc **Active** để đưa workflow vào trạng thái sẵn sàng hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack Bot:** Các sếp có thể mở rộng workflow để khi chat với Bot Telegram, Bot sẽ tự động gọi YOURLS MCP Server để rút gọn link và gửi lại kết quả ngay lập tức.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets phía sau tool Shorten a URL để lưu lại lịch sử mỗi khi có một link mới được tạo ra.
- **Báo cáo định kỳ:** Tạo thêm workflow định kỳ kiểm tra thông tin thống kê các link có lượng truy cập cao và gửi báo cáo về email hoặc Slack.

### 📌 Kết luận
Việc tích hợp YOURLS thông qua MCP Server trên n8n mở ra cánh cửa cực kỳ mạnh mẽ để đưa các công cụ quản trị cá nhân vào các tác vụ tự động hóa AI. Hãy import workflow ngay hôm nay để tối ưu hóa cách các sếp quản lý đường dẫn!