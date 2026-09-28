---
title: "🚀 Tự Động Hóa Bài Đăng Instagram Chứng Minh Xác Thực (Testimonial) Từ Airtable Với Bannerbear & Instagram API – Không Cần Code"
description: "Workflow tự động hóa lấy đánh giá 5 sao từ Airtable, tạo card hình ảnh cá nhân hóa bằng Bannerbear, đăng lên Instagram với caption tự động hóa và thông báo Slack. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng, tăng độ tin cậy và tự động hóa hoàn toàn quy trình marketing xã hội."
slug: "tu-dong-hoa-bai-dang-instagram-chung-minh-xac-thuc"
tags: [n8n, automation, social-media, instagram-automation, airtable, bannerbear, no-code, crm-automation]
keywords: [n8n workflow instagram, tự động hóa bài đăng instagram, airtable instagram, bannerbear api, tự động hóa marketing xã hội, tự động hóa review instagram]
---

# 🚀 **Tự Động Hóa Bài Đăng Instagram Chứng Minh Xác Thực (Testimonial) Từ Airtable – Không Cần Code**

## **🔥 Nỗi Đau Của Các Sếp: Tốn Thời Gian Và Làm Thủ Công?**
Các sếp đã từng phải:
- **Lấy thủ công** các đánh giá 5 sao từ Google, Trustpilot, hoặc Typeform.
- **Tạo hình ảnh** bằng Canva/Photoshop để cá nhân hóa bài đăng.
- **Đăng bài lên Instagram** và cập nhật trạng thái đã đăng thủ công.
- **Phải nhớ** gửi thông báo cho team mỗi khi có bài mới.

**Kết quả?** Tốn **10+ giờ/tháng**, dễ bị lỗi nhân sự, và không thể hoạt động 24/7.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** – từ lấy review đến đăng bài, chỉ cần **cài đặt 1 lần** và chạy tự động hàng ngày!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 10+ giờ/tháng** – Không cần làm thủ công mỗi ngày.
✅ **Chất lượng cao nhất** – Chỉ lấy review **5 sao** và cá nhân hóa hình ảnh.
✅ **Hoạt động liên tục** – Chạy tự động hàng ngày vào **10h sáng**.
✅ **Thông báo tự động** – Slack gửi thông báo chi tiết cho team.
✅ **Dữ liệu sạch** – Cập nhật trạng thái đã đăng vào Airtable, tránh trùng lặp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LÀM**]
Các sếp cần chuẩn bị:
✔ **Airtable Base** với bảng **Reviews** có các trường:
   - `Reviewer Name` (Tên người đánh giá)
   - `Review Text` (Nội dung review)
   - `Rating` (Đánh giá sao)
   - `Star Label` (Dấu sao)
   - `Posted` (Trạng thái đã đăng, mặc định `false`)

✔ **Bannerbear API Key** + **Template ID** của một template **quote card** (hình ảnh bài đăng Instagram).
   - **Hướng dẫn lấy Template ID**:
     1. Tạo template trên [Bannerbear](https://bannerbear.com/).
     2. Chọn template **quote card** (có ô trống cho tên và review).
     3. Copy **Template ID** từ URL.

✔ **Instagram Graph API Token** (để đăng bài tự động).
   - **Hướng dẫn lấy token**:
     1. Tạo **Business Account** trên Instagram.
     2. Đăng ký **Facebook Developer App** và yêu cầu **Instagram Graph API**.
     3. Tạo **Access Token** với quyền `instagram_basic`, `pages_show_list`, `pages_read_engagement`.

✔ **Upload to URL Node Credentials** (để upload hình ảnh lên CDN).
   - Có thể dùng **Cloudflare API**, **AWS S3**, hoặc dịch vụ khác hỗ trợ upload file.

✔ **Slack API Token** (tùy chọn, để thông báo team).
   - Tạo **Slack App** và lấy **Bot Token**.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)** để chạy workflow 24/7 ổn định.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
#### **Cách 1: Import từ file JSON**
1. Tải file JSON từ [n8n.io/workflows/14597](https://n8n.io/workflows/14597).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON.
3. Chọn **Self-hosted** (nếu dùng VPS) hoặc **n8n.cloud** (nếu dùng miễn phí).

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/14597](https://n8n.io/workflows/14597).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Self-hosted** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Trigger (Đặt Lịch Trình)**
- **Cài đặt mặc định**: **Daily at 10:00 AM**.
- **Cách chỉnh sửa**:
  - Nhấn vào node **Schedule — Daily 10AM**.
  - Chọn **Edit** → Thay đổi **cron expression** nếu muốn chạy khác (ví dụ: `0 12 * * *` để chạy 12h trưa).
  - **Không cần thay đổi** nếu muốn giữ mặc định.

#### **🔹 Node 2 & 3: Airtable — Fetch Review & IF Filter**
- **Airtable — Fetch 5-Star Review**:
  - **Base ID** và **Table Name** phải khớp với bảng **Reviews** của các sếp.
  - **Filter Formula**:
    ```plaintext
    {Rating} = 5 AND {Posted} = false
    ```
    (Chỉ lấy review **5 sao** và **chưa đăng**).
  - **Limit**: Đặt **5** để lấy tối đa 5 review mới nhất.

- **IF — Has Valid Review?**:
  - **Không cần chỉnh** nếu cấu hình Airtable đúng.
  - Nếu không có review 5 sao, workflow sẽ **thoát an toàn** qua node **No Review — Exit Gracefully**.

#### **🔹 Node 4: Code — Prepare Bannerbear Payload**
- **Mã JavaScript** sẽ tự động:
  - Lấy **Reviewer Name** và **Review Text** từ Airtable.
  - **Truncated text** (cắt review xuống 140 ký tự để phù hợp Instagram).
  - **Tạo caption** tự động:
    ```
    "🌟 Review từ @{Reviewer Name} 🌟
    {Review Text}
    #TênDoanhNghiệp #Chứng Minh Xác Thực"
    ```
  - **Không cần chỉnh** nếu muốn giữ mặc định.

#### **🔹 Node 5 & 6: HTTP — Bannerbear API**
- **HTTP — Bannerbear: Create Image Job**:
  - **URL**: `https://api.bannerbear.com/v2/jobs`
  - **Headers**:
    - `Authorization: Bearer {API_KEY}` (điền API Key của Bannerbear).
    - `Content-Type: application/json`
  - **Body** (JSON):
    ```json
    {
      "template_id": "{TEMPLATE_ID}",
      "data": {
        "name": "{{$node["Airtable — Fetch 5-Star Review"].json["fields"]["Reviewer Name"]}}",
        "text": "{{$node["Airtable — Fetch 5-Star Review"].json["fields"]["Review Text"].substring(0, 140)}}"
      }
    }
    ```
  - **Không cần chỉnh** nếu đã điền đúng **API Key** và **Template ID**.

- **HTTP — Bannerbear: Poll Status**:
  - **URL**: `https://api.bannerbear.com/v2/jobs/{job_uid}/status`
  - **Headers**: Giống như trên.
  - **Không cần chỉnh** nếu cấu hình đúng.

#### **🔹 Node 7: IF — Image Ready?**
- **Kiểm tra trạng thái**:
  - Nếu `status = completed`, workflow tiếp tục.
  - Nếu chưa ready, **wait 3s + re-poll** (tối đa 5 lần).
  - Nếu **image không ready**, workflow **thoát an toàn** qua node **Image Not Ready — Exit with Alert**.

#### **🔹 Node 8: Upload to URL**
- **Mục đích**: Upload hình ảnh từ Bannerbear lên CDN để Instagram có thể lấy.
- **Cấu hình**:
  - **Endpoint URL**: Điền URL của dịch vụ upload (ví dụ: Cloudflare API).
  - **Headers**:
    - `Authorization: Bearer {API_KEY}` (nếu cần).
  - **Body**:
    ```json
    {
      "url": "{{$node["HTTP — Fetch Rendered Card"].json["image_url"]}}",
      "filename": "review_{{$node["Airtable — Fetch 5-Star Review"].json["fields"]["Reviewer Name"]}}_{{ $datetime.format('YYYY-MM-DD_HH-mm-ss', new Date()) }}.jpg"
    }
    ```
  - **Lưu ý**:
    - **Upload to URL** là **bước bắt buộc** vì Instagram **không chấp nhận** base64 hoặc binary payload.
    - Nếu không có node này, workflow **sẽ thất bại** khi đăng bài.

#### **🔹 Node 9 & 10: Instagram — Create & Publish Media**
- **IG — Create Media Container**:
  - **URL**: `https://graph.facebook.com/v19.0/{IG_ACCOUNT_ID}/media`
  - **Headers**:
    - `Authorization: Bearer {INSTAGRAM_API_TOKEN}`
    - `Content-Type: application/json`
  - **Body**:
    ```json
    {
      "creation_id": "{IG_ACCOUNT_ID}",
      "image_url": "{{$node["Upload a File"].json["url"]}}",
      "caption": "{{$node["Code — Merge Upload + Caption Data"].json["caption"]}}"
    }
    ```
  - **Không cần chỉnh** nếu đã điền đúng **API Token** và **Account ID**.

- **Wait — 6s IG Buffer**:
  - **Không cần chỉnh**, nhưng có thể tăng lên **10s** nếu Instagram chậm.

- **IG — Publish Container**:
  - **URL**: `https://graph.facebook.com/v19.0/media_publish`
  - **Headers**: Giống như trên.
  - **Body**:
    ```json
    {
      "creation_id": "{{$node["IG — Create Media Container"].json["id"]}}"
    }
    ```
  - **Không cần chỉnh**.

#### **🔹 Node 11: Airtable — Mark as Posted**
- **Cập nhật trạng thái**:
  - Đặt `Posted = true`.
  - Lưu **Instagram Post ID** và **timestamp** vào trường `Posted`.
- **Không cần chỉnh** nếu cấu hình Airtable đúng.

#### **🔹 Node 12: Slack — Notify Team**
- **Thông báo chi tiết**:
  - Gửi **block message** với:
    - Tên người đánh giá.
    - Đoạn review.
    - Link bài đăng Instagram.
    - Link hình ảnh CDN.
- **Cấu hình**:
  - **Webhook URL**: Điền URL Slack Webhook.
  - **Message**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*🌟 Bài Đăng Mới 🌟*"
          }
        },
        {
          "type": "divider"
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "👤 *Người đánh giá:* <{Reviewer Name}>"
          }
        },
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "💬 *Review:*\n{Review Text}"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Xem Bài Đăng",
                "emoji": true
              },
              "url": "{{$node["IG — Publish Container"].json["id"]}}"
            }
          ]
        }
      ]
    }
    ```
  - **Không cần chỉnh** nếu muốn giữ mặc định.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1 review mẫu**:
   - Chọn **Run Workflow** và chọn **1 record** từ Airtable.
   - Kiểm tra từng node để đảm bảo **không lỗi**.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tăng Tính Cá Nhân Hóa Hình Ảnh**
- **Sử dụng AI để tạo hình ảnh**:
  - Thay vì Bannerbear, các sếp có thể dùng **MidJourney API** hoặc **DALL·E** để tạo hình ảnh động từ review.
  - **Cách làm**:
    - Thêm node **HTTP Request** gọi API MidJourney.
    - Chỉnh **prompt** như:
      ```
      "A professional testimonial card for {Reviewer Name} from {Doanh Nghiệp}. The card has a clean design with {Reviewer Name}'s photo on the left and a quote in the center: '{Review Text}'. Modern, corporate style, high quality, 1080x1080 pixels."
      ```

### **2. Lưu Log & Theo Dõi Lỗi**
- **Thêm node StickyNote** để ghi log:
  ```json
  {
    "type": "stickyNote",
    "content": "📝 *Log:* Review '{Reviewer Name}' đã được xử lý thành công vào {timestamp}."
  }
  ```
- **Dùng node Email** để gửi báo cáo lỗi:
  - Thêm node **HTTP Request** gọi Gmail API để gửi email khi có lỗi.

### **3. Chạy Workflow Theo Thời Gian Khác**
- **Chỉ chạy vào ngày làm việc**:
  - Chỉnh **cron expression** thành:
    ```
    0 10 * * MON-FRI
    ```
    (Chỉ chạy từ