---
title: "🚀 Tích hợp Trợ lý AI Telegram Tra cứu Giá & Thông tin Crypto Real-time với DexScreener và GPT-4o"
description: "Hướng dẫn xây dựng chatbot Telegram sử dụng n8n, AI Agent (GPT-4o) và DexScreener API để tra cứu thông tin token, phân tích thị trường crypto tự động 24/7."
slug: "chatbot-telegram-crypto-insights-dexscreener-gpt4o"
tags: [n8n, automation, no-code, crypto, ai-agent, telegram, openai]
keywords: [n8n workflow, dexscreener api, telegram bot crypto, gpt-4o ai agent, tự động hóa crypto, tra cứu token real-time]
---

# 🚀 Tích hợp Trợ lý AI Telegram Tra cứu Giá & Thông tin Crypto Real-time với DexScreener và GPT-4o

Trong thị trường tiền mã hóa (crypto) biến động từng giây, việc cập nhật thông tin token, giá cả, thanh khoản hay các token đang được "boost" một cách thủ công là cực kỳ mất thời gian và dễ bỏ lỡ cơ hội. Nhiều nhà đầu tư phải liên tục chuyển đổi giữa các tab trình duyệt để check dữ liệu trên DexScreener.

Giải pháp là đây! Workflow n8n này sẽ giúp các sếp tạo ra một trợ lý AI thông minh ngay trên **Telegram**. Chỉ cần nhắn tin hỏi, AI Agent tích hợp **GPT-4o** sẽ tự động gọi các API của **DexScreener** để trả về biểu đồ, giá, thanh khoản, token mới nổi... cực kỳ chính xác và nhanh chóng mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thời gian thực:** Lấy dữ liệu trực tiếp từ DexScreener qua các công cụ API chuyên sâu (Latest Profiles, Boosted Tokens, Search Pairs...).
- **Tương tác tự nhiên:** Trò chuyện trực tiếp với AI qua Telegram Bot như một chuyên gia tư vấn tài chính thực thụ.
- **Tự động hóa 24/7:** Bot hoạt động không nghỉ, giúp nắm bắt thông tin token mọi lúc mọi nơi.
- **Tiết kiệm thời gian:** Không cần tra cứu thủ công nhiều bước, chỉ cần một câu lệnh chat đơn giản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua [@BotFather](https://t.me/BotFather)).
- **OpenAI API Key** (Có quyền truy cập model `gpt-4o-mini` hoặc `gpt-4o`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ hệ thống n8n hoặc copy toàn bộ JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thông số quan trọng sau tại các nodes:

- **Telegram Trigger & Telegram Node**: 
  - Kết nối với `telegramApi` credentials bằng cách nhập Telegram Bot Token lấy từ BotFather. Node này giúp nhận tin nhắn từ người dùng và gửi phản hồi trả về.
- **OpenAI Chat Model**: 
  - Chọn credentials `openAiApi` với OpenAI API Key của các sếp.
  - Đảm bảo model được chọn là `gpt-4o-mini` hoặc `gpt-4o` để AI có tư duy phân tích tốt nhất.
- **Blockchain DEX Screener Insights Agent**: 
  - Đây là trung tâm đầu não điều phối AI, kết nối các công cụ (Tools) bên dưới để trả lời câu hỏi của user.
- **Các tool DexScreener (HTTP Request Tools)**: 
  - Các node như `DexScreener Latest Token Profiles`, `DexScreener Search Pairs`, `DexScreener Token Pools`... đã được cấu hình sẵn endpoint chuẩn của DexScreener. AI Agent sẽ tự động chọn tool phù hợp dựa theo câu hỏi của người dùng (ví dụ: hỏi về token mới -> dùng Latest Profiles; hỏi về giá cặp giao dịch -> dùng Search Pairs).
- **Adds SessionId (Set Node)**: 
  - Đảm bảo việc lưu trữ ngữ cảnh hội thoại, giúp bot nhớ được lịch sử chat của người dùng trong phiên làm việc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn test tới Telegram Bot của các sếp (ví dụ: *"Tìm giúp tôi thông tin về token PEPE"*).
- Kiểm tra kết quả trả về trên Telegram. Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để chatbot chính thức đi vào hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm tính năng ghi log lịch sử:** Kết nối thêm một node Google Sheets hoặc Airtable để lưu lại các câu hỏi của user nhằm phân tích nhu cầu tìm kiếm token.
- **Cảnh báo giá tự động:** Kết hợp thêm node Cron (Schedule Trigger) để định kỳ quét các token hot trên DexScreener và chủ động bắn tin nhắn cảnh báo về Telegram channel của các sếp.
- **Mở rộng AI Tools:** Có thể tích hợp thêm các API phân tích on-chain khác như Etherscan, CoinGecko hoặc Birdeye để AI có lượng kiến thức đa dạng hơn.

### 📌 Kết luận
Với workflow n8n này, các sếp đã có ngay một "trợ lý ảo" crypto cực kỳ chuyên nghiệp trên Telegram mà không cần tốn chi phí thuê lập trình viên hay mua các tool đắt đỏ. Hãy cài đặt ngay và tối ưu hóa quy trình đầu tư crypto của mình thôi nào!