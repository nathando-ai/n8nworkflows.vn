---
title: "🚀 Xây dựng trợ lý AI chỉnh sửa ảnh qua Telegram với Nano Banana và n8n"
description: "Hướng dẫn tích hợp Nano Banana AI (Gemini 2.5 Flash qua OpenRouter) vào Telegram bot bằng n8n để tự động phân tích và xử lý ảnh siêu tốc."
slug: "nano-banana-ai-image-editor-telegram-n8n"
tags: [n8n, automation, telegram, ai, openrouter, gemini, image-processing]
keywords: [n8n workflow, telegram bot AI, chỉnh sửa ảnh AI, Nano Banana OpenRouter, Gemini 2.5 Flash n8n]
---

# 🚀 Tự động hóa chỉnh sửa và phân tích ảnh qua Telegram với Nano Banana AI

Các sếp có bao giờ cảm thấy việc mở các phần mềm chỉnh sửa ảnh phức tạp chỉ để chỉnh sửa nhanh hoặc phân tích nội dung hình ảnh qua điện thoại quá mất thời gian? Chưa kể việc xây dựng một hệ thống AI xử lý ảnh thường đòi hỏi lập trình phức tạp.

Với workflow n8n **Nano Banana AI Image Editor via Telegram**, các sếp sẽ sở hữu ngay một trợ lý AI thông minh ngay trên ứng dụng chat Telegram quen thuộc. Chỉ cần gửi ảnh kèm câu lệnh (caption), AI sẽ tự động xử lý, phân tích và trả lại kết quả ngay lập tức mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác trực quan:** Biến Telegram thành trạm điều khiển AI xử lý ảnh di động mọi lúc mọi nơi.
- **Tích hợp AI đỉnh cao:** Sử dụng mô hình Nano Banana (Gemini 2.5 Flash Preview) thông qua OpenRouter với chi phí cực rẻ (hoặc miễn phí).
- **Tự động hóa 100%:** Luồng dữ liệu tự động từ nhận ảnh, chuyển đổi Base64, gọi API AI, chuyển đổi ngược về file và gửi trả lại người dùng.
- **Tiết kiệm thời gian:** Không cần chuyển đổi qua lại giữa nhiều ứng dụng hay mở máy tính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram.
- **OpenRouter API Key:** Tài khoản tại OpenRouter để kết nối với mô hình Nano Banana (Gemini 2.5 Flash).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n, chọn **Add workflow** -> **Import from File** / **Paste JSON** để đưa workflow lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Photo Message Receiver (Telegram Trigger):** Kết nối với Telegram Credentials của sếp và chọn Bot đã tạo. Node này sẽ lắng nghe mọi tin nhắn hình ảnh gửi tới bot.
- **Download Telegram Photo (Telegram Node):** Đảm bảo cấu hình resource là `file` để tải tệp hình ảnh từ server Telegram về n8n.
- **Nano Banana Image Processor (HTTP Request Node):** 
  - Cấu hình kết nối tới API của OpenRouter.
  - Sử dụng mô hình **Nano Banana (Gemini 2.5 Flash Image Preview)**.
  - Đảm bảo truyền đúng API Key và payload chứa dữ liệu ảnh đã được định dạng dạng Data URL (`Format Image Data URL`).
- **Send Processed Photo (Telegram Node):** Cấu hình operation là `sendPhoto`, trỏ đến `Chat ID` của người gửi hoặc nhóm đích để trả kết quả ảnh đã xử lý về Telegram.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một bức ảnh kèm nội dung yêu cầu tới Bot Telegram của sếp để kiểm tra log dữ liệu.
- Nếu mọi thứ hiển thị màu xanh thành công, hãy gạt công tắc **Active** ở góc trên bên phải để bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Thêm node Telegram hoặc Slack phụ để gửi thông báo về admin mỗi khi có người dùng sử dụng bot.
- **Lưu trữ dữ liệu:** Kết nối thêm Google Sheets hoặc Airtable để lưu lịch sử các bức ảnh và nội dung yêu cầu của người dùng.
- **Phân quyền người dùng:** Thêm node **If** để giới hạn chỉ cho phép các Chat ID nằm trong danh sách trắng (whitelist) mới được sử dụng bot, tránh bị bên thứ ba "spam" API.

### 📌 Kết luận
Workflow **Nano Banana AI Image Editor via Telegram** là một minh chứng tuyệt vời cho sức mạnh kết hợp giữa No-Code (n8n) và Multimodal AI. Hãy triển khai ngay hôm nay để tối ưu hóa công việc xử lý hình ảnh của sếp và mang lại những trải nghiệm tự động hóa vô cùng thú vị!