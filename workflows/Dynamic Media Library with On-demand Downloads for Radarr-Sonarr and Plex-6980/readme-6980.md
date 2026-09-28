---
title: "🚀 Quản lý Thư viện Media Thông minh: Tự động hóa Radarr, Sonarr và Plex với n8n"
description: "Xây dựng hệ thống Placeholdarr tự động tạo tệp giả (dummy files) cho Plex, đồng thời tự động tải xuống qua Radarr/Sonarr khi người dùng phát nội dung."
slug: "quan-ly-thu-vien-media-radarr-sonarr-plex-n8n"
tags: [n8n, automation, plex, radarr, sonarr, tautulli]
keywords: [n8n workflow, placeholdarr, plex automation, radarr sonarr n8n, tautulli webhook, quản lý media tự động]
---

# 🚀 Quản lý Thư viện Media Thông minh: Tự động hóa Radarr, Sonarr và Plex với n8n

Các sếp đang vận hành hệ thống Media Server (Plex, Radarr, Sonarr) chắc chắn đã từng gặp đau đầu về vấn đề dung lượng lưu trữ ổ cứng, hoặc muốn hiển thị một thư viện phim/show khổng lồ (như toàn bộ danh sách từ JustWatch hoặc Trakt) mà không muốn tốn băng thông và dung lượng tải về khi chưa ai xem. 

Workflow n8n "Dynamic Media Library with On-demand Downloads for Radarr-Sonarr and Plex" (hay còn gọi là **Placeholdarr**) chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán này. Hệ thống sẽ tự động tạo các tệp giả (dummy files) siêu nhẹ cho Plex. Khi có người bấm xem tệp giả đó, n8n sẽ tự động ra lệnh cho Radarr/Sonarr tải nội dung thật về ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm dung lượng lưu trữ tối đa:** Chỉ tải phim/show về khi thực sự có nhu cầu xem (On-demand Download).
- **Thư viện Plex luôn phong phú:** Đồng bộ tự động các danh sách từ Trakt.tv hoặc JustWatch.com thành các Collection trực quan trên Plex mà không tốn dung lượng ổ cứng.
- **Tự động hóa hoàn toàn:** Từ việc tạo file giả qua SSH, cập nhật metadata, cho đến việc tự động monitor và queue download khi người dùng bấm phát.
- **Trải nghiệm mượt mà:** Tích hợp Tautulli để xử lý ngắt luồng thông minh hoặc thông báo trạng thái.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị:
- Một server chạy **n8n** (đã cấu hình SSH credentials để tạo file giả).
- Hệ thống **Plex Media Server**, **Radarr**, **Sonarr**, và **Tautulli** đang hoạt động.
- Tài khoản/API Key từ **Trakt.tv** (nếu muốn dùng tính năng đồng bộ danh sách Trakt).
- Máy chủ lưu trữ file giả cần đã cài đặt sẵn **FFmpeg** (hoặc cấu hình copy file dummy thủ công).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp) để đưa 81 nodes vào hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì đây là một workflow kết hợp hệ thống homelab phức tạp, các sếp cần chú ý cấu hình kỹ các node sau:

- **Cấu hình SSH Nodes** (`Create dummy file`, `Create dummy file for movie`, `Remove all dummy files`,...): Điền chính xác thông tin kết nối SSH (`sshPassword` credentials) tới thư mục chứa media để hệ thống có quyền tạo file giả (`.mp4/.mkv` dung lượng 0kb hoặc có thời lượng ngắn bằng FFmpeg).
- **Cấu hình HTTP Request Nodes** (Radarr, Sonarr, Plex, Overseerr): Đảm bảo các node gọi API (như `Radarr movie`, `Sonarr series`, `Get Radarr information from tmdbId`,...) được gán đúng API Key / Header Auth và URL endpoint trỏ đến các service của sếp.
- **Webhook Nodes** (`Webhook Arrs custom list JustWatch`, `Webhook Arrs custom list Trakt`, `Webhook Tautulli`, `Webhook Arrs Dummy file update`): 
  - Lấy URL webhook do n8n sinh ra và điền vào phần **Notification Triggers** trong Radarr/Sonarr (Sự kiện: *On File Import, On File Update, On Movie Added* với Tag là `dummy-unprocessed`).
  - Điền URL Webhook vào **Tautulli Notification Agent** (Sự kiện: *Playback Start*, điều kiện: *Filename contains dummy*).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một vài bản ghi mẫu từ Trakt hoặc JustWatch để kiểm tra kết nối API.
- Sau khi mọi thứ trả về mã `200 OK` xanh mướt, hãy gạt công tắc **Active** để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm node gửi tin nhắn mỗi khi có một "dummy file" được kích hoạt tải xuống, giúp các sếp nắm bắt nội dung nào đang được gia đình/bạn bè quan tâm trên Plex.
- **Tự động dọn dẹp:** Kết hợp thêm lịch trình (Schedule Trigger) để quét và xóa các file dummy cũ không còn sử dụng hoặc đã được thay thế bằng file thật hoàn chỉnh.
- **Mở rộng nguồn List:** Ngoài Trakt và JustWatch, các sếp có thể tùy biến thêm các nguồn danh sách cá nhân qua file JSON hoặc Google Sheets.

### 📌 Kết luận
Workflow "Dynamic Media Library with On-demand Downloads" là một kiệt tác tự động hóa dành riêng cho các tín đồ Self-hosted Media Server. Hãy thiết lập ngay hôm nay để biến chiếc Plex ở nhà thành một dịch vụ streaming chuyên nghiệp, tiết kiệm và thông minh hơn bao giờ hết!