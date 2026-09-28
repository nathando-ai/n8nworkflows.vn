---
title: "🚀 Tự động hóa tạo video ngắn AI từ YouTube với Reka Vision API và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt video mới từ kênh YouTube, sử dụng Reka AI để cắt dựng video ngắn thông minh và gửi thông báo qua Gmail."
slug: "tu-dong-hoa-tao-video-ngan-ai-tu-youtube-voi-reka-vision-api"
tags: [n8n, automation, no-code, reka-ai, youtube, content-creation, ai-video]
keywords: [n8n workflow, tạo video ai tự động, reka vision api, youtube automation, gmail n8n, cat video ai]
---

# 🚀 Tự động hóa tạo video ngắn AI từ YouTube với Reka Vision API và n8n

Việc sản xuất nội dung ngắn (Shorts, Reels, TikTok) từ các video dài trên YouTube đòi hỏi rất nhiều thời gian thủ công: từ việc xem lại video, chọn phân cảnh hấp dẫn, cắt ghép đến thêm phụ đề. Nếu các sếp đang đau đầu vì tốn quá nhiều nhân lực cho việc này, workflow n8n này chính là lời giải hoàn hảo! 

Workflow này sẽ tự động hóa 100% quy trình: Phát hiện video YouTube mới 👉 Gửi yêu cầu phân tích & cắt dựng cho Reka Vision AI 👉 Kiểm tra tiến độ 👉 Gửi email thông báo kết quả khi video sẵn sàng hoặc báo lỗi nếu có sự cố.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Bắt trọn mọi video mới đăng tải trên kênh YouTube mục tiêu mà không cần thao tác tay.
- **Sức mạnh Multimodal AI**: Tận dụng Reka Vision API để phân tích nội dung, chọn lọc khoảnh khắc đắt giá và dựng video ngắn (tỷ lệ 9:16, kèm phụ đề) tự động.
- **Quy trình thông minh**: Tích hợp cơ chế chờ (Wait), lặp kiểm tra trạng thái (Loop) và vòng lặp an toàn chống lặp vô tận (Max Reached).
- **Chủ động thông báo**: Nhận email qua Gmail ngay khi video hoàn tất hoặc nhận cảnh báo ngay lập tức nếu tiến trình gặp lỗi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Reka AI Account & API Key**: Đăng ký tài khoản và lấy API key miễn phí từ trang chủ Reka AI.
- **Gmail Account**: Tài khoản Gmail để cấu hình gửi thông báo qua OAuth2.
- **YouTube RSS Feed**: Đường dẫn RSS feed của kênh YouTube mà các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ template gốc (ID: 12926) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:

- **When New Video (`rssFeedReadTrigger`)**: 
  - Thay đổi URL của RSS Feed thành kênh YouTube mục tiêu. 
  - *Ví dụ mẫu*: `https://www.youtube.com/feeds/videos.xml?channel_id=UCAr20GBQayL-nFPWFnUHNAA`
- **Create Reel Creation Job (`httpRequest`)**:
  - Thêm Credentials dạng `httpBearerAuth` sử dụng **Reka AI API Key**.
  - Tinh chỉnh Prompt, thời lượng tối đa/tối thiểu (`min_duration_seconds`, `max_duration_seconds`), mẫu template (`moments` hoặc `compilation`) và cấu hình rendering (bật phụ đề `subtitles: true`, tỷ lệ khung hình `aspect_ratio: "9:16"`).
- **Get Job Status (`httpRequest`)**:
  - Sử dụng chung Credentials `httpBearerAuth` với Reka AI để gọi API kiểm tra trạng thái xử lý đoạn video.
- **Wait 10 minutes (`wait`)**:
  - Thời gian AI tải, phân tích và render video có thể dao động tùy thuộc vào độ dài video gốc. Các sếp hãy điều chỉnh thời gian chờ cho phù hợp (Ví dụ: Video 5-8 phút nên đặt chờ khoảng 15 phút).
- **Send Clip Ready EMail & Send Failure EMail (`gmail`)**:
  - Kết nối tài khoản Gmail thông qua `gmailOAuth2`.
  - Cá nhân hóa nội dung email (tiêu đề, người nhận) để dễ dàng theo dõi đường dẫn video trả về từ Reka AI.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) từng node để đảm bảo kết nối API Reka và Gmail không gặp lỗi xác thực.
- Bật công tắc **Active** để workflow bắt đầu tự động lắng nghe video mới từ YouTube 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Thay vì chỉ dùng Gmail, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận thông báo tức thì trên điện thoại khi video ngắn đã sẵn sàng.
- **Lưu trữ tự động**: Thêm node **Google Sheets** để lưu lại lịch sử các video đã được AI cắt dựng, giúp dễ dàng kiểm tra và quản lý kho nội dung.
- **Tối ưu Prompt**: Tùy biến câu lệnh (prompt) trong node tạo job để AI tập trung vào các chủ đề cụ thể hoặc phong cách giật gân, hài hước tùy theo định hướng kênh.

### 📌 Kết luận
Workflow tự động hóa tạo video ngắn từ YouTube bằng Reka Vision API và n8n là trợ đắc lực giúp tối ưu hóa hiệu suất sản xuất nội dung đa nền tảng. Hãy triển khai ngay hôm nay để tiết kiệm hàng giờ đồng hồ làm việc thủ công và bùng nổ traffic cho kênh của các sếp!