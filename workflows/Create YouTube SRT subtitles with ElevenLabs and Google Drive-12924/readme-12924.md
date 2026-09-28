---
title: "🚀 Tự động tạo phụ đề SRT cho YouTube bằng ElevenLabs và Google Drive trên n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa trích xuất âm thanh, chuyển đổi giọng nói thành văn bản với AI ElevenLabs và lưu file SRT trực tiếp lên Google Drive."
slug: "tu-dong-tao-phu-de-srt-youtube-elevenlabs-google-drive-n8n"
tags: [n8n, automation, elevenlabs, google-drive, youtube, ai, subtitles]
keywords: [n8n workflow, tạo phụ đề tự động, elevenlabs speech to text, google drive automation, srt generator]
---

# 🚀 Tự động tạo phụ đề SRT cho YouTube bằng ElevenLabs và Google Drive

Các nhà sáng tạo nội dung và biên tập video thường mất hàng giờ đồng hồ chỉ để nghe lại video, gõ chữ và căn chỉnh thời gian (timestamps) làm phụ đề SRT. Công việc thủ công này cực kỳ nhàm chán và chiếm nhiều thời gian quý báu.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình trên: Nhận một đường dẫn video, tự động bóc tách âm thanh, sử dụng trí tuệ nhân tạo (AI) đỉnh cao của **ElevenLabs** để nhận diện giọng nói và chuyển đổi thành file phụ đề SRT chuẩn chỉnh, sau đó tự động lưu trữ gọn gàng lên **Google Drive**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải ngồi gõ từng dòng caption hay căn chỉnh timestamp thủ công.
- **Độ chính xác cao:** Ứng dụng mô hình AI nhận diện giọng nói tiên tiến từ ElevenLabs, tự động phân đoạn dựa trên dấu câu và độ dài hợp lý.
- **Sẵn sàng sử dụng:** File đầu ra đúng chuẩn định dạng SubRip (.srt), có thể upload thẳng lên YouTube hoặc các nền tảng video khác.
- **Lưu trữ tự động:** File SRT được gom về đúng thư mục chỉ định trên Google Drive, dễ dàng quản lý và chia sẻ với đội ngũ dựng phim.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **ElevenLabs Account & API Key:** Cần tài khoản ElevenLabs có tích hợp Speech-to-Text. 👉 [Đăng ký ElevenLabs](https://try.elevenlabs.io/ahkbf00hocnu)
- **Google Drive Account:** Tài khoản Google để cấu hình OAuth2 kết nối với n8n phục vụ việc upload file.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sao chép trực tiếp từ n8n template, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được liên kết chặt chẽ. Các sếp cần chú ý cấu hình các node sau:

- **Node `Set Video Url` (Set):** 
  - Điền đường dẫn video (ví dụ: link YouTube hợp lệ) vào tham số đầu vào, hoặc cấu hình nhận dữ liệu động từ webhook/trigger khác nếu muốn tích hợp vào hệ thống lớn hơn.
- **Node `Get Video` (HTTP Request):** 
  - Đảm bảo node này lấy được nội dung video/audio chuẩn bị cho bước xử lý tiếp theo.
- **Node `Transcribe audio or video` (ElevenLabs):** 
  - Chọn credentials `elevenLabsApi` và điền **ElevenLabs API Key** của các sếp.
  - Cấu hình Resource là `speech` và Operation là `speechToText`.
- **Node `From Elevenlabs to Srt` & `From Json to Binary` (Code):** 
  - Các node JavaScript có sẵn nhiệm vụ xử lý dữ liệu JSON trả về từ ElevenLabs, gom nhóm theo thời gian và dịch sang định dạng SRT chuẩn, sau đó chuyển thành file nhị phân (binary). *Hầu như không cần sửa code ở đây nếu giữ nguyên cấu trúc mặc định.*
- **Node `Upload file` (Google Drive):** 
  - Cấu hình credentials `googleDriveOAuth2Api` của tài khoản Google.
  - Chọn đúng **Google Drive Folder ID** nơi các sếp muốn lưu trữ các file SRT được tạo ra.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Execute Workflow"** tại node `When clicking ‘Execute workflow’` để test chạy thử với một video mẫu.
- Kiểm tra kết quả trên Google Drive xem file `.srt` đã xuất hiện chưa.
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook/Form:** Thay vì chạy thủ công bằng tay, hãy thay node `Manual Trigger` bằng `Webhook` hoặc `n8n Form` để tạo một trang web mini cho phép team content tự dán link YouTube và nhận file SRT tự động.
- **Gửi thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo kèm link Google Drive ngay khi file phụ đề được tạo xong.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để lưu lại lịch sử các video đã được tạo phụ đề (Tên video, Link gốc, Thời gian tạo, Link file SRT trên Drive).

### 📌 Kết luận
Việc tạo phụ đề chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n và sức mạnh AI của ElevenLabs. Áp dụng ngay workflow này để giải phóng sức lao động cho team sản xuất nội dung của các sếp!