---
title: "🎬 **Tự Động Hóa Tạo YouTube Shorts Siêu Nhanh với yt-dlp & FFmpeg (Không Cần Code!)**"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tải xuống video/music từ Google Sheets, xử lý bằng AI, tạo Shorts 10s và upload lên YouTube 24/7. Giảm thời gian tạo nội dung xuống còn 0 giây!"
slug: "tay-dong-hoa-tao-youtube-shorts-yt-dlp-ffmpeg"
tags: [n8n, automation, content-creation, youtube-shorts, yt-dlp, ffmpeg, google-sheets]
keywords: [tự động hóa youtube shorts, n8n workflow youtube, tải video youtube tự động, tạo shorts từ video, ffmpeg n8n, tự động hóa nội dung video]
---

# 🚀 **Tự Động Hóa Tạo YouTube Shorts Siêu Nhanh với yt-dlp & FFmpeg**

## **🔥 Nỗi Đau Của Các Sếp Khi Tạo YouTube Shorts**
- **Tốn thời gian**: Tải video, cắt clip, thêm nhạc, upload lên YouTube thủ công mất hàng giờ mỗi ngày.
- **Không đồng bộ**: Quên theo dõi tiến độ, dẫn đến nội dung không liên tục.
- **Chất lượng thấp**: Video không được tối ưu hóa, thiếu hiệu ứng hoặc text overlay.
- **Khó quản lý**: Không biết liệu video đã được upload thành công hay không.

**Workflow này giải quyết tất cả!** Với **2 pipeline tự động hóa hoàn chỉnh**, các sếp chỉ cần cung cấp danh sách video/music trên Google Sheets, hệ thống sẽ:
✅ **Tải video/music** từ YouTube (chất lượng cao).
✅ **Xử lý bằng FFmpeg** (cắt, thêm nhạc, text overlay).
✅ **Tạo Shorts 10s** tự động.
✅ **Upload lên YouTube** và cập nhật trạng thái trên Google Sheets.
✅ **Xóa file tạm** để tiết kiệm không gian.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tốc độ và tính bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày**: Không cần cắt video, thêm nhạc hay upload thủ công.
- **Nội dung liên tục**: Tạo Shorts định kỳ (ví dụ: hàng ngày) mà không cần can thiệp.
- **Chất lượng chuyên nghiệp**: Video được cắt, thêm text overlay và nhạc tự động.
- **Quản lý dễ dàng**: Tất cả trạng thái được ghi lại trên Google Sheets.
- **Không giới hạn**: Hoạt động 24/7, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách video/music và kết quả).
2. **API Key YouTube** (để upload video):
   - Tạo tại [Google Cloud Console](https://console.cloud.google.com/).
   - Chọn **YouTube Data API v3** và **YouTube Upload API**.
   - Cấp quyền cho ứng dụng n8n.
3. **Cài đặt yt-dlp và FFmpeg** trên VPS:
   ```bash
   sudo apt update && sudo apt install yt-dlp ffmpeg -y
   ```
4. **Thư mục lưu tạm** trên VPS (ví dụ: `/tmp/youtube-shorts`).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7036).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1: Tải video/music** (chạy khi kích hoạt thủ công hoặc theo lịch).
- **Phần 2: Xử lý và upload Shorts** (chạy tự động theo lịch).

##### **A. Cấu Hình Google Sheets**
1. **Tạo 3 Sheet** trong Google Sheets (tên tùy ý):
   - **`videos`**: Danh sách video YouTube (cột: `url`, `title`, `status`).
   - **`music`**: Danh sách nhạc (cột: `url`, `title`, `status`).
   - **`quotes`**: Danh sách text overlay (cột: `text`, `font_color`).
2. **Cấp quyền OAuth2** cho n8n:
   - Trong n8n Dashboard → **Credentials** → **Add Google Sheets OAuth2**.
   - Theo hướng dẫn để kết nối với Google Sheets.

##### **B. Cấu Hình YouTube API**
1. **Tạo OAuth2 Credential cho YouTube**:
   - Trong n8n Dashboard → **Credentials** → **Add YouTube OAuth2**.
   - Chọn **YouTube Data API v3** và **YouTube Upload API**.
   - Theo hướng dẫn để cấp quyền.

##### **C. Cấu Hình Tham Số Cụ Thể**
| **Node**               | **Tham Số Cần Chỉnh**                          | **Ghi Chú**                                                                 |
|------------------------|-----------------------------------------------|-----------------------------------------------------------------------------|
| **GetYTvideo**         | Sheet Name: `videos`                          | Chọn sheet chứa danh sách video.                                           |
| **GetYTmusic**         | Sheet Name: `music`                          | Chọn sheet chứa danh sách nhạc.                                           |
| **GetQuotes**          | Sheet Name: `quotes`                         | Chọn sheet chứa text overlay.                                               |
| **DownloadVideoFootage** | Command: `yt-dlp -f "bestvideo+bestaudio" --merge-output-format mp4` | Đảm bảo yt-dlp và FFmpeg đã cài đặt.                                       |
| **DownloadMusic**      | Command: `yt-dlp -x --audio-format mp3 --embed-thumbnail` | Tải nhạc với thumbnail.                                                     |
| **GenrateTextOverlayForVideo** | Code (Node `set` trước đó) | Chỉnh sửa mã JavaScript để thay đổi font, màu, vị trí text.               |
| **GenerateVideo**      | Command: `ffmpeg -i input.mp4 -i audio.mp3 -i overlay.png -vf "drawtext=text='${text}':fontfile=/path/to/font.ttf:fontsize=30:fontcolor=white:x=100:y=100" -c:a copy -c:v libx264 -t 10 output.mp4` | Thay đổi đường dẫn font và vị trí text.                                   |
| **UploadVideo**        | API Endpoint: `https://www.googleapis.com/youtube/v3/videos` | Đảm bảo API Key YouTube đã được cấu hình.                                |

##### **D. Cấu Hình Lịch (Schedule Trigger)**
- **Phần tải video/music**:
  - Cài đặt **Schedule Trigger** để chạy hàng ngày (ví dụ: 8h sáng).
- **Phần xử lý và upload**:
  - Cài đặt **Schedule Trigger1** để chạy sau khi tải xong (ví dụ: 9h sáng).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual trigger** để kiểm tra việc tải video/music.
   - Kiểm tra file đã được tạo ở thư mục `/tmp/youtube-shorts`.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** cho cả hai workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động thêm hashtag**:
   - Sử dụng **Node `set`** trước khi upload để thêm hashtag vào mô tả video.
   - Ví dụ:
     ```json
     {
       "json": {
         "snippet": {
           "description": "Video tự động tạo! #YouTubeShorts #Automation #FFmpeg"
         }
       }
     }
     ```

2. **Gửi thông báo Slack/Telegram khi upload thành công**:
   - Thêm **Node `httpRequest`** để gửi thông báo đến Slack/Telegram.
   - Ví dụ:
     ```json
     {
       "url": "https://api.telegram.org/bot<BOT_TOKEN>/sendMessage",
       "method": "POST",
       "body": {
         "chat_id": "<CHAT_ID>",
         "text": "Shorts đã upload thành công: {{ $json.url }}"
       }
     }
     ```

3. **Lưu log hoạt động**:
   - Thêm **Node `readWriteFile`** để ghi log vào file CSV.
   - Ví dụ:
     ```json
     {
       "file": "/tmp/youtube-shorts/logs.csv",
       "mode": "a",
       "data": "{{ $json | toString }}"
     }
     ```

4. **Tùy chỉnh thời gian Shorts**:
   - Thay đổi tham số `-t 10` trong command FFmpeg để thay đổi độ dài Shorts (ví dụ: `-t 15` cho 15 giây).

5. **Sử dụng AI tạo mô tả**:
   - Thêm **Node `n8n-nodes-base.llm`** (nếu có) để tự động tạo mô tả video bằng AI.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào nội dung chất lượng cao hơn. Bằng cách tự động hóa **tất cả quá trình từ tải video đến upload Shorts**, các sếp không chỉ tiết kiệm thời gian mà còn **tăng cường sự hiện diện trên YouTube** một cách liên tục.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm video/music** vào Google Sheets.
3. **Bật Active** và để hệ thống làm việc cho bạn!

**Chia sẻ kết quả** của mình với #n8nVietnam để cùng học hỏi! 🚀