---
title: "🚀 Tự động tạo hàng loạt video TikTok & Instagram Reels triệu view từ YouTube bằng Vizard AI và n8n"
description: "Biến một video YouTube dài thành hàng loạt video ngắn viral nhờ tích hợp Vizard AI và n8n. Tự động hóa hoàn toàn quy trình cắt ghép, chấm điểm viral và gửi thông báo qua Slack."
slug: "tu-dong-tao-tiktok-instagram-reels-tu-youtube-vizard-ai"
tags: [n8n, automation, no-code, vizard-ai, content-creation, ai-video]
keywords: [n8n workflow, tạo video ngắn tự động, vizard ai n8n, youtube to tiktok automation, ai content workflow]
---

# 🚀 Biến video YouTube dài thành chuỗi TikTok & IG Reels triệu view tự động với Vizard AI

Các sếp làm nội dung chắc đều hiểu cảm giác "ngợp" khi phải ngồi hàng giờ liền xem lại các video YouTube dài để tìm ra những đoạn hay nhất, sau đó cắt gọt, thêm phụ đề để đăng TikTok hay Instagram Reels. Công việc thủ công này cực kỳ ngốn thời gian và năng lượng!

Đừng lo, workflow n8n siêu việt này sinh ra là để giải cứu các sếp. Bằng cách kết hợp sức mạnh của **Form Trigger**, **Vizard AI** và **Slack**, hệ thống sẽ tự động hóa từ A-Z: nhận link YouTube, yêu cầu AI phân tích, cắt ra các đoạn ngắn có tiềm năng viral cao nhất, chấm điểm và gửi thẳng vào kênh Slack của team để duyệt. Không cần code, hoạt động tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công lọc video, cắt ghép hay chấm điểm. AI sẽ làm thay toàn bộ.
- **Bắt trọn xu hướng:** Chỉ chọn lọc các đoạn clip có điểm viral từ 9/10 trở lên, đảm bảo chất lượng nội dung đầu ra.
- **Tập trung duyệt nội dung:** Nhận ngay link tải video và tiêu đề trực tiếp trên Slack, team chỉ việc click và tải về đăng.
- **Mở rộng dễ dàng:** Dễ dàng tích hợp thêm các bước tự động tạo caption bằng LLM hoặc tự động đăng lên mạng xã hội.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **Tài khoản n8n:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Vizard.ai:** Cần có API Key hoặc thông tin xác thực HTTP Header Auth để gọi API phân tích video.
- **Workspace Slack:** Tài khoản kết nối Slack (OAuth2) để nhận thông báo video clip chất lượng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **`form_trigger`**: Tạo một giao diện form đơn giản để nhập URL video YouTube đầu vào.
- **`submit_video` (HTTP Request)**: Cấu hình API endpoint của Vizard AI kèm theo `httpHeaderAuth` để gửi yêu cầu phân tích video dài.
- **`wait`**: Thiết lập thời gian chờ hợp lý để Vizard AI hoàn thành việc xử lý video (vì AI cần thời gian render).
- **`get_clipping_status` (HTTP Request)**: Gọi endpoint `/query` của Vizard AI để kiểm tra trạng thái và lấy kết quả các đoạn clip đã cắt.
- **`filter_viral_score` (Filter)**: Đặt điều kiện lọc chỉ giữ lại những đoạn video clip có **viral score từ 9/10 trở lên**.
- **`send_initial_msg` & `send_video_msg` (Slack)**: Cấu hình kết nối `slackOAuth2Api` để đẩy thông báo trạng thái ban đầu và gửi link tải các video đạt chuẩn vào kênh Slack chỉ định.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một link YouTube ngắn để kiểm tra luồng dữ liệu qua các node `split_videos`, `filter_viral_score`.
- Sau khi test thành công, gạt công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa toàn bộ phễu sáng tạo nội dung, các sếp có thể mở rộng workflow này bằng cách:
- **Tích hợp LLM (OpenAI/Claude):** Tự động viết caption, hashtag siêu cuốn hút dựa trên nội dung tóm tắt của từng đoạn clip.
- **Kết hợp Blotato hoặc Make/Buffer:** Tự động lên lịch đăng tải các video ngắn này lên TikTok, Instagram Reels và YouTube Shorts mà không cần can thiệp thủ công.
- **Lưu trữ dữ liệu:** Đẩy toàn bộ thông tin video, link tải và điểm số viral vào Google Sheets để làm báo cáo nội dung hàng tuần.

### 📌 Kết luận
Tự động hóa quy trình sản xuất video ngắn chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n và Vizard AI. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho đội ngũ sáng tạo nội dung của các sếp!