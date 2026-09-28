---
title: "🤖 Smart AI Router: Tự động chuyển hướng truy vấn đến GPT, Claude, Gemini hoặc Perplexity dựa trên loại nội dung"
description: "Hướng dẫn tự động hóa chuyển hướng truy vấn đến các mô hình AI phù hợp nhất dựa trên loại nội dung, tối ưu hóa hiệu suất và chi phí trong các cuộc trò chuyện AI."
slug: "smart-ai-router-tu-dong-chuyen-huong-truy-van-den-gpt-claude-gemini-perplexity"
tags: [n8n, automation, no-code, AI, chatbot]
keywords: [n8n workflow, tự động hóa, AI chatbot, model selector, LLM]
---

# 🤖 Smart AI Router: Tự động chuyển hướng truy vấn đến GPT, Claude, Gemini hoặc Perplexity dựa trên loại nội dung

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu hóa hiệu suất**: Tự động chọn mô hình AI phù hợp nhất cho từng loại truy vấn, đảm bảo phản hồi nhanh chóng và chính xác.
- **Tiết kiệm chi phí**: Chuyển hướng truy vấn đến mô hình AI rẻ hơn khi không cần độ chính xác cao.
- **Tăng trải nghiệm người dùng**: Cung cấp phản hồi nhanh chóng và liên tục cho người dùng.
- **Tích hợp dễ dàng**: Kết nối với các nền tảng chat hiện có như Slack, Telegram, hoặc các nền tảng tự động hóa khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản API từ các nhà cung cấp AI như OpenAI, Anthropic, Google Gemini, và OpenRouter.
- Kiến thức cơ bản về cách thiết lập và quản lý các tài khoản API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấp vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/7004](https://n8n.io/workflows/7004).
3. Nhấp vào "Import" để tải workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **When chat message received**: Cấu hình để nhận tin nhắn từ các nền tảng chat như Slack, Telegram, hoặc các nền tảng tự động hóa khác.
- **AI Agent**: Cấu hình để xử lý và phân loại các truy vấn từ người dùng.
- **Model Selector**: Cấu hình để chọn mô hình AI phù hợp nhất cho từng loại truy vấn.
- **Structured Output Parser**: Cấu hình để phân tích và định dạng đầu ra từ các mô hình AI.
- **Simple Memory**: Cấu hình để lưu trữ và truy xuất lịch sử cuộc trò chuyện.
- **Request Type**: Cấu hình để phân loại các truy vấn từ người dùng.
- **Opus 4**: Cấu hình để sử dụng mô hình AI của Anthropic.
- **Gemini Thinking Pro**: Cấu hình để sử dụng mô hình AI của Google Gemini.
- **GPT 4.1 mini**: Cấu hình để sử dụng mô hình AI của OpenAI.
- **Perplexity**: Cấu hình để sử dụng mô hình AI của OpenRouter.
- **OpenAI Chat Model**: Cấu hình để sử dụng mô hình AI của OpenAI.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Kết nối workflow với các nền tảng chat để tự động hóa các cuộc trò chuyện.
- **Lưu log**: Lưu trữ lịch sử các truy vấn và phản hồi để phân tích và cải thiện hiệu suất.
- **Gửi báo cáo định kỳ**: Tự động gửi báo cáo về hiệu suất và chi phí của các mô hình AI.
- **Tích hợp với các công cụ khác**: Kết nối workflow với các công cụ khác như Google Sheets, Notion, hoặc các công cụ quản lý dự án để lưu trữ và quản lý dữ liệu.

### 📌 Kết luận
Smart AI Router là một giải pháp tự động hóa mạnh mẽ để tối ưu hóa hiệu suất và chi phí trong các cuộc trò chuyện AI. Với khả năng tự động chuyển hướng truy vấn đến các mô hình AI phù hợp nhất, workflow này giúp các sếp tiết kiệm thời gian và tăng trải nghiệm người dùng. Hãy áp dụng ngay để trải nghiệm sự khác biệt!