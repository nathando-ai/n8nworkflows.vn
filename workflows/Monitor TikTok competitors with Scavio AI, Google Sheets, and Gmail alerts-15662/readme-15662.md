---
title: "🚀 Giám sát đối thủ cạnh tranh trên TikTok tự động với Scavio AI, Google Sheets và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng mới nhất của đối thủ trên TikTok mỗi 6 giờ, ghi nhận vào Google Sheets và gửi cảnh báo qua Gmail."
slug: "giam-sat-doi-thu-tiktok-tu-dong-n8n-scavio"
tags: [n8n, automation, tiktok, market-research, google-sheets, gmail, scavio-ai]
keywords: [n8n workflow, tự động hóa tiktok, giám sát đối thủ cạnh tranh, scavio api, google sheets automation]
---

# 🚀 Giám sát đối thủ cạnh tranh trên TikTok tự động với Scavio AI, Google Sheets và Gmail

Các sếp có đang tốn hàng giờ mỗi ngày để "soi" trang cá nhân của đối thủ trên TikTok xem họ ra video gì, nội dung ra sao, tương tác thế nào không? Việc làm thủ công này cực kỳ mất thời gian và rất dễ bỏ sót các xu hướng mới.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa 100%. Hệ thống sẽ tự động quét các tài khoản TikTok đối thủ định kỳ mỗi 6 giờ, so sánh video mới, lưu trữ toàn bộ số liệu vào Google Sheets và gửi email thông báo ngay lập tức qua Gmail khi có video mới xuất hiện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Không cần canh chừng, hệ thống tự động kiểm tra đối thủ mỗi 6 giờ.
- **Cảnh báo tức thì:** Nhận email qua Gmail ngay khi đối thủ vừa đăng video mới kèm theo số liệu view, like, comment, share và link trực tiếp.
- **Dữ liệu tập trung:** Tự động lưu toàn bộ lịch sử bài đăng vào Google Sheets giúp dễ dàng phân tích và làm báo cáo.
- **Tiết kiệm nguồn lực:** Thay vì tốn nhân sự lướt TikTok thủ công, thời gian đó có thể dành cho việc lên chiến lược nội dung đột phá.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Scavio Community Node & API Key:** Cần cài đặt node cộng đồng `n8n-nodes-scavio` và lấy API key miễn phí tại [scavio.dev](https://dashboard.scavio.dev) (miễn phí 250-500 credits/tháng).
- **Google Sheets:** Tài khoản Google để đọc/ghi dữ liệu danh sách đối thủ và log bài đăng.
- **Gmail Account:** Tài khoản Gmail để nhận thông báo cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes được sắp xếp thông minh. Các sếp cần chú ý cấu hình kỹ các phần sau:

- **Cài đặt Scavio Node:** 
  - Vào `Settings` -> `Community Nodes` -> Tìm và cài đặt gói `n8n-nodes-scavio`.
  - Tạo `Scavio API` credentials bằng cách dán API key lấy từ trang quản trị Scavio.
- **Cấu hình Google Sheets:**
  - Chuẩn bị sẵn một Google Sheet có 2 tab chính:
    1. Tab **Competitors**: Các cột gồm `username`, `sec_user_id` (để trống), `last_video_id` (để trống). Điền sẵn các username TikTok của đối thủ vào đây.
    2. Tab **Posts**: Các cột gồm `username`, `description`, `views`, `likes`, `comments`, `shares`, `link`, `detected_at`.
  - Kết nối tài khoản Google Sheets OAuth2 cho các node: **Read competitors**, **Log posts**, và **Save state**.
- **Cấu hình Gmail:**
  - Kết nối tài khoản Gmail OAuth2 cho node **Alert new posts**.
  - Mở node **Alert new posts** và điền địa chỉ email nhận thông báo của các sếp vào trường `sendTo`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) để kiểm tra xem hệ thống có đọc được dữ liệu từ Google Sheets và gọi API Scavio thành công hay không.
- Sau khi kiểm tra mọi thứ chạy mượt mà, hãy gạt công tắc **Active** để workflow tự động chạy ngầm theo lịch trình từ node **Every 6 Hours**.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ nhận qua Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để team cùng theo dõi sát sao hoạt động của đối thủ.
- **Lần chạy đầu tiên:** Trong lần chạy đầu tiên, hệ thống sẽ tiến hành khởi tạo (seed) giá trị `last_video_id` mà chưa gửi cảnh báo ngay để tránh làm phiền. Các cảnh báo sẽ hoạt động chính thức từ lần chạy thứ hai trở đi.
- **Tối ưu chi phí API:** Với tần suất 6 tiếng/lần cho vài đối thủ, lượng credit miễn phí từ Scavio hoàn toàn đáp ứng đủ nhu cầu nghiên cứu thị trường cơ bản.

### 📌 Kết luận
Việc nắm bắt nhanh nội dung của đối thủ trên TikTok chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, Scavio AI và Google Sheets. Hãy áp dụng ngay workflow này để nâng cao lợi thế cạnh tranh cho thương hiệu của các sếp!