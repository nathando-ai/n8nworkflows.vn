---
title: "🎬 Tự Động Hoá Tạo Video Reels AI Từ Hình Ảnh: GPT Image 2 + Seedance + Blotato (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí chuyển đổi hình ảnh thành video reels AI sẵn sàng đăng lên TikTok, Instagram và Facebook chỉ với 1 cú nhấp chuột. Giúp marketer, doanh nghiệp và creator tiết kiệm thời gian lên đến 80% trong việc tạo nội dung video."
slug: "tay-dong-hoa-tao-video-reels-ai-tu-hinh-anh"
tags: [n8n, automation, ai-video, social-media, blotato, atlascloud, no-code]
keywords: [n8n workflow video reels, tự động hóa tạo video tiktok, seedance 2.0, gpt image 2, blotato tự động đăng bài]
---

# 🚀 **Tạo Video Reels AI Từ Hình Ảnh: Từ Ảnh → Video → Đăng Trên TikTok/Instagram/Facebook (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp đang mất thời gian và công sức để:
- **Tạo video reels thủ công** từ hình ảnh, phải cắt ghép, thêm nhạc, hiệu ứng...
- **Đăng bài trên nhiều nền tảng** (TikTok, Instagram, Facebook) một cách tẻ nhạt, không đồng bộ.
- **Không có thời gian** để thử nghiệm các phong cách video mới, vì quá trình tạo nội dung quá phức tạp.

**Workflow này giải quyết tất cả!** Chỉ cần **gửi một hình ảnh và hai prompt (mô tả hình ảnh + mô tả động tác)**, n8n sẽ tự động:
✅ **Tạo hình ảnh AI** từ GPT Image 2 (AtlasCloud) với phong cách mới.
✅ **Chuyển hình ảnh thành video reels** với Seedance 2.0 (AI Motion).
✅ **Đăng video lên TikTok, Instagram và Facebook** một lần với Blotato.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Video sẵn sàng đăng** với định dạng 9:16 (phù hợp cho vertical feeds).
- **Đăng bài đồng bộ** trên 3 nền tảng (TikTok, Instagram, Facebook) chỉ với 1 lần setup.
- **Cá nhân hóa nội dung** với các prompt khác nhau (sản phẩm, cảnh phim, nghệ thuật 3D...).
- **Hoạt động 24/7** trên VPS tự host, không phụ thuộc vào thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản AtlasCloud** (miễn phí) để sử dụng:
   - [GPT Image 2](https://www.atlascloud.ai/?ref=8QKPJE) (tạo hình ảnh AI).
   - [Seedance 2.0](https://www.atlascloud.ai/?ref=8QKPJE) (chuyển hình ảnh thành video).
   - *Lưu ý:* AtlasCloud **không hỗ trợ hình ảnh có mặt người thực**, chỉ chấp nhận sản phẩm, cảnh phim hoặc nghệ thuật 3D.

2. **Tài khoản Blotato** (miễn phí) để đăng bài trên:
   - [TikTok](https://blotato.com/?ref=firas)
   - [Instagram](https://blotato.com/?ref=firas)
   - [Facebook](https://blotato.com/?ref=firas)
   - *Cần liên kết tài khoản Facebook, TikTok và Instagram vào Blotato trước.*

3. **n8n Self-hosted** (không hỗ trợ trên n8n Cloud do sử dụng node Blotato cộng đồng).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

4. **API Keys cần thiết**:
   - **AtlasCloud API Key** (Header Auth: `Authorization: Bearer YOUR_KEY`).
   - **Blotato API Key** (tự động tạo khi liên kết tài khoản).
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/16168) và import vào n8n Editor.
- **Copy/paste JSON** từ file vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không cần chỉnh sửa code** trong node `Extract Image URL` và `Extract Video URL` (đã tối ưu sẵn).
- **Không cần cài đặt node Blotato** nếu tự host n8n (node này là cộng đồng).
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **A. Node "Config" (Set)**
- **Thêm biến môi trường** (variables) cần thiết:
  | Biến Môi Trường       | Giá Trị (Điền Theo Tài Khoản Của Các Sếp) |
  |-----------------------|---------------------------------------------|
  | `sourceImageUrl`      | URL hình ảnh gốc (ví dụ: `https://example.com/image.jpg`) |
  | `facebookAccountId`   | ID tài khoản Facebook (lấy từ Blotato) |
  | `tiktokAccountId`     | ID tài khoản TikTok (lấy từ Blotato) |
  | `instagramAccountId` | ID tài khoản Instagram (lấy từ Blotato) |

##### **B. Node "Webhook Trigger"**
- **Không cần chỉnh sửa** (sẵn sàng nhận dữ liệu từ bên ngoài).
- **Test webhook** bằng cách gửi request POST đến:
  ```
  https://[your-n8n-domain]/webhook/489e51cf-c257-4cb3-acb5-b1136eed2010
  ```
  với payload:
  ```json
  {
    "prompt": "A futuristic cityscape with neon lights and flying cars",
    "prompt_video": "The city moves dynamically with cars flying, buildings glowing",
    "caption": "Future City - Explore the world of tomorrow!"
  }
  ```

##### **C. Node "Generate Image with GPT Image 2 Model" (HTTP Request)**
- **Tham số cần điền**:
  - **Method**: `POST`
  - **URL**: `https://api.atlascloud.ai/v1/gpt-image-2`
  - **Headers**:
    ```
    Authorization: Bearer YOUR_ATLASCLOUD_API_KEY
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "prompt": "$$.json["prompt"],
      "image_url": "$$.json["sourceImageUrl"],
      "width": 1080,
      "height": 1920,
      "ratio": "2:3"
    }
    ```

##### **D. Node "Generate Video" (HTTP Request)**
- **Tham số cần điền**:
  - **Method**: `POST`
  - **URL**: `https://api.atlascloud.ai/v1/seedance-2`
  - **Headers**:
    ```
    Authorization: Bearer YOUR_ATLASCLOUD_API_KEY
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "image_url": "$$.json["imageUrl"],
      "prompt": "$$.json["prompt_video"],
      "duration": 5,
      "fps": 30,
      "generate_audio": false,
      "ratio": "9:16"
    }
    ```

##### **E. Node "Create post [TikTok/Instagram/Facebook]" (Blotato)**
- **Không cần chỉnh sửa** (sẽ tự động lấy `videoUrl` từ node trước).
- **Đảm bảo đã liên kết tài khoản** trong Blotato trước khi chạy.

##### **F. Node "Image Status" & "Video Status" (Switch)**
- **Không cần chỉnh sửa** (sẽ tự động kiểm tra trạng thái `completed`/`succeeded`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi request webhook với payload như trên.
   - Kiểm tra log trong n8n để xem workflow có chạy thành công không.
2. **Bật Active workflow** sau khi test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TẾ]
1. **Tối ưu Seedance**:
   - Thay đổi `duration` (giây) và `fps` (frame per second) để điều chỉnh độ dài video.
   - Ví dụ: `duration: 7` cho video 7 giây (phù hợp cho TikTok).

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Video Status` để thông báo khi video sẵn sàng.

3. **Lưu log tự động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử tạo video (URL, caption, ngày tạo).

4. **Tự động gửi báo cáo**:
   - Thêm node **Email** (Gmail/SendGrid) để gửi báo cáo tuần/month về số lượng video đã tạo.

5. **Sử dụng nhiều hình ảnh**:
   - Thêm node **Queue** để xử lý nhiều hình ảnh đồng thời (nếu có nhiều request).
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tạo video reels AI** một cách nhanh chóng, không cần kỹ năng edit.
✔ **Đăng bài đồng bộ** trên TikTok, Instagram và Facebook chỉ với 1 lần setup.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược marketing thay vì công việc thủ công.

**Hành động ngay!**
1. **Setup VPS** và cài đặt n8n (sử dụng mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình tài khoản AtlasCloud + Blotato.
3. **Test với hình ảnh đầu tiên** và bắt đầu tạo video reels AI!

🚀 **Chia sẻ kết quả của các sếp với #n8nVietnam để cùng học hỏi!**