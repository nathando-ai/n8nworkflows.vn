---
title: "🚀 Tự động tạo bài đăng Instagram với AI (GPT & Gemini) qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa 100% quy trình tạo trích dẫn, hình ảnh minh họa bằng AI và gửi báo cáo qua Email mỗi ngày."
slug: "tu-dong-tao-bai-dang-instagram-voi-ai-gpt-va-gemini"
tags: [n8n, automation, instagram, openai, google-gemini, ai-content]
keywords: [n8n workflow, tự động hóa instagram, ai content generator, openai gpt, google gemini image]
---

# 🚀 Tự động tạo bài đăng Instagram với AI (GPT & Gemini) qua n8n

Việc duy trì nội dung đều đặn trên mạng xã hội như Instagram đòi hỏi rất nhiều thời gian từ khâu lên ý tưởng câu nói hay (quote), thiết kế hình ảnh cho đến viết caption và hashtag. Đôi khi, các sếp phải mất hàng giờ mỗi tuần chỉ để làm những công việc lặp đi lặp lại này.

Đừng lo lắng nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh, tận dụng sức mạnh của **OpenAI GPT** và **Google Gemini** để tự động sản xuất trích dẫn độc đáo, thiết kế ảnh minh họa, soạn sẵn caption chuẩn SEO kèm hashtag và gửi thẳng vào hộp thư email của các sếp mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tự nghĩ câu nói hay hay tự tay thiết kế ảnh thủ công mỗi ngày.
- **Nội dung độc bản & Không trùng lặp:** Hệ thống tự động đọc lịch sử các câu quote cũ để AI không bị lặp lại nội dung.
- **Tự động hóa hoàn toàn:** Chạy tự động theo lịch trình (Schedule) định sẵn, gửi gọn gàng qua email để các sếp chỉ cần copy-paste lên Instagram.
- **Dễ dàng mở rộng:** Có thể kết hợp thêm API Facebook/Instagram để đăng bài tự động 100% mà không cần qua bước trung gian.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyến nghị bản self-hosted để dùng các node đọc/ghi file cục bộ).
- **OpenAI API Key:** Cho mô hình GPT (Node `OpenAI Chat Model`).
- **Google Gemini API Key (Google Palm API):** Cho tính năng tạo hình ảnh (Node `Generate an image`).
- **SMTP Server:** Tài khoản email (Gmail, SendGrid, v.v.) để gửi email thông báo (Node `Send email`).
- **File lưu trữ cục bộ:** Một file text trên server (`/home/node/instagram_posts.txt`) để lưu lịch sử các quote.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File / Clipboard** và dán đoạn JSON vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Schedule Trigger:** Cấu hình tần suất chạy (ví dụ: mỗi ngày 1 lần vào 8 giờ sáng).
- **Read Text Files from Disk & Write Text Files from Disk:** Trỏ đường dẫn đến file lưu lịch sử câu quote trên server của các sếp (mặc định: `/home/node/instagram_posts.txt`) nhằm tránh việc AI tạo ra các câu trích dẫn bị trùng lặp ở các lần chạy sau.
- **OpenAI Chat Model & Basic LLM Chain:** Kết nối **OpenAI Credentials** và chọn mô hình mong muốn (ví dụ: `gpt-4.1-mini`). Tại đây, các sếp có thể tinh chỉnh System Prompt/User Prompt để AI sinh ra câu quote, caption và hashtag phù hợp với ngách của mình.
- **Code-Split-LangChain:** Node này có nhiệm vụ xử lý code JavaScript để tách kết quả trả về từ LLM thành các thành phần riêng biệt: Quote, Caption, và Hashtag.
- **Generate an image (Google Gemini):** Kết nối **Google Palm API Credentials**. Kiểm tra lại tham số `prompt` để đảm bảo Gemini hiểu đúng yêu cầu thiết kế (mặc định tạo ảnh đơn giản, làm nổi bật trích dẫn với màu sắc tương phản).
- **Send email (SMTP):** Cấu hình thông tin SMTP của các sếp, điền địa chỉ email nhận kết quả và đính kèm hình ảnh vừa được tạo ra cùng nội dung text.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm xem email có về hộp thư hay không.
- Kiểm tra lại định dạng ảnh, text trong email. Nếu mọi thứ đã mượt mà, hãy bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì gửi email, các sếp có thể đổi node `Send email` thành node Telegram hoặc Slack để nhận thông báo ngay trên điện thoại cực kỳ tiện lợi.
- **Tự động hóa hoàn toàn với Facebook Graph API:** Thay vì copy thủ công từ email lên Instagram, các sếp có thể nối tiếp một HTTP Request node gọi thẳng vào Instagram Graph API để tự động publish bài viết lên kênh.
- **Lưu trữ Google Sheets:** Thay vì lưu file text cục bộ, có thể dùng Google Sheets để lưu trữ kho tàng quote đã tạo, giúp việc quản lý và kiểm tra trực quan hơn.

### 📌 Kết luận
Workflow tạo bài đăng Instagram tự động bằng GPT và Gemini là một "vũ khí" tuyệt vời giúp các nhà sáng tạo nội dung tối ưu hóa hiệu suất làm việc. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và để AI phục vụ công việc kinh doanh của các sếp!