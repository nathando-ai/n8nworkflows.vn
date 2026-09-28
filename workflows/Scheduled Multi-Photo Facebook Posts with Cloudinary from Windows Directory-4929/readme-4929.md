---
title: "🚀 Tự Động Hóa Bài Đăng Ảnh Nhiều Hình Trên Facebook Từ Thư Mục Điện Tử (Cloudinary + API) - N8n"
description: "Workflow tự động hóa đăng bài ảnh nhiều hình lên Facebook từ thư mục Windows, kết hợp Cloudinary để tối ưu hóa chất lượng hình ảnh và sử dụng API Facebook Graph API. Giúp content creator tiết kiệm thời gian lên đến 80% khi quản lý nội dung đa hình ảnh."
slug: "tu-dong-hoa-bai-dang-anh-nhieu-hinh-facebook-cloudinary"
tags: [n8n, automation, facebook-graph-api, cloudinary, content-creator, no-code, marketing-automation]
keywords: [n8n workflow facebook, tự động hóa bài đăng facebook, cloudinary api, đăng ảnh nhiều hình facebook, tự động hóa content creator, api facebook graph]
---

# 🚀 **Tự Động Hóa Bài Đăng Ảnh Nhiều Hình Trên Facebook Từ Thư Mục Điện Tử (Cloudinary + API)**

## **🔥 Nỗi Đau Của Content Creator**
Các sếp content creator thường phải mất **giờ đồng hồ** để:
- **Tải hình ảnh** từ máy tính lên Facebook một cách thủ công.
- **Chỉnh sửa và tối ưu hóa** chất lượng hình ảnh trước khi đăng.
- **Quản lý nhiều bài đăng** với nhiều hình ảnh khác nhau, dễ bị quên hoặc mất trật tự.
- **Lặp lại công việc** hàng ngày, gây mệt mỏi và giảm hiệu suất.

**Workflow này giải quyết tất cả đó!** Với **n8n**, các sếp có thể **tự động hóa hoàn toàn** quá trình đăng bài ảnh nhiều hình lên Facebook, kết hợp **Cloudinary** để tối ưu hóa hình ảnh và **API Facebook Graph** để đăng bài chính xác, nhanh chóng.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** – Không cần tải hình thủ công mỗi ngày.
✅ **Chất lượng hình ảnh tối ưu** – Cloudinary tự động nén và tối ưu hóa kích thước.
✅ **Đăng bài nhiều hình một lúc** – Hỗ trợ tối đa **3 hình ảnh/trang bài**.
✅ **Hoạt động 24/7** – Workflow chạy tự động theo lịch trình đã thiết lập.
✅ **Giảm thiểu lỗi** – Không còn quên đăng hoặc đăng sai thời gian.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Facebook Business** (để sử dụng **Facebook Graph API**).
2. **API Key của Cloudinary** (để tối ưu hóa hình ảnh).
3. **Thư mục Windows** chứa:
   - **Hình ảnh** (tên file: `image_*.jpg/png`).
   - **Tên bài viết** (tên file: `description_*.txt`).
   - **Hashtag** (tên file: `hashtag_*.txt`).
4. **n8n Self-hosted** (để chạy workflow 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/4929](https://n8n.io/workflows/4929) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ trang trên vào **n8n Editor** (tab "Import").

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Cấu Hình API Facebook Graph**
- **Tạo Credential mới** trong n8n:
  - **Node**: `Facebook Graph API`
  - **Thiết lập**:
    - **App ID & App Secret**: Lấy từ [Facebook Developer](https://developers.facebook.com/).
    - **Page Access Token**: Lấy từ **Page Token Generator** (đảm bảo có quyền `publish_pages`).
    - **Page ID**: ID của trang Facebook muốn đăng bài.

#### **🔹 Cấu Hình Cloudinary (nếu sử dụng)**
- **Node**: `HTTP Request` (để upload hình lên Cloudinary).
- **Tham số cần điền**:
  - **URL API Cloudinary**: `https://api.cloudinary.com/v1_1/{cloud_name}/image/upload`
  - **Headers**:
    ```json
    {
      "X-Requested-With": "XMLHttpRequest",
      "Authorization": "Bearer {API_KEY}"
    }
    ```
  - **Body (Form Data)**:
    - `file`: Chọn file hình ảnh từ `readWriteFile`.
    - `upload_preset`: `{UPLOAD_PRESET}` (lấy từ Cloudinary Dashboard).

#### **🔹 Cấu Hình Thư Mục Hình Ảnh & Tệp Kèm**
- **Node `readWriteFile`**:
  - **File Path**:
    - `Image`: `C:/Users/{username}/Desktop/facebook_posts/images/*.jpg`
    - `Description`: `C:/Users/{username}/Desktop/facebook_posts/descriptions/*.txt`
    - `Hashtag`: `C:/Users/{username}/Desktop/facebook_posts/hashtags/*.txt`
  - **Chú ý**: Các file phải theo **định dạng nhất quán** (ví dụ: `image_1.jpg`, `description_1.txt`).

#### **🔹 Cấu Hình Lịch Trình (Schedule Trigger)**
- **Node `Schedule Trigger`**:
  - **Cron Expression**: `0 0 * * *` (đăng bài vào **giờ 00:00 hàng ngày**).
  - **Thời gian bắt đầu**: Chọn thời điểm phù hợp (ví dụ: 6h sáng).

#### **🔹 Cấu Hình Đăng Bài Nhiều Hình (Multi-Photo)**
- **Node `Facebook Graph API - Photo`**:
  - **Action**: `POST /{page-id}/photos`
  - **Body**:
    ```json
    {
      "source": "{URL_HINH_AFTER_UPLOAD}",
      "caption": "{NOI_DUNG_BAI_VIET}",
      "published": true
    }
    ```
  - **Limit**: **3 hình/trang bài** (do Cloudinary tối ưu).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **1-2 hình mẫu** để kiểm tra:
   - Hình ảnh có upload lên Cloudinary thành công không?
   - Bài viết có đăng lên Facebook không?
2. **Bật `Active`** workflow sau khi kiểm tra xong.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Hợp Slack/Telegram Báo Lỗi**
- **Node `HTTP Request`** gửi thông báo lỗi lên **Slack/Telegram**:
  ```json
  {
    "text": "Lỗi đăng bài Facebook: {{ $node.error.message }}"
  }
  ```
- **Node `Set`** lưu **ID bài đăng** vào biến để theo dõi.

### **🔹 Lưu Log Tất Cả Bài Đăng**
- **Node `Code`** ghi log vào file CSV:
  ```javascript
  const fs = require('fs');
  const data = JSON.stringify({ date: new Date(), postId: $node.output.data.id });
  fs.appendFileSync('facebook_posts_log.csv', data + '\n');
  ```

### **🔹 Tự Động Xóa Hình Sau Khi Đăng**
- **Node `executeCommand`** xóa hình sau khi đăng:
  ```bash
  del "C:/Users/{username}/Desktop/facebook_posts/images/image_*.jpg"
  ```

### **🔹 Sử Dụng AI Tự Động Tạo Mô Tả**
- **Node `LLM` (n8n-nodes-ai)** tự động tạo **mô tả bài viết** từ hình ảnh:
  ```json
  {
    "prompt": "Tạo mô tả bài viết Facebook cho hình ảnh này: {{ $node.input.data.image_url }}"
  }
  ```

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp content creator, giúp họ **tự động hóa hoàn toàn** quá trình đăng bài ảnh nhiều hình lên Facebook. **Không cần code**, chỉ cần **cấu hình đơn giản** và **chạy 24/7**!

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho công việc sáng tạo!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/4929) | 📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**