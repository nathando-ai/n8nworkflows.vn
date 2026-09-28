---
title: "🎙️ Tự động tải podcast lên Spotify qua RSS & Google Drive"
description: "Hướng dẫn tự động hóa quy trình tải podcast lên Spotify bằng n8n, tiết kiệm thời gian và đảm bảo tính nhất quán của nội dung."
slug: "tu-dong-tai-podcast-len-spotify-qua-rss-google-drive"
tags: [n8n, automation, no-code, podcast, spotify]
keywords: [n8n workflow, tự động hóa podcast, spotify api, google drive, rss feed]
---

# 🎙️ Tự động tải podcast lên Spotify qua RSS & Google Drive

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình từ 30-60 phút xuống còn vài giây.
- Đảm bảo tính nhất quán: Loại bỏ lỗi do nhập liệu thủ công.
- Tăng hiệu quả: Tự động cập nhật RSS feed và tải lên Spotify ngay lập tức.
- Tích hợp liền mạch: Kết nối tự động giữa các dịch vụ (GitHub, Google Drive, Spotify).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập vào repository chứa file RSS.
- Tài khoản Google Drive với quyền tạo và chia sẻ file.
- API credentials cho Spotify (Client ID và Secret).
- File audio đã được tạo sẵn (có thể từ workflow trước đó).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn.
2. Nhấn vào menu "Workflow" > "Import from File".
3. Chọn file JSON của workflow này hoặc copy/paste nội dung JSON vào editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Get RSS File (GitHub Node)**
   - Cấu hình credentials cho GitHub API.
   - Điền thông tin:
     - Owner: Tên tài khoản GitHub của bạn.
     - Repository: Tên repository chứa file RSS.
     - File Path: Đường dẫn đến file RSS (ví dụ: `n8n/rss.xml`).

2. **Upload to Google Drive**
   - Cấu hình credentials cho Google Drive OAuth2.
   - Điền thông tin:
     - File Name: Sử dụng biểu thức `={{ $json.fileName }}`.
     - Folder ID: ID của thư mục trong Google Drive để lưu file podcast.

3. **Set Public URL (Google Drive)**
   - Đảm bảo file đã được upload thành công trước khi chạy node này.
   - Điền thông tin:
     - fileId: Sử dụng biểu thức `={{ $json.id }}`.

4. **Edit a File (GitHub Node)**
   - Cấu hình credentials cho GitHub API.
   - Điền thông tin:
     - Owner: Tên tài khoản GitHub của bạn.
     - Repository: Tên repository chứa file RSS.
     - File Path: Đường dẫn đến file RSS.
     - File Content: Sử dụng biểu thức `={{ $json.updatedRssXml }}`.
     - Commit Message: Ví dụ: `Update RSS feed with new episode`.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng.
- Bật Active workflow để tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log hoạt động của workflow để theo dõi lịch sử tải podcast.
- Tự động gửi báo cáo hàng tuần về số lượng podcast đã tải lên Spotify.
- Thêm bước xác thực nội dung trước khi tải lên Spotify để đảm bảo chất lượng.

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc quản lý và tải podcast lên Spotify. Bằng cách tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào nội dung sáng tạo hơn. Hãy thử áp dụng ngay để trải nghiệm hiệu quả của tự động hóa!