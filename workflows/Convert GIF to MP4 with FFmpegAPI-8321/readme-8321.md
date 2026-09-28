---
title: "🎬 Chuyển GIF sang MP4 Tự Động với FFmpegAPI - Không Cần Code!"
description: "Tự động hóa quy trình chuyển đổi GIF sang MP4 chỉ trong vài giây với n8n và FFmpegAPI, tiết kiệm thời gian và nâng cao hiệu suất content creation."
slug: "chuyen-gif-sang-mp4-voi-ffmpegapi"
tags: [n8n, automation, content-creation, ffmpeg, no-code, video-processing]
keywords: [n8n workflow chuyển đổi video, tự động hóa GIF sang MP4, FFmpegAPI, tự động hóa không code, chuyển đổi file đa phương tiện]
---

# 🚀 Chuyển GIF sang MP4 Tự Động với FFmpegAPI - Không Cần Code!

### 💡 **Giải quyết vấn đề gì?**
Các sếp đang phải tốn thời gian thủ công chuyển đổi GIF sang MP4 để sử dụng trong video marketing, bài viết blog hay nội dung social media? Hay đang gặp khó khăn khi phải sử dụng các công cụ phức tạp như Adobe Premiere chỉ để làm việc đơn giản này? **Workflow này sẽ tự động hóa toàn bộ quy trình chỉ trong vài giây**, giúp tiết kiệm thời gian và nâng cao hiệu suất công việc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi GIF sang MP4 chỉ trong vài giây thay vì thủ công.
- **Chính xác và ổn định**: Không lo mất chất lượng video do quá trình tự động hóa.
- **Tích hợp dễ dàng**: Sử dụng được trong các dự án content creation, email marketing, hoặc website.
- **Hoạt động liên tục**: Workflow có thể chạy 24/7 trên VPS, không cần can thiệp thủ công.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản FFmpegAPI**: Các sếp cần tạo tài khoản và lấy **API Key** từ [trang web FFmpegAPI](https://ffmpeg-api.com/).
- **File GIF**: File GIF cần chuyển đổi (có thể là file từ máy tính hoặc được tải lên từ các dịch vụ cloud).
- **n8n Workflow**: Các sếp cần một tài khoản n8n (cả phiên bản cloud lẫn self-hosted).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và tạo một workflow mới.
2. Nhấn vào **Import** và chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/8321).
3. Sau khi import xong, các sếp sẽ thấy workflow với 6 node như mô tả dưới đây.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
##### **Bước 1: Cấu hình API Key FFmpegAPI**
- **Node**: **Process File** (type: `httpRequest`)
  - Các sếp cần thêm **API Key** vào biến môi trường:
    1. Vào **Variables** (phía bên trái của n8n Editor).
    2. Tạo một biến mới với tên **`FFMPEG_API_KEY`** và điền **API Key** từ FFmpegAPI.
    3. Lưu biến này.

##### **Bước 2: Cấu hình Node "Attach file"**
- **Node**: **Attach file** (type: `formTrigger`)
  - Các sếp cần chọn **File Upload** để cho phép người dùng tải file GIF lên.
  - Đảm bảo **File Upload** được kích hoạt trong **Form Trigger**.

##### **Bước 3: Cấu hình Node "Download URL"**
- **Node**: **Download URL** (type: `form`)
  - Các sếp cần đảm bảo **keyParameters** được đặt là `operation: completion` như trong workflow gốc.
  - Sau khi chuyển đổi xong, URL tải file MP4 sẽ được trả về trong **Form**.

##### **Bước 4: Kiểm tra các Node HTTP Request**
- **Node**: **Get Upload URL**, **Upload File**, **Process File** (tất cả type: `httpRequest`)
  - Các sếp cần đảm bảo **Method** được đặt là `POST` và **URL** là các endpoint của FFmpegAPI:
    - **Get Upload URL**: `https://api.ffmpegapi.com/upload`
    - **Upload File**: `https://api.ffmpegapi.com/upload`
    - **Process File**: `https://api.ffmpegapi.com/convert`
  - Thêm **Headers** như sau:
    ```
    {
      "Authorization": "Bearer {{ $node["FFMPEG_API_KEY"].json["value"] }}"
    }
    ```
  - Thêm **Body** (JSON) cho các node:
    - **Get Upload URL**:
      ```json
      {
        "operation": "upload"
      }
      ```
    - **Upload File**:
      ```json
      {
        "url": "{{ $json["url"].json["value"] }}",
        "file": "{{ $file }}"
      }
      ```
    - **Process File**:
      ```json
      {
        "operation": "completion",
        "input": "{{ $json["url"].json["value"] }}",
        "output": "mp4"
      }
      ```

#### 3. Kích hoạt ⚡️
1. **Test Run**: Các sếp có thể chạy workflow với một file GIF mẫu để kiểm tra.
2. **Active Workflow**: Sau khi kiểm tra thành công, các sếp có thể bật **Active** để workflow hoạt động tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Sau khi chuyển đổi xong, các sếp có thể gửi thông báo kết quả qua Slack hoặc Telegram bằng node **Webhook** để được thông báo ngay khi hoàn thành.
2. **Lưu log chuyển đổi**: Sử dụng node **Google Sheets** hoặc **Notion** để lưu lại lịch sử chuyển đổi, bao gồm tên file, thời gian chuyển đổi và URL tải file MP4.
3. **Tự động hóa định kỳ**: Nếu các sếp có nhiều file GIF cần chuyển đổi, có thể sử dụng **n8n Cron Trigger** để chạy workflow định kỳ.
4. **Tích hợp với Google Drive/Dropbox**: Sử dụng node **Google Drive** hoặc **Dropbox** để tự động tải file GIF từ cloud và chuyển đổi sang MP4.

---

### 📌 Kết luận
Workflow này giúp các sếp **tự động hóa quy trình chuyển đổi GIF sang MP4 một cách nhanh chóng và hiệu quả**, không cần sử dụng bất kỳ công cụ nào ngoài n8n và FFmpegAPI. **Hãy thử ngay và tiết kiệm thời gian cho công việc content creation của mình!**

👉 **Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/8321) và import vào n8n của các sếp!