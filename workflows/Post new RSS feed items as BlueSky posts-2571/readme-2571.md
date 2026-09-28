---
title: "🚀 Tự Động Hóa RSS Feed Sang Bài Đăng BlueSky - Giảm Thiểu Công Việc Marketing 90%"
description: "Workflow tự động hóa chuyển đổi bài viết mới từ RSS Feed thành bài đăng BlueSky với hình ảnh, tiêu đề và nội dung tự động, tiết kiệm thời gian cho các sếp marketing 24/7."
slug: "tu-dong-hoa-rss-sang-ba-dang-blueskyn8n"
tags: [n8n, automation, marketing, blue-sky, rss-feed]
keywords: [tự động hóa n8n, chuyển đổi rss sang blue sky, marketing tự động, blue sky api, workflow n8n marketing]
---

# 🚀 **Tự Động Hóa RSS Feed Sang Bài Đăng BlueSky - Giải Pháp Marketing 100% Không Code**

### **Nỗi Đau Của Các Sếp Marketing**
Hàng ngày, các sếp phải:
- **Quét thủ công** các tin tức mới từ RSS Feed (như TechCrunch, Forbes, hoặc blog cá nhân).
- **Tạo bài đăng** trên BlueSky với tiêu đề, hình ảnh và nội dung phù hợp.
- **Tốn thời gian** để cá nhân hóa mỗi bài, dẫn đến hiệu suất thấp và mất tập trung vào chiến lược lớn hơn.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức mới** từ RSS Feed.
✅ **Tạo bài đăng BlueSky** với tiêu đề, hình ảnh và liên kết tự động.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho công việc lặp lại.
- **Tăng độ chính xác** với tiêu đề và nội dung tự động từ nguồn RSS.
- **Cá nhân hóa tự động** bằng cách thêm logo hoặc hình ảnh tùy chỉnh.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Tăng tương tác** trên BlueSky với nội dung mới liên tục.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần:
1. **Tài khoản BlueSky** và [tạo mật khẩu ứng dụng (App Password)](https://bsky.app/settings/app-passwords) để kết nối API.
2. **URL RSS Feed** của nguồn tin tức muốn tự động hóa (ví dụ: `https://techcrunch.com/feed/`).
3. **URL hình ảnh tùy chỉnh** (nếu muốn thay thế hình ảnh mặc định từ Feed).
4. **Thời gian refresh** (cài đặt trong node `RSS Feed Trigger`).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2571) hoặc copy toàn bộ JSON từ canvas.
- **Mở n8n Editor** → Nhấn **Import** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình như sau:

##### **A. Node `RSS Feed Trigger` (n8n-nodes-base.rssFeedReadTrigger)**
- **Tham số cần thiết**:
  - **URL Feed**: Nhập URL RSS của nguồn tin tức (ví dụ: `https://techcrunch.com/feed/`).
  - **Refresh Interval**: Cài đặt thời gian refresh (ví dụ: **5 phút** để cập nhật nhanh).
  - **Credentials**: Chọn hoặc tạo mới (nếu chưa có).

##### **B. Node `Get current datetime` (n8n-nodes-base.dateTime)**
- **Lưu ý**: Node này **không cần chỉnh sửa**, nó tự động lấy thời gian hiện tại để gắn vào bài đăng.

##### **C. Node `Create Session` (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **Method**: `POST`
  - **URL**: `https://bsky.app/api/v1/session`
  - **Headers**:
    ```
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "identifier": "{{$authentication.identifier}}",
      "password": "{{$authentication.password}}"
    }
    ```
    *(Thay `$authentication.identifier` và `$authentication.password` bằng **App Password** của BlueSky từ bước chuẩn bị.)*

##### **D. Node `Download image` (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **Method**: `GET`
  - **URL**: `{{$json.image_url}}` (URL hình ảnh từ RSS Feed).
  - **Headers**:
    ```
    Accept: image/jpeg, image/png
    ```
  - **Lưu ý**: Nếu muốn **thay thế hình ảnh mặc định**, thay `{{$json.image_url}}` bằng URL hình ảnh tùy chỉnh (ví dụ: `https://tinohost.vn/logo.png`).

##### **E. Node `Upload image` (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **Method**: `POST`
  - **URL**: `https://bsky.app/api/v1/atproto/storage/upload`
  - **Headers**:
    ```
    Authorization: Bearer {{ $json.accessToken }}
    Content-Type: multipart/form-data
    ```
  - **Body (Form Data)**:
    - **File**: Chọn file từ node `Download image`.
    - **Name**: `file` (không cần đổi).

##### **F. Node `Create Post` (n8n-nodes-base.httpRequest)**
- **Tham số cần thiết**:
  - **Method**: `POST`
  - **URL**: `https://bsky.app/api/v1/atproto/repo/createRecord`
  - **Headers**:
    ```
    Authorization: Bearer {{ $json.accessToken }}
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "collection": "app.bsky.feed.post",
      "record": {
        "text": "{{$json.description}}", // Nội dung từ RSS
        "createdAt": "{{$json.datetime}}", // Thời gian hiện tại
        "embed": {
          "$type": "app.bsky.embed.images",
          "images": [
            {
              "fullsize": "{{$json.image_url}}",
              "alt": "{{$json.title}}"
            }
          ]
        },
        "reply": {
          "root": "{{$json.link}}"
        }
      }
    }
    ```
    *(Các sếp có thể **tùy chỉnh văn bản** bằng cách thay `{{$json.description}}` bằng nội dung cá nhân hóa.)*

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi bài đăng được tạo thành công.
   - *Cách làm*: Sau node `Create Post`, thêm node `Slack` với message:
     ```json
     "Bài đăng mới trên BlueSky:\n📌 {{$json.title}}\n🔗 {{$json.link}}"
     ```

2. **Lưu Log Tự Động**:
   - Thêm node **Google Sheets** hoặc **Notion** để ghi lại lịch sử bài đăng (tiêu đề, thời gian, link).

3. **Chỉnh Lọc Nội Dung**:
   - Sử dụng **node `Set`** để lọc chỉ lấy bài viết có từ khóa cụ thể (ví dụ: "AI", "Marketing").

4. **Tự Động Xóa Bài Đăng Trùng Lặp**:
   - Thêm node **`if`** để kiểm tra nếu bài đăng đã tồn tại trước đó.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing để tập trung vào chiến lược lớn hơn, trong khi tự động hóa việc chia sẻ tin tức mới trên BlueSky. **Chỉ cần 10 phút setup**, bạn đã có một hệ thống hoạt động **24/7**!

👉 **Bắt đầu ngay**:
1. **Import workflow** từ [đây](https://n8n.io/workflows/2571).
2. **Cấu hình BlueSky App Password** và URL RSS.
3. **Bật Active** và xem bài đăng tự động xuất hiện!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::