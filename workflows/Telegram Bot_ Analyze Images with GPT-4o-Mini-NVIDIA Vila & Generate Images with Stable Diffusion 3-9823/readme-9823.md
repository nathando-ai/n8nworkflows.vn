---
title: "🤖 Telegram Bot: Phân tích hình ảnh với GPT-4o-Mini-NVIDIA Vila & Tạo hình với Stable Diffusion 3"
description: "Tự động hóa phân tích hình ảnh và tạo hình từ Telegram bằng công nghệ AI tiên tiến của NVIDIA và OpenAI. Tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "telegram-bot-phan-tich-tao-hinh-ai"
tags: [n8n, automation, no-code, telegram, ai, nvidia, openai]
keywords: [n8n workflow, tự động hóa, telegram bot, ai phân tích hình ảnh, tạo hình ai, stable diffusion, gpt-4o-mini]
---

# 🤖 Telegram Bot: Phân tích hình ảnh với GPT-4o-Mini-NVIDIA Vila & Tạo hình với Stable Diffusion 3

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Phân tích hình ảnh chỉ trong vài giây thay vì hàng giờ làm thủ công
- **Chính xác cao**: Công nghệ AI tiên tiến của NVIDIA và OpenAI mang lại kết quả phân tích đáng tin cậy
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
- **Nâng cao hiệu suất**: Xử lý hàng loạt hình ảnh và văn bản một cách nhanh chóng và hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Telegram Bot Token**: Tạo bot qua @BotFather và lấy token
- **OpenAI API Key**: Đăng ký tài khoản OpenAI và tạo API key
- **NVIDIA API Key**: Đăng ký tài khoản NVIDIA và tạo API key (có thể dùng gói miễn phí)
- **Gmail OAuth2 Credentials**: Cấu hình xác thực OAuth2 cho Gmail
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/9823)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Telegram Trigger**:
   - Cấu hình credentials "telegramApi" với token của bot Telegram
   - Đảm bảo bot có quyền truy cập vào các kênh/nhóm cần xử lý

2. **HTTP Request Nodes**:
   - Cấu hình credentials "httpBearerAuth" cho cả hai node HTTP Request
   - Điền API key của NVIDIA vào phần Authorization header

3. **Gmail Nodes**:
   - Cấu hình credentials "gmailOAuth2" cho cả hai node Gmail
   - Đảm bảo tài khoản Gmail có quyền gửi email

4. **OpenAI Node**:
   - Cấu hình credentials "openAiApi" với API key của OpenAI
   - Đảm bảo tài khoản OpenAI có quyền truy cập vào GPT-4 Vision

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Gửi một hình ảnh đến bot Telegram để kiểm tra phân tích
   - Gửi một đoạn văn bản để kiểm tra tạo hình
2. Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối với Slack/Discord**: Thay thế node Gmail bằng node Slack/Discord để nhận thông báo
2. **Lưu trữ kết quả**: Kết nối với Google Sheets hoặc cơ sở dữ liệu để lưu trữ lịch sử phân tích
3. **Tích hợp thêm AI models**: Thêm node Anthropic hoặc Gemini để mở rộng khả năng xử lý
4. **Xử lý âm thanh/tài liệu**: Thêm node để xử lý âm thanh và tài liệu PDF

### 📌 Kết luận
Workflow này biến Telegram bot của bạn thành một hệ thống AI toàn diện, có thể phân tích hình ảnh và tạo hình một cách tự động. Với công nghệ tiên tiến của NVIDIA và OpenAI, bạn có thể tiết kiệm thời gian đáng kể và nâng cao hiệu suất làm việc. Hãy thử ngay và trải nghiệm sức mạnh của tự động hóa AI!