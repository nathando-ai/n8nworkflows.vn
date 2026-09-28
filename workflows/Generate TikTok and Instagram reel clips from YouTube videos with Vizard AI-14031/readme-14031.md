---
title: "🚀 Tự động biến video YouTube thành Reels & TikTok ngắn vạn view với Vizard AI và n8n"
description: "Biến video YouTube dài thành hàng loạt short clip xu hướng cho TikTok và Instagram Reels tự động 100% nhờ Vizard AI và n8n, tiết kiệm 90% thời gian biên tập."
slug: "tu-dong-tao-tiktok-instagram-reel-tu-youtube-vizard-ai"
tags: [n8n, automation, vizard-ai, content-creation, youtube, tiktok, instagram-reels]
keywords: [n8n workflow, vizard ai, tao clip tiktok tu youtube, tu dong hoa video, ai clipper]
---

# 🚀 Tự động biến video YouTube thành Reels & TikTok ngắn vạn view với Vizard AI

Các sếp có kênh TikTok, Instagram Reels hay YouTube Shorts chắc chắn hiểu cảm giác "ngợp" khi phải ngồi hàng giờ lướt qua một video YouTube dài để cắt ra những đoạn hay nhất, chèn phụ đề và đăng tải. Công việc thủ công này cực kỳ tốn thời gian mà đôi khi hiệu quả lại không như ý.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, kết hợp sức mạnh của **Vizard AI**. Hệ thống sẽ tự động nhận link YouTube, phân tích các khoảnh khắc "viral", chấm điểm, lọc nội dung chất lượng cao và tự động tải về hoặc đăng ngay lên mạng xã hội. Hoàn toàn tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tua video, cắt ghép thủ công từng đoạn ngắn.
- **Bắt trọn xu hướng:** Vizard AI tự động tìm ra những khoảnh khắc đắt giá, có tiềm năng viral cao nhất từ video gốc.
- **Lọc thông minh:** Tự động chỉ chọn những clip đạt ngưỡng điểm viral (Viral Score) do các sếp thiết lập.
- **Linh hoạt đầu ra:** Tùy chọn tải video về để kiểm duyệt trước hoặc tự động lên lịch/đăng ngay lên TikTok và Instagram Reels.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Vizard AI Account:** Tài khoản Vizard.ai để lấy API Key chuyên dụng cho việc cắt video bằng AI.
- **Tài khoản mạng xã hội:** Đã kết nối TikTok/Instagram với bảng điều khiển của Vizard AI (nếu dùng tính năng auto-publish).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua menu `Import from File`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Configuration` (Set):** 
  - Thay thế `[ENTER_YOUR_API_KEY_HERE]` bằng **Vizard API Key** thực tế của các sếp.
  - Cài đặt `viral_score_threshold` (mặc định là `5`, thang điểm từ `0-10`).
  - Chọn `export_mode`: `download` (để tải về review) hoặc `auto_publish` (đăng tự động).
  - Tùy chọn `schedule_time` dưới dạng Unix timestamp nếu muốn hẹn giờ đăng.
- **Node `form_trigger`:** Cung cấp giao diện form đơn giản để các sếp nhập link YouTube trực tiếp.
- **Node `AI Clipper`, `Get Status`, `Download`, `Scheduled Publish`, `Instant Post` (HTTP Request):** Đảm bảo đã liên kết đúng credentials hoặc header truyền API từ node `Configuration`.
- **Node `ViralSocre Filter` (Code):** Xử lý logic lọc các clip vượt qua điểm chuẩn viral mà các sếp đã đặt ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một form submission với một link YouTube bất kỳ để kiểm tra quá trình AI xử lý.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tăng độ chất lượng clip:** Điều chỉnh `viral_score_threshold` lên `7` hoặc `8` nếu các sếp chỉ muốn lấy những khoảnh khắc cực kỳ xuất sắc.
- **Tùy chỉnh thời lượng:** Thay đổi tham số `preferLength` trong node `AI Clipper` để tạo ra các clip ngắn dài/ngắn tùy theo sở thích (ví dụ: dưới 30s hoặc từ 30-60s).
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào sau bước xuất bản hoặc tải xuống để nhận thông báo ngay khi video ngắn đã được tạo xong.

### 📌 Kết luận
Việc sản xuất nội dung video ngắn chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy tích hợp ngay workflow này vào quy trình sáng tạo nội dung của doanh nghiệp hoặc kênh cá nhân để bùng nổ traffic ngay hôm nay!