---
title: "🎥 Tự Động Chuyển YouTube Video Sang MP4 & MP3 Với API RapidAPI + Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa chuyển đổi video YouTube thành định dạng MP4 và MP3 với chất lượng cao, đồng thời ghi log chi tiết vào Google Sheets. Giúp các sếp tiết kiệm thời gian và quản lý nội dung video hiệu quả."
slug: "tuy-dong-hoa-chuyen-doi-youtube-sang-mp4-mp3"
tags: [n8n, automation, file-management, youtube-downloader, google-sheets]
keywords: [n8n workflow youtube, tự động hóa chuyển đổi video, download youtube mp4 mp3, api rapidapi, google sheets logging]
---

# 🚀 **Tự Động Chuyển YouTube Video Sang MP4 & MP3 Với API RapidAPI + Google Sheets**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm thời gian** khi chuyển đổi video YouTube sang định dạng MP4/MP3 thủ công.
- **Quản lý nội dung video** một cách hệ thống với log chi tiết trên Google Sheets.
- **Tận dụng API RapidAPI** để lấy các định dạng chất lượng cao (360p, 720p, 1080p) và MP3.
- **Không cần viết code** – chỉ cần cấu hình workflow trên n8n.

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi video chỉ trong vài giây thay vì thủ công.
- **Chất lượng cao**: Lấy các định dạng MP4 với độ phân giải 360p, 720p, 1080p và MP3.
- **Quản lý hệ thống**: Ghi log tất cả video đã chuyển đổi vào Google Sheets với thông tin chi tiết.
- **Hoạt động 24/7**: Workflow tự động chạy khi có yêu cầu từ form.
- **Mở rộng dễ dàng**: Có thể kết nối với Slack/Telegram để thông báo kết quả.
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
- **Tài khoản RapidAPI** (để sử dụng [YouTube Video Downloader API](https://rapidapi.com/skdeveloper/api/youtube-video-downloader-fast)).
- **Google Sheets** (để lưu log video).
- **Credentials cho n8n**:
  - **Google API Key** (để kết nối với Google Sheets).
  - **API Key của RapidAPI** (để gọi API YouTube Downloader).
- **Form nhập URL YouTube** (có thể sử dụng n8n Form Trigger hoặc kết nối với một trang web bên ngoài).

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/6924) hoặc sao chép mã JSON từ trang gốc.
- **Bước 2**: Mở **n8n Editor** → Nhấn **Import** → Dán mã JSON và nhấn **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: On Form Submission (n8n-nodes-base.formTrigger)**
- **Chức năng**: Nhận URL YouTube từ người dùng.
- **Cấu hình**:
  - Thêm một **form** với trường nhập **URL YouTube** (ví dụ: `https://www.youtube.com/watch?v=dQw4v...`).
  - Nếu muốn thêm tính năng chọn định dạng (MP4/MP3), có thể mở rộng form thêm trường dropdown.

##### **🔹 Node 2: HTTP Request (n8n-nodes-base.httpRequest)**
- **Chức năng**: Gọi API RapidAPI để lấy các liên kết tải video.
- **Cấu hình BẮT BUỘC**:
  - **Method**: POST.
  - **URL**: `https://youtube-video-downloader-fast.p.rapidapi.com/download`
  - **Headers**:
    - `x-rapidapi-key`: Điền **API Key** của bạn từ RapidAPI.
    - `x-rapidapi-host`: `youtube-video-downloader-fast.p.rapidapi.com`.
  - **Body (JSON)**:
    ```json
    {
      "url": "{{ $node["On form submission"].json["url"] }}"
    }
    ```
    (Thay `{{ $node["On form submission"].json["url"] }}` bằng cách trích xuất URL từ form.)

##### **🔹 Node 3: If (n8n-nodes-base.if)**
- **Chức năng**: Kiểm tra API trả về thành công hay không.
- **Cấu hình**:
  - **Condition**: Kiểm tra `statusCode` trong response API có bằng `200` không.
  - Nếu thành công, tiếp tục xử lý; nếu thất bại, có thể gửi thông báo lỗi (ví dụ: qua Slack).

##### **🔹 Node 4: Google Sheets (n8n-nodes-base.googleSheets)**
- **Chức năng**: Ghi log video vào Google Sheets.
- **Cấu hình BẮT BUỘC**:
  - **Credentials**: Chọn `googleApi` (đã cấu hình trước).
  - **Operation**: `append` (thêm mới dữ liệu).
  - **Sheet Name**: Đặt tên cho sheet (ví dụ: `YouTube_Download_Logs`).
  - **Range**: `Sheet1!A1` (hoặc tùy chỉnh).
  - **Data**:
    - **Original URL**: `{{ $node["HTTP Request"].json["url"] }}`
    - **MP4 360p**: `{{ $node["HTTP Request"].json["data"]["mp4_360p"] }}`
    - **MP4 720p**: `{{ $node["HTTP Request"].json["data"]["mp4_720p"] }}`
    - **MP4 1080p**: `{{ $node["HTTP Request"].json["data"]["mp4_1080p"] }}`
    - **MP3**: `{{ $node["HTTP Request"].json["data"]["mp3"] }}`
    - **Timestamp**: `{{ $node["HTTP Request"].json["timestamp"] }}` (thêm tự động).

---
#### **3. Kích hoạt ⚡️**
- **Bước 1**: Nhấn **Test Run** với một URL YouTube mẫu (ví dụ: `https://www.youtube.com/watch?v=dQw4v...`).
- **Bước 2**: Kiểm tra Google Sheets có xuất hiện log không.
- **Bước 3**: Nếu test thành công, nhấn **Active** để workflow hoạt động tự động.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết nối với Slack/Telegram**: Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả chuyển đổi.
- **Lưu video vào Google Drive**: Sử dụng node **Google Drive** để tự động tải video xuống.
- **Tự động chia sẻ link**: Sau khi chuyển đổi, có thể gửi link MP4/MP3 qua email (node **Email**) hoặc Slack.
- **Lọc video theo tiêu chí**: Thêm node **Set** để lọc video theo tiêu đề, duration, hoặc thẻ (nếu API hỗ trợ).
- **Duy trì log dài hạn**: Sử dụng node **Google Sheets** với **operation: append** để không mất dữ liệu cũ.
:::

---
### **📌 Kết luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình chuyển đổi YouTube sang MP4/MP3** mà không cần viết code. Bằng cách kết hợp **API RapidAPI** và **Google Sheets**, bạn có thể quản lý nội dung video một cách hiệu quả, tiết kiệm thời gian và giảm thiểu lỗi thủ công.

**🚀 Hãy áp dụng ngay và nâng cao hiệu suất công việc của mình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::