---
title: "🚀 Tự động tạo YouTube Shorts bằng WayinVideo AI và lưu trữ Google Drive với n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động biến video dài thành các đoạn Short 9:16 gắn sub bằng AI và lưu trực tiếp vào Google Drive."
slug: "tu-dong-tao-youtube-shorts-wayinvideo-ai-google-drive-n8n"
tags: [n8n, automation, ai, video-generation, google-drive, content-creation]
keywords: [n8n workflow, WayinVideo AI, tạo video ngắn tự động, YouTube Shorts automation, Google Drive API]
---

# 🚀 Tự động tạo YouTube Shorts bằng WayinVideo AI và lưu trữ Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi cắt hàng tá video dài thành các đoạn Short/Reels 9:16, chèn phụ đề và đăng tải thủ công không? Việc này vừa tốn thời gian, vừa đòi hỏi kỹ năng dựng phim cơ bản.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một siêu workflow n8n tự động hóa 100%: Nhận URL video, dùng AI của WayinVideo để chọn các khoảnh khắc vàng, tự động reframe chuẩn 9:16, thêm sub và gom thẳng về Google Drive của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh thủ công xem lại video dài để cắt cúp.
- **AI thông minh:** Tự động phát hiện các phân đoạn hấp dẫn nhất, chấm điểm và gắn thẻ.
- **Tối ưu nền tảng:** Video xuất ra định dạng dọc 9:16 hoàn hảo cho YouTube Shorts, TikTok và Reels.
- **Lưu trữ gọn gàng:** Tự động tải về và phân loại toàn bộ vào thư mục Google Drive định sẵn.
:::

### 🇾ÊU CẦU CẦN THIẾT
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã chạy ổn định (Cloud hoặc Self-hosted).
- **WayinVideo Account:** Tài khoản và API Key từ [WayinVideo Dashboard](https://wayinvideo.com/dashboard/api).
- **Google Drive:** Tài khoản Google để kết nối OAuth2 trên n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã JSON của workflow (hoặc import file JSON tương ứng) và dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 7 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **🎬 Submit Video to WayinVideo API (`httpRequest`):**
  - Thay thế `YOUR_WAYINVIDEO_API_KEY` bằng Bearer Token thực tế của các sếp trong phần Header (Authorization).
  - Tùy chỉnh payload gửi đi (trong Body):
    - `target_duration`: Chọn độ dài clip (ví dụ: `DURATION_30_60`).
    - `limit`: Số lượng clip muốn AI tạo ra (ví dụ: `3`).
    - `resolution`: Độ phân giải (`HD_720` hoặc `FULL_HD_1080`).
    - `ratio`: Tỷ lệ khung hình (`RATIO_9_16` cho video dọc).

- **⏳ Wait 30 Seconds & 🔄 Poll for Clip Results (`wait` & `httpRequest`):**
  - Hệ thống AI cần thời gian render video. Node `Wait` sẽ giữ nhịp 30 giây, sau đó gọi lại API kiểm tra trạng thái thông qua Job ID. Vòng lặp `IF` sẽ kiểm tra xem clip đã sẵn sàng chưa, nếu chưa sẽ tiếp tục chờ.

- **⚙️ Extract Clip Details (`code`):**
  - Node Javascript này giúp lọc kết quả JSON trả về từ API, trích xuất tiêu đề clip, link tải, điểm số (score) và tags một cách sạch sẽ.

- **⬇️ Download Clip File (`httpRequest`):**
  - Tải file video trực tiếp từ đường dẫn xuất của WayinVideo về n8n dưới dạng nhị phân (Binary).

- **☁️ Upload Clip to Google Drive (`googleDrive`):**
  - Kết nối tài khoản Google Drive thông qua **OAuth2 credential**.
  - Điền `YOUR_GOOGLE_DRIVE_FOLDER_ID` (lấy phần ID trên URL thư mục Google Drive của các sếp).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một URL video mẫu (YouTube) để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dán link thủ công trong n8n, hãy nối thêm node Telegram hoặc Slack ở đầu để các sếp có thể gửi link qua chat và nhận thông báo khi video hoàn thành.
- **Tự động đăng YouTube:** Nối thêm node YouTube vào cuối chuỗi để tự động lên lịch publish các Short vừa tạo lên kênh của bạn.
- **Lưu log vào Google Sheets:** Ghi lại tiêu đề clip, điểm số AI và link Drive vào Sheets để dễ dàng quản lý kho nội dung.

### 📌 Kết luận
Việc sản xuất video ngắn hàng loạt chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của AI và tự động hóa n8n. Hãy thiết lập ngay hôm nay để tối ưu hóa kênh YouTube Shorts của các sếp!