---
title: "🎬 Tự Động Chuyển Webinar Thành Clip Video Xã Hội Chất Lượng Với WayinVideo, Google Sheets & Gmail (Không Cần Code)"
description: "Giải pháp tự động hóa 100% cho content marketer và đội ngũ xã hội hóa nội dung, biến 1-2 giờ webinar thành video clip ngắn 9:16 sẵn sàng đăng tải chỉ trong 10-15 phút. Kết quả: tiết kiệm thời gian, nội dung cá nhân hóa, và phân tích hiệu suất chi tiết."
slug: "tieu-dong-chuyen-webinar-thanh-clip-video-xa-hoi"
tags: [n8n, automation, content-creation, multimodal-ai, wayinvide, google-sheets, gmail, no-code]
keywords: [n8n workflow tự động hóa video, tạo clip từ webinar, WayinVideo API, tự động hóa content marketing, Google Sheets + Gmail, video clip 9:16]
---

# 🚀 **Tự Động Chuyển Webinar Sang Clip Video Xã Hội Chất Lượng (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp content marketer và đội ngũ xã hội hóa nội dung thường phải đối mặt với vấn đề:
- **Thời gian dài** để biên tập video webinar thành clip ngắn (1-2 giờ webinar → hàng giờ để cắt gọt).
- **Nội dung không được tối ưu hóa** cho các nền tảng xã hội (TikTok, Instagram Reels, YouTube Shorts).
- **Không theo dõi hiệu suất** của từng clip (viral score, tags, duration).
- **Phải làm thủ công** mỗi khi có video mới, gây mất thời gian và hiệu suất thấp.

**Workflow này giải quyết tất cả!** Với công nghệ AI của **WayinVideo**, n8n sẽ tự động:
✅ **Chia video webinar thành clip viral** (được AI đánh giá độ hấp dẫn).
✅ **Tạo video clip 9:16 sẵn sàng đăng tải** (cộng animated captions, AI hook, và reframing).
✅ **Gửi báo cáo chi tiết** (Google Sheets + Gmail) với link download và phân tích hiệu suất.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với biên tập thủ công (chỉ 10-15 phút cho 1 webinar).
- **Nội dung tối ưu hóa** cho tất cả nền tảng xã hội (TikTok, Instagram, YouTube).
- **Phân tích hiệu suất** chi tiết (viral score, tags, duration) trong Google Sheets.
- **Báo cáo tự động** được gửi qua Gmail với link download và cảnh báo thời hạn.
- **Hoạt động liên tục** (không cần can thiệp thủ công, chỉ cần submit URL).
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (API Key) để phân tích và tạo clip.
2. **Google Sheets** với tab **"Social Media Clips"** (cấu trúc chi tiết dưới đây).
3. **Tài khoản Gmail** (để nhận báo cáo tự động).
4. **Credentials OAuth2** cho:
   - **Google Sheets** (để ghi dữ liệu).
   - **Gmail** (để gửi báo cáo).
5. **URL webinar** (YouTube, Vimeo, hoặc Zoom) để tự động chuyển đổi.
:::

---

## 📌 **Cấu Trúc Google Sheets (Tab: Social Media Clips)**
| **Cột**               | **Mô Tả**                          | **Dữ Liệu Ghi**                          |
|------------------------|-------------------------------------|------------------------------------------|
| Date                   | Ngày tạo clip                      | `=NOW()` (hoặc ngày submit)             |
| Video Title            | Tiêu đề video webinar               | Do người dùng nhập                     |
| Clip #                 | Số thứ tự clip                     | Tự động sinh (1, 2, 3...)              |
| Clip Title             | Tiêu đề clip (do AI tự động tạo)   | Từ WayinVideo                          |
| Duration (sec)         | Thời lượng clip                     | Giá trị từ WayinVideo                   |
| Viral Score            | Điểm hấp dẫn (AI đánh giá)        | Từ 0-100 (100 = viral nhất)             |
| Tags                   | Tags tự động (do AI đề xuất)       | Ví dụ: #Marketing, #AI, #Webinar        |
| Description            | Mô tả clip                         | Do AI tự động tạo                      |
| Export Link            | Link download clip                  | Do WayinVideo cung cấp                  |
| Logged At              | Thời gian ghi dữ liệu              | `=NOW()`                                |

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/15118](https://n8n.io/workflows/15118) (hoặc copy JSON từ trang này).
- **Mở n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.
- **Kích hoạt workflow** (Active) sau khi cấu hình xong.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **A. Cấu Hình Node "2. Set — Config Values"**
- **Thay thế các giá trị sau** (điền vào các trường `YOUR_*`):
  ```json
  {
    "WAYINVIDEO_API_KEY": "YOUR_WAYINVIDEO_API_KEY", // API Key từ WayinVideo
    "GOOGLE_SHEET_ID": "YOUR_GOOGLE_SHEET_ID",       // ID của Google Sheet (tìm trong URL)
    "RECIPIENT_EMAIL": "your-email@example.com",     // Email nhận báo cáo
    "SENDER_NAME": "Your Brand Name",                 // Tên người gửi (hiển thị trong Gmail)
    "MAX_CLIP_COUNT": 5,                             // Số clip tối đa (mặc định 5)
    "CLIP_DURATION": 15,                             // Thời lượng clip (giây)
    "ASPECT_RATIO": "9:16"                           // Kích thước video (9:16 cho TikTok/Reels)
  }
  ```

#### **B. Cấu Hình Node "19. Google Sheets — Log Clips"**
- **Kết nối OAuth2**:
  - Nhấn **Connect** → Chọn **Google Sheets**.
  - Đăng nhập tài khoản Google và cấp quyền.
- **Chọn Sheet ID** (đã điền trong "Config Values").
- **Chọn tab** là **"Social Media Clips"**.

#### **C. Cấu Hình Node "22. Gmail — Send Clips Digest"**
- **Kết nối OAuth2**:
  - Nhấn **Connect** → Chọn **Gmail**.
  - Đăng nhập tài khoản Gmail và cấp quyền.
- **Điền thông tin**:
  - **From**: `{{ $json["SENDER_NAME"] }} <your-email@example.com>`
  - **To**: `{{ $json["RECIPIENT_EMAIL"] }}`
  - **Subject**: `📌 [{{ $json["VIDEO_TITLE"] }}] {{ $json["CLIP_COUNT"] }} Clip Sẵn Sàng Download`

#### **D. Node "1. Form — Enter Video URL"**
- **Cấu hình form** để người dùng nhập:
  - **Video URL** (YouTube/Vimeo/Zoom).
  - **Video Title** (tiêu đề webinar).
  - **Your Name** (tên người submit).
  - **Clip Count** (số clip muốn tạo, tối đa 5).

#### **E. Node "3. HTTP — Submit AI Clipping Task"**
- **Không cần chỉnh** (API URL và header đã cấu hình sẵn).
- **Chỉ cần đảm bảo `WAYINVIDEO_API_KEY` đúng**.

#### **F. Node "11. HTTP — Submit Export Task"**
- **Không cần chỉnh** (API URL và header đã cấu hình sẵn).
- **Đảm bảo `enable_export: true`** (đã cấu hình trong "Config Values").

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một video mẫu:
   - Submit URL webinar qua form.
   - Kiểm tra **Google Sheets** và **Gmail** để xác nhận dữ liệu.
2. **Bật Active workflow** khi đã kiểm tra xong.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **"22. Gmail — Send Clips Digest"** để thông báo tức thời khi clip sẵn sàng.

2. **Lưu log hoạt động**:
   - Thêm node **Google Drive** hoặc **Notion** để lưu lịch sử tất cả các clip đã tạo.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Trigger** (n8n.io/triggers) để gửi báo cáo hàng tuần/month cho team.

4. **Tối ưu hóa WayinVideo**:
   - Thử các **tags tự động** khác (ví dụ: `#Trending`, `#Educational`) để tăng viral score.

5. **Tạo template email cá nhân hóa**:
   - Sử dụng **n8n Code Node** để thay đổi nội dung email theo từng video (ví dụ: thêm logo của brand).
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp content marketer muốn:
✔ **Tiết kiệm thời gian** (không cần biên tập thủ công).
✔ **Tạo nội dung tối ưu hóa** cho tất cả nền tảng xã hội.
✔ **Theo dõi hiệu suất** chi tiết (viral score, tags, duration).
✔ **Hoạt động tự động** 24/7 mà không cần can thiệp.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy ổn định:
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Submit URL webinar đầu tiên** và xem AI làm việc!

**Chúc các sếp thành công với chiến dịch content mới!** 🚀