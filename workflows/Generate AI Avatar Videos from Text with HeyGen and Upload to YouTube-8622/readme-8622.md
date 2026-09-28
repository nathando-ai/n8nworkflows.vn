---
title: "🚀 Tự động hóa sản xuất Video Avatar AI từ Text bằng HeyGen và đăng lên YouTube với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa toàn bộ quy trình: nhận kịch bản qua Webhook, tạo video avatar AI bằng HeyGen và tự động đăng tải lên kênh YouTube."
slug: "tu-dong-hoa-video-avatar-ai-heygen-youtube-n8n"
tags: [n8n, automation, heygen, youtube, ai-video, content-creation]
keywords: [n8n workflow, tạo video ai, heygen api, tự động đăng youtube, n8n heygen youtube]
---

# 🚀 Tự động hóa sản xuất Video Avatar AI từ Text bằng HeyGen và đăng lên YouTube

Các sếp có bao giờ cảm thấy đuối sức khi phải liên tục sản xuất video ngắn, video chia sẻ kiến thức cho kênh YouTube của mình? Việc viết kịch bản, vào tool tạo avatar AI (như HeyGen), chờ đợi render, tải xuống rồi lại hì hục up lên YouTube, thêm tiêu đề, mô tả... tốn vô số thời gian và công sức. 

Đừng lo, giải pháp ở đây rồi! Với workflow n8n này, các sếp chỉ cần gửi kịch bản dạng chữ (text) thông qua một Webhook, toàn bộ quy trình từ gọi API HeyGen tạo video, chờ đợi xử lý, tải file về và tự động đẩy thẳng lên YouTube sẽ được diễn ra hoàn toàn tự động 100% không cần chạm tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn các thao tác thủ công lặp đi lặp lại từ khâu render video đến upload.
- **Sản xuất video hàng loạt (Scale):** Dễ dàng kết hợp với các công cụ AI khác (như ChatGPT, Make, Google Sheets) để tạo ra hàng chục video mỗi ngày.
- **Vận hành 24/7:** Workflow tự động xử lý hàng đợi, kiểm tra trạng thái render của HeyGen và tự động đăng bài ngay khi video hoàn tất.
- **Chính xác & Mượt mà:** Cơ chế kiểm tra trạng thái thông minh giúp đảm bảo video không bị lỗi trước khi xuất bản lên YouTube.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **HeyGen Account & API Key:** Tài khoản HeyGen có hạn mức (credits) và API Key để gọi dịch vụ tạo video avatar.
- **YouTube Account / Google Cloud Project:** Đã cấu hình OAuth2 Credentials để n8n có quyền upload video lên kênh YouTube của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này (hoặc copy toàn bộ mã JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **WebHook Node:** Điểm tiếp nhận dữ liệu đầu vào. Các sếp có thể cấu hình phương thức `POST` và lấy URL Webhook này để tích hợp với các hệ thống khác (Form, CRM, hoặc ChatGPT).
- **Code Node ("Sanitize the video script"):** Node này có nhiệm vụ làm sạch và định dạng lại kịch bản văn bản để HeyGen không bị lỗi cú pháp khi xử lý.
- **Setup Heygen Parameters (Set Node):** Nơi các sếp cấu hình các thông số mặc định như `script`, `voice_id`, `avatar_id`, tỉ lệ khung hình (`aspect`), và phụ đề (`sub=false/true`). Hãy thay thế bằng `avatar_id` và `voice_id` của riêng các sếp lấy từ tài khoản HeyGen.
- **Create Avatar Video (HeyGen) & Get Avatar Video Status (HeyGen) (HTTP Request Nodes):** Cần điền HeyGen API Key vào phần Header Authentication để kết nối thành công với nền tảng HeyGen.
- **Wait for Video (HeyGen) (Wait Node):** Cấu hình thời gian chờ giữa các lần kiểm tra (polling) để tránh vượt quá giới hạn gọi API (rate limit) của HeyGen.
- **If Processing Completed (If Node):** Kiểm tra trạng thái render của video. Nếu thành công sẽ chuyển sang bước tải xuống, nếu lỗi sẽ dừng lại hoặc báo cáo.
- **Download Video (HTTP Request Node):** Tải file video hoàn thiện từ đường dẫn trả về của HeyGen về bộ nhớ tạm của n8n.
- **Upload a video (YouTube Node):** Cần kết nối tài khoản YouTube thông qua **youTubeOAuth2Api**. Sau đó chọn thao tác (`operation: upload`, `resource: video`) và map dữ liệu video vừa tải về để đẩy lên kênh.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một đoạn kịch bản ngắn để kiểm tra toàn bộ luồng từ HeyGen đến YouTube.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để bắt đầu tự động hóa thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Kết nối node WebHook với **Google Sheets** hoặc **Airtable**. Các sếp chỉ cần điền danh sách kịch bản vào bảng, n8n sẽ tự động đọc và xử lý tuần tự từng video.
- **Thêm thông báo (Notifications):** Thêm một node **Telegram** hoặc **Slack** ở cuối workflow để nhận thông báo kèm link YouTube ngay khi video được xuất bản thành công.
- **Lưu lịch sử:** Ghi lại log trạng thái, tiêu đề và link video vào cơ sở dữ liệu hoặc Notion để dễ dàng quản lý nội dung kênh.

### 📌 Kết luận
Với workflow tự động hóa HeyGen kết hợp YouTube trên n8n này, việc xây dựng một kênh video AI triệu view chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tối ưu hóa hiệu suất làm nội dung của các sếp!