---
title: "🚀 Tự động tạo video AI với Veo3 Fast API, Google Drive và Email thông báo"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình tạo video từ văn bản bằng Veo3 Fast API, lưu trữ Google Drive và gửi email thông báo cho người dùng."
slug: "tu-dong-tao-video-ai-voi-veo3-fast-api-google-drive"
tags: [n8n, automation, no-code, AI Video, Google Drive, Veo3 API]
keywords: [n8n workflow, tạo video AI tự động, Veo3 Fast API, google drive automation, n8n form trigger]
---

# 🚀 Tự động tạo video AI với Veo3 Fast API, Google Drive và Email thông báo

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ liền chỉ để tạo, tải xuống, cấu hình quyền truy cập và gửi thủ công từng video do AI tạo ra cho khách hàng hoặc đội ngũ? Quy trình thủ công này vừa tốn thời gian, vừa dễ xảy ra sai sót trong khâu quản lý file.

Giải pháp ở đây là gì? Hãy để **n8n** lo toàn bộ! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow tự động hóa 100% không cần code: Nhận yêu cầu từ Form, gọi **Veo3 Fast API** để tạo video, tự động tải về, lưu trữ lên **Google Drive**, phân quyền chia sẻ và gửi link trực tiếp qua **Email** cho người dùng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Biến ý tưởng/prompt thành video hoàn chỉnh chỉ thông qua một biểu mẫu (Form) đơn giản.
- **Xử lý bất đồng bộ thông minh**: Tự động kiểm tra trạng thái render video, chờ đợi (wait/retry) và xử lý lỗi phát sinh mà không cần con người can thiệp.
- **Lưu trữ và phân quyền chuyên nghiệp**: Video hoàn thành tự động được đẩy lên Google Drive và cấu hình sẵn quyền chia sẻ an toàn.
- **Cảnh báo lỗi tức thì**: Tự động gửi email thông báo cho quản trị viên hoặc người dùng nếu tác vụ tạo video gặp lỗi hoặc thiếu Task ID.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Veo 3 Fast API**: Tài khoản và API Key/Endpoint để gọi dịch vụ tạo video.
- **Google Drive Credentials**: Tài khoản Google Cloud/OAuth2 để upload và phân quyền file.
- **SMTP Credentials**: Thông tin máy chủ gửi mail (Gmail, SendGrid, Amazon SES,...) để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (từ nguồn n8n.io/workflows/10860) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:
- **On form submission (`formTrigger`)**: Nơi người dùng nhập prompt để tạo video. Các sếp có thể tùy chỉnh giao diện form theo ý muốn.
- **Veo 3 Fast API Processor (`httpRequest`)**: Cấu hình endpoint API, Header và truyền tham số `prompt` từ Form vào body request.
- **Condition: Check Task Id (`if`) & Send Email: API Error - Task ID Missing (`emailSend`)**: Kiểm tra xem API trả về Task ID hay chưa. Nếu thiếu, hệ thống sẽ gửi email báo lỗi qua cấu hình **SMTP**.
- **Wait for API Response & Wait for Task to Complete (`wait`)**: Các node chờ (30-35 giây) để hệ thống AI kịp xử lý video trước khi gọi lại API kiểm tra trạng thái.
- **API Request: Check Task Status (`httpRequest`) & Condition: Check Task Output Status (`switch`)**: Kiểm tra vòng đời task (thành công, đang xử lý, hoặc thất bại). Nếu thất bại, node **Send Email: API Error - Task Failed** sẽ kích hoạt.
- **Download Video (`httpRequest`)**: Tải file video xuống từ URL kết quả của API.
- **Upload File to Google Drive & Set Google Drive Permissions (`googleDrive`)**: Kết nối tài khoản Google Drive thông qua **GoogleDriveOAuth2Api**, chỉ định thư mục lưu trữ và cấu hình quyền chia sẻ file (`operation: share`) để người nhận có thể xem/tải dễ dàng.
- **Send an email : Video Link (`emailSend`)**: Soạn nội dung email gửi kèm đường dẫn Google Drive của video hoàn thiện cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấp vào **Execute Workflow** và test thử bằng cách điền một prompt bất kỳ lên form.
- Kiểm tra log trên n8n để đảm bảo các bước chạy thông suốt.
- Bật công tắc **Active** ở góc trên bên phải để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot**: Thay vì dùng Form Trigger, các sếp có thể thay bằng **Telegram Trigger** hoặc **Slack Trigger** để nhận prompt tạo video trực tiếp từ nhóm chat.
- **Lưu lịch sử vào Google Sheets**: Thêm một node Google Sheets ở bước cuối để lưu lại lịch sử prompt, thời gian tạo và link video phục vụ cho việc thống kê.
- **Quản lý dung lượng**: Thiết lập quy định tự động xóa file tạm trên server n8n (nếu có) sau khi đã upload thành công lên Google Drive để tiết kiệm tài nguyên ổ cứng VPS.

### 📌 Kết luận
Workflow tích hợp **Veo3 Fast API, Google Drive và Email** là một trợ thủ đắc lực cho các nhà sáng tạo nội dung, marketer hoặc các doanh nghiệp muốn tự động hóa quy trình sản xuất video bằng AI. Hãy áp dụng ngay hôm nay để tối ưu hóa thời gian và nâng tầm hiệu suất làm việc!