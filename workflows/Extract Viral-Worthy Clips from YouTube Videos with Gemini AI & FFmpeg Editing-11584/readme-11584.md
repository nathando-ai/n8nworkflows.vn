---
title: "🚀 Tự động hóa cắt video ngắn triệu view từ YouTube bằng Google Gemini AI và FFmpeg trong n8n"
description: "Biến video dài thành các đoạn short/reels viral tự động 100% nhờ Gemini AI phân tích nội dung, kết hợp yt-dlp và FFmpeg để cắt dựng chuyên nghiệp."
slug: "tu-dong-hoa-cat-video-ngan-youtube-gemini-ai-ffmpeg"
tags: [n8n, automation, no-code, ai, gemini, ffmpeg, youtube]
keywords: [n8n workflow, tạo video ngắn tự động, youtube shorts automation, gemini ai, ffmpeg automation, yt-dlp n8n]
---

# 🚀 Tự động hóa cắt video ngắn triệu view từ YouTube bằng Google Gemini AI và FFmpeg

Các sếp làm sáng tạo nội dung (Content Creator) chắc đều hiểu cảm giác "nản" cỡ nào khi phải ngồi hàng giờ lướt xem các video dài trên YouTube để chọn ra những khoảnh khắc đắt giá, rồi lại cặm cụi cắt ghép, chèn sub, chỉnh khung hình dọc cho TikTok, Reels hay Shorts. Quá tốn thời gian và công sức!

Bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ này. Hệ thống sẽ tự động hóa từ A-Z: tải video, dùng **Google Gemini AI** phân tích đa phương thức để tìm các đoạn "triệu view", tiến hành cắt dựng bằng **FFmpeg**, tự động đóng sub và gửi kết quả thẳng vào email cho các sếp. Hoàn toàn tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Vì workflow này cần thực thi các lệnh hệ thống (CLI) như FFmpeg và yt-dlp, các sếp **bắt buộc phải chạy n8n dạng Self-hosted (trên VPS riêng)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh trượt thủ công từng phút video để tìm khoảnh khắc vàng.
- **AI chọn lọc thông minh:** Google Gemini AI phân tích cả transcript lẫn nội dung video để tìm ra 3-5 đoạn có tiềm năng viral cao nhất.
- **Dựng video tự động chuyên nghiệp:** Tự động cắt clip, đổi khung hình sang dọc (9:16), tính toán kích thước và render sub trực tiếp lên video.
- **Vận hành trơn tru:** Nhận thông báo qua Gmail ngay khi các đoạn short hoàn tất và sẵn sàng xuất bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống Self-hosted n8n** có cài sẵn:
  - `FFmpeg` ([Hướng dẫn cài đặt](https://docs.n8n.io/integrations/community-nodes/installation/gui-install/#install-via-npm))
  - `yt-dlp` ([Hướng dẫn cài đặt](https://github.com/yt-dlp/yt-dlp#installation))
- **Tài khoản & API Keys:**
  - Google Gemini API Key ([Lấy key tại đây](https://ai.google.dev/))
  - Tài khoản Gmail (cấu hình OAuth2 để gửi email thông báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 37 nodes được chia thành các phân đoạn xử lý từ tải video, phân tích AI, đến cắt dựng. Các sếp cần chú ý các điểm sau:
- **On form submission:** Form nhập tiêu đề và link YouTube đầu vào. Các sếp có thể thay thế bằng Webhook hoặc Trigger tùy ý.
- **video download with yt-dlp** & **get transcript from yt-dlp** (Node `executeCommand`): Đảm bảo VPS đã cài đặt thành công `yt-dlp` và `ffmpeg` để các lệnh gọi terminal không bị lỗi.
- **viral clips identification** & **Analyze the actual whole video** (Node `googleGemini`): Kết nối với credentials `googlePalmApi` bằng Gemini API Key của các sếp. Prompt trong này đã được thiết kế sẵn để tìm các khoảnh khắc viral.
- **filter out top clips according to score** (Node `code`): Nơi lọc ra các clip có điểm số cao nhất (mặc định lấy top các đoạn xuất sắc nhất).
- **Call subworkflow** / Sub-workflow chỉnh sửa: Phần xử lý cắt dựng clip (`EDITING` trigger), chèn sub và render video. Các sếp có thể tách thành sub-workflow như hướng dẫn trên canvas của tác giả để quản lý gọn gàng hơn.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng một link YouTube ngắn trước để kiểm tra quyền truy cập thư mục lưu trữ trên VPS (`/data/clips/`).
- Sau khi kiểm tra mọi thứ chạy mượt mà, bật **Active workflow** để hệ thống tự động hóa toàn diện.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Thay vì chỉ nhận email qua node `Send a message (gmail)`, các sếp có thể đấu nối thêm Telegram Bot hoặc Slack để nhận video trực tiếp ngay trên điện thoại.
- **Lưu trữ đám mây:** Thêm node Google Drive hoặc AWS S3 vào cuối luồng để tự động tải các file video đã render xong lên cloud, tiết kiệm dung lượng ổ cứng VPS.
- **Tinh chỉnh Wait Nodes:** Vì xử lý video nặng tốn nhiều RAM và CPU, hãy điều chỉnh thời gian ở các node `Wait` cho phù hợp với cấu hình VPS thực tế của các sếp để tránh quá tải (Out of Memory).

### 📌 Kết luận
Việc sản xuất nội dung ngắn dạng Short/Reels nay đã được tự động hóa hoàn toàn nhờ sức mạnh của AI và các công cụ mã nguồn mở. Hãy thiết lập ngay workflow này trên hệ thống n8n của các sếp để giải phóng sức lao động và bùng nổ lượt xem trên các nền tảng mạng xã hội!