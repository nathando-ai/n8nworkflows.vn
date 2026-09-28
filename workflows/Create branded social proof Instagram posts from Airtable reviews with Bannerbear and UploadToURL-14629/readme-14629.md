---
title: "🚀 Tự Động Hóa Xây Đăng Bài Proof Social Branded Từ Đánh Giá Airtable Sang Instagram (Không Cần Code)"
description: "Workflow tự động hóa 24/7 chuyển đổi đánh giá 5 sao từ Airtable thành bài đăng Instagram chuyên nghiệp với Bannerbear, tự động đăng tải và báo cáo Slack. Giúp doanh nghiệp tiết kiệm 10+ giờ/tháng, tăng độ tin cậy thương hiệu và tự động hóa nội dung xã hội."
slug: "tieu-dong-hoa-xay-dang-bai-proof-social-branded-tu-airtable-sang-instagram"
tags: [n8n, automation, social-media, airtable, instagram, bannerbear, no-code, ai-multimodal]
keywords: [n8n workflow instagram, tự động hóa bài đăng instagram, bannerbear n8n, airtable instagram automation, tự động hóa proof social, tự động hóa nội dung xã hội]
---

# 🚀 **Tự Động Hóa Xây Đăng Bài Proof Social Branded Từ Airtable Sang Instagram (Không Cần Code)**

## **Nỗi Đau Của Các Sếp**
Các sếp đang phải **thủ công** quản lý hàng trăm đánh giá 5 sao từ khách hàng trên Airtable, sau đó **tạo hình ảnh chuyên nghiệp**, **đăng tải lên Instagram**, và **báo cáo kết quả** cho team. Quá trình này tiêu tốn **tối thiểu 10-15 giờ/tháng**, dễ xảy ra lỗi nhân sự (quên đăng, sai thông tin), và **không thể hoạt động 24/7**.

**Workflow này giải quyết tất cả:**
✅ **Tự động lấy đánh giá 5 sao** từ Airtable theo thứ tự FIFO (First-In-First-Out).
✅ **Tạo hình ảnh branded** với Bannerbear (không cần thiết kế).
✅ **Đăng tải tự động lên Instagram** với caption cá nhân hóa.
✅ **Cập nhật trạng thái** trong Airtable và báo cáo Slack.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** (hoặc hơn) cho việc quản lý proof social.
- **Tăng độ tin cậy thương hiệu** với bài đăng chuyên nghiệp, tự động hóa.
- **Cá nhân hóa nội dung** cho mỗi bài đăng (tên khách hàng, đánh giá, hình ảnh độc quyền).
- **Hoạt động liên tục** (không phụ thuộc vào giờ làm việc của nhân viên).
- **Báo cáo tự động** trên Slack, giúp team theo dõi hiệu quả.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| Tài Khoản/Dịch Vụ          | Thông Tin Cần Thiết                          | Ghi Chú                                  |
|----------------------------|-----------------------------------------------|-------------------------------------------|
| **Airtable**               | `AIRTABLE_BASE_ID` (ID của Base)             | Lấy từ URL Airtable (vd: `abc123` trong `https://airtable.com/abc123`) |
|                            | `API Key` (tạo từ [Airtable API Docs](https://airtable.com/api)) | Chỉnh quyền `Read & Write` cho Base. |
| **Instagram Business**     | `IG_USER_ID` (ID người dùng)                 | Lấy từ [Meta Developer Portal](https://developers.facebook.com/) |
|                            | `IG_ACCESS_TOKEN` (Token API)                | Tạo token với quyền `instagram_basic`, `pages_show_list`, `pages_read_engagement`. |
| **Bannerbear**             | `BANNERBEAR_API_KEY`                          | Tạo từ [Bannerbear Dashboard](https://bannerbear.com/) |
|                            | `BANNERBEAR_TEMPLATE_ID`                      | ID của template đã tạo (vd: `12345678`). |
| **Slack**                  | `SLACK_CHANNEL_ID`                           | ID của channel Slack (vd: `C12345678`). |
|                            | `SLACK_API_TOKEN`                            | Tạo từ [Slack API Tokens](https://api.slack.com/apps). |

#### **2. Cấu Trúc Bảng Airtable**
Bảng phải có các trường sau (đảm bảo tên trùng khớp với workflow):
| Trường (Field)          | Loại Dữ Liệu | Ghi Chú                          |
|-------------------------|--------------|-----------------------------------|
| `Reviewer Name`         | Text         | Tên khách hàng đánh giá.          |
| `Review Text`           | Long Text    | Nội dung đánh giá (truncated 180 ký tự). |
| `Rating`                | Number       | Đánh giá (chỉ lấy `5` sao).       |
| `Posted`                | Checkbox     | `FALSE` (mặc định), sau đó cập nhật thành `TRUE`. |
| `Submitted At`          | Date         | Thời gian nhận đánh giá.         |
| `Instagram Post ID`     | Text         | ID bài đăng Instagram (sau khi đăng). |
| `Posted At`             | Date         | Thời gian đăng bài.               |
| `Card Image URL`        | Text         | Link hình ảnh bài đăng.            |

#### **3. Template Bannerbear**
Template phải có **3 layer** với tên trùng khớp:
- `reviewer_name` (hiển thị tên khách hàng).
- `review_text` (hiển thị đánh giá).
- `star_label` (hiển thị `★★★★★`).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
:::info[HƯỚNG DẪN IMPORT]
1. **Tải file JSON** từ [n8n.io/workflows/14629](https://n8n.io/workflows/14629) (nếu có).
2. **Copy JSON** từ link trên hoặc file tải về.
3. **Mở n8n Editor** (trang chủ của workflow).
4. **Nhấn "Import"** và dán JSON vào.
5. **Chọn "Import"** để tạo workflow mới.

**Lưu ý:** Nếu không tải được file JSON, có thể **copy/paste** JSON từ [đây](https://gist.githubusercontent.com/JiteshDugar/...) (nếu có).
:::

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow có **16 node**, nhưng các bước sau **cần cấu hình cẩn thận**:

##### **A. Cấu Hình Credentials (Tất Cả Các Node)**
- **Airtable Fetch Review1**:
  - **Base ID**: Điền `{{ $env.AIRTABLE_BASE_ID }}`.
  - **API Key**: Điền `{{ $env.AIRTABLE_API_KEY }}`.
  - **Filter By Formula**:
    ```plaintext
    AND({Rating}=5, {Posted}=FALSE())
    ```
  - **Sort By**: `Submitted At (asc)`.
  - **Max Records**: `1`.

- **HTTP Bannerbear Create Job1 & Poll Status1**:
  - **URL**: `https://api.bannerbear.com/v2/images`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{ $env.BANNERBEAR_API_KEY }}",
      "Content-Type": "application/json"
    }
    ```
  - **Body (Create Job)**:
    ```json
    {
      "templateId": "{{ $env.BANNERBEAR_TEMPLATE_ID }}",
      "modifications": [
        { "layerName": "reviewer_name", "text": "{{ $json.reviewer_name }}" },
        { "layerName": "review_text", "text": "{{ $json.review_text }}" },
        { "layerName": "star_label", "text": "★★★★★" }
      ],
      "width": 1080,
      "height": 1080
    }
    ```

- **IG Create Media Container1 & Publish Container1**:
  - **URL**:
    - `https://graph.instagram.com/media` (Create).
    - `https://graph.instagram.com/media_publish` (Publish).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{ $env.IG_ACCESS_TOKEN }}"
    }
    ```
  - **Body (Create Media)**:
    ```json
    {
      "creation_id": "{{ $json.container_id }}",
      "caption": "{{ $json.caption }}"
    }
    ```

- **Slack Notify Team1**:
  - **Channel**: `{{ $env.SLACK_CHANNEL_ID }}`.
  - **Token**: `{{ $env.SLACK_API_TOKEN }}`.
  - **Message Template**:
    ```json
    {
      "text": ":tada: New Instagram Post! 📸\n\n*Reviewer*: {{ $json.reviewer_name }}\n*Review*: {{ $json.review_text | truncate(50) }}\n*Post ID*: {{ $json.post_id }}\n*Card URL*: {{ $json.card_image_url }}"
    }
    ```

##### **B. Node Code (Cần Chỉnh Sửa)**
- **Code Prepare Bannerbear Payload1**:
  - **JavaScript**:
    ```javascript
    // Truncate review text to 180 chars
    const truncatedReview = $input.all().review_text.substring(0, 180);

    // Build Instagram caption (max 2200 chars)
    const caption = `🌟 Chia sẻ tích cực từ khách hàng ${$input.all().reviewer_name}:\n\n${truncatedReview}\n\n#${$input.all().reviewer_name} #${$input.all().review_text.split(' ')[0]} #BrandedSocialProof`;

    // Return payload for Bannerbear
    return {
      json: {
        reviewer_name: $input.all().Reviewer_Name,
        review_text: truncatedReview,
        caption: caption
      }
    };
    ```

- **Code Merge Upload and Caption1**:
  - **JavaScript**:
    ```javascript
    // Merge CDN URL and caption
    return {
      json: {
        card_image_url: $input.all().public_url,
        caption: $input.all().json.caption,
        reviewer_name: $input.all().json.reviewer_name
      }
    };
    ```

##### **C. Node Airtable Mark as Posted1**
- **Base ID**: `{{ $env.AIRTABLE_BASE_ID }}`.
- **API Key**: `{{ $env.AIRTABLE_API_KEY }}`.
- **Record ID**: Lấy từ `{{ $input.all().id }}` (ID của review từ Airtable).
- **Update Fields**:
  ```json
  {
    "fields": {
      "Posted": true,
      "Instagram Post ID": "{{ $input.all().json.post_id }}",
      "Posted At": "{{ $now('YYYY-MM-DD HH:mm:ss') }}",
      "Card Image URL": "{{ $input.all().json.card_image_url }}"
    }
  }
    ```

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm Log Lịch Sử**:
   - Sử dụng **Sticky Note** để ghi lại lỗi hoặc thông tin debug (ví dụ: nếu Bannerbear thất bại).
   - **Node StickyNote** có thể thêm vào sau `IF Image Ready1` để ghi log.

2. **Kết Nối Slack với Notifications Chi Tiết**:
   - Thêm **Slack Block Kit** để hiển thị hình ảnh bài đăng trong Slack (sử dụng `attachments` trong message).

3. **Tự Động Xóa Bài Đăng Sau Thời Gian**:
   - Thêm **node Airtable** để xóa bài đăng sau 30 ngày (nếu không cần lưu lại).

4. **Kết Hợp với Google Drive**:
   - Thay vì UploadToURL, có thể **upload hình ảnh lên Google Drive** và lấy link chia sẻ.

5. **Báo Cáo Hàng Tuần**:
   - Sử dụng **node ScheduleTrigger** khác để gửi báo cáo tổng hợp số bài đăng/tuần lên Slack/Email.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, đồng thời **tăng cường hiệu quả marketing** với proof social tự động hóa. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động **24/7** mà không cần can thiệp.

**Bắt đầu ngay!**
1. **Chuẩn bị tài khoản** (Airtable, Instagram, Bannerbear, Slack).
2. **Import workflow** và cấu hình credentials.
3. **Bật Active** và theo dõi kết quả trên Slack.

**💡 Lời khuyên cuối cùng:**
Nếu gặp lỗi, hãy kiểm tra:
- **Credentials** có đúng không?
- **Template Bannerbear** có layer trùng khớp không?
- **Instagram API Token** có quyền đầy đủ không?

**Chúc các sếp thành công!** 🚀