---
title: "🚀 Tự động tạo âm thanh mới cho video và ghép nối hoàn chỉnh với Fal.run & Google Drive qua n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình tạo âm thanh AI cho video, ghép nối bằng FFmpeg qua Fal.run và lưu trữ trực tiếp lên Google Drive bằng n8n."
slug: "tu-dong-tao-am-thanh-video-fal-run-google-drive-n8n"
tags: [n8n, automation, ai, fal-run, google-drive, video-editing]
keywords: [n8n workflow, tao am thanh video ai, fal run sonilo, ffmpeg merge video, google drive automation]
---

# 🚀 Tự động tạo âm thanh mới cho video và ghép nối hoàn chỉnh với Fal.run & Google Drive

Các sếp làm sáng tạo nội dung, marketing hay sản xuất video chắc hẳn đều hiểu cảm giác tốn kém thời gian thế nào khi phải chỉnh sửa thủ công: từ việc tạo hiệu ứng âm thanh, lồng tiếng, cho đến khâu mix và render lại video. Việc này không chỉ chậm chạp mà còn khó scale khi cần sản xuất số lượng lớn video ngắn (Reels, TikTok, Shorts).

Workflow n8n tuyệt vời này (được phát triển bởi chuyên gia Davide Boizza) sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động nhận video từ form đầu vào, gửi sang Fal.run (sử dụng Sonilo API) để tạo âm thanh mới, dùng FFmpeg API để ghép âm thanh vào video gốc, kiểm tra trạng thái liên tục (polling) và cuối cùng tự động tải về, lưu trữ gọn gàng lên Google Drive. 100% tự động hóa không cần code thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần gửi video qua Form, hệ thống tự lo phần còn lại từ A-Z.
- **Ứng dụng AI tiên tiến:** Tích hợp các mô hình xử lý media mạnh mẽ trên Fal.run (Sonilo API & FFmpeg).
- **Cơ chế thông minh (Polling Loop):** Tự động chờ và kiểm tra trạng thái xử lý âm thanh và render video mà không sợ lỗi timeout.
- **Lưu trữ khoa học:** Tự động đồng bộ và lưu video thành phẩm trực tiếp vào Google Drive để dễ dàng sử dụng hoặc chia sẻ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Fal.run:** API Key để gọi các dịch vụ AI Sonilo và FFmpeg.
- **Tài khoản Google Drive:** Kết nối OAuth2 để n8n có quyền upload file lên thư mục chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor, hoặc tải file JSON về và import thông qua menu quản lý workflow.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các điểm sau:
- **When Form Submitted:** Cấu hình các trường input trên form để người dùng có thể tải lên hoặc cung cấp đường dẫn video nguồn hợp lệ.
- **Các HTTP Request Nodes (`Convert Video to Sound`, `Merge Audio with Video`,...):** 
  - Thêm thông tin xác thực (`httpHeaderAuth`) với API Key của **Fal.run**.
  - Kiểm tra lại các endpoint URL của Sonilo API và FFmpeg queue trên Fal.run.
- **Kiểm tra biểu thức (Expressions):** Đảm bảo các node điều kiện (`Check Audio Conversion Status`, `Check Video Merge Status`) nhận đúng ID yêu cầu, audio URL và video URL được truyền qua lại giữa các bước.
- **Upload to Google Drive:** Chọn đúng kết nối tài khoản Google Drive (`googleDriveOAuth2Api`) và chọn thư mục đích (Destination Folder) nơi lưu trữ video hoàn chỉnh.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một file video mẫu ngắn để kiểm tra toàn bộ chuỗi xử lý từ tạo âm thanh đến ghép video.
- Sau khi test thành công, bật trạng thái **Active** cho workflow để hệ thống bắt đầu nhận request từ form tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để hệ thống tự động gửi tin nhắn báo cáo kèm link Google Drive ngay khi video render xong.
- **Tối ưu thời gian chờ:** Điều chỉnh thời gian ở các node `Wait 60 Seconds for Conversion` và `Wait 30 Seconds for Merge` tùy thuộc vào độ dài video và tốc độ xử lý thực tế của phía Fal.run.
- **Mở rộng lưu trữ:** Kết hợp thêm các bước cập nhật link video vào Google Sheets hoặc Airtable để dễ dàng quản lý kho nội dung.

*(Đừng quên ghé thăm và ủng hộ kênh YouTube chính thức của tác giả tại [Youtube.com/@n3witalia](https://youtube.com/@n3witalia) để cập nhật thêm nhiều template n8n miễn phí và hữu ích khác!)*

### 📌 Kết luận
Workflow "Generate new video audio and merge the final result with Fal.run and Google Drive" là một giải pháp cực kỳ mạnh mẽ giúp tối ưu hóa quy trình sản xuất video bằng AI. Hãy áp dụng ngay vào hệ thống của các sếp để tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi ngày!