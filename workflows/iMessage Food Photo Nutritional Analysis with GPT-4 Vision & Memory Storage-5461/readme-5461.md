---
title: "🚀 Phân tích dinh dưỡng món ăn qua iMessage tự động với GPT-4 Vision & n8n"
description: "Xây dựng trợ lý dinh dưỡng thông minh ngay trên iMessage sử dụng n8n, Blooio API, GPT-4 Vision và Postgres Chat Memory để phân tích ảnh bữa ăn và lưu trữ lịch sử."
slug: "phan-tich-dinh-duong-imessage-gpt-4-vision-n8n"
tags: [n8n, automation, no-code, ai-agent, openai, postgres]
keywords: [n8n workflow, phan tich dinh duong, gpt-4 vision, blooio, imessage automation, ai agent]
---

# 🚀 Phân tích dinh dưỡng món ăn qua iMessage tự động với GPT-4 Vision & n8n

Các sếp có đang chật vật với việc đếm calories, ghi chép lại từng bữa ăn hằng ngày nhưng rồi lại bỏ cuộc chỉ sau vài ngày vì quá thủ công và mất thời gian? Việc mở các ứng dụng tracking phức tạp đôi khi trở thành một gánh nặng tâm lý. 

Giải pháp hoàn hảo ở đây là gì? Hãy biến ngay ứng dụng **iMessage** quen thuộc thành một trợ lý dinh dưỡng cá nhân thông minh tuyệt đối. Chỉ cần gửi một tấm ảnh chụp món ăn qua iMessage, workflow n8n này sẽ tự động tiếp nhận, dùng sức mạnh của **GPT-4 Vision** để soi từng thành phần, tính toán lượng calories, chất dinh dưỡng, đồng thời lưu trữ lịch sử qua **Postgres Chat Memory** để chat và tra cứu lại bất cứ lúc nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% qua iMessage**: Gửi ảnh hoặc mô tả món ăn trực tiếp từ điện thoại mà không cần cài app rườm rà nào khác.
- **Phân tích siêu chuẩn xác**: Ứng dụng **GPT-4 Vision** nhận diện thành phần món ăn trong ảnh, bóc tách lượng calo, protein, carbs, fat chính xác.
- **Bộ nhớ thông minh**: Sử dụng **Postgres Chat Memory** giúp trợ lý AI ghi nhớ các bữa ăn trước đó, cho phép hỏi đáp, tổng kết theo ngày/tuần/tháng cực mượt.
- **Hoạt động 24/7 trên mây**: Tự động phản hồi tin nhắn ngay lập tức bất cứ lúc nào sếp gửi ảnh đến.
:::

### 📥 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Tài khoản Blooio.com**: Dịch vụ kết nối iMessage/SMS API (Lấy API Token tại *Settings → API Keys*).
3. **OpenAI API Key**: Để sử dụng mô hình `gpt-4.1-mini` với khả năng xử lý hình ảnh (Vision).
4. **PostgreSQL Database**: Dùng để lưu trữ ngữ cảnh trò chuyện (Chat Memory).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy trực tiếp mã nguồn, sau đó paste vào giao diện n8n Editor của các sếp thông qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes được liên kết chặt chẽ. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Receive Message (From Blooio)** (Node Webhook):
  - Nhận sự kiện tin nhắn mới gửi đến (`new-message`). Đảm bảo URL webhook của n8n được trỏ đúng vào cấu hình trên trang quản lý Blooio.
- **Don't respond to yourself** & **If has images, download them** (Node If):
  - Bộ lọc thông minh giúp loại bỏ các tin nhắn do chính hệ thống gửi đi và kiểm tra xem tin nhắn có kèm hình ảnh (attachment) hay không để tiến hành tải về qua node **HTTP Request**.
- **AI Agent** & **AI Agent1** (Node Agent):
  - Cấu hình prompt hệ thống để AI đóng vai một chuyên gia dinh dưỡng tận tâm.
- **OpenAI Chat Model** & **OpenAI Chat Model1** (Node LmChatOpenAi):
  - Chọn model là `gpt-4.1-mini` (hoặc model hỗ trợ Vision tương đương) và kết nối với **OpenAI API Credentials**.
- **Postgres Chat Memory** (Node MemoryPostgresChat):
  - Điền thông tin kết nối cơ sở dữ liệu PostgreSQL để AI ghi nhớ lịch sử trò chuyện và các bữa ăn trước đó của người dùng.
- **Send Message** (Node HttpRequest):
  - Cấu hình gửi phản hồi ngược lại qua Blooio API theo các thông số:
    - **Method**: `POST`
    - **URL**: `https://api.blooio.com/send-message`
    - **Headers**: 
      - `Accept`: `application/json`
      - `Authorization`: `Bearer YOUR_API_TOKEN` (Thay bằng Token thực tế từ Blooio)
      - `Content-Type`: `application/json`

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một tin nhắn kèm hình ảnh món ăn qua số iMessage đã liên kết với Blooio để test hệ thống.
- Kiểm tra logs xem AI đã phân tích chính xác chưa và tin nhắn phản hồi đã về điện thoại hay chưa.
- Gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ Google Sheets**: Thêm một node Google Sheets vào sau bước phân tích của AI để tự động ghi log calories mỗi ngày vào bảng tính, tiện theo dõi xu hướng cân nặng.
- **Tích hợp Telegram/Slack**: Ngoài iMessage, các sếp có thể nhân bản nhánh trigger để nhận ảnh món ăn qua Telegram Bot hoặc Slack.
- **Báo cáo định kỳ**: Thiết lập một Cron node chạy vào 9 giờ tối mỗi ngày để AI tự động nhắn tin tổng kết tổng lượng calo đã nạp trong ngày.

### 📌 Kết luận
Việc tự động hóa theo dõi dinh dưỡng chưa bao giờ dễ dàng và mượt mà đến thế khi kết hợp n8n, Blooio iMessage và GPT-4 Vision. Hãy triển khai ngay hôm nay để làm chủ vóc dáng và sức khỏe mà không cần tốn chút công sức ghi chép thủ công nào các sếp nhé!