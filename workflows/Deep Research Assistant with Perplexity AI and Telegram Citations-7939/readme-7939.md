---
title: "🚀 Xây dựng Trợ lý Nghiên cứu Chiều sâu (Deep Research) tích hợp Perplexity AI và Telegram"
description: "Hướng dẫn tự động hóa trợ lý nghiên cứu thông minh trên Telegram sử dụng AI Agent, OpenAI GPT-4o-mini và Perplexity AI để tra cứu thông tin kèm trích dẫn nguồn."
slug: "tro-ly-nghien-cuu-deep-research-perplexity-telegram"
tags: [n8n, automation, ai-agent, telegram, perplexity, openai]
keywords: [n8n workflow, deep research ai, telegram bot ai, perplexity sonar, openai gpt-4o-mini, tu dong hoa nghien cuu]
useStrictParsing: true
---

# 🚀 Xây dựng Trợ lý Nghiên cứu Chiều sâu (Deep Research) tích hợp Perplexity AI và Telegram

Việc tìm kiếm thông tin chuyên sâu, phân tích thị trường hay tổng hợp tài liệu học thuật thường tiêu tốn hàng giờ đồng hồ lướt web thủ công. Thay vì làm việc đó bằng tay, các sếp hoàn toàn có thể sở hữu một "Trợ lý Nghiên cứu" (Deep Research Assistant) trực chiến 24/7 ngay trên ứng dụng Telegram của mình.

Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: Nhận câu hỏi từ Telegram, điều phối thông minh qua AI Agent, kết hợp sức mạnh tìm kiếm thời gian thực của Perplexity (Sonar & Sonar Pro) và trả về kết quả chuẩn xác kèm trích dẫn nguồn ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tra cứu thời gian thực:** Kết hợp dữ liệu mới nhất từ internet thông qua Perplexity AI.
- **Định tuyến thông minh:** AI tự động chọn mô hình Sonar (cho tra cứu nhanh) hoặc Sonar Pro (cho nghiên cứu chuyên sâu, tổng hợp đa nguồn) tùy thuộc độ phức tạp của câu hỏi.
- **Duy trì ngữ cảnh:** Tích hợp bộ nhớ (Window Buffer Memory) giúp bot hiểu lịch sử trò chuyện trong từng phiên chat.
- **Bảo mật tuyệt đối:** Bộ lọc (Filter) chỉ cho phép ID Telegram của các sếp hoặc người được cấp phép sử dụng bot.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (Tạo qua `@BotFather`).
- **OpenAI API Key** (Dùng cho mô hình `gpt-4o-mini`).
- **Perplexity API Key** (Dùng cho công cụ tìm kiếm `sonar` và `sonar-pro`).
- **Telegram User ID** của các sếp (Lấy qua `@userinfobot`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

- **Node `Telegram Trigger` & `Telegram`:** 
  - Tạo bot thông qua `@BotFather` trên Telegram để lấy token.
  - Thêm Telegram credentials mới vào n8n và dán Token vào.
- **Node `Filter` (Bảo mật quan trọng):** 
  - Mở node **Filter** và thay thế giá trị User ID mặc định (`5675741296`) thành **Telegram User ID thực tế** của các sếp (lấy bằng cách nhắn tin với `@userinfobot`). Điều này giúp chặn đứng các truy cập trái phép vào bot của các sếp.
- **Node `OpenAI Chat Model`:** 
  - Thêm OpenAI API credentials.
  - Chọn model `gpt-4o-mini` (lựa chọn tối ưu chi phí và tốc độ) hoặc các model khác tùy nhu cầu.
- **Node `Perplexity Sonar` & `Perplexity Sonar Pro`:** 
  - Thêm Perplexity API credentials (sử dụng Header Auth với `Authorization: Bearer <YOUR_API_KEY>`).
  - *Sonar Model:* Phù hợp cho tra cứu nhanh, tóm tắt sự kiện, định nghĩa.
  - *Sonar Pro Model:* Chuyên sâu cho phân tích cạnh tranh, nghiên cứu tài chính, tổng hợp tài liệu học thuật.
- **Node `Window Buffer Memory`:** 
  - Giữ nguyên cấu hình để duy trì ngữ cảnh trò chuyện dựa theo Chat ID.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn đến bot Telegram của các sếp để kiểm tra phản hồi.
- Nếu mọi thứ hoạt động trơn tru, hãy gạt công tắc sang **Active** để bot chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông tin:** Các sếp có thể thay thế hoặc bổ sung `Slack Trigger` hoặc `Discord` bên cạnh Telegram để làm việc nhóm hiệu quả hơn.
- **Lưu lịch sử nghiên cứu:** Thêm một node `Google Sheets` hoặc `Notion` phía sau AI Agent để tự động lưu lại các câu hỏi và báo cáo nghiên cứu phục vụ tra cứu sau này.
- **Tùy chỉnh System Prompt:** Trong node **AI Agent**, các sếp có thể tinh chỉnh System Message để bot nói chuyện theo văn phong riêng (chuyên gia tài chính, trợ lý học tập, v.v.).

### 📌 Kết luận
Workflow Deep Research Assistant này là một "vũ khí" cực kỳ mạnh mẽ giúp các sếp tiết kiệm hàng giờ tra cứu mỗi ngày. Hãy triển khai ngay lên VPS của mình và tận hưởng sức mạnh của AI tự động hóa!