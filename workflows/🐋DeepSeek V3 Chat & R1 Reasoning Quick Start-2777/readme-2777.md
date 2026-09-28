---
title: "🚀 DeepSeek V3 Chat & R1 Reasoning - Tự động hóa AI không cần code"
description: "Hướng dẫn chi tiết cách tự động hóa chatbot DeepSeek V3 và mô hình lý luận R1 bằng n8n. Giải phóng thời gian và nâng cao hiệu suất làm việc với AI."
slug: "deepseek-v3-chat-r1-reasoning-n8n"
tags: [n8n, automation, no-code, AI, DeepSeek]
keywords: [n8n workflow, tự động hóa AI, DeepSeek, chatbot, lý luận AI]
---

# 🚀 DeepSeek V3 Chat & R1 Reasoning - Tự động hóa AI không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý nhiều yêu cầu chatbot và lý luận AI. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn các tương tác chatbot với DeepSeek V3
- Xử lý lý luận phức tạp với mô hình DeepSeek R1
- Tiết kiệm thời gian lên tới 80% so với làm thủ công
- Tích hợp dễ dàng với các hệ thống khác thông qua HTTP API
- Lưu trữ lịch sử hội thoại với bộ nhớ cửa sổ trượt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản DeepSeek với API key (https://platform.deepseek.com/api_keys)
- (Tùy chọn) Máy chủ Ollama để chạy mô hình local (https://ollama.com/)
- Kiến thức cơ bản về n8n và cấu hình API
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/2777
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **When chat message received (chatTrigger)**
   - Cấu hình webhook endpoint để nhận tin nhắn
   - Đặt tên biến cho tin nhắn nhận được (ví dụ: `userMessage`)

2. **DeepSeek (lmChatOpenAi)**
   - Tạo credential mới với loại "OpenAI API"
   - Điền thông tin:
     - Base URL: `https://api.deepseek.com`
     - API Key: [API key của bạn từ DeepSeek]
   - Trong node DeepSeek, chọn credential vừa tạo
   - Đảm bảo tham số `model` được đặt là `deepseek-reasoner`

3. **Ollama DeepSeek (lmChatOllama)**
   - Tạo credential mới với loại "Ollama API"
   - Điền thông tin:
     - Base URL: `http://localhost:11434` (hoặc địa chỉ máy chủ Ollama của bạn)
   - Trong node Ollama DeepSeek, chọn credential vừa tạo
   - Đảm bảo tham số `model` được đặt là `deepseek-r1:14b`

4. **DeepSeek JSON Body (httpRequest)**
   - Tạo credential mới với loại "HTTP Header Auth"
   - Điền thông tin:
     - Header Name: `Authorization`
     - Header Value: `Bearer [API key của bạn từ DeepSeek]`
   - Trong node DeepSeek JSON Body, chọn credential vừa tạo
   - Đặt URL: `https://api.deepseek.com/v1/chat/completions`
   - Đảm bảo phương thức là POST

5. **DeepSeek Raw Body (httpRequest)**
   - Sử dụng cùng credential với node DeepSeek JSON Body
   - Đặt URL: `https://api.deepseek.com/v1/chat/completions`
   - Đảm bảo phương thức là POST

#### 3. Kích hoạt ⚡️
1. Thử chạy workflow với dữ liệu mẫu để kiểm tra kết nối
2. Kiểm tra các node DeepSeek và Ollama DeepSeek trả về kết quả như mong đợi
3. Bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để tạo chatbot hoàn chỉnh
- Thêm node để lưu lịch sử hội thoại vào Google Sheets hoặc cơ sở dữ liệu
- Tạo báo cáo định kỳ về các tương tác chatbot
- Kết hợp với các công cụ phân tích dữ liệu để cải thiện mô hình

### 📌 Kết luận
Workflow DeepSeek V3 Chat & R1 Reasoning giúp các sếp tự động hóa hoàn toàn các tương tác chatbot và lý luận AI với DeepSeek. Với cấu hình đơn giản và kết quả mạnh mẽ, đây là giải pháp lý tưởng cho các doanh nghiệp muốn nâng cao hiệu suất làm việc mà không cần viết code. Hãy thử ngay và thấy sự khác biệt!