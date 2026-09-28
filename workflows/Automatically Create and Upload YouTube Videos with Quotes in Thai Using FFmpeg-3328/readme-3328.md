---
title: "🎬 Tự Động Hoàn Chỉnh & Đăng Video YouTube Có Chữ Ký (Thái Ngữ) Với FFmpeg - N8n Workflow"
description: "Workflow tự động hóa 100% không code để tạo và đăng video YouTube có chữ ký Thái ngữ từ dữ liệu Google Sheets và Google Drive. Giúp tiết kiệm thời gian lên tới 90% so với thủ công."
slug: "tu-dong-hoan-chinh-dang-video-youTube-co-chu-ky-thai-ngu"
tags: [n8n, automation, youtube, google-drive, google-sheets, ffmpeg, no-code]
keywords: [tự động hóa video YouTube, workflow n8n, tự động tạo video có chữ ký, ffmpeg tự động hóa, google sheets youtube, tự động hóa nội dung video]
---

# 🚀 **Tự Động Hoàn Chỉnh & Đăng Video YouTube Có Chữ Ký Thái Ngữ Với FFmpeg**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp thường phải **tốn thời gian dài** để:
- **Tìm kiếm và chọn** video nền, nhạc nền và chữ ký Thái ngữ phù hợp từ hàng trăm tài liệu trên Google Drive.
- **Chỉnh sửa video** bằng FFmpeg để chèn chữ ký, âm thanh và hiệu ứng.
- **Đăng video lên YouTube** thủ công, mất thời gian kiểm tra và cập nhật trạng thái.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy dữ liệu** từ Google Sheets (video nền, nhạc nền, chữ ký Thái ngữ).
✅ **Chọn ngẫu nhiên** một video, nhạc và chữ ký.
✅ **Tải xuống và xử lý** bằng FFmpeg.
✅ **Đăng video lên YouTube** và cập nhật trạng thái tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 90%** so với thủ công.
- **Chất lượng video đồng nhất** do tự động hóa FFmpeg.
- **Cập nhật trạng thái tự động** trên Google Sheets.
- **Hoạt động 24/7** mà không cần can thiệp.
- **Dễ dàng mở rộng** với nhiều chủ đề, ngôn ngữ khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (để kết nối Google Sheets & Google Drive).
✔ **API Key YouTube** (để đăng video).
✔ **Google Sheets** với 3 bảng dữ liệu:
   - **Video Background Data** (danh sách video nền).
   - **Music Background Data** (danh sách nhạc nền).
   - **Quote Data** (chữ ký Thái ngữ + tác giả).
✔ **Google Drive** chứa các file video, nhạc nền.
✔ **FFmpeg** cài đặt trên máy chủ n8n (hoặc VPS).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3328](https://n8n.io/workflows/3328).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
- **Hoặc copy/paste** JSON vào Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **3 phần chính**, các sếp cần chú ý:

##### **📌 Phần 1: Lấy Dữ Liệu & Chọn Ngẫu Nhiên**
- **Nodes quan trọng:**
  - **"Retrieve Video Background Data"** → Điền **ID Sheet** và **Sheet Name** (ví dụ: `VideoBackgrounds`).
  - **"Retrieve Quote Data"** → Điền **ID Sheet** và **Sheet Name** (ví dụ: `Quotes`).
  - **"List Video Background Files"** → Chọn **Folder ID** trong Google Drive.
  - **"List Music Background Files"** → Chọn **Folder ID** khác (nếu nhạc nền ở folder riêng).
  - **"Select Random Video, Music & Quote"** → Node **Code** này sẽ chọn ngẫu nhiên. **Không cần chỉnh**, chỉ cần đảm bảo dữ liệu đầu vào đầy đủ.

##### **📌 Phần 2: Tải File & Xử Lý Video**
- **Nodes quan trọng:**
  - **"Download Selected Video Background"** → **Không cần chỉnh**, tự động lấy từ Google Drive.
  - **"Prepare Overlay Text (Quote & Author)"** → Node **Code** này **không cần chỉnh**, nhưng các sếp nên kiểm tra **format chữ ký** trong Google Sheets.
  - **"Generate Final Video Clip"** → **Node `executeCommand`** này sử dụng FFmpeg. Các sếp cần **cài FFmpeg** trên VPS và **không cần chỉnh** (nếu sử dụng cấu hình mặc định).

##### **📌 Phần 3: Đăng Video & Cập Nhật Trạng Thái**
- **Nodes quan trọng:**
  - **"Initiate YouTube Resumable Upload"** → Điền **OAuth2 API Key YouTube**.
  - **"Upload Video to YouTube"** → **Không cần chỉnh**, tự động upload sau khi FFmpeg hoàn thành.
  - **"Update Quote Upload Status"** → Cập nhật trạng thái trên Google Sheets (ví dụ: `Đã đăng`).
  - **"Mark Background as Used"** → Đánh dấu video/music nền đã được sử dụng.

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chọn **"Run Workflow"** và kiểm tra **log** để đảm bảo không lỗi.
- **Bật Active:** Sau khi test thành công, **bật `Active`** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Thêm Slack/Telegram Notification:** Sau khi đăng video thành công, gửi thông báo tự động.
- **Lưu Log Chi Tiết:** Sử dụng **Google Sheets** hoặc **Google Drive** để lưu lịch sử upload.
- **Tự Động Xóa File Tạm:** Sau khi upload, xóa file tạm trên VPS để tiết kiệm dung lượng.
- **Chuyển Động Video:** Sử dụng **YouTube API** để tự động chuyển động video sang định dạng khác (nếu cần).
- **Tự Động Chia Sẻ:** Sau khi đăng, tự động chia sẻ video lên **Facebook/Instagram** bằng API.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **nội dung chất lượng** thay vì công việc thủ công. **Chỉ cần setup 1 lần**, workflow sẽ **hoạt động tự động** mỗi khi kích hoạt.

**🚀 Hãy áp dụng ngay và tự động hóa video YouTube của mình!**
Nếu có vấn đề, **hãy liên hệ với tác giả [Jaruphat J.](https://n8n.io/workflows/3328)** để hỗ trợ.

---
**#TựĐộngHóa #N8n #YouTubeAutomation #FFmpeg #GoogleSheets**