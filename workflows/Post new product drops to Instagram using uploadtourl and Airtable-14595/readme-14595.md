---
title: "🚀 Tự Động Hóa Bài Đăng Sản Phẩm Mới Trên Instagram Không Cần Code - Từ Webhook Đến Post Live"
description: "Workflow này tự động hóa toàn bộ quy trình từ nhận thông báo sản phẩm mới (Shopify, Airtable) đến đăng bài lên Instagram với caption chuyên nghiệp, hình ảnh tối ưu và ghi log chi tiết - hoàn toàn không cần viết code."
slug: "tieu-dong-hoa-bai-dang-san-pham-moi-tren-instagram"
tags: [n8n, automation, instagram-business, airtable, shopify, social-media-automation, no-code]
keywords: [n8n workflow instagram, tự động hóa instagram, đăng sản phẩm mới tự động, shopify instagram automation, airtable instagram post, upload image to instagram api]
---

# 🚀 **Tự Động Hóa Bài Đăng Sản Phẩm Mới Trên Instagram - Từ Webhook Đến Post Live**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải làm thủ công:
✅ **Nhận thông báo sản phẩm mới** từ Shopify/Airtable
✅ **Tải hình ảnh** từ CDN/S3 lên Instagram
✅ **Viết caption** chuyên nghiệp với emoji, giá sản phẩm, hashtag
✅ **Đăng bài** và chờ xác nhận
✅ **Ghi log** để theo dõi hiệu suất
✅ **Thông báo** cho team khi bài đăng live

**Kết quả?** Tốn thời gian, dễ lỗi, không đồng bộ với quy trình kinh doanh.

### **Giải Pháp: Workflow Tự Động Hóa 100% Không Code**
Workflow này **tự động hóa toàn bộ quy trình** từ nhận thông báo sản phẩm mới đến đăng bài lên Instagram với:
✔ **Caption tự động** (tối đa 2.200 ký tự)
✔ **Hình ảnh tối ưu** (tải từ URL bất kỳ lên CDN)
✔ **Ghi log chi tiết** (Airtable/Google Sheets)
✔ **Thông báo team** (Slack/Email/Discord)
✔ **Hoạt động 24/7** (không cần can thiệp thủ công)

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30-50% thời gian** so với thủ công
- **Chính xác 100%** (không sai caption, hình ảnh, hashtag)
- **Cá nhân hóa** (caption tự động bao gồm tên sản phẩm, giá, liên kết)
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc)
- **Dễ dàng theo dõi** (log chi tiết trên Airtable)
- **Thông báo tức thời** cho team khi bài đăng live
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Instagram Business Account** (đăng ký tại [Meta for Business](https://www.facebook.com/business/))
2. **Instagram Graph API Access Token** (cấp từ [Meta Developer Portal](https://developers.facebook.com/))
3. **Instagram Business Account ID** (tìm trong Settings > Business Settings)
4. **uploadToUrl Node Credentials** (cấu hình trong n8n để upload hình ảnh)
5. **(Tùy chọn)** Airtable API Key + Base ID (để ghi log bài đăng)
6. **(Tùy chọn)** Slack API Token (để thông báo team)
7. **Webhook URL** (để nhận thông báo từ Shopify/Airtable)

**Lưu ý:** Nếu không có Instagram Business Account, workflow **không thể đăng bài** (chỉ có thể tạo media container).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14595](https://n8n.io/workflows/14595)
- **Nhấn "Import"** trong n8n Editor (trang chủ)
- **Hoặc copy/paste JSON** vào tab "Import" của n8n

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **11 node** chính, các sếp cần cấu hình kỹ các phần sau:

##### **A. Webhook Trigger (Nhận Thông Báo)**
- **Node:** `Webhook — Product Trigger1`
- **Cấu hình:**
  - **Path:** `product-drop` (không đổi)
  - **HTTP Method:** `POST`
  - **Credentials:** Không cần (sử dụng default)
- **Lưu ý:**
  - **Không cần Webhook Respond** nếu không muốn trả về 200 OK (có thể xóa node này nếu không cần).
  - **Test webhook** bằng Postman hoặc cURL:
    ```bash
    curl -X POST https://[YOUR_N8N_URL]/webhook/product-drop \
    -H "Content-Type: application/json" \
    -d '{"product_name": "Sản phẩm mới", "image_url": "https://example.com/image.jpg", "price": "1.000.000 VNĐ", "caption": "Caption mẫu..."}'
    ```

##### **B. Set — Normalize Fields (Định Hình Dữ Liệu)**
- **Node:** `Set — Normalize Fields1`
- **Cấu hình:**
  - **Fallback values** (nếu thiếu dữ liệu):
    ```json
    {
      "caption": "Không có caption mặc định",
      "hashtags": "#mẫuhashtag #sảnphẩm",
      "ig_account_id": "{{ $env.IG_ACCOUNT_ID }}" // Nếu không có trong payload
    }
    ```
  - **Mapping fields** (ví dụ từ Shopify):
    ```json
    {
      "product_name": "{{ $input.payload.body.title }}",
      "price": "{{ $input.payload.body.variants[0].price }}",
      "image_url": "{{ $input.payload.body.featured_image.src }}"
    }
    ```

##### **C. HTTP — Fetch Product Image (Tải Hình Ảnh)**
- **Node:** `HTTP — Fetch Product Image1`
- **Cấu hình:**
  - **Method:** `GET`
  - **URL:** `{{ $node["Set — Normalize Fields1"].json["image_url"] }}`
  - **Headers:**
    ```
    Accept: image/jpeg, image/png
    ```
  - **Output:** Lưu vào biến `imageData` (binary)

##### **D. Upload to URL (Upload Hình Ảnh Lên CDN)**
- **Node:** `Upload a File`
- **Cấu hình:**
  - **Credentials:** `uploadToUrlApi` (đã cấu hình trước)
  - **File:** `{{ $node["HTTP — Fetch Product Image1"].json["imageData"] }}`
  - **Output:** Lưu URL CDN vào biến `image_url_cdn`

##### **E. Code — Build Caption (Xây Dựng Caption)**
- **Node:** `Code — Build Caption1`
- **Mã JavaScript (chỉnh sửa theo nhu cầu):**
  ```javascript
  // Thêm emoji, giá, liên kết, hashtag
  const caption = `
  🚀 **${$input.json.product_name}** 🚀

  Giá: **${$input.json.price} VNĐ**

  Mô tả: ${$input.json.caption || "Mô tả sản phẩm..."}

  #${$input.json.hashtags}
  `;

  // Cắt caption nếu quá 2.200 ký tự
  const finalCaption = caption.length > 2200
    ? caption.substring(0, 2200) + "..."
    : caption;

  return { final_caption: finalCaption };
  ```

##### **F. IG — Create Media Container (Tạo Media Container)**
- **Node:** `IG — Create Media Container1`
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://graph.facebook.com/v19.0/[IG_ACCOUNT_ID]/media`
  - **Headers:**
    ```
    Authorization: Bearer [IG_ACCESS_TOKEN]
    ```
  - **Body (JSON):**
    ```json
    {
      "creation_id": "n8n_${Date.now()}",
      "message": "{{ $node["Code — Build Caption1"].json["final_caption"] }}",
      "image_url": "{{ $node["Upload a File"].json["url"] }}"
    }
    ```
  - **Output:** Lưu `container_id` vào biến `container_id`

##### **G. Wait — 5s Processing Buffer (Đợi Instagram Xử Lý)**
- **Node:** `Wait — 5s Processing Buffer1`
- **Cấu hình:**
  - **Time:** `5000` (5 giây)
  - **Lưu ý:** Nếu hình ảnh lớn, có thể tăng thời gian hoặc thêm node **polling status** để kiểm tra trạng thái.

##### **H. IG — Publish Container (Đăng Bài)**
- **Node:** `IG — Publish Container1`
- **Cấu hình:**
  - **Method:** `POST`
  - **URL:** `https://graph.facebook.com/v19.0/[IG_ACCOUNT_ID]/media_publish`
  - **Headers:**
    ```
    Authorization: Bearer [IG_ACCESS_TOKEN]
    ```
  - **Body (JSON):**
    ```json
    {
      "creation_id": "{{ $node["IG — Create Media Container1"].json["container_id"] }}"
    }
    ```
  - **Output:** Lưu `id` của bài đăng vào biến `post_id`

##### **I. Airtable — Log Post (Ghi Log Bài Đăng)**
- **Node:** `Airtable — Log Post1`
- **Cấu hình:**
  - **API Key:** Điền API Key của Airtable
  - **Base ID:** Điền ID của Base Airtable
  - **Table:** Chọn bảng muốn ghi log
  - **Fields:**
    ```json
    {
      "Post ID": "{{ $node["IG — Publish Container1"].json["id"] }}",
      "Product Name": "{{ $node["Set — Normalize Fields1"].json["product_name"] }}",
      "Caption": "{{ $node["Code — Build Caption1"].json["final_caption"] }}",
      "Image URL": "{{ $node["Upload a File"].json["url"] }}",
      "Timestamp": "{{ $now }}",
      "Status": "Published"
    }
    ```

##### **J. Slack — Notify Team (Thông Báo Team)**
- **Node:** `Slack — Notify Team1`
- **Cấu hình:**
  - **Webhook URL:** Điền URL Webhook từ Slack (tạo tại [Slack API](https://api.slack.com/messaging/composing))
  - **Message:**
    ```json
    {
      "text": "🚀 **Bài đăng mới live!**",
      "attachments": [
        {
          "title": "{{ $node["Set — Normalize Fields1"].json["product_name"] }}",
          "title_link": "https://instagram.com/p/{{ $node["IG — Publish Container1"].json["id"] }}",
          "text": "{{ $node["Code — Build Caption1"].json["final_caption"].substring(0, 100) }}...",
          "image_url": "{{ $node["Upload a File"].json["url"] }}"
        }
      ]
    }
    ```

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Shopify Webhook**
   - Cấu hình webhook từ Shopify tại **Settings > Notifications > Webhooks** để tự động nhận thông báo sản phẩm mới.

2. **Thêm Node Polling Status (Nếu Hình Ảnh Lớn)**
   - Thay thế node `Wait` bằng một node **HTTP Request** để kiểm tra trạng thái của `container_id`:
     ```json
     {
       "url": "https://graph.facebook.com/v19.0/[IG_ACCOUNT_ID]/media?creation_ids={{ $node["IG — Create Media Container1"].json["container_id"] }}",
       "method": "GET"
     }
     ```
   - Chạy loop cho đến khi `status` = `completed`.

3. **Lưu Log vào Google Sheets**
   - Thay thế node Airtable bằng **Google Sheets (n8n-nodes-google-sheets)** với API Key và Sheet ID.

4. **Thêm Node Email Notification**
   - Sử dụng **n8n-nodes-email** để gửi email khi bài đăng live.

5. **Tự Động Chọn Hình Ảnh Phù Hợp**
   - Thêm logic trong node `Code — Build Caption1` để chọn hình ảnh từ nhiều URL:
     ```javascript
     const images = ["https://example.com/image1.jpg", "https://example.com/image2.jpg"];
     const selectedImage = images[Math.floor(Math.random() * images.length)];
     return { image_url: selectedImage };
     ```

6. **Xử Lý Lỗi (Error Handling)**
   - Thêm node **Set Error** để ghi log lỗi vào Airtable/Slack:
     ```json
     {
       "error": "{{ $node.error.message }}",
       "timestamp": "{{ $now }}",
       "product_name": "{{ $node["Set — Normalize Fields1"].json["product_name"] }}"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc đăng bài thủ công lên Instagram, đồng thời **đảm bảo tính nhất quán** với caption, hình ảnh và thông tin sản phẩm. Với **n8n**, các sếp có thể tự động hóa toàn bộ quy trình **không cần viết một dòng code nào**.

**Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/14595](https://n8n.io/workflows/14595)
2. **Cấu hình các node** theo hướng dẫn trên
3. **Test với dữ liệu mẫu** trước khi kích hoạt
4. **Bật Active** và để workflow hoạt động 24/7!

**💡 Mẹo cuối:** Nếu cần **đăng nhiều hình ảnh** (carousel), hãy tham khảo workflow [n8n.io/workflows/14600](https://n8n.io/workflows/14600) để mở rộng tính năng.

---
**Chia sẻ & phản hồi:** Các sếp có thể comment bên dưới hoặc liên hệ tại [n8n Community](https://community.n8n.io/) để chia sẻ kinh