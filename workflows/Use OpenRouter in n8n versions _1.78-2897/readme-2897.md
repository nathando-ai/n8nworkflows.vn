---
title: "🚀 Tự động hóa Chatbot AI với OpenRouter trong n8n - Hỗ trợ 10+ LLM"
description: "Hướng dẫn cấu hình workflow n8n để tạo chatbot AI linh hoạt, hỗ trợ nhiều LLM như OpenAI, Google Gemini, Mistral... mà không cần code"
slug: "tu-dong-hoa-chatbot-ai-openrouter-n8n"
tags: [n8n, automation, no-code, AI, chatbot]
keywords: [n8n workflow, tự động hóa, chatbot AI, OpenRouter, LLM]
---

# 🚀 Tự động hóa Chatbot AI với OpenRouter trong n8n - Hỗ trợ 10+ LLM

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải chuyển đổi giữa nhiều nền tảng AI khác nhau. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian chuyển đổi giữa các nền tảng AI khác nhau
- Hỗ trợ 10+ LLM lớn như OpenAI, Google Gemini, Mistral...
- Ghi nhớ lịch sử chat tự động (memory buffer)
- Tích hợp dễ dàng với các kênh chat phổ biến
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenRouter (https://openrouter.ai/)
- API Key từ OpenRouter
- Kiến thức cơ bản về n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
```bash
# Copy JSON từ link gốc: https://n8n.io/workflows/2897
# Hoặc tải file JSON về máy
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Settings"**:
   - Thêm biến môi trường `model` với giá trị mặc định (ví dụ: `openai/o3-mini`)
   - Ví dụ các model có sẵn:
     ```json
     {
       "model": "openai/o3-mini"
     }
     ```

2. **Node "LLM Model"**:
   - Chọn credentials `openAiApi` (đã cấu hình API Key từ OpenRouter)
   - Đảm bảo tham số `model` được truyền đúng từ node Settings

3. **Node "When chat message received"**:
   - Cấu hình kênh chat (Slack, Telegram, Webhook...)
   - Đảm bảo webhook được kích hoạt nếu sử dụng kênh này

#### 3. Kích hoạt ⚡️
- Test run với câu hỏi mẫu: "Giới thiệu về OpenRouter"
- Kiểm tra kết quả trả về từ LLM
- Bật Active workflow khi đã ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. Thêm node "Email" để gửi báo cáo hàng ngày về các cuộc trò chuyện
2. Kết hợp với node "Google Sheets" để lưu trữ lịch sử chat
3. Tạo nhiều phiên chat song song bằng cách sao chép node "Chat Memory"
4. Thêm node "Slack" để thông báo khi có câu hỏi phức tạp cần can thiệp

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa chatbot AI một cách linh hoạt, hỗ trợ nhiều nền tảng LLM lớn mà không cần viết code. Hãy thử ngay để tiết kiệm thời gian và nâng cao trải nghiệm khách hàng!