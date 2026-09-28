---
title: "🚀 Tự động phân tích món ăn và tính calo qua Telegram bằng Vision AI và n8n"
description: "Hướng dẫn cài đặt workflow n8n tích hợp Telegram Bot và OpenRouter AI để phân tích hình ảnh món ăn, ước tính calo và gửi báo cáo dinh dưỡng tự động."
slug: "phan-tich-mon-an-tinh-calo-ai-telegram-n8n"
tags: [n8n, automation, ai-agent, openrouter, telegram, nutrition]
keywords: [n8n workflow, tính calo bằng ai, vision ai n8n, telegram bot ai, openrouter gpt, tự động hóa n8n]
---

# 🚀 Tự động phân tích món ăn và tính calo qua Telegram bằng Vision AI và n8n

Các sếp có đang chật vật ghi chép lại lượng calo mỗi bữa ăn hay loay hoay xây dựng ứng dụng tracking dinh dưỡng thủ công không? Việc đếm calo bằng tay vừa tốn thời gian, vừa dễ sai sót, khiến việc theo dõi sức khỏe trở thành một "gánh nặng".

Giải pháp ở đây là gì? Hãy để **Vision AI** lo việc đó thay các sếp! Workflow n8n này sẽ biến chiếc **Telegram Bot** thành một chuyên gia dinh dưỡng cá nhân: chỉ cần gửi ảnh chụp món ăn vào chat, AI sẽ tự động phân tích thành phần, ước tính trọng lượng, tính tổng calo và đưa ra nhận xét dinh dưỡng chi tiết dưới dạng JSON chuẩn xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần gửi ảnh qua Telegram, nhận lại kết quả phân tích ngay lập tức mà không cần thao tác phức tạp.
- **AI thông minh vượt trội:** Sử dụng mô hình Vision AI qua OpenRouter để nhận diện chính xác từng nguyên liệu, định lượng theo gram và tính toán calo sát thực tế.
- **Cấu trúc dữ liệu chuẩn (Structured Output):** Trả về định dạng JSON mạch lạc, dễ dàng lưu trữ vào Database hoặc chuyển tiếp qua Email/Slack.
- **Tiết kiệm thời gian & Nâng cao trải nghiệm:** Xây dựng một trợ lý sức khỏe cá nhân (hoặc phục vụ khách hàng F&B) với chi phí gần như bằng không.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **OpenRouter API Key** (để gọi các mô hình Vision AI cao cấp như GPT-4o / GPT-4o-mini).
- **Tài khoản Gmail** (tùy chọn, nếu muốn nhận báo cáo qua email thông qua node `Send a message1`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu `...` (góc trên bên phải) chọn **Import from File** hoặc **Import from Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần lưu ý cấu hình kỹ các điểm sau:

- **Telegram Trigger**: 
  - Kết nối `credentials` với **Telegram API**.
  - Đảm bảo Bot đã được kích hoạt và lắng nghe sự kiện tin nhắn hình ảnh từ người dùng.
- **OpenRouter Chat Model**:
  - Chọn `credentials` là **OpenRouter API**.
  - Kiểm tra thông số model tại mục `keyParameters`: Đặt là `openai/gpt-4o-mini` hoặc các model có khả năng đọc ảnh (vision-capable) khác.
- **AI Agent - 食材分析 & Structured Output Parser**:
  - Cấu hình prompt cho AI Agent yêu cầu trả về đúng định dạng JSON bao gồm: tên món ăn (`dishName`), danh sách nguyên liệu (`ingredients` gồm tên, trọng lượng gram, calo), tổng calo (`totalCalories`), và đánh giá dinh dưỡng (`nutritionEvaluation`).
  - Đảm bảo Output Parser ép kiểu dữ liệu trả về chuẩn xác theo schema cố định tránh lỗi tràn text.
- **Format for Gmail & Send a message1**:
  - Node Code dùng để định dạng lại kết quả JSON thành nội dung email dễ đọc.
  - Kết nối `credentials` **Gmail OAuth2** để gửi báo cáo về hộp thư của sếp (hoặc có thể thay thế bằng node Telegram/Slack nếu không dùng Gmail).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi một bức ảnh món ăn bất kỳ vào Telegram Bot để test run.
- Kiểm tra kết quả trả về ở các node. Nếu mọi thứ xanh mướt (success), hãy gạt công tắc sang **Active** để Bot hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử ăn uống:** Thay vì chỉ gửi qua email hay chat, hãy tích hợp thêm node **Google Sheets** hoặc **Notion** để lưu lại nhật ký calo mỗi ngày giúp tracking quá trình giảm cân/tăng cơ.
- **Đa ngôn ngữ:** Tinh chỉnh system prompt trong AI Agent để nhận diện món ăn Việt Nam chuẩn xác hơn (ví dụ: Phở bò, Bún chả, Cơm tấm) và trả về kết quả bằng tiếng Việt.
- **Cảnh báo dinh dưỡng:** Mở rộng workflow bằng một điều kiện (If Node) để nếu tổng calo vượt ngưỡng cho phép, Bot sẽ tự động gửi lời cảnh báo "hơi gắt" hài hước cho người dùng.

### 📌 Kết luận
Workflow **Food Image Analysis for Calorie Estimation** là một ứng dụng tuyệt vời để khai thác sức mạnh của Vision AI kết hợp No-code automation. Hãy "lên đồ" ngay cho bot Telegram của các sếp để bắt đầu hành trình tự động hóa việc chăm sóc sức khỏe cá nhân nhé!