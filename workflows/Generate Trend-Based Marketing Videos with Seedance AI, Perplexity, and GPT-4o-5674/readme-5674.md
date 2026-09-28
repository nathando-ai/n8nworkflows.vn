---
title: "🚀 Tự động tạo video marketing theo xu hướng với Seedance AI, Perplexity và GPT-4o qua Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình nghiên cứu xu hướng, viết prompt và tạo video quảng cáo ngắn bằng AI chỉ từ một tin nhắn Telegram."
slug: "tao-video-marketing-xu-huong-seedance-ai-perplexity-gpt4o"
tags: [n8n, automation, no-code, ai-video, telegram, openai]
keywords: [n8n workflow, tao video ai, seedance ai, perplexity ai, gpt-4o, tu dong hoa marketing]
---

# 🚀 Tự động tạo video marketing theo xu hướng với Seedance AI, Perplexity và GPT-4o

Các sếp có đang cảm thấy mệt mỏi mỗi khi cần "bắt trend" để làm nội dung ngắn (Reels, TikTok, Shorts)? Việc ngồi nghiên cứu xu hướng, lên kịch bản, rồi hì hục dựng video tốn hàng giờ đồng hồ nhưng đôi khi lại lỗi mốt ngay khi vừa ra mắt. 

Đừng lo, workflow n8n tuyệt vời từ tác giả **Automate With Marc** sẽ giúp các sếp giải quyết triệt để bài toán này. Chỉ với một tin nhắn ngắn gọn qua Telegram, hệ thống sẽ tự động nghiên cứu xu hướng thị trường, tối ưu hóa kịch bản video và gọi API tạo ra một video quảng cáo hoàn chỉnh bằng AI mà không cần chạm tay vào phần mềm dựng phim nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% từ ý tưởng đến video:** Chuyển đổi một câu lệnh thô trên Telegram thành video quảng cáo hoàn chỉnh.
- **Bắt trend cực nhanh:** Ứng dụng Perplexity AI để quét các xu hướng mới nhất trong 14 ngày qua, giúp nội dung luôn "hot" và đúng thị hiếu.
- **Tiết kiệm thời gian và nhân lực:** Không cần đội ngũ thiết kế, dựng phim hay nghiên cứu thị trường phức tạp.
- **Trả kết quả trực tiếp:** Nhận ngay link video hoàn thiện thẳng vào ứng dụng Telegram cá nhân.
:::

### 📦 Các Nodes chính trong Workflow
Workflow này bao gồm 9 nodes hoạt động nhịp nhàng:
1. **Telegram Trigger**: Nhận yêu cầu đầu vào từ người dùng.
2. **Trend Research Agent (Perplexity - Sonar Pro)**: Nghiên cứu xu hướng và góc tiếp thị.
3. **Video Prompt Engineer (OpenAI - GPT-4o)**: Chuyển đổi insights thành prompt tạo video tối ưu.
4. **Post Request - Wavespeed**: Gửi yêu cầu tạo video đến Seedance API.
5. **Wait 30 sec / Wait 30 Sec**: Chờ xử lý render video.
6. **If & GET Request Wavespeed**: Vòng lặp kiểm tra trạng thái video đã hoàn thành chưa.
7. **Send a text message (Telegram)**: Gửi thành quả video về lại cho người dùng.

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Telegram Bot Token**: Tạo qua BotFather để nhận trigger và gửi phản hồi.
- **Perplexity API Key**: Để sử dụng mô hình Sonar Pro nghiên cứu xu hướng.
- **OpenAI API Key**: Sử dụng GPT-4o để viết prompt chi tiết cho video.
- **Wavespeed API Key / Header Auth**: Nền tảng trung gian tích hợp Seedance API để render video.

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở giao diện n8n của các sếp, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Telegram Trigger & Send a text message**: Thêm Credentials `telegramApi` bằng Bot Token của các sếp. Đảm bảo bot đã được kích hoạt (nhấn `/start`).
- **Trend Research Agent**: Chọn credential `perplexityApi` và giữ nguyên model `sonar-pro` để đảm bảo chất lượng quét thông tin thị trường.
- **Video Prompt Engineer**: Kết nối với credential `openaiApi`, chọn model `gpt-4o` để AI viết prompt trực quan, chi tiết cho video ngắn.
- **Post Request - Wavespeed & GET Request Wavespeed**: Cấu hình chuẩn Header Auth (`httpHeaderAuth`) với API key từ nền tảng Wavespeed để gọi Seedance API tạo và kiểm tra trạng thái video.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn qua Telegram (Ví dụ: *"Create a 5-second IG ad for my new eco-friendly water bottle"*).
- Theo dõi luồng chạy, đợi qua các node `Wait` và kiểm tra xem video có trả về Telegram thành công không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** sang màu xanh để workflow hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Ngoài Telegram, các sếp có thể thay thế bằng node Slack, Discord hoặc lưu trực tiếp link video vào Google Sheets để làm thư viện nội dung.
- **Tạo cơ chế lưu Log**: Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các prompt và xu hướng mà AI đã tìm kiếm, phục vụ cho việc phân tích chiến dịch marketing về sau.
- **Tùy chỉnh thời gian chờ**: Tùy thuộc vào tốc độ render của Seedance API, các sếp có thể tinh chỉnh thời gian ở các node `Wait` cho phù hợp để tránh việc gọi GET quá sớm khi video chưa render xong.

---

### 📌 Kết luận
Việc kết hợp giữa sức mạnh nghiên cứu của Perplexity, khả năng ngôn ngữ của GPT-4o và công nghệ tạo video đỉnh cao của Seedance qua n8n chính là "vũ khí bí mật" giúp các marketer tối ưu hóa hiệu suất công việc lên gấp nhiều lần. Hãy cài đặt ngay workflow này và trải nghiệm sức mạnh của AI Agent trong việc sáng tạo nội dung!