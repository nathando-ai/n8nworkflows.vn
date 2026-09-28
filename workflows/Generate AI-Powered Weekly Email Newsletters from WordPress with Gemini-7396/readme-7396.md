---
title: "🚀 Tự động tạo bản tin hàng tuần từ WordPress bằng AI Gemini trong n8n"
description: "Hướng dẫn tự động hóa quy trình gom bài viết WordPress mới nhất, sử dụng AI Gemini để viết bản tin hấp dẫn và gửi tự động qua email hàng tuần."
slug: "tu-dong-tao-ban-tin-hang-tuan-tu-wordpress-bang-ai-gemini"
tags: [n8n, automation, wordpress, google-gemini, ai, newsletter, email-marketing]
keywords: [n8n workflow, tự động hóa wordpress, ai newsletter, google gemini n8n, gửi email tự động]
---

# 🚀 Tự động tạo bản tin hàng tuần từ WordPress bằng AI Gemini

Việc duy trì gửi bản tin (newsletter) đều đặn cho khách hàng là chìa khóa giữ chân họ, nhưng tốn rất nhiều thời gian thủ công: từ việc lọc bài viết mới, tóm tắt nội dung, viết lời dẫn cho đến thiết kế và bấm gửi. 

Đừng để những công việc lặp đi lặp lại này làm chậm tốc độ phát triển doanh nghiệp của các sếp! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: tự động lấy bài viết WordPress mới nhất, dùng trí tuệ nhân tạo **Google Gemini AI** để biên tập thành một bản tin chuyên nghiệp, hấp dẫn và tự động gửi đi vào mỗi thứ Sáu hàng tuần mà không cần chạm tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần:** Không còn phải copy-paste bài viết hay ngồi nghĩ văn phong viết email.
- **Cá nhân hóa bằng AI:** Google Gemini giúp biên tập nội dung bài viết thành một bản tin có cấu trúc cuốn hút, tiêu đề giật gân và lời mở đầu thân thiện.
- **Tự động 100%:** Lên lịch chạy định kỳ (Ví dụ: 10 giờ sáng thứ Sáu hàng tuần), hoạt động liên tục không gián đoạn.
- **Duy trì tương tác:** Giúp độc giả và khách hàng luôn cập nhật các bài viết mới nhất trên website của các sếp một cách đều đặn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **WordPress Site:** Tài khoản quản trị website WordPress (cần kết nối API/Application Password).
- **Google Gemini API Key:** Tài khoản Google AI Studio để lấy khóa API cho mô hình Gemini.
- **SMTP Email Credentials:** Thông tin kết nối SMTP (Gmail, SendGrid, Mailgun, v.v.) để gửi email đi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON tải về từ nguồn gốc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Weekly Friday 10AM (`scheduleTrigger`):** 
  - Mặc định lịch chạy là 10:00 sáng mỗi thứ Sáu hàng tuần. Các sếp có thể bấm vào node này để đổi lại khung giờ phù hợp với chiến lược của doanh nghiệp.
- **Fetch Recent Posts (`wordpress`):** 
  - Thêm Credentials kết nối đến trang WordPress của các sếp.
  - Cấu hình thông số `operation` là `getAll` để lấy danh sách các bài viết gần đây nhất.
- **Check Posts Exist (`if`):** 
  - Node này dùng để kiểm tra xem trong tuần qua có bài viết mới nào không. Nếu có thì tiếp tục quy trình, nếu không có thì dừng lại để tránh gửi email trống.
- **Google Gemini Chat Model (`lmChatGoogleGemini`) & AI Newsletter Creator (`agent`):** 
  - Điền **Google Gemini API Key** vào credentials của node mô hình chat.
  - Tại node AI Agent, các sếp có thể tinh chỉnh System Prompt để AI viết bản tin theo đúng giọng điệu (tone of voice) thương hiệu của các sếp (chuyên nghiệp, hài hước, ngắn gọn,...).
- **Parse Newsletter Content (`code`):** 
  - Node này dùng đoạn mã JavaScript để bóc tách và định dạng lại kết quả đầu ra từ AI thành nội dung HTML hoàn chỉnh cho email.
- **Send Newsletter (`emailSend`):** 
  - Điền thông tin tài khoản SMTP của các sếp.
  - Thay thế địa chỉ email người nhận (hoặc danh sách subscriber) và tiêu đề email cho phù hợp với chiến dịch.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu hiện tại và kiểm tra hộp thư xem email đến có đúng định dạng không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để n8n tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi email, các sếp có thể nối thêm node Telegram hoặc Slack để bắn một tin nhắn thông báo nội dung bản tin đã được AI tạo thành công cho đội ngũ Marketing duyệt trước.
- **Lưu Log vào Google Sheets:** Thêm một node Google Sheets vào cuối luồng để ghi lại tiêu đề bài viết, ngày gửi và trạng thái gửi email giúp dễ dàng thống kê.
- **Tùy chỉnh số lượng bài viết:** Tại node WordPress, các sếp có thể giới hạn số lượng bài viết lấy ra mỗi tuần (ví dụ: top 3 bài viết nổi bật nhất) để bản tin cô đọng hơn.

### 📌 Kết luận
Việc tự động hóa quy trình làm content và email marketing chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và AI Gemini. Hãy thiết lập ngay workflow này để tối ưu hóa thời gian và gia tăng tỷ lệ chuyển đổi cho doanh nghiệp của các sếp ngay hôm nay!