---
title: "🚀 Tự động hóa đồng bộ bài hát yêu thích trên Spotify với n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để tự động tạo và cập nhật danh sách bài hát yêu thích gần đây trên Spotify vào playlist 'Downloads'."
slug: "tu-dong-hoa-bai-hat-yeu-thich-spotify"
tags: [n8n, automation, no-code, spotify, music, workflow]
keywords: [n8n workflow, tự động hóa spotify, download nhạc spotify, n8n spotify oauth2, quan ly playlist spotify]
---

# 🚀 Tự động hóa đồng bộ bài hát yêu thích trên Spotify với n8n

Các sếp có bao giờ cảm thấy phiền phức khi mỗi lần thích một bài hát mới trên Spotify, thiết bị di động lại tải toàn bộ thư viện nhạc khổng lồ, làm đầy bộ nhớ một cách nhanh chóng? Việc chọn lọc thủ công từng bài hát để tải xuống ngoại tuyến tốn rất nhiều thời gian.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% việc quản lý một playlist riêng biệt mang tên **"Downloads"** trên Spotify của các sếp. Nó sẽ tự động cập nhật các bài hát mới nhất mà các sếp vừa bấm "Thích" (Like) và tự động xóa các bài cũ vượt quá giới hạn cho phép. Nhờ đó, các sếp chỉ cần cài đặt chế độ tải tự động (offline download) cho riêng playlist "Downloads" này để tiết kiệm tối đa dung lượng bộ nhớ thiết bị!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm bộ nhớ:** Chỉ tải xuống giới hạn số lượng bài hát yêu thích gần nhất (mặc định tối đa 50 bài), giải phóng dung lượng điện thoại/máy tính.
- **Tự động hoàn toàn:** Hoạt động ngầm theo lịch trình định sẵn mà không cần can thiệp thủ công.
- **Đồng bộ thông minh:** Tự động thêm bài mới và dọn dẹp các bài hát cũ vượt ngưỡng giới hạn khỏi playlist "Downloads".
- **Trải nghiệm mượt mà:** Thích bài nào trên Spotify là tự động sẵn sàng nghe offline trên thiết bị đó.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Spotify cá nhân và quyền truy cập **Spotify Developer Dashboard** để tạo một ứng dụng (App) lấy `Client ID` và `Client Secret` cấu hình xác thực OAuth2.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở giao diện n8n Editor, nhấn vào nút **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp mã JSON vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node quan trọng sau đây để workflow chạy mượt mà:

- **Spotify Credentials (`spotifyOAuth2Api`):** Áp dụng cho các node như `Get Liked Tracks`, `Get all Playlists`, `Create Downloads Playlist`, `Add tracks to Downloads`, `Remove oldest tracks from Downloads`, v.v. Các sếp cần kết nối tài khoản Spotify của mình thông qua xác thực OAuth2. *(Lưu ý: Ứng dụng Spotify Developer mới tạo có thể mất vài phút để hoạt động ổn định).*
- **Globals (`Globals` - Set Node):** Node này dùng để định nghĩa biến `download_limit` (giới hạn số lượng bài hát muốn giữ lại trong playlist Downloads). Thiết lập hiện tại hỗ trợ tối đa 50 bài. Các sếp có thể thay đổi con số này tùy theo nhu cầu bộ nhớ.
- **Schedule Trigger (`Schedule Trigger`):** Node quyết định tần suất chạy workflow. Mặc định playlist sẽ được cập nhật tự động 1 lần mỗi ngày. Các sếp có thể tùy chỉnh lại thời gian chạy theo ý thích.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm lần đầu và kiểm tra xem hệ thống đã tạo playlist "Downloads" cũng như đồng bộ các bài hát thành công chưa.
- Sau khi test không có lỗi, bật công tắc **Active** ở góc trên bên phải để n8n tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo Telegram/Slack:** Kết hợp thêm node Telegram hoặc Slack vào sau quá trình thêm bài hát để nhận thông báo mỗi khi có bài hát mới được tự động thêm vào playlist "Downloads".
- **Mở rộng giới hạn:** Nếu bộ nhớ thiết bị thoải mái, các sếp có thể tăng thông số `download_limit` trong node `Globals` lên 100 hoặc 200 bài.
- **Lưu lịch sử:** Thêm một node Google Sheets để ghi lại danh sách các bài hát đã từng được tải xuống nhằm phân tích thói quen nghe nhạc theo thời gian.

### 📌 Kết luận
Workflow tự động hóa đồng bộ bài hát yêu thích trên Spotify là một "món quà" tuyệt vời cho các tín đồ âm nhạc muốn tối ưu hóa dung lượng thiết bị mà vẫn giữ nguyên trải nghiệm nghe nhạc không giới hạn. Hãy triển khai ngay để tận hưởng sự tiện lợi này các sếp nhé!