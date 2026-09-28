---
title: "🚀 Tự động hóa tối ưu hóa Prompt AI với GPT-4o-mini và Telegram"
description: "Hướng dẫn cài đặt workflow n8n sử dụng AI Agent và GPT-4o-mini để biến các câu lệnh (prompt) thô sơ, mơ hồ thành các prompt chuyên nghiệp và gửi thẳng qua Telegram."
slug: "toi-uu-hoa-ai-prompt-gpt-4o-mini-telegram-n8n"
tags: [n8n, automation, ai-agent, openai, telegram, no-code]
keywords: [n8n workflow, tối ưu prompt, gpt-4o-mini, tự động hóa telegram, ai agent n8n]
---

# 🚀 Tự động hóa tối ưu hóa Prompt AI với GPT-4o-mini và Telegram

Các sếp có bao giờ gặp tình trạng nhập câu lệnh (prompt) cho AI rất chung chung, dẫn đến kết quả trả về không được như ý muốn? Việc viết prompt chi tiết, rõ ràng đòi hỏi nhiều thời gian và kinh nghiệm. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp biến những ý tưởng hoặc câu hỏi sơ khai của người dùng thành các prompt sắc bén, chi tiết và chuyên nghiệp nhờ sức mạnh của **GPT-4o-mini**, sau đó trả kết quả trực tiếp qua **Telegram**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Biến hóa prompt thô**: Nhận các input mơ hồ và tự động bổ sung ngữ cảnh, chi tiết, độ rõ ràng.
- **Tiết kiệm thời gian**: Không cần mất công tinh chỉnh prompt thủ công nhiều lần.
- **Tích hợp linh hoạt**: Có thể gọi workflow này lồng ghép vào bên trong các hệ thống tự động hóa lớn hơn.
- **Phản hồi tức thì**: Gửi kết quả tối ưu trực tiếp về tài khoản Telegram của người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
1. **Hệ thống n8n** (Cloud hoặc Self-hosted).
2. **OpenAI API Key**: Để sử dụng mô hình `gpt-4o-mini`.
3. **Telegram Bot Token**: Tạo qua `@BotFather` để bot có thể gửi tin nhắn trả về.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **OpenAI Chat Model**: 
  - Chọn model: `gpt-4o-mini` (tiết kiệm chi phí và tốc độ cực nhanh).
  - Kết nối `OpenAI API Credentials` của các sếp vào đây.
- **AI Agent & Simple Memory**: 
  - Cấu hình System Prompt cho Agent với nhiệm vụ chuyên biệt là "Prompt Engineer" (phân tích ý người dùng và viết lại thành một prompt chuẩn chỉnh, tối ưu cho LLM).
- **Telegram3**: 
  - Kết nối `Telegram API Credentials` (Bot Token).
  - Cấu hình Chat ID nhận tin nhắn và định dạng nội dung trả về từ AI Agent.
- **When Executed by Another Workflow & Split into chunks1**: 
  - Node kích hoạt nhận dữ liệu đầu vào từ một workflow cha (hoặc webhook nhắn tin từ Telegram) và xử lý cắt đoạn văn bản nếu dữ liệu quá dài.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** và truyền vào một đoạn prompt mẫu thô sơ để kiểm tra phản hồi.
- Nếu AI Agent trả về prompt đã được tối ưu ngon lành và gửi về Telegram thành công, các sếp chỉ cần gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Ngoài Telegram, các sếp có thể nối thêm node Slack, Discord hoặc lưu trữ trực tiếp prompt đã tối ưu vào Google Sheets / Notion để làm thư viện prompt.
- **Lưu lịch sử hội thoại**: Tận dụng node `Simple Memory` để AI hiểu được ngữ cảnh các câu lệnh trước đó, giúp tối ưu prompt theo dạng trau dồi qua lại (multi-turn).

### 📌 Kết luận
Workflow này là một trợ thủ đắc lực cho bất kỳ ai muốn nâng tầm chất lượng tương tác với AI mà không tốn công sức suy nghĩ cách viết prompt dài dòng. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp!