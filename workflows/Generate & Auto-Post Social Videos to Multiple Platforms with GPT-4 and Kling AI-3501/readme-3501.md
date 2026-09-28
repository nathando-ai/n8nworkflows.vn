---
title: "🚀 Tự động hóa sản xuất và đăng video đa nền tảng bằng GPT-4 và Kling AI qua n8n"
description: "Hướng dẫn xây dựng hệ thống AI tự động hoàn toàn: nhận prompt từ Telegram, tạo video điện ảnh với Kling AI, lồng tiếng, chèn sub, lưu Google Sheets và đăng lên 9 mạng xã hội."
slug: "tu-dong-hoa-tao-va-dang-video-ai-da-nen-tang-n8n"
tags: [n8n, automation, ai-video, gpt-4, kling-ai, social-media, telegram]
keywords: [n8n workflow, tạo video ai tự động, kling ai n8n, đăng video đa nền tảng, gpt-4 automation, auto post social media]
---

# 🚀 Tự động hóa sản xuất và đăng video đa nền tảng bằng GPT-4 và Kling AI

Việc sản xuất video ngắn (Shorts, Reels, TikTok) thủ công ngốn rất nhiều thời gian của các nhà sáng tạo nội dung và doanh nghiệp: từ khâu lên ý tưởng, viết kịch bản, tạo hình ảnh/video, thu âm lồng tiếng, dựng phim, thêm phụ đề cho đến việc phải đăng thủ công lên từng nền tảng. 

Đừng để công việc lặp đi lặp lại này làm chậm tốc độ phát triển kênh của các sếp! Bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n tự động hóa **100% quy trình sản xuất video bằng AI và đăng tải đa nền tảng** chỉ với một tin nhắn Telegram đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần gửi một câu lệnh (prompt) qua **Trigger: Telegram Prompt**, hệ thống tự lo phần còn lại từ A-Z.
- **Chất lượng đỉnh cao**: Kết hợp sức mạnh AI đỉnh cao từ GPT-4o-mini, Kling AI (tạo video), OpenAI TTS (lồng tiếng) và công cụ tự động hóa phụ đề chuyên nghiệp.
- **Phủ sóng đa kênh**: Tự động đăng video hoàn thiện lên tới **9 mạng xã hội** (Instagram, YouTube, TikTok, Facebook, LinkedIn, Threads, X, Bluesky, Pinterest) cùng lúc.
- **Quản lý tập trung**: Tự động lưu trữ metadata, tiêu đề, caption vào **Google Sheets** và gửi thông báo thành quả về Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Telegram Bot**: Tạo bot qua BotFather để nhận trigger và gửi thông báo.
- **OpenAI API Key**: Sử dụng cho GPT-4o-mini (viết kịch bản, tối ưu prompt) và Text-to-Speech (TTS).
- **Kling AI & Cloudinary / Video Processing API**: Tài khoản và API key để xử lý, render video, ghép âm thanh và phụ đề.
- **Google Sheets API / OAuth2**: Tài khoản Google để lưu trữ log metadata video.
- **Blotato API (hoặc dịch vụ tương đương)**: Dùng để phân phối video lên 9 nền tảng mạng xã hội.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn gốc hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 33 nodes được chia thành các bước rõ ràng trên canvas:

- **Trigger: Telegram Prompt**: Kết nối với Telegram Credentials của bạn để lắng nghe tin nhắn chứa prompt video.
- **Transform Prompt for Kling (GPT-4)** & **OpenAI Model Bridge**: Chọn `OpenAI Model Bridge` sử dụng model `gpt-4o-mini`, cấu hình OpenAI API key để tinh chỉnh prompt thô từ Telegram thành prompt chuẩn cho Kling AI.
- **Generate Video via Kling API**, **Get Generated Video URL**: Điền thông tin HTTP Header Auth để gọi API sinh video từ Kling.
- **Convert Script to Audio (TTS)** & **Upload Audio to Cloudinary**: Cấu hình OpenAI node để chuyển kịch bản thành giọng đọc (Audio) và tải lên Cloudinary.
- **Merge Audio + Video**, **Add Captions/Subtitles to Video**: Các node HTTP Request yêu cầu cấu hình API để ghép âm thanh vào video và tự động phủ phụ đề chuyên nghiệp.
- **Save Video Metadata to Google Sheets**: Chọn Google Sheets Credentials, trỏ tới file Google Sheet của bạn để tự động ghi log tiêu đề, caption và link video.
- **Send Final Video to Telegram**: Cấu hình node Telegram gửi video thành phẩm kèm caption về chat cá nhân hoặc nhóm để kiểm duyệt.
- **Post to [Social Platforms]**: Các node HTTP Request từ Instagram, YouTube, TikTok đến Pinterest cần được kết nối với tài khoản phân phối nội dung (ví dụ Blotato API) để thực hiện lệnh auto-publish.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn test qua Telegram Bot của bạn để kiểm tra toàn bộ luồng chạy (đặc biệt chú ý thời gian chờ ở các node `Wait` vì việc render video AI cần thời gian).
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước kiểm duyệt thủ công (Human-in-the-loop)**: Thay vì tự động đăng ngay lên 9 mạng xã hội, các sếp có thể chèn thêm node Telegram yêu cầu bấm nút "Approve/Reject" trước khi tiến hành gọi API đăng bài.
- **Mở rộng kênh lưu trữ**: Ngoài Google Sheets, có thể tích hợp thêm Notion hoặc Airtable để làm kho lưu trữ nội dung trực quan hơn.
- **Tạo bảng thống kê hiệu suất**: Định kỳ dùng n8n quét lại lượng tương tác từ các nền tảng xã hội và cập nhật ngược lại Google Sheets để đánh giá hiệu quả video.

### 📌 Kết luận
Hệ thống tự động hóa này chính là "vũ khí bí mật" giúp các sếp tiết kiệm hàng chục giờ làm việc mỗi tuần, biến ý tưởng thô thành video chuyên nghiệp và phủ sóng khắp các nền tảng mạng xã hội chỉ trong một nốt nhạc. Triển khai ngay thôi nào các sếp ơi!