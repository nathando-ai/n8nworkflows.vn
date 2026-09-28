---
title: "🎬 Tự động hóa Dubbing Video YouTube với ElevenLabs & Google Drive"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình dubbing video YouTube bằng AI của ElevenLabs, lưu trữ trên Google Drive và đăng tải lên YouTube. Tiết kiệm thời gian và nâng cao hiệu quả sản xuất nội dung."
slug: "tu-dong-hoa-dubbing-video-youtube-voi-elevenlabs-google-drive"
tags: [n8n, automation, no-code, youtube, google-drive, elevenlabs, ai]
keywords: [n8n workflow, tự động hóa nội dung, dubbing video, elevenlabs, google drive, youtube]
---

# 🎬 Tự động hóa Dubbing Video YouTube với ElevenLabs & Google Drive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý video từ 70% đến 90%
- Tự động hóa quy trình dubbing video bằng AI của ElevenLabs
- Lưu trữ an toàn video trên Google Drive
- Đăng tải tự động lên YouTube với metadata hoàn chỉnh
- Xử lý hàng loạt video một cách hiệu quả
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản ElevenLabs API Key
- Tài khoản Google Drive với quyền truy cập đầy đủ
- Tài khoản Postiz API (tùy chọn)
- Tài khoản Upload-Post.com API (tùy chọn)
- URL video nguồn và mã ngôn ngữ mục tiêu (ví dụ: en, es, it)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12723](https://n8n.io/workflows/12723)
2. Nhấn nút "Import" để thêm workflow vào n8n của bạn
3. Hoặc copy JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Set params** (n8n-nodes-base.set):
   - Cấu hình tham số đầu vào:
     - `video_url`: URL trực tiếp đến video nguồn
     - `target_audio`: Mã ngôn ngữ mục tiêu (ví dụ: `en`, `es`, `it`)

2. **Elevenlabs Dubbing** (n8n-nodes-base.httpRequest):
   - Đảm bảo đã cấu hình credentials ElevenLabs API
   - Kiểm tra các tham số đầu vào như video URL và ngôn ngữ mục tiêu

3. **Upload file** (n8n-nodes-base.googleDrive):
   - Cấu hình Google Drive OAuth2 credentials
   - Chọn thư mục lưu trữ trên Google Drive

4. **Youtube Upload-Post** (n8n-nodes-base.httpRequest):
   - Cấu hình HTTP Header Auth credentials
   - Điền đầy đủ thông tin metadata cho video (tiêu đề, mô tả, tags...)

5. **Youtube Postiz** (n8n-nodes-postiz.postiz):
   - Cấu hình Postiz API credentials
   - Kiểm tra lịch đăng tải và các thiết lập khác

#### 3. Kích hoạt ⚡️
1. Kiểm tra kết nối với tất cả các dịch vụ bên ngoài
2. Chạy test với video mẫu để đảm bảo quy trình hoạt động đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi quy trình hoàn thành
- Lưu log hoạt động vào Google Sheets để theo dõi hiệu suất
- Tự động gửi báo cáo hàng tuần về số lượng video đã xử lý
- Thêm node để kiểm tra chất lượng video sau khi dubbing
- Tích hợp với các nền tảng quản lý nội dung khác như Vimeo

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa quy trình dubbing video YouTube, giúp tiết kiệm thời gian và nâng cao hiệu quả sản xuất nội dung. Với khả năng xử lý hàng loạt và tích hợp với các dịch vụ lưu trữ và đăng tải phổ biến, đây là công cụ lý tưởng cho các nhà sáng tạo nội dung, cơ quan truyền thông và các doanh nghiệp cần quản lý khối lượng lớn video.