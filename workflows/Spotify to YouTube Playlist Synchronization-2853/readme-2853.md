---
title: "🎵 Tự động đồng bộ playlist Spotify sang YouTube - Giải pháp hoàn hảo cho các sếp quản lý âm nhạc"
description: "Hướng dẫn chi tiết cách tự động đồng bộ playlist Spotify sang YouTube bằng n8n. Tiết kiệm thời gian, đảm bảo độ chính xác và duy trì danh sách phát liên tục."
slug: "tu-dong-dong-bo-playlist-spotify-sang-youtube"
tags: [n8n, automation, no-code, Spotify, YouTube, Supabase]
keywords: [n8n workflow, tự động hóa, Spotify, YouTube, playlist, đồng bộ, no-code]
---

# 🎵 Tự động đồng bộ playlist Spotify sang YouTube - Giải pháp hoàn hảo cho các sếp quản lý âm nhạc

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải tốn thời gian quý giá để chuyển đổi thủ công danh sách phát từ Spotify sang YouTube? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách hoàn hảo, đảm bảo danh sách phát luôn đồng bộ và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc quản lý danh sách phát âm nhạc
- Đảm bảo độ chính xác cao trong việc đồng bộ giữa các nền tảng
- Tự động hóa toàn bộ quá trình đồng bộ mà không cần can thiệp thủ công
- Duy trì danh sách phát liên tục và cập nhật theo thời gian thực
- Tích hợp thông báo để theo dõi quá trình đồng bộ
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Spotify và YouTube với quyền truy cập đầy đủ
- API keys cho Spotify, YouTube và Supabase
- Bảng dữ liệu trong Supabase với cấu trúc sau:
```sql
CREATE TABLE IF NOT EXISTS musics (
    id TEXT PRIMARY KEY,
    title TEXT NOT NULL,
    artist TEXT NOT NULL,
    duration INT8 NOT NULL,
    youtube_video_id TEXT,
    to_delete BOOLEAN DEFAULT FALSE
);
```
- Danh sách phát YouTube trống (khuyến nghị để tránh trùng lặp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Get playlist snapshot** và **Get playlist snapshot1**: Cấu hình credentials cho Spotify và chọn playlist cần đồng bộ.
- **Get all musics**: Cấu hình credentials cho Supabase và chọn bảng dữ liệu chứa thông tin âm nhạc.
- **Search video**: Cấu hình credentials cho YouTube và chọn playlist đích.
- **Discord** và **Discord1**: Cấu hình thông báo qua Discord (tùy chọn).
- **variables, variables1, variables2, variables3, variables4**: Cấu hình các biến cần thiết cho workflow.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể tách các workflow thành các file riêng biệt để dễ dàng theo dõi và quản lý.
- Khuyến nghị chạy workflow hàng giờ để đảm bảo danh sách phát luôn đồng bộ.
- Sử dụng thông báo qua Discord hoặc các nền tảng khác để theo dõi quá trình đồng bộ.

### 📌 Kết luận
Workflow này cung cấp giải pháp hoàn hảo cho các sếp quản lý danh sách phát âm nhạc. Với khả năng tự động hóa toàn bộ quá trình đồng bộ, các sếp có thể tiết kiệm thời gian và đảm bảo độ chính xác cao. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!