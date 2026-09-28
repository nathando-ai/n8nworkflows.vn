---
title: "🚀 Thiết kế giao diện UI tự động qua Telegram với Google Stitch, MCP và Gemini trong n8n"
description: "Hướng dẫn xây dựng trợ lý AI thiết kế và tạo nguyên mẫu (prototype) giao diện trực tiếp trên Telegram sử dụng Google Gemini, Google Stitch MCP và n8n."
slug: "thiet-ke-giao-dien-ui-qua-telegram-voi-google-stitch-mcp-gemini"
tags: [n8n, automation, telegram, ai-agent, google-gemini, mcp]
keywords: [n8n workflow, google stitch, mcp client, telegram bot, google gemini ai, ui design automation]
---

# 🚀 Thiết kế giao diện UI tự động qua Telegram với Google Stitch, MCP và Gemini

Các sếp có bao giờ mơ ước có thể yêu cầu một trợ lý AI tạo ra các màn hình giao diện (UI screen) hoặc quản lý các dự án thiết kế chỉ bằng một tin nhắn chat đơn giản trên Telegram chưa? Việc phải chuyển đổi qua lại giữa nhiều công cụ thiết kế thủ công cực kỳ mất thời gian.

Workflow này chính là giải pháp tự động hóa 100% không cần code (No-code), kết hợp sức mạnh của **Telegram Bot**, **Google Gemini AI**, và **Google Stitch (MCP - Model Context Protocol)** để biến mọi ý tưởng ngôn ngữ tự nhiên thành hiện thực ngay trên chiếc điện thoại của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Điều khiển qua Telegram:** Gửi lệnh `/stitch` kèm theo yêu cầu thiết kế bất cứ lúc nào, ở bất cứ đâu.
- **Tích hợp Google Stitch MCP:** Tự động tạo dự án, lấy danh sách màn hình, quản lý và sinh UI screen tự động thông qua giao thức MCP.
- **Bộ não AI thông minh:** Sử dụng Google Gemini kết hợp bộ nhớ ngữ cảnh (`Simple Memory`) và công cụ tìm kiếm web (`Perplexity Tool`) để đưa ra câu trả lời chính xác nhất.
- **Định dạng hiển thị chuẩn:** Tự động chuyển đổi từ Markdown sang HTML để hiển thị mượt mà trên khung chat Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Google Gemini API Key** (Google Palm/Gemini credentials).
- **Google Stitch API Key** và cấu hình HTTP Header Auth (Xem tài liệu tại [Google Stitch MCP Setup](https://stitch.withgoogle.com/docs/mcp/setup)).
- **Perplexity API Key** (dùng cho công cụ tìm kiếm web bổ trợ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các thành phần sau:
- **Get Message (telegramTrigger)** & **Send a text message (telegram):** Kết nối với Telegram Bot Credentials của các sếp.
- **Clean query (code) & is Telegram? (if):** Cấu hình ID Telegram cá nhân hoặc nhóm được phép tương tác trong node mã nguồn, đảm bảo bot chỉ phản hồi khi tin nhắn chứa lệnh `/stitch`.
- **Create Project, Get Project, List projects, List screen, Get screen, Generate Screen (mcpClientTool):** Tất cả các node MCP Client này đều yêu cầu sử dụng chung một cấu hình **HTTP Header Auth** với tên Header là `"X-Goog-Api-Key"` và giá trị là API Key lấy từ [Google Stitch](https://stitch.withgoogle.com/docs/mcp/setup).
- **Google Gemini Chat Model (lmChatGoogleGemini):** Nhập Google API Key để kích hoạt mô hình AI Gemini.
- **Search on web (perplexityTool):** Thêm Perplexity API Key để AI có thể tra cứu thông tin web khi cần thiết.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với tin nhắn mẫu trên Telegram chứa lệnh `/stitch [yêu cầu thiết kế của bạn]`.
- Kiểm tra kết quả trả về và bật trạng thái **Active** cho workflow để chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord để đồng thời gửi các bản thiết kế UI hoặc thông báo dự án về kênh làm việc chung của team.
- **Lưu trữ dữ liệu dự án:** Thêm Google Sheets hoặc Airtable node để lưu lịch sử các yêu cầu thiết kế và trạng thái dự án.
- **Báo cáo định kỳ:** Tạo thêm một nhánh cron (Schedule Trigger) để tổng hợp số lượng màn hình được thiết kế trong tuần gửi về Telegram cho các sếp.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc kết hợp giữa AI Agent, công nghệ MCP tiên tiến và các ứng dụng nhắn tin hàng ngày. Hãy cài đặt ngay để sở hữu một trợ lý thiết kế UI tự động hóa thông minh ngay trong tầm tay các sếp!