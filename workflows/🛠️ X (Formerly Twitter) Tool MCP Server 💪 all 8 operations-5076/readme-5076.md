---
title: "🚀 X (Twitter) Tool MCP Server – Tự động hóa 8 thao tác trên X không cần code"
description: "Workflow cho phép thực hiện 8 thao tác trên X (Twitter) như tạo tweet, gửi DM, tìm kiếm, like, retweet, xóa tweet, lấy thông tin user và thêm thành viên vào list qua MCP Trigger, tích hợp dễ dàng với AI agents."
slug: "x-twitter-tool-mcp-server-8-operations"
tags: [n8n, automation, no-code, twitter, x, mcp, ai, social-media]
keywords: [n8n workflow twitter, tự động hóa twitter, mcp trigger, x tool, twitter automation]
---

# 🚀 X (Twitter) Tool MCP Server – Tự động hóa 8 thao tác trên X không cần code

Quản lý tài khoản X (Twitter) thủ công tốn thời gian: phải đăng nhập liên tục để đăng tweet, trả lời tin nhắn, theo dõi mentions, tìm kiếm từ khóa, tương tác với bài viết… Khi số lượng tài khoản hoặc nhu cầu tương tác tăng lên, việc làm thủ công nhanh trở nên không hiệu quả và dễ gây lỗi. Workflow **X (Twitter) Tool MCP Server** giải quyết triệt để bằng cách biến 8 thao tác phổ biến trên X thành các API có thể gọi từ bất kỳ agent AI nào (qua MCP Trigger) hoặc từ các workflow n8n khác, giúp bạn tự động hoá toàn bộ quy trình mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ làm việc**: Một lệnh duyệt hoặc agent AI có thể thực hiện ngay 8 thao tác mà trước đây phải làm thủ công từng bước.
- **Độ chính xác cao**: Loại bỏ lỗi nhầm lẫn ID, nội dung tweet hoặc danh sách khi thao tác thủ công.
- **Cá nhân hóa linh hoạt**: Tham số như nội dung tweet, ID người nhận, từ khóa tìm kiếm… đều có thể được truyền vào động từ dữ liệu đầu vào (webhook, Google Sheets, AI…).
- **Hoạt động liên tục 24/7**: MCP Trigger cho phép workflow luôn sẵn sàng nhận request từ bất kỳ client nào (LangChain, LlamaIndex, custom agent…).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản X (Twitter)** và **API keys/tokens** (Bearer Token, API Key & Secret, Access Token & Secret) để tạo credential loại *Twitter API* trong n8n.
- **Access đến MCP Server**: Node *mcpTrigger* cần được expose qua HTTP (công khai hoặc trong mạng nội bộ) để các agent AI có thể gọi.
- (Tùy chọn) **Danh sách X (List) ID** nếu muốn sử dụng nút *Add Member to List*.
- (Tùy chọn) **Google Sheets / Webhook** nếu muốn cung cấp dữ liệu đầu vào động (nội dung tweet, ID người dùng…).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Trong n8n Editor, chọn **Import** → **Upload file JSON** hoặc **Copy/Paste** toàn bộ JSON workflow từ trang gốc.
- Sau khi import, workflow sẽ xuất hiện với tên **X (Formerly Twitter) Tool MCP Server**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình bắt buộc |
|------|-------------------|
| **X (Formerly Twitter) Tool MCP Server** (`mcpTrigger`) | - Chọn **Credential** Twitter API đã tạo.<br>- Đặt **Path** (ví dụ: `/twitter-mcp`) để các agent gọi.<br>- Kích hoạt **Enable CORS** nếu gọi từ domain khác. |
| **Create Direct Message** (`twitterTool`) | - Chọn **Operation** = *Create Direct Message*.<br>- Ánh trương **Recipient ID** (có thể lấy từ node trước hoặc input).<br>- Nhập **Text** (nội dung DM). |
| **Add Member to List** (`twitterTool`) | - Chọn **Operation** = *Add Member to List*.<br>- Cung cấp **List ID** (số ID của list X).<br>- Nhập **User ID** của thành viên cần thêm. |
| **Create Tweet** (`twitterTool`) | - Chọn **Operation** = *Create Tweet*.<br>- Nhập **Text** (nội dung tweet, tối đa 280 ký tự).<br>- (Tùy chọn) Đính kèm **Media IDs** nếu muốn thêm hình ảnh/video. |
| **Delete Tweet** (`twitterTool`) | - Chọn **Operation** = *Delete Tweet*.<br>- Nhập **Tweet ID** cần xóa. |
| **Like Tweet** (`twitterTool`) | - Chọn **Operation** = *Like Tweet*.<br>- Nhập **Tweet ID** muốn thích. |
| **Retweet Tweet** (`twitterTool`) | - Chọn **Operation** = *Retweet Tweet*.<br>- Nhập **Tweet ID** muốn retweet. |
| **Search Tweets** (`twitterTool`) | - Chọn **Operation** = *Search Tweets*.<br>- Nhập **Query** (từ khóa tìm kiếm, hỗ trợ toán tử X).<br>- Đặt **Max Results** (số tweet trả về, tối đa 100). |
| **Get User** (`twitterTool`) | - Chọn **Operation** = *Get User*.<br>- Nhập **User ID** hoặc **Username** (bắt đầu bằng `@`) để lấy thông tin hồ sơ. |

> **Mẹo:** Sau khi thiết lập xong mỗi node, hãy sử dụng nút **Execute Node** với dữ liệu mẫu để kiểm tra kết quả trước khi bật workflow.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy một lần test với dữ liệu mẫu (có thể dùng nút **Manual Trigger** hoặc **Webhook** nếu đã nối).
- Xác nhận tất cả các node trả về kết quả mong muốn (tweet được tạo, DM được gửi…).
- Bật toggle **Active** ở góc trên cùng bên phải để workflow luôn lắng nghe request từ MCP Trigger.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo tự động**: Kết nối node *Slack* hoặc *Telegram* sau mỗi thao tác thành công để team nhận được cảnh báo ngay lập tức.
- **Lưu log hoạt động**: Thêm node *Google Sheets* hoặc *PostgreSQL* để ghi lại mỗi lệnh gọi (timestamp, operation, status) để審計 và phân tích hiệu suất.
- **Báo cáo tuần**: Sử dụng node *Cron* để trigger workflow mỗi tuần, tổng hợp số tweet đã đăng, lượt like, số DM đã gửi và gửi báo cáo qua email.
- **Xây dựng AI Agent**: Kết hợp workflow này với LangChain hoặc LlamaIndex để tạo agent có thể trả lời câu hỏi như “Tweet mới nhất về #AI là gì?” hoặc “Gửi DM cảm ơn cho mọi người đã retweet bài viết của tôi”.
- **Quản lý Rate Limit**: Thêm node *Wait* (exponential backoff) giữa các lệnh gọi để tránh vượt quá giới hạn API của X (300 request/15 phút cho hầu hết endpoints).

### 📌 Kết luận
Workflow **X (Twitter) Tool MCP Server** biến 8 thao tác thường dùng trên X thành các API sẵn sàng để gọi từ bất kỳ đâu, giúp các sếp tự động hoá quản lý mạng xã hội mà không cần viết code. Với chỉ một few clicks để cấu hình credentials và tham số, bạn đã có thể tiết kiệm giờ làm việc, nâng độ chính xác và mở rộng khả năng tương tác với AI agents. Hãy import ngay hôm nay và trải nghiệm sức mạnh của tự động hóa n8n trên X!