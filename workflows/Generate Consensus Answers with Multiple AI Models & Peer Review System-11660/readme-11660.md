---
title: "🚀 Tạo Hội Đồng AI Đa Mô Hình và Đánh Giá Chéo (Peer Review) với n8n"
description: "Hướng dẫn xây dựng hệ thống AI Consensus tự động trên n8n, kết hợp nhiều mô hình LLM qua OpenRouter để tự động trả lời câu hỏi, phản biện chéo và tổng hợp kết quả tối ưu."
slug: "tao-hoi-dong-ai-da-mo-hinh-peer-review-n8n"
tags: [n8n, automation, ai, openrouter, deepseek, llm]
keywords: [n8n workflow, ai council, peer review ai, openrouter n8n, multi model llm, tu dong hoa ai]
---

# 🚀 Tạo Hội Đồng AI Đa Mô Hình và Đánh Giá Chéo (Peer Review) với n8n

Các sếp có bao giờ cảm thấy câu trả lời từ một mô hình AI đơn lẻ đôi khi chưa đủ độ khách quan, hoặc có hiện tượng "ảo giác" (hallucination)? Việc phụ thuộc vào duy nhất một LLM có thể bỏ sót nhiều góc nhìn quan trọng. 

Được truyền cảm hứng từ dự án nổi tiếng *LLM Council* của Andrej Karpathy, workflow n8n này sẽ giúp các sếp tạo ra một **"Hội đồng AI" (AI Council)** thu nhỏ. Hệ thống sẽ để nhiều mô hình AI độc lập trả lời câu hỏi của bạn, sau đó chúng sẽ tự động đọc, chấm điểm và phản biện chéo (peer review) lẫn nhau trước khi một mô hình trọng tài (như DeepSeek R1) tổng hợp ra câu trả lời hoàn hảo nhất! Giải pháp tự động hóa 100% không cần code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng độ chính xác vượt trội:** Nhờ cơ chế tổng hợp đa góc nhìn từ nhiều dòng mô hình khác nhau (Google, Meta, Mistral, DeepSeek).
- **Loại bỏ độ lệch (Bias):** Quá trình phản biện chéo diễn ra hoàn toàn ẩn danh, giúp các mô hình đánh giá khách quan ưu/nhược điểm câu trả lời của nhau.
- **Tiết kiệm thời gian nghiên cứu:** Thay vì phải mở nhiều tab chat với các AI khác nhau rồi tự so sánh, hệ thống tự động làm tất cả trong một luồng duy nhất.
- **Tùy biến linh hoạt:** Dễ dàng thay thế, thêm bớt các mô hình AI thông qua OpenRouter chỉ bằng vài cú click.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [n8n](https://n8n.io) (Self-hosted hoặc Cloud).
- Tài khoản [OpenRouter](https://openrouter.ai/) có sẵn API Key và một ít credit để gọi các mô hình AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện chính thức của n8n (Link: `https://n8n.io/workflows/11660`) và tiến hành Import trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node sau:
- **Cấu hình Credentials OpenRouter:** Tại các node như `Gemini Model`, `Mistral Model`, `Gemma Model`, `Llama Model`, và `Deepseek R1 model`, hãy tạo và chọn `OpenRouter API Credentials` bằng cách dán API Key của các sếp vào.
- **Kiểm tra Model Parameters:** Workflow mẫu đang sử dụng các model ID phổ biến trên OpenRouter:
  - `Gemini Model`: `google/gemini-2.0-flash-001`
  - `Mistral Model`: `mistralai/mistral-nemo`
  - `Gemma Model`: `google/gemma-3n-e4b-it`
  - `Llama Model`: `meta-llama/llama-3.2-1b-instruct`
  - `Deepseek R1 model`: `deepseek/deepseek-r1` (đóng vai trò tổng hợp cuối cùng).
  Các sếp có thể thay đổi model tuỳ ý thích hoặc nhu cầu ngân sách.
- **Chat Trigger:** Node khởi đầu luồng, cho phép nhập câu hỏi trực tiếp qua giao diện chat của n8n.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng giao diện Chat Trigger để xem các mô hình trả lời và phản biện nhau.
- Sau khi kiểm tra mọi thứ hoạt động ổn định, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy chỉnh tiêu chí đánh giá:** Tại các node `Review Agent #1` đến `#4`, các sếp có thể tinh chỉnh prompt để yêu cầu AI chấm điểm theo các tiêu chí cụ thể như: tính thực tế, độ ngắn gọn, hoặc tính bảo mật.
- **Mở rộng kênh giao tiếp:** Thay vì chỉ dùng Chat Trigger nội bộ của n8n, các sếp có thể tích hợp thêm Webhook để nhận câu hỏi từ **Slack, Discord hoặc Telegram**.
- **Lưu lịch sử:** Thêm một node Google Sheets hoặc Database ở cuối luồng để lưu lại câu hỏi và bản tổng hợp consensus nhằm phục vụ việc tra cứu về sau.

### 📌 Kết luận
Mô hình "Hội đồng AI" với cơ chế Peer Review là một bước tiến lớn giúp nâng tầm chất lượng câu trả lời từ LLM trong các tác vụ phức tạp. Hãy cài đặt ngay workflow này lên hệ thống n8n của các sếp để trải nghiệm sức mạnh của việc kết hợp đa mô hình thông minh!