---
title: "🤖 Instagram MCP AI Agent – Đọc, Trả lời & Quản lý Bình luận bằng GPT‑4o"
description: "Workflow tự động hóa tương tác trên Instagram: khi có tin nhắn hoặc bình luận mới, AI Agent đọc nội dung, tìm kiếm bài viết, phân tích cảm xúc và tự động trả lời hoặc gửi DM bằng GPT‑4o, giúp bạn duy trì sự hiện diện 24/7 mà không cần can thiệp thủ công."
slug: "instagram-mcp-ai-agent-gpt4o"
tags: [n8n, automation, no-code, instagram, ai-agent, gpt-4o, mcp, social-media]
keywords: [n8n workflow, instagram automation, ai comment reply, gpt-4o instagram, mcp instagram, no-code social media]
---

# 🤖 Instagram MCP AI Agent – Đọc, Trả lời & Quản lý Bình luận bằng GPT‑4o

Bạn từng cảm thấy mệt mỏi khi phải liên tục kiểm tra bình luận, tin nhắn trên Instagram để trả lời kịp thời? Quá trình thủ công không chỉ tốn thời gian mà còn dễ bỏ lỡ cơ hội tương tác với khách hàng. Workflow **Instagram MCP AI Agent** giải quyết triệt để vấn đề này bằng cách kết hợp sức mạnh của **MCP (Model Context Protocol)** để truy cập dữ liệu Instagram và **GPT‑4o** để hiểu ý định, tạo phản hồi tự nhiên. Tout chỉ cần một lần cấu hình, workflow sẽ hoạt động 24/7, đọc, phân tích và trả lời bình luận hoặc gửi tin nhắn riêng tư tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ làm việc**: AI xử lý bình luận ngay khi xuất hiện, không cần can thiệp thủ công.
- **Trả lời chính xác & cá nhân hóa**: GPT‑4o hiểu ngữ cảnh và tạo phản hồi phù hợp với brand voice.
- **Hoạt động liên tục 24/7**: Workflow luôn lắng nghe, ngay cả khi bạn ngủ.
- **Mở rộng dễ dàng**: Thêm công cụ mới (Slack, Telegram, Google Sheets…) để ghi log hoặc báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Instagram** có quyền truy cập Graph API (Access Token & User ID) – sẽ được cấu hình trong node **MCP Instagram** (mcpTrigger & mcpClientTool).
- **API Key OpenAI** để truy cập model **gpt-4o** – cấu hình trong node **Chat Model** (lmChatOpenAi).
- (Tùy chọn) Tài khoản n8n để import workflow và lưu credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Trong n8n Editor, nhấn **Import** → **From JSON** (hoặc copy/paste toàn bộ JSON workflow từ link gốc).
2. Nhấn **Import** để thêm workflow vào danh sách của bạn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình các node sau để workflow hoạt động:

| Node | Loại | Cấu hình bắt buộc |
|------|------|-------------------|
| **When chat message received** | `chatTrigger` | Kích hoạt trigger để lắng nghe tin nhắn từ n8n Chat (hoặc tích hợp với Slack/Telegram nếu muốn). Không cần credential đặc biệt. |
| **AI Agent** | `agent` | Chọn **Tools** → thêm tất cả các tool sau: `MCP Instagram`, `Search Media`, `Media Details`, `Search Comment`, `Reply Comment`, `Send Direct Message`. Đảm bảo **Memory** được gán là node **Simple Memory**. |
| **Simple Memory** | `memoryBufferWindow` | Để mặc định (window size = 5) hoặc tùy chỉnh nếu muốn ghi nhớ hơn. |
| **🗂️ MCP Instagram** | `mcpTrigger` | Cấu hình credential **Instagram MCP** (cung cấp **Access Token** và **User ID** của trang Instagram bạn muốn quản lý). |
| **MCP Instagram** | `mcpClientTool` | Sử dụng cùng credential Instagram MCP như trên. Tool này cung cấp các hàm như `getUserMedia`, `getComments`, `replyComment`, `sendDirectMessage`. |
| **Search Media** | `toolHttpRequest` | Phương thức `GET`, endpoint: `https://graph.instagram.com/me/media?fields=id,caption,media_type,thumbnail_url&access_token={{ $json["access_token"] }}`. Credential: **Instagram MCP** (access token sẽ được truyền tự động từ node trước). |
| **Instagram Mapping** | `set` | Ánh xạ dữ liệu từ `Search Media` sang định dạng mà Agent cần (ví dụ: `mediaId`, `caption`). Không cần credential. |
| **Media Details** | `toolHttpRequest` | Lấy chi tiết một bài viết cụ thể: `https://graph.instagram.com/{{ $json["mediaId"] }}?fields=id,caption,media_type,permalink&access_token={{ $json["access_token"] }}`. |
| **Search Comment** | `toolHttpRequest` | Tìm comment mới nhất trên bài viết: `https://graph.instagram.com/{{ $json["mediaId"] }}/comments?fields=id,text,username,timestamp&access_token={{ $json["access_token"] }}&limit=5`. |
| **Reply Comment** | `toolHttpRequest` | Phương thức `POST` đến `https://graph.instagram.com/{{ $json["commentId"] }}/replies` với body `{ "message": "{{ $json["aiResponse"] }}", "access_token": "{{ $json["access_token"] }}" }`. |
| **Send Direct Message** | `toolHttpRequest` | Phương thức `POST` đến `https://graph.instagram.com/{{ $json["userId"] }}/messages` với body `{ "recipient_id": "{{ $json["targetUserId"] }}", "message": "{{ $json["aiResponse"] }}", "access_token": "{{ $json["access_token"] }}" }`. |
| **Chat Model** | `lmChatOpenAi` | Cấu hình credential **OpenAI API Key**, chọn model **gpt-4o**, temperature ~0.7 để phản hồi sáng tạo nhưng vẫn cohærent. |

> **Lưu ý quan trọng**: Sau khi nhập credentials, hãy nhấn **Save** trên mỗi node rồi thực hiện **Test Workflow** với một tin nhắn mẫu (ví dụ: “Hey, bài viết mới này hay quá!”) để xác nhận AI trả lời đúng và các thao tác trên Instagram được thực hiện.

#### 3. Kích hoạt ⚡️
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải workflow.
- Từ giờ workflow sẽ tự động lắng nghe tin nhắn qua n8n Chat (hoặc các kênh bạn đã tích hợp) và thực hiện chuỗi hành động trên Instagram mà không cần can thiệp nào khác.

### ✍️ Mẹo & gợi ý nâng cao
- **Ghi log vào Google Sheets**: Thêm node **Google Sheets** sau mỗi phản hồi để lưu lại nội dung tin nhắn, thời gian và phản hồi AI – giúp bạn phân tích hiệu suất.
- **Thông báo Slack/Telegram**: Khi AI phát hiện bình luận tiêu cực (negative sentiment), gửi cảnh báo ngay tới kênh nội bộ để팀 can thiệp kịp thời.
- **Tùy chỉnh prompt**: Trong node **Chat Model**, chỉnh sửa **System Message** để định hình tone của AI (ví dụ: “Bạn là trợ lý thương hiệu thân thiện, luôn sử dụng tiếng Việt và thêm emoticon phù hợp.”).
- **Giới hạn tần suất**: Thêm node **Cron** hoặc **Interval** trước `chatTrigger` nếu bạn chỉ muốn kiểm tra mỗi 5 phút thay vì real‑time (giảm lượng API call).
- **Quản lý nhiều tài khoản Instagram**: Sao chép bộ節 `MCP Instagram` + các tool liên quan và thay đổi credential để chạy đồng thời cho nhiều trang.

### 📌 Kết luận
Workflow **Instagram MCP AI Agent** giúp bạn biến Instagram từ kênh tương tác thủ công thành một hệ thống tự động thông minh, luôn sẵn sàng trả lời, trò chuyện và chăm sóc cộng đồng 24/7. Với chỉ một lần cấu hình credential và một chút tinh chỉnh prompt, bạn sẽ tiết kiệm hàng giờ mỗi tuần đồng thời nâng trải nghiệm khách hàng lên một tầm cao mới. Hãy import ngay hôm nay và để AI làm việc thay bạn! 🚀