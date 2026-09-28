---
title: "🚀 Tích hợp IP2WHOIS Domain Lookup MCP Server vào AI Agent với n8n"
description: "Hướng dẫn xây dựng MCP Server tra cứu thông tin WHOIS tên miền tự động cho AI Agent sử dụng n8n và IP2WHOIS API, giúp AI truy vấn dữ liệu tên miền chuẩn xác."
slug: "tich-hop-ip2whois-domain-lookup-mcp-server-n8n"
tags: [n8n, automation, no-code, mcp, ai-agent, ip2whois]
keywords: [n8n workflow, ip2whois mcp server, ai agent tool, tra cứu whois tự động, mcp trigger n8n]
---

# 🚀 Tích hợp IP2WHOIS Domain Lookup MCP Server vào AI Agent với n8n

Trong kỷ nguyên AI Agent, việc trang bị cho AI khả năng tương tác trực tiếp với các công cụ bên ngoài (Tools) là cực kỳ quan trọng. Việc tra cứu thông tin tên miền (WHOIS) thủ công bằng cách truy cập từng website vừa tốn thời gian, vừa khó tích hợp vào các chuỗi hội thoại thông minh của AI.

Workflow này giải quyết triệt để vấn đề đó bằng cách biến **IP2WHOIS API** thành một **MCP Server (Model Context Protocol)** chạy trên n8n. Giờ đây, các AI Agent của các sếp có thể tự động gọi công cụ này để tra cứu thông tin sở hữu tên miền, ngày đăng ký, nhà đăng ký (registrar) và nhiều dữ liệu khác chỉ bằng một câu lệnh tự nhiên.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và làm MCP Server kết nối mượt mà với AI Agent, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** AI Agent tự động hiểu và gọi API tra cứu WHOIS mà không cần can thiệp thủ công.
- **Tích hợp chuẩn MCP:** Biến n8n thành MCP Server chuyên nghiệp, dễ dàng kết nối với các AI framework hỗ trợ MCP.
- **Dữ liệu chính xác:** Lấy thông tin chủ sở hữu, thông tin liên hệ, vị trí và thời hạn tên miền trực tiếp từ nguồn IP2WHOIS.
- **Hoạt động liên tục 24/7:** Phục vụ các yêu cầu tra cứu của AI bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc Cloud).
- Tài khoản và API Key tại [IP2WHOIS](https://www.ip2whois.com/).
- AI Agent hỗ trợ giao thức MCP (Model Context Protocol).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow này hoặc tải file JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác 2 node quan trọng sau trong workflow:

- **Node `IP2WHOIS Domain Lookup MCP Server` (mcpTrigger):**
  - Kiểm tra đường dẫn (`path`) được cấu hình mặc định (ví dụ: `ip2whois-domain-lookup-mcp`).
  - Sau khi kích hoạt workflow, sao chép URL webhook của MCP Trigger này để cấu hình vào AI Agent.

- **Node `Lookup WHOIS Data` (httpRequestTool):**
  - Kết nối tới API endpoint: `https://api.ip2whois.com/v2`
  - Cấu hình thông tin xác thực (Credentials) bằng API Key của tài khoản IP2WHOIS.
  - Đảm bảo các tham số (parameters) được thiết lập tự động lấy từ AI thông qua biểu thức `$fromAI()`.

#### 3. Kích hoạt ⚡️
- Kiểm tra lại cấu hình API Key tại node HTTP Request.
- Chuyển công tắc trạng thái từ **Inactive** sang **Active** để bật MCP Server.
- Lấy URL endpoint từ MCP Trigger và dán vào phần cấu hình Tools/MCP của AI Agent.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng công cụ:** Các sếp có thể bổ sung thêm các HTTP Request Tool khác để tra cứu IP, DNS hoặc SSL trong cùng một MCP Server.
- **Lưu lịch sử tra cứu:** Thêm node Google Sheets hoặc Database phía sau tool để ghi lại danh sách các tên miền mà AI đã tra cứu.
- **Xử lý lỗi tùy chỉnh:** Thêm các node Error Trigger để thông báo về Telegram/Slack nếu API IP2WHOIS gặp sự cố hoặc hết hạn mức (quota).

### 📌 Kết luận
Việc tích hợp IP2WHOIS Domain Lookup thông qua MCP Server trên n8n mở ra khả năng tự động hóa cực kỳ mạnh mẽ cho các AI Agent chuyên về lĩnh vực IT, Bảo mật hoặc Quản trị tên miền. Hãy "lên đồ" ngay cho hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!