---
title: "🚀 Tự động hóa sản xuất kênh YouTube truyện ngủ (Bedtime Story) với AI và n8n"
description: "Xây dựng hệ thống tự động hóa 100% quy trình tạo video truyện ngủ cho YouTube từ viết kịch bản, tạo giọng đọc, vẽ ảnh minh họa, ghép nhạc nền đến xuất bản video bằng n8n."
slug: "tu-dong-hoa-youtube-bedtime-story-ai-n8n"
tags: [n8n, automation, ai, openai, youtube, content-creation]
keywords: [n8n workflow, tự động hóa youtube, ai video generator, tạo video tự động, openai tts, sam automation]
keywords: [n8n workflow, tự động hóa youtube, ai video generator, tạo video tự động, openai tts, sam automation]
---

# 🚀 Tự động hóa sản xuất kênh YouTube truyện ngủ (Bedtime Story) với AI và n8n

Viết kịch bản, lồng tiếng, thiết kế hình ảnh, ghép nhạc và dựng video thủ công cho một kênh YouTube chủ đề truyện ngủ (Bedtime Story) ngốn của các sếp hàng tá thời gian mỗi ngày. Chưa kể việc duy trì tần suất đăng tải đều đặn là một thử thách thực sự đối với bất kỳ nhà sáng tạo nội dung nào.

Workflow n8n đỉnh cao được phát triển bởi **Samautomation.work** này sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động hóa toàn bộ quy trình từ A-Z: từ việc lên ý tưởng, viết câu chuyện bằng AI, tạo giọng đọc, sinh prompt và vẽ ảnh minh họa, chọn nhạc nền ngẫu nhiên, dựng video tự động qua API, lưu trữ đám mây, quản lý qua Google Sheets, thông báo qua Telegram và cuối cùng là đăng tải lên YouTube mà không cần động tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt khi phải xử lý các tác vụ render video nặng nhọc), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sản xuất nội dung 24/7 không gián đoạn**: Lên lịch tự động chạy định kỳ nhờ `Schedule Trigger1` mà không cần con người can thiệp.
- **Tự động hóa toàn diện**: Kết hợp mượt mà giữa OpenAI (Text, TTS, Whisper), Gemini (Image Prompts), Google Cloud Storage, Google Sheets và Telegram.
- **Chất lượng chuyên nghiệp**: Tự động tạo giọng đọc truyền cảm, tạo hình ảnh minh họa bám sát nội dung, lồng nhạc nền thư giãn và render video hoàn chỉnh.
- **Quản lý dữ liệu trực quan**: Tự động cập nhật tiến độ render, lưu trữ link video và log hoạt động trực tiếp vào Google Sheets, đồng thời gửi thông báo trạng thái qua Telegram.
:::

### 🚀 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance**: Đã cài đặt phiên bản n8n (Khuyến nghị Self-hosted trên VPS).
- **OpenAI API Key**: Dùng cho việc tạo kịch bản (`Generate Transcript With AI`), tạo tiêu đề (`Generate Title with AI`), Text-to-Speech (`OPENai TTS`) và Whisper Transcription.
- **Google Gemini API Key**: Dùng cho node `Make Image Prompts Gemini` để sinh prompt tạo ảnh.
- **Google Cloud Storage (GCS)**: Tài khoản lưu trữ để lưu tệp âm thanh, nhạc nền (`Get Random BG music`, `Save Audio GSC`) và hình ảnh minh họa (`Save images to GC`).
- **Google Sheets**: Bảng tính quản lý dữ liệu đầu vào/đầu ra (`Append GS`, `Grab Video from GS`, `Upgrade Progress on GS`).
- **Telegram Bot Token**: Để nhận thông báo trạng thái qua node `Send message with Telegram`.
- **Dịch vụ Video Render API**: Cấu hình tài khoản tương thích với node `Create Video` để dựng video từ JSON.
- **YouTube Data API Credentials**: Kết nối tài khoản YouTube qua node `YouTube Seos Kanaal`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và tải file JSON lên. Hoặc đơn giản là copy toàn bộ mã JSON và dán trực tiếp vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một siêu workflow phức tạp gồm 41 nodes, các sếp cần chú ý cấu hình kỹ lưỡng các node trọng điểm sau:
- **Schedule Trigger1**: Thiết lập lịch chạy định kỳ (ví dụ: chạy mỗi ngày 1 lần hoặc 3 lần/tuần tùy chiến lược kênh).
- **Grab Animal / Grab Video from GS**: Trỏ tới file Google Sheets của các sếp để nợ dữ liệu đầu vào (chủ đề, nhân vật, từ khóa...).
- **Generate Transcript With AI & Generate Title with AI**: Cấu hình credentials OpenAI và kiểm tra lại System Prompt để đảm bảo AI viết đúng phong cách truyện ngủ thiếu nhi/thư giãn.
- **OPENai TTS & Transcribe with OpenAI Whisper**: Đảm bảo kết nối đúng tài khoản OpenAI và chọn giọng đọc (voice) phù hợp (ví dụ: *alloy*, *echo*, *fable*, *onyx*, *nova*, hoặc *shimmer*).
- **Get Random BG music / Save Audio GSC / Save images to GC**: Cấu hình thông tin xác thực Google Cloud Storage (Bucket Name, Project ID) để hệ thống tải nhạc nền và lưu trữ tài nguyên đúng thư mục.
- **Make Image Prompts Gemini**: Nhập API key của Google Gemini để sinh prompt vẽ ảnh chi tiết.
- **Create Video & Get Video Progress**: Liên kết với API render video của các sếp, cấu hình thời gian chờ (`Wait 6 min for Rendering`) cho phù hợp với độ dài video.
- **Send message with Telegram**: Điền Chat ID và Bot Token để nhận tin nhắn báo cáo khi video hoàn thành hoặc có lỗi xảy ra.
- **YouTube Seos Kanaal**: Kết nối OAuth2 với tài khoản YouTube của kênh để tự động publish video lên chuỗi xuất bản.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với dữ liệu mẫu nhỏ để kiểm tra từng chặng (từ kịch bản -> âm thanh -> hình ảnh -> render video).
- Sau khi kiểm tra mọi thứ chạy mượt mà không lỗi, hãy bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Telegram, các sếp có thể nối thêm node Slack hoặc Discord để đội ngũ content cùng theo dõi tiến độ sản xuất video.
- **Tối ưu hóa chi phí AI**: Cân nhắc sử dụng các mô hình AI có chi phí tối ưu hơn cho các bước sinh prompt ảnh nếu cần sản xuất số lượng lớn video mỗi ngày.
- **Tự động đăng mạng xã hội khác**: Bổ sung thêm các node tự động cắt ngắn video (Shorts/Reels) để đăng đồng loạt lên TikTok, Instagram Reels và Facebook Reels, tối đa hóa traffic về kênh YouTube chính.

### 📌 Kết luận
Tự động hóa sản xuất nội dung YouTube chưa bao giờ dễ dàng và mượt mà đến thế với sự trợ giúp của n8n và các mô hình AI thế hệ mới. Hãy thiết lập ngay workflow này để giải phóng sức lao động thủ công và bùng nổ lượng view cho kênh của các sếp!