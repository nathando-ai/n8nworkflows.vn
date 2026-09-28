---
title: "🎵 Tự động đồng bộ bài hát yêu thích Spotify sang playlist - Workflow n8n hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động đồng bộ danh sách bài hát yêu thích Spotify sang playlist của bạn mỗi ngày, giúp quản lý nhạc dễ dàng hơn"
slug: "tu-dong-dong-bo-bai-hat-yeu-thich-spotify-sang-playlist"
tags: [n8n, automation, no-code, spotify, music]
keywords: [n8n workflow, tự động hóa, spotify, playlist, nhạc]
---

# 🎵 Tự động đồng bộ bài hát yêu thích Spotify sang playlist - Workflow n8n hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của người dùng Spotify khi phải thủ công quản lý danh sách bài hát yêu thích và playlist. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động đồng bộ danh sách bài hát yêu thích hàng ngày
- Tự động xóa các bài hát không còn trong danh sách yêu thích
- Tự động thêm các bài hát mới vào playlist
- Nhận thông báo về số lượng bài hát đã thêm/xóa
- Quản lý nhạc dễ dàng mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Spotify
- Playlist mục tiêu trên Spotify
- Credentials cho Spotify trong n8n
- (Tùy chọn) Tài khoản Gotify để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2634)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Spotify get Liked Songs"**:
   - Chọn credentials của tài khoản Spotify của bạn
   - Đảm bảo tài khoản này có quyền truy cập vào danh sách bài hát yêu thích

2. **Node "Spotify get all playlists"**:
   - Chọn credentials của tài khoản Spotify của bạn
   - Đảm bảo tài khoản này có quyền truy cập vào tất cả playlist

3. **Node "Filter Playlist x"**:
   - Thay đổi giá trị trong node này thành tên của playlist mục tiêu của bạn
   - Ví dụ: Nếu playlist của bạn tên là "My Favorite Songs", thay đổi giá trị thành "My Favorite Songs"

4. **Node "Spotify add Missing to x"**:
   - Thay đổi giá trị trong node này thành tên của playlist mục tiêu của bạn
   - Đảm bảo giá trị này khớp với giá trị trong node "Filter Playlist x"

5. **Node "Schedule Trigger"**:
   - Đặt lịch chạy workflow hàng ngày vào lúc 00:00 (hoặc thời gian bạn muốn)
   - Có thể điều chỉnh theo định dạng cron: `0 0 * * *`

6. **Node "Gotify Send deleted n from x"** (tùy chọn):
   - Nếu muốn nhận thông báo, cấu hình credentials Gotify
   - Đảm bảo Gotify server đang chạy và có thể nhận thông báo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kích hoạt workflow bằng cách nhấn nút "Active" trên thanh công cụ

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để nhận thông báo thay vì Gotify
- Thêm node lưu log để theo dõi lịch sử thay đổi
- Tạo báo cáo hàng tuần về các thay đổi trong playlist
- Kết hợp với workflow khác để tự động tạo playlist hàng ngày dựa trên các bài hát mới

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý danh sách bài hát yêu thích và playlist trên Spotify. Bằng cách tự động hóa quá trình này, các sếp có thể tập trung vào việc thưởng thức nhạc hơn là quản lý danh sách. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!