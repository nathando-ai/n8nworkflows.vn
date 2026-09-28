---
title: "🚀 Tự động tạo và đa ngôn ngữ hóa video ngắn với AI, WayinVideo và Google Drive"
description: "Hướng dẫn xây dựng workflow n8n tự động cắt video, dịch phụ đề sang nhiều ngôn ngữ bằng AI thông qua WayinVideo và lưu trữ gọn gàng lên Google Drive."
slug: "tu-dong-tao-video-ngan-da-ngon-ngu-wayinvideo-google-drive"
tags: [n8n, automation, ai-video, wayinvideo, google-drive, content-creation]
keywords: [n8n workflow, tạo video ngắn ai, wayinvideo api, dịch phụ đề video tự động, n8n google drive]
---

# 🚀 Tự động tạo và đa ngôn ngữ hóa video ngắn với AI, WayinVideo và Google Drive

Việc sản xuất video ngắn (Reels, TikTok, Shorts) đa ngôn ngữ từ một video dài thủ công là một cơn ác mộng thực sự: bạn phải tải video về, cắt đoạn, dịch nội dung, làm phụ đề cho từng thứ tiếng và xuất file liên tục. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: Nhận link video từ Form, tách thành nhiều ngôn ngữ mong muốn, gửi đến AI của **WayinVideo** để tạo các clip dọc kèm phụ đề dịch thuật, tự động kiểm tra trạng thái, tải về và lưu trữ gọn gàng vào **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa ngôn ngữ:** Chỉ cần nhập 1 link video và danh sách mã ngôn ngữ (vd: `en,hi,es,fr`), hệ thống tự tách thành các luồng xử lý độc lập.
- **AI thông minh:** Tự động tạo các clip dọc tỉ lệ 9:16 kèm phụ đề dịch chuẩn xác bằng AI thông qua WayinVideo.
- **Quản lý file khoa học:** Tự động tải video hoàn thiện về và đồng bộ thẳng lên thư mục Google Drive định sẵn với tên chuẩn AI.
- **Chạy ngầm thông minh:** Cơ chế chờ (Wait) và kiểm tra trạng thái (Polling) đảm bảo workflow không bị lỗi khi video đang render.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản và **API Key (Bearer Token)** từ [WayinVideo](https://wayinvideo.com).
- Tài khoản **Google Drive** để cấu hình OAuth2 kết nối với n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **Node `3. WayinVideo — Submit Clipping Task` & `5. WayinVideo — Get Clip Results` (HTTP Request):** Thay thế đoạn `YOUR_WAYINVIDEO_API_KEY` bằng mã Bearer Token thực tế của các sếp.
- **Node `10. Google Drive — Upload Clip`:** 
  - Kết nối tài khoản Google Drive thông qua `googleDriveOAuth2Api`.
  - Thay thế `YOUR_GDRIVE_FOLDER_ID` bằng ID thư mục Google Drive nơi các sếp muốn lưu trữ các video đầu ra.
- **Cấu hình tùy chỉnh nâng cao (Tùy chọn):**
  - Thay đổi `target_duration` thành `DURATION_15_30` nếu muốn các clip ngắn hơn cho Reels/Shorts.
  - Thay đổi `ratio` thành `RATIO_1_1` nếu muốn video dạng vuông.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và điền thử nghiệm thông tin vào Form trigger để kiểm tra vòng lặp render video.
- Sau khi test thành công, gạt nút **Active** để đưa workflow vào vận hành tự động 24/7.

:::warning[CẢNH BÁO: Rủi ro vòng lặp vô hạn]
Nếu WayinVideo không trả về trạng thái `SUCCEEDED` (ví dụ: video lỗi, URL không hợp lệ), workflow có thể bị kẹt trong vòng lặp vô hạn giữa node `Wait` và node `Get Result`. 

👉 **Khắc phục:** Nên bổ sung một Set node để đếm số lần thử lại (retry count) và một IF node để dừng hẳn tiến trình nếu số lần thử vượt quá giới hạn (ví dụ: tối đa 5-10 lần).
:::

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node Slack hoặc Telegram ngay sau node Google Drive để bot tự động bắn thông báo kèm tên video và link Drive khi render xong.
- **Lưu log vào Google Sheets:** Ghi lại lịch sử các lần chạy workflow (Link video gốc, ngôn ngữ, thời gian hoàn thành) để dễ dàng quản lý.
- **Mở rộng nguồn đầu vào:** Thay vì dùng Form Trigger, có thể nhận yêu cầu từ Webhook của hệ thống CRM hoặc Airtable.

### 📌 Kết luận
Workflow tạo video đa ngôn ngữ bằng WayinVideo và Google Drive là mảnh ghép hoàn hảo giúp các đội ngũ Content Marketing nhân bản nội dung toàn cầu một cách tự động và tiết kiệm thời gian nhất. Lên đồ ngay và tối ưu hóa quy trình sản xuất video của các sếp thôi!