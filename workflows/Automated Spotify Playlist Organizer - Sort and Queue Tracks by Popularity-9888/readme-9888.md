---
title: "🚀 Tự động sắp xếp playlist Spotify theo độ phổ biến"
description: "Giải pháp tự động hoá 100% không cần code để sắp xếp và đặt hàng các bài hát trong playlist Spotify dựa trên độ phổ biến."
slug: "automated-spotify-playlist-organizer"
tags: [n8n, automation, no-code, spotify, playlist]
keywords: [n8n workflow, tự động hóa, Spotify playlist, sắp xếp bài hát, queue Spotify]
---

# 🚀 Tự động sắp xếp playlist Spotify theo độ phổ biến

Bạn đang phải lướt qua hàng trăm bài hát trong playlist Spotify, tìm kiếm những ca khúc hot nhất để nghe trong lúc làm việc hay thư giãn? Việc này không chỉ tốn thời gian mà còn dễ dẫn đến lỗi khi chọn nhầm track. Workflow **Automated Spotify Playlist Organizer** giúp bạn:

- Lấy toàn bộ playlist của mình một lần duy nhất.
- Loại bỏ các bản sao và dọn dẹp dữ liệu.
- Sắp xếp các bài hát theo độ phổ biến (popularity) ngay trong playlist.
- Thêm tự động các track vào queue để bạn có thể nghe ngay mà không cần thao tác thủ công.

> **Tác giả**: Arthur Dimeglio (Former data engineer, now full-time automation creator)

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần lướt qua từng track, workflow tự động xử lý hết.
- **Độ chính xác cao**: Dữ liệu được dọn dẹp, loại bỏ bản sao, tránh lỗi khi thêm vào queue.
- **Cá nhân hóa**: Bạn có thể tùy chỉnh tiêu chí sắp xếp (popularity, date, custom).
- **Hoạt động liên tục**: Khi playlist được cập nhật, chỉ cần chạy lại workflow, queue luôn được cập nhật.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Tài khoản Spotify**: Đã đăng ký và có quyền truy cập API.
- **Spotify Developer Account**: Tạo ứng dụng để lấy `Client ID` và `Client Secret`.
- **Redirect URI**: Đặt `https://your-n8n-domain.com/rest/oauth2-credential/callback` (hoặc `http://localhost:5678/rest/oauth2-credential/callback` khi chạy local).
- **n8n**: Cài đặt phiên bản mới nhất (>= v1.0).  
- **Credentials**: Tạo credential `Spotify OAuth2` trong n8n, nhập `Client ID`, `Client Secret`, và chọn scope `playlist-read-private playlist-modify-public playlist-modify-private user-read-private user-read-email`.

:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥

1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/9888) hoặc sao chép nội dung JSON.
2. Mở n8n Editor → **Import** → **JSON** → dán nội dung hoặc tải file.
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

| Node | Mô tả | Tham số cần cấu hình |
|------|-------|----------------------|
| **When clicking ‘Execute workflow’** | Trigger thủ công | Không cần cấu hình |
| **Get a user's playlists** | Lấy danh sách playlist | Chọn credential Spotify |
| **Get a playlist's tracks by URI or ID** | Lấy track của playlist | Chọn credential Spotify |
| **Loop Over Items (splitInBatches)** | Xử lý từng playlist một | `Batch size` (đặt 1 để tránh rate limit) |
| **Clean & Deduplicate** | Dọn dẹp dữ liệu | Đảm bảo code JS trả về `items` dạng array |
| **Playlist reorganizer** | Sắp xếp theo popularity | Đảm bảo code JS trả về `sortedTracks` |
| **Add a song to a queue** | Thêm track vào queue | Chọn credential Spotify, `Track ID` từ output của node trước |

> **Lưu ý**: Các node `code` sử dụng JavaScript. Nếu bạn muốn thay đổi tiêu chí sắp xếp, hãy chỉnh sửa phần `sortedTracks = items.sort((a, b) => b.popularity - a.popularity);` trong node **Playlist reorganizer**.

### 3. Kích hoạt ⚡️

1. **Test run**: Nhấn **Execute Workflow** → chọn một playlist mẫu → kiểm tra log để chắc chắn dữ liệu được xử lý đúng.
2. **Bật Active**: Sau khi test thành công, bật toggle **Active** để workflow chạy khi trigger được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao

- **Thêm Slack/Telegram notification**: Thêm node `Slack` hoặc `Telegram` sau node **Add a song to a queue** để nhận thông báo khi queue được cập nhật.
- **Lưu log vào Google Sheet**: Dùng node `Google Sheets` để ghi lại danh sách track đã được queue, giúp theo dõi lịch sử.
- **Lên lịch tự động**: Thay vì trigger thủ công, sử dụng node `Cron` để chạy workflow hàng ngày/tuần.
- **Tùy chỉnh tiêu chí sắp xếp**: Thay `popularity` bằng `added_at` hoặc `duration_ms` để sắp xếp theo ngày thêm hoặc độ dài.

## 📌 Kết luận

Workflow **Automated Spotify Playlist Organizer** là công cụ tuyệt vời giúp các sếp tiết kiệm thời gian, giảm lỗi và luôn có playlist được sắp xếp theo độ phổ biến. Hãy thử ngay, điều chỉnh theo nhu cầu và tận hưởng nhạc mà không cần thao tác thủ công!