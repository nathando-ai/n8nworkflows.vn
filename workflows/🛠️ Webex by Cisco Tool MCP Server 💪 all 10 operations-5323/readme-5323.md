---
title: "🛠️ Webex by Cisco Tool MCP Server 💪 all 10 operations"
description: "Workflow tự động hóa cung cấp một MCP Server tích hợp 10 thao tác Cisco Webex (tạo, lấy, cập nhật, xóa cuộc họp và tin nhắn) để AI hoặc các workflow khác có thể gọi trực tiếp mà không cần viết code."
slug: "webex-cisco-mcp-server-10-operations"
tags: [n8n, automation, no-code, cisco webex, mcp, ai]
keywords: [n8n workflow, tự động hóa webex, cisco webex tool, mcp server, integration webex]
---

# 🚀 Webex by Cisco Tool MCP Server – Kết nối 10 thao tác Webex vào n8n mà không cần code

Bạn từng phải mở nhiều tab, sao chép API key, viết script chỉ để tạo một cuộc họp Webex hoặc gửi tin nhắn? Với workflow này, bạn chỉ cần **import** một lần, cấu hình credentials và ngay lập tức có một **MCP Server** sẵn sàng nhận lệnh từ bất kỳ AI agent, chatbot hoặc workflow n8n nào khác. Tất cả 10 thao tác thường dùng trên Cisco Webex (meeting & message) được đóng gói thành các node `ciscoWebexTool` và được truy cập qua một endpoint MCP Trigger – giúp bạn tự động hóa công việc liên lạc, lên lịch họp và quản lý tin nhắn một cách liền mạch, 100% không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tích hợp nhanh**: MCP Server cung cấp 10 endpoint Webex sẵn sàng để gọi từ AI, chatbot hoặc workflow khác.
- **Tiết kiệm thời gian**: Không cần viết script hay quản lý token thủ công – mọi thao tác chỉ là một HTTP request.
- **Chính xác & nhất quán**: Sử dụng API chính thức của Cisco Webex, giảm lỗi do nhập sai tham số.
- **Hoạt động liên tục**: Sau khi kích hoạt, server luôn lắng nghe và phản hồi trong giây lát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Cisco Webex** (có quyền quản lý cuộc họp và tin nhắn) – cần tạo **Access Token** hoặc cấu hình OAuth trong n8n.
- **Node `ciscoWebexTool`** cần một credential loại **Cisco Webex** (API key hoặc OAuth2).
- **MCP Trigger** (`mcpTrigger`) không cần credential bổ sung, nhưng bạn nên cổng (port) mà nó lắng nghe (mặc định 5678) để truy cập từ bên ngoài.
- (Tùy chọn) **Domain hoặc IP công khai** nếu bạn muốn gọi MCP Server từ internet hoặc từ các dịch vụ AI bên ngoài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang n8n.io (link gốc) hoặc tải file JSON về.
2. Trong n8n Editor, nhấn **Import** → **From File** (hoặc dán JSON vào ô clipboard) → **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình các node sau:

| Node | Cấu hình bắt buộc |
|------|-------------------|
| **MCP Trigger** (`Webex by Cisco Tool MCP Server`) | Đảm bảo node đang **Active**. Nếu muốn thay đổi port, chỉnh trường **Port** (mặc định 5678). |
| **Create a meeting**, **Get a meeting**, **Get many meetings**, **Update a meeting**, **Delete a meeting** | Mỗi node cần chọn **Credential** Cisco Webex bạn đã tạo. Điền các tham số bắt buộc (ví dụ: `topic`, `startTime`, `endTime` cho tạo meeting; `meetingId` cho get/update/delete). |
| **Create a message**, **Get a message**, **Get many messages**, **Update a message**, **Delete a message** | Tương tự, chọn credential Webex. Điền `roomId` (hoặc `personId` cho tin nhắn cá nhân) và `text` (nội dung tin nhắn). |

> **Mẹo:** Để kiểm tra nhanh, bạn có thể sử dụng node **Set** trước mỗi thao tác để gán giá trị mẫu (ví dụ: `meetingId = "abc123"`), sau đó chạy **Test Workflow** để xem phản hồi từ Webex.

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, nhấn **Test Workflow** để đảm bảo mỗi thao tác trả về dữ liệu mong đỗi (không lỗi 401/403).
- Nếu test thành công, bật nút **Active** ở góc trên bên phải workflow.
- MCP Server sẽ bắt đầu lắng nghe; bạn có thể gọi nó qua `http://<YOUR_N8N_HOST>:5678/mcp` (hoặc đường dẫn bạn đã cấu hình) bằng bất kỳ client HTTP nào (Postman, curl, AI agent).

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram sau mỗi thao tác Webex để gửi thông báo khi cuộc họp được tạo hoặc tin nhắn mới đến.
- **Lưu log vào Google Sheets**: Kết hợp node Google Sheets để ghi lại ID meeting, thời gian tạo, người tạo – giúp audit dễ dàng.
- **Lên lịch tự động**: Sử dụng node Cron để gọi MCP Server mỗi sáng và tự động tạo cuộc họp hàng tuần theo mẫu đã có sẵn.
- **Xử lý lỗi**: Bắt lỗi từ node Cisco Webex bằng node **IF** hoặc **Try/Catch** và gửi email cảnh báo khi token hết hạn hoặc quota vượt mức.
- **Bảo mật**: Giới hạn truy cập đến MCP Server bằng IP whitelist hoặc sử dụng n8n’s built‑in **Basic Auth** trên webhook nếu bạn expose nó ra internet.

### 📌 Kết luận
Workflow **Webex by Cisco Tool MCP Server** biến dieci thao tác thường dùng trên Cisco Webex thành một dịch vụ API chuẩn, dễ dàng gọi từ bất kỳ AI agent, chatbot hoặc workflow n8n nào khác. Với chỉ một lần import và cấu hình credential, bạn có thể tự động hóa cuộc họp, quản lý tin nhắn và thông báo liên lạc mà không cần viết một dòng code nào. Hãy áp dụng ngay để tiết kiệm giờ làm việc và tập trung vào những việc thực sự quan trọng!