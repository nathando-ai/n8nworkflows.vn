---
title: "🚀 🧠 Claude 3.7 Extended Thinking AI Agent – Tự động hóa trí tuệ nhân tạo mạnh mẽ"
description: "Workflow n8n cho phép bạn tạo một AI Agent dựa trên Claude 3.7 Extended Thinking qua một form đơn giản, trả về câu trả lời sâu sắc và suy nghĩ mở rộng mà không cần viết code."
slug: "claude-3-7-extended-thinking-ai-agent"
tags: [n8n, automation, no-code, AI, Claude, LLM, form-trigger]
keywords: [n8n workflow, Claude 3.7, AI agent, tự động hóa, form trigger, http request]
---

# 🚀 🧠 Claude 3.7 Extended Thinking AI Agent – Tự động hóa trí tuệ nhân tạo mạnh mẽ

Bạn từng cảm thấy mệt mỏi khi phải lặp đi lặp lại các câu hỏi phức tạp, nghiên cứu thông tin hoặc viết bài phân tích sâu? Với cách làm thủ công, thời gian tiêu tốn cho mỗi lần suy nghĩ có thể lên tới hàng giờ. Workflow **Claude 3.7 Extended Thinking AI Agent** giải quyết vấn đề này bằng cách biến một form đơn giản thành một “não bộ” AI mạnh mẽ – bạn chỉ cần nhập câu hỏi, nhấn gửi và nhận ngay câu trả lời suy nghĩ mở rộng từ Claude 3.7, tất cả tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Nhận câu trả lời chi tiết trong giây, thay vì phải tìm kiếm và tổng hợp thủ công.
- **Chất lượng cao**: Claude 3.7 Extended Thinking cung cấp câu trả lời có độ sâu, logic và sáng tạo vượt trội.
- **Dễ sử dụng**: Giao diện form thân thiện, không cần kiến thức lập trình.
- **Hoạt động liên tục**: Workflow có thể được kích hoạt 24/7, sẵn sàng trả lời bất cứ khi nào bạn cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Claude (Anthropic)**: Cần có API Key để gọi model Claude 3.7.
- **n8n instance**: Đã cài đặt và có thể truy cập editor (self‑hosted hoặc n8n.cloud).
- (Tùy chọn) **Credentials lưu trữ**: Nếu muốn lưu lịch sử trò chuyện, cần chuẩn bị Google Sheets, Airtable hoặc database tương tự.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Trong n8n Editor, nhấn **Import** → **From JSON** hoặc dán trực tiếp JSON của workflow vào ô **Paste JSON**.
- Nhấn **Import** để workflow xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình các node sau để workflow hoạt động đúng:

| Node (tên trong workflow) | Loại node | Cấu hình bắt buộc |
|---------------------------|-----------|-------------------|
| **On form submission** | `formTrigger` | Kích hoạt trigger, không cần thay đổi gì thêm. |
| **Form** | `form` | Thiết lập các trường bạn muốn thu thập (ví dụ: “Câu hỏi” – loại Text, bắt buộc). Đảm bảo trường này có **Name** là `question` (hoặc tên bạn chọn) để node sau có thể truy cập. |
| **Claude Message** | `httpRequest` | - **Method**: `POST`<br>- **URL**: `https://api.anthropic.com/v1/messages`<br>- **Headers**: Thêm `x-api-key` (value = API Key Claude của bạn) và `anthropic-version: 2023-06-01`.<br>- **Body** (JSON):<br>```json\n{\n  \"model\": \"claude-3-7-sonnet-20240620\",\n  \"max_tokens\": 2000,\n  \"messages\": [\n    {\n      \"role\": \"user\",\n      \"content\": {{$json[\"question\"]}}\n    }\n  ]\n}\n```<br>*(Nếu bạn đổi tên trường trong Form, hãy thay `question` bằng tên trường tương ứng.)*<br>- **Authentication**: Không cần thêm nếu đã đặt API Key trong Header. |

> **Lưu ý**: Nếu bạn muốn lưu trữ cuộc trò chuyện, hãy thêm một node sau `Claude Message` (ví dụ: Google Sheets) và map `response` từ node HTTP Request vào sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Test Workflow** và gửi một câu hỏi mẫu qua form để kiểm tra phản hồi từ Claude.
- Nếu mọi thứ ổn, bật nút **Active** ở góc trên bên phải để workflow bắt đầu lắng nghe sự kiện form submission.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram sau `Claude Message` để tự động gửi câu trả lời vào kênh team của bạn.
- **Lưu lịch sử**: Kết hợp với Google Sheets hoặc Airtable để lưu trữ câu hỏi và câu trả lời, tạo thành cơ sở dữ liệu tri thức nội bộ.
- **Phân loại chủ đề**: Sử dụng node `IF` hoặc `Switch` để kiểm tra từ khóa trong câu hỏi và định tuyến tới các prompt khác nhau (ví dụ: code, marketing, hỗ trợ khách hàng).
- **Định kỳ tóm tắt**: Kết hợp với node `Cron` để mỗi ngày tự động tóm tắt các cuộc trò chuyện và gửi báo cáo qua email.
- **Tối ưu chi phí**: Thay đổi `max_tokens` trong body request để kiểm soát lượng token sử dụng và tiết kiệm chi phí API.

### 📌 Kết luận
Workflow **Claude 3.7 Extended Thinking AI Agent** mang lại sức mạnh của AI tiên tiến vào tay bạn mà không cần viết code. Với chỉ một form đơn giản, bạn có thể nhận được câu trả lời sâu sắc, sáng tạo và có thể mở rộng ngay lập tức. Hãy import, cấu hình và kích hoạt ngay hôm nay để tự động hóa quá trình suy nghĩ, giải phóng thời gian cho những việc thực sự quan trọng. 🚀