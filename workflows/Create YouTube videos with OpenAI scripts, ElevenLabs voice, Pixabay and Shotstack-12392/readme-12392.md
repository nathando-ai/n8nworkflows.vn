---
title: "🚀 Tự động hóa tạo video YouTube chuyên nghiệp với OpenAI, ElevenLabs, Pixabay và Shotstack qua n8n"
description: "Hướng dẫn chi tiết cách xây dựng hệ thống tự động tạo video YouTube từ kịch bản AI, lồng tiếng chân thực, ghép video stock và dựng hình tự động 100% không cần chạm tay."
slug: "tu-dong-hoa-tao-video-youtube-openai-elevenlabs-shotstack-n8n"
tags: [n8n, automation, youtube, ai-video, openai, elevenlabs, shotstack, pixabay]
keywords: [n8n workflow, tạo video tự động, openai script, elevenlabs voice, shotstack api, pixabay videos, tự động hóa youtube]
---

# 🚀 Tự động hóa tạo video YouTube chuyên nghiệp với OpenAI, ElevenLabs, Pixabay và Shotstack

Các sếp có đang cảm thấy mệt mỏi và tốn quá nhiều thời gian mỗi khi cần sản xuất video cho kênh YouTube? Việc lên ý tưởng kịch bản, thuê diễn viên lồng tiếng, tìm kiếm tư liệu video, rồi lại cặm cụi dựng hình (editing) hàng giờ đồng hồ thực sự ngốn quá nhiều nguồn lực.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một "nhà máy sản xuất video tự động" siêu cấp với n8n. Workflow này sẽ tự động hóa toàn bộ quy trình: từ việc **dùng OpenAI viết kịch bản**, **ElevenLabs tạo giọng đọc AI**, **Pixabay lấy kho video stock**, cho đến **Shotstack dựng phim tự động** và **lưu trữ trực tiếp lên Google Drive**. Các sếp chỉ việc ngồi chơi xơi nước và nhận thành quả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tệp video nặng và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ từ khóa ban đầu cho ra một video hoàn chỉnh sẵn sàng đăng tải lên YouTube.
- **Chất lượng đỉnh cao:** Kịch bản sắc sảo từ OpenAI kết hợp giọng đọc AI mượt mà như người thật từ ElevenLabs.
- **Tiết kiệm chi phí nhân sự:** Không cần thuê biên tập viên, diễn viên lồng tiếng hay editor đắt đỏ.
- **Sản xuất hàng loạt:** Dễ dàng mở rộng quy mô xuất bản video mỗi ngày cho nhiều kênh khác nhau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Dùng cho node `Generate Script2`).
- **ElevenLabs API Key** (Dùng cho HTTP Request gọi giọng đọc).
- **Pixabay API Key** (Dùng cho node `Search Pixabay Videos`).
- **Shotstack API Key** (Dùng cho các node render video).
- **Google Cloud Console Credentials** (OAuth2 cho Google Drive để lưu trữ voiceover và video hoàn chỉnh).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà không lỗi vặt, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **`Schedule Trigger`**: Đặt lịch chạy tự động (ví dụ: chạy mỗi ngày vào 8 giờ sáng hoặc chạy thủ công khi test).
- **`Set Video Parameters1`**: Thiết lập chủ đề video, từ khóa tìm kiếm và các tham số đầu vào cơ bản.
- **`Generate Script2` (OpenAI)**: Kết nối `openAiApi` credentials và cấu hình prompt chi tiết trong phần tham số để AI viết kịch bản đúng ý đồ của các sếp.
- **`HTTP Request` (ElevenLabs)**: Cấu hình Header Auth với API Key của ElevenLabs để chuyển hóa kịch bản văn bản thành tệp âm thanh (voiceover).
- **`Upload Voiceover to Drive` & `Make Voiceover Public` (Google Drive)**: Kết nối `googleDriveOAuth2Api` để tải file giọng đọc lên Drive và bật quyền truy cập công khai giúp các dịch vụ render video dễ dàng truy xuất.
- **`Search Pixabay Videos` (HTTP Request)**: Cấu hình API Key của Pixabay để tự động tìm kiếm các đoạn video stock phù hợp với chủ đề kịch bản.
- **`Build Shotstack JSON1` & `Submit Render Job1` (Code & HTTP Request)**: Đóng gói dữ liệu kịch bản, âm thanh, video thành cú pháp JSON chuẩn của Shotstack và gửi yêu cầu render.
- **`Wait for Render1` & `Check Render Status1`**: Node chờ và kiểm tra tiến độ render video từ phía Shotstack.
- **`Is Render Complete?1` (If) & `Download Final Video1`**: Kiểm tra xem video đã render xong chưa. Nếu xong sẽ tiến hành tải video về.
- **`Save to Google Drive1` (Google Drive)**: Lưu trữ video hoàn thiện cuối cùng vào thư mục chỉ định trên Google Drive của các sếp.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) thủ công từng bước để đảm bảo các API kết nối thành công và không gặp lỗi xác thực.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node gửi thông báo về Telegram hoặc Slack ngay khi video được render xong và lưu vào Google Drive để các sếp kịp thời kiểm duyệt.
- **Tự động đăng YouTube:** Kết nối thêm node YouTube API ở cuối workflow để tự động upload video lên kênh ở chế độ Private hoặc Public.
- **Quản lý Sheet:** Lưu lịch sử các chủ đề video và link Google Drive vào Google Sheets để dễ dàng theo dõi tiến độ sản xuất nội dung hàng tuần.

### 📌 Kết luận
Workflow tự động hóa tạo video YouTube với OpenAI, ElevenLabs, Pixabay và Shotstack thực sự là một "vũ khí tối thượng" cho các nhà sáng tạo nội dung và doanh nghiệp muốn tối ưu hóa chiến lược Marketing đa kênh. Hãy cài đặt ngay hôm nay để giải phóng sức lao động thủ công và bứt phá lượng view cùng n8n nhé các sếp!