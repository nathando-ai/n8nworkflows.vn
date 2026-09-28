---
title: "🚀 Tự động tạo bài đăng LinkedIn bằng AI & MCP Server"
description: "Giải pháp tự động tạo nội dung bài đăng LinkedIn bằng AI, tích hợp MCP Server, giảm thời gian soạn thảo và tăng hiệu quả."
slug: "tao-bai-dang-linkedin-voi-ai-mcp"
tags: [n8n, automation, no-code, LinkedIn, AI, MCP]
keywords: [n8n workflow, tự động hóa, LinkedIn, AI, MCP server]
---

# 🚀 Tự động tạo bài đăng LinkedIn bằng AI & MCP Server

Bạn có bao giờ phải ngồi gõ đi gõ lại những bài đăng LinkedIn, mất hàng giờ để suy nghĩ nội dung, chỉnh sửa, rồi vẫn không chắc chúng có “đánh trúng” mục tiêu?  
Việc này không chỉ tốn thời gian mà còn làm giảm năng suất của đội ngũ marketing và sales.  

**Workflow này** sẽ giải quyết toàn bộ quy trình: từ việc AI tạo nội dung, truyền tham số qua MCP Server, tới việc tự động đăng lên LinkedIn chỉ bằng một cú click – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo và đăng bài trong vòng vài giây.  
- **Nội dung chuẩn SEO**: AI tối ưu từ khóa, hashtags, và cấu trúc bài viết.  
- **Độ chính xác cao**: Không còn lỗi chính tả hay định dạng sai.  
- **Hoạt động liên tục**: MCP Server luôn sẵn sàng nhận yêu cầu từ AI agents.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản LinkedIn** có quyền sử dụng LinkedIn Tool (API).  
- **Credentials LinkedIn Tool** trong n8n (OAuth hoặc API token).  
- **MCP Server** đã được triển khai và có URL truy cập (được tạo tự động khi kích hoạt node `LinkedIn Tool MCP Server`).  
- **n8n phiên bản mới nhất** (để hỗ trợ node `@n8n/n8n-nodes-langchain`).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file workflow (hoặc copy/paste JSON vào ô).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **LinkedIn Tool MCP Server** (`mcpTrigger`) | Trigger nhận yêu cầu từ AI agents qua MCP. | - **Path**: `linkedin-tool-mcp` (đã có sẵn). <br> - **Credentials**: Không cần, đây là trigger nội bộ. |
| **Create a post** (`linkedInTool`) | Thực hiện hành động **Post → create** lên LinkedIn. | - **Credentials**: Chọn **LinkedIn Tool** đã tạo ở mục chuẩn bị. <br> - **Parameters**: Để trống, AI sẽ tự điền qua biểu thức `$fromAI()` (không cần chỉnh sửa nếu không muốn tùy biến). |

> **⚠️ Lưu ý:** Sau khi thêm credentials cho node **Create a post**, nhấn **Save** và **Close** mọi cửa sổ cấu hình để tránh lỗi “missing credentials”.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → gửi một payload mẫu từ MCP (hoặc dùng nút **Test** trong node `mcpTrigger`). Kiểm tra log để chắc chắn bài đăng được tạo thành công.  
2. Khi mọi thứ ổn, bật **Active** (góc trên bên phải) để workflow chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram ngay sau `Create a post` để nhận thông báo “Bài đăng đã được đăng thành công”.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại thời gian, nội dung, và ID bài đăng, giúp theo dõi hiệu suất.  
- **Lên lịch tự động**: Kết hợp node **Cron** để kích hoạt MCP theo lịch (hàng ngày, hàng tuần) và tự động tạo nội dung mới.  
- **Tùy biến Prompt AI**: Sửa tham số `prompt` trong node `Create a post` (nếu bạn muốn AI tạo nội dung theo chủ đề cụ thể).  

### 📌 Kết luận
Với workflow **Create LinkedIn Posts with AI Agents using MCP Server**, các sếp có thể loại bỏ hoàn toàn công đoạn soạn thảo thủ công, giảm thiểu sai sót, và duy trì hoạt động liên tục trên LinkedIn. Hãy import ngay, cấu hình credentials, và bật workflow – để AI và MCP Server làm việc thay bạn! 🚀