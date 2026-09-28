---
title: "🚀 Tự Động Hóa Tải Lên Video Instagram Reels lên YouTube Với Giữa Khoảng Thời Gian Được Đặt Lịch"
description: "Workflow tự động hóa hoàn toàn không cần code để tải lên video Reels từ Instagram lên YouTube với thời gian chờ giữa các upload được cấu hình, giúp tối ưu hóa chiến dịch content và tránh vi phạm chính sách YouTube."
slug: "tieu-dong-hoa-tai-len-video-instagram-reels-len-youtube"
tags: [n8n, automation, social-media, youtube, instagram, no-code, ai-multimodal]
keywords: [n8n workflow instagram youtube, tự động hóa tải video, upload reels lên youtube tự động, công cụ tự động hóa content, tối ưu hóa video marketing]
---

# 🚀 **Tự Động Hóa Tải Video Instagram Reels lên YouTube Với Giữa Khoảng Thời Gian Được Đặt Lịch**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Bạn đã bao giờ phải **tải video Reels từ Instagram lên YouTube thủ công**, mất nhiều thời gian và dễ bị quên hoặc vi phạm chính sách YouTube về **tần suất upload quá nhanh**? Hoặc bạn muốn **tối ưu hóa chiến dịch content** bằng cách chia nhỏ video thành nhiều phần với khoảng cách thời gian giữa các upload?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tải tự động** video Reels từ Instagram lên YouTube **không cần code**
✅ **Chia nhỏ upload** với khoảng thời gian giữa các video được cấu hình (ví dụ: 15 phút/1 giờ/ngày)
✅ **Lọc video duy nhất** (không trùng lặp) bằng cơ chế **deduplication**
✅ **Tự động thêm tiêu đề, thẻ, mô tả** từ Instagram (có thể tùy chỉnh)
✅ **Tuân thủ COPPA** và chính sách YouTube (độ tuổi, quyền riêng tư)

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tải video một một, tự động hóa toàn bộ quy trình.
- **Tối ưu SEO YouTube**: Tự động thêm thẻ từ hashtag Instagram và mô tả chi tiết.
- **Tránh bị shadowban**: YouTube không bị cảnh báo về **tần suất upload quá cao**.
- **Dễ dàng quản lý content**: Tất cả cấu hình tập trung ở **một node Configuration**, không cần spreadsheet phức tạp.
- **Hoạt động 24/7**: Chạy tự động theo lịch trình (daily/weekly) mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Instagram Business/Creator** (có API access):
   - **Bearer Token** (để fetch video từ Instagram).
   - *Lưu ý*: Instagram Graph API yêu cầu **đăng ký developer** và **đăng ký app** trên [Meta Developer Portal](https://developers.facebook.com/).
2. **Tài khoản YouTube** (đã kết nối với Google OAuth2):
   - **OAuth2 API Key** (để upload video lên YouTube).
3. **Bảng dữ liệu (Data Table)** để lưu trữ danh sách video đã upload:
   - Cột: `postId` (ID video Instagram) và `youtubeId` (ID video YouTube).
4. **Cấu hình cơ bản** trong node **Configuration** (xem chi tiết dưới đây).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12773](https://n8n.io/workflows/12773) hoặc copy toàn bộ JSON từ trang này.
- **Dán vào n8n Editor** (trong tab **Import Workflow**).
- **Chọn phiên bản n8n** phù hợp (n8n 1.x hoặc 2.x).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **14 node** quan trọng, các sếp cần chú ý cấu hình sau:

##### **A. Node "Configuration" (Cấu Hình Chính)**
- Mở node này và chỉnh sửa JSON theo mẫu sau (để phù hợp với chiến dịch của bạn):
  ```json
  {
    "includeSourceLink": true,    // Thêm link Instagram vào mô tả (true/false)
    "waitTimeoutSeconds": 900,    // Giữa khoảng thời gian giữa các upload (900s = 15 phút)
    "maxTitleLength": 100,        // Độ dài tối đa tiêu đề (tránh bị cắt)
    "categoryId": "24",           // ID danh mục YouTube (24 = Entertainment)
    "privacyStatus": "public",    // Trạng thái quyền riêng tư (public/private/unlisted)
    "notifySubscribers": false,   // Gửi thông báo khi upload (true/false)
    "defaultLanguage": "en",      // Ngôn ngữ mặc định video
    "ageRestricted": false        // Bật nếu video dành cho người trên 18 tuổi
  }
  ```
  - **Lưu ý**:
    - `waitTimeoutSeconds`: Điều chỉnh để tránh bị YouTube cảnh báo (khuyến nghị **≥ 900s**).
    - `categoryId`: Tham khảo [danh sách ID danh mục YouTube](https://developers.google.com/youtube/v3/docs/videoCategories/list) (ví dụ: 22 = People & Blogs, 20 = Gaming).

##### **B. Node "Fetch Instagram Posts" (Lấy Video từ Instagram)**
- **Credentials**: Chọn **httpBearerAuth** (đã cấu hình Bearer Token từ Instagram API).
- **URL Example**:
  ```
  https://graph.instagram.com/me/media?fields=id,caption,media_type,media_url,permalink&access_token={YOUR_ACCESS_TOKEN}
  ```
- **Headers**:
  - `Authorization: Bearer {YOUR_ACCESS_TOKEN}`
  - `Content-Type: application/json`

##### **C. Node "Data Table" (Deduplication)**
- **Tạo bảng mới** với 2 cột:
  - `postId` (ID video Instagram)
  - `youtubeId` (ID video YouTube sau khi upload)
- **Mục đích**: Tránh upload lại video đã tồn tại.

##### **D. Node "YouTube" (Upload Video)**
- **Credentials**: Chọn **youTubeOAuth2Api** (đã cấu hình OAuth2 từ Google).
- **Key Parameters**:
  - `operation`: `upload`
  - `resource`: `video`
- **Tham số tự động thêm**:
  - **Tiêu đề**: Lấy từ caption Instagram (hoặc tùy chỉnh).
  - **Thẻ**: Chuyển đổi từ hashtag Instagram.
  - **Mô tả**: Nếu `includeSourceLink: true`, sẽ thêm link Instagram.

##### **E. Node "Wait" (Đợi Giữa Khoảng Thời Gian)**
- **Thời gian đợi**: Được cấu hình trong **Configuration** (`waitTimeoutSeconds`).
- **Mục đích**: Tránh upload quá nhanh, tránh bị YouTube cảnh báo.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với 1-2 video mẫu để kiểm tra:
   - Video có được tải lên YouTube không?
   - Thẻ/titlle/mô tả có đúng không?
   - Giữa khoảng thời gian giữa các upload có hoạt động không?
2. **Bật Active** workflow và **lưu lại**.
3. **Kích hoạt Schedule Trigger** (nếu muốn chạy theo lịch):
   - Mở node **Schedule Trigger** và chọn **Daily/Weekly** (ví dụ: chạy hàng ngày lúc 8h sáng).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TIỆN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau **Upload to YouTube** để thông báo khi video đã upload thành công.
   - Ví dụ: `{"text": "Video đã upload lên YouTube: {{$node["Upload to YouTube"].json["snippet"]["title"]}}"}`

2. **Lưu Log Upload**:
   - Thêm node **Google Sheets** hoặc **Airtable** sau **Save Upload Record** để theo dõi lịch sử upload.

3. **Tự động thêm Thumbnail**:
   - Sử dụng node **Image Processing** (n8n-nodes-base.image) để cắt ảnh từ video Reels làm thumbnail.

4. **Chia nhỏ video dài**:
   - Nếu video Reels dài >15 phút, sử dụng **n8n-nodes-base.video** để cắt thành nhiều phần trước khi upload.

5. **Tùy chỉnh mô tả**:
   - Sử dụng node **Code** trong **Process Title and Tags** để thêm mô tả chi tiết từ một file JSON hoặc API khác.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi công việc **tải video thủ công**, đồng thời **tối ưu hóa chiến dịch content** bằng cách:
✔ **Tự động hóa toàn bộ quy trình** (không cần code).
✔ **Tránh vi phạm chính sách YouTube** với thời gian chờ giữa các upload.
✔ **Tự động thêm thẻ/tiêu đề** từ Instagram.
✔ **Dễ dàng mở rộng** với Slack, Google Sheets, hoặc AI (nếu cần phân tích video).

**🚀 Hành động ngay**:
1. **Cài đặt n8n trên VPS** để workflow chạy 24/7 (không phụ thuộc vào máy tính cá nhân).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Schedule Trigger** để tự động hóa từ ngày mai!

---
:::note[CHÚ Ý CUỐI CUNG]
- **Instagram API có giới hạn**: Nếu tài khoản Instagram của bạn bị hạn chế, workflow sẽ không hoạt động. Đăng ký lại **Bearer Token** mới trên [Meta Developer Portal](https://developers.facebook.com/).
- **YouTube API cũng có hạn chế**: Đăng ký **OAuth2** mới nếu gặp lỗi `quotaExceeded`.
- **Nếu video không upload được**, kiểm tra:
  - **Dung lượng video** (YouTube cho phép tối đa 128GB).
  - **Độ phân giải** (khuyến nghị ≥720p).
  - **Nội dung phù hợp** (không có spam, bạo lực, nội dung nhạy cảm).
:::