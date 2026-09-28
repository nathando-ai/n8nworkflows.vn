---
title: "🚀 Trợ lý Email tự động cho Nhà cung cấp – Tích hợp OpenAI & Google Sheets"
description: "Giải pháp tự động gửi email cho nhà cung cấp, lấy dữ liệu từ Google Sheets và xử lý bằng AI, hoàn toàn không cần code."
slug: "trợ-ly-email-tự-dong-cho-nha-cung-cap"
tags: [n8n, automation, no-code, AI, email, suppliers]
keywords: [n8n workflow, tự động hóa, email, nhà cung cấp, OpenAI, Google Sheets]
---

# 🚀 Trợ lý Email tự động cho Nhà cung cấp

Bạn đang phải gửi hàng loạt email cho nhà cung cấp, nhưng lại phải làm thủ công, mất thời gian và dễ sai sót?  
Workflow này sẽ giúp bạn **tự động** lấy thông tin nhà cung cấp từ Google Sheets, **xử lý yêu cầu** bằng OpenAI, và **gửi email** qua Gmail – hoàn toàn **không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Gửi hàng trăm email chỉ trong vài giây.  
- **Chính xác**: Dữ liệu luôn được lấy trực tiếp từ Google Sheets, tránh lỗi nhập liệu.  
- **Cá nhân hóa**: AI viết nội dung email phù hợp với từng nhà cung cấp.  
- **Hoạt động liên tục**: Chạy 24/7, không cần giám sát thủ công.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets**: Tạo file “Suppliers” với 2 cột: `Supplier Name`, `Contact Email`.  
- **Google Sheets OAuth2**: Cấp quyền đọc/ghi cho n8n.  
- **Gmail OAuth2**: Cấp quyền gửi email.  
- **OpenAI API Key**: Đăng ký tại https://platform.openai.com.  
- **MCP Server**: Định nghĩa đường dẫn `/cbbbcf9a-2105-4289-9874-45d3ca20dd2e` (được tạo trong Google Sheets).  
- **MCP Client**: Định nghĩa đường dẫn `/cbbbcf9a-2105-4289-9874-45d3ca20dd2e` (được tạo trong n8n).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/4067).  
2. Mở n8n Editor → **Import** → **Upload JSON**.  
3. Chọn file vừa tải và nhấn **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Tên node | Cấu hình cần chỉnh | Mô tả |
|------|----------|---------------------|-------|
| `MCP Server Trigger` | MCP Server Trigger | `path` = `/cbbbcf9a-2105-4289-9874-45d3ca20dd2e` | Kích hoạt khi có dữ liệu mới trong Google Sheets. |
| `Send message by Gmail` | Gmail Tool | Credentials = `gmailOAuth2` | Gửi email. |
| `Entry Point: Chat with the Agent` | Chat Trigger | - | Bắt đầu cuộc trò chuyện với AI. |
| `Personal Email Assistant` | Agent | - | Xử lý logic gửi email. |
| `AI Model Open AI` | lmChatOpenAi | Credentials = `openAiApi`, Model = `gpt-4o-mini` | Đánh giá và tạo nội dung email. |
| `Chat Memory` | memoryBufferWindow | - | Lưu trữ lịch sử hội thoại. |
| `Node that connects to the MCP server.` | mcpClientTool | Credentials = `mcpClientTool` | Gửi dữ liệu trở lại MCP Server. |
| `Thinker, think before executing.` | toolThink | - | Đưa ra quyết định trước khi thực thi. |
| `Supplier database.` | googleSheetsTool | Credentials = `googleSheetsOAuth2Api` | Tìm kiếm nhà cung cấp. |

> **Tip**: Đảm bảo các credentials đã được cấu hình trong **Credentials** của n8n. Nếu chưa, vào **Credentials** → **New Credential** → chọn loại tương ứng.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** với dữ liệu mẫu (đặt tên nhà cung cấp và nội dung email).  
2. Kiểm tra log: Đảm bảo AI trả về nội dung email đúng và Gmail Tool đã gửi thành công.  
3. Bật **Active**: Khi mọi thứ ổn, bật toggle “Active” để workflow tự động chạy khi có trigger.

## ✍️ Mẹo & gợi ý nâng cao

- **Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo khi email được gửi.  
- **Lưu log**: Dùng Google Sheets hoặc Airtable để ghi lại lịch sử gửi email.  
- **Báo cáo định kỳ**: Thêm node “Cron” để gửi báo cáo hàng ngày/tuần về số lượng email đã gửi.  
- **Tùy chỉnh mẫu email**: Sử dụng biến `${subject}` và `${body}` trong Gmail Tool để dễ dàng thay đổi.  
- **Xử lý lỗi**: Thêm node “Error Trigger” để gửi cảnh báo khi có lỗi gửi email.

## 📌 Kết luận

Workflow “Automated Email Assistant for Suppliers” giúp các sếp **tiết kiệm thời gian**, **đảm bảo chính xác** và **tăng tính chuyên nghiệp** trong giao tiếp với nhà cung cấp.  
Hãy thử ngay, tùy chỉnh theo nhu cầu và mở rộng thêm các tính năng khác để tối ưu hoá quy trình kinh doanh của bạn!

---