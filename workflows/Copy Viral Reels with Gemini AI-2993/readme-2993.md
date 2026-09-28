---
title: "🚀 Tự Động Hóa Copy & Phân Tích Reels Viral Sử Dụng Gemini AI - Giảm Thời Gian Làm Việc Gấp 10 Lần"
description: "Workflow tự động hóa lấy dữ liệu Reels viral từ Instagram, phân tích nội dung bằng Gemini AI, lưu trữ kết quả vào Airtable và tạo báo cáo tự động - giúp các sếp marketing tiết kiệm thời gian, tối ưu chiến dịch và ra quyết định dựa trên dữ liệu chính xác."
slug: "tieu-dong-hoa-copy-reels-viral-gemini-ai"
tags: [n8n, automation, ai, marketing, instagram, airtable, gemini-ai]
keywords: [tự động hóa marketing instagram, copy reels viral, gemini ai n8n, phân tích video viral, airtable automation, n8n workflow marketing]
---

# 🚀 **Tự Động Hóa Copy & Phân Tích Reels Viral Sử Dụng Gemini AI**

## **🔥 Nỗi Đau Của Các Sếp Marketing Hiện Nay**
Bạn đã từng phải:
- **Tốn nhiều giờ** để tìm kiếm và sao chép nội dung Reels viral từ Instagram?
- **Không biết cách phân tích** xem tại sao một video lại thành công?
- **Lưu trữ dữ liệu rải rác** trên nhiều sheet Excel hoặc Google Docs, khó theo dõi?
- **Phải làm thủ công** mỗi khi muốn cập nhật danh sách video mới?

**Workflow này giải quyết tất cả!** Với **Gemini AI** và **n8n**, bạn có thể:
✅ **Tự động lấy** Reels viral từ các creator nổi tiếng.
✅ **Phân tích nội dung** bằng trí tuệ nhân tạo để hiểu tại sao video thành công.
✅ **Lưu trữ dữ liệu** vào **Airtable** (hoặc Google Sheets) để theo dõi và báo cáo dễ dàng.
✅ **Chạy 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-20 giờ/tuần** so với cách làm thủ công.
- **Nắm bắt xu hướng** từ Reels viral nhanh chóng, áp dụng vào chiến dịch của mình.
- **Dữ liệu chính xác** được tự động phân tích và lưu trữ, không sai sót.
- **Hoạt động liên tục** (24/7) mà không cần giám sát.
- **Tối ưu nội dung** bằng cách học từ những video thành công nhất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Airtable** (để lưu trữ dữ liệu video và phân tích).
✔ **Tài khoản Apify** (để lấy dữ liệu Reels từ Instagram).
✔ **API Key của Gemini AI** (để phân tích nội dung video).
✔ **Tài khoản n8n** (self-hosted hoặc dùng miễn phí trên cloud).
✔ **Danh sách creator** (ID hoặc tên tài khoản Instagram) muốn theo dõi.
✔ **Prompt tùy chỉnh** (để Gemini AI phân tích video theo yêu cầu của bạn).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/2993](https://n8n.io/workflows/2993) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên browser hoặc self-hosted).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/2993](https://n8n.io/workflows/2993).
2. **Trên n8n Editor**, nhấn **"Import"** → **"Paste JSON"** → Dán và nhấn **"Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần 1: Lấy dữ liệu Reels từ Instagram** (sử dụng Apify).
- **Phần 2: Phân tích và lưu trữ** (sử dụng Gemini AI + Airtable).

#### **🔹 Bước 1: Cấu Hình Credentials (API Keys)**
| **Node** | **Tham Số Cần Chỉnh** | **Hướng Dẫn** |
|----------|----------------------|----------------|
| **Apify - Fetch Reels** | `API Token` | Đăng nhập [Apify](https://apify.com/), tạo **API Token** và điền vào `Authorization: Bearer YOUR_TOKEN`. |
| **Gemini - Generate Upload URL** | `API Key` | Đăng ký [Google AI Studio](https://makersuite.google.com/), tạo **API Key** và điền vào `Authorization: Bearer YOUR_GEMINI_KEY`. |
| **Gemini - Upload File & Ask Questions** | `API Key` | Giống như trên, sử dụng cùng **API Key Gemini**. |
| **Airtable** | `Airtable API Key` | Tạo **API Key** từ [Airtable](https://airtable.com/api) và chọn `airtableTokenApi` trong n8n. |

#### **🔹 Bước 2: Cấu Hình Dữ liệu Input**
1. **Node "Apify - Fetch Reels"**:
   - Điền **ID hoặc tên creator** bạn muốn theo dõi (ví dụ: `tiktok`, `influencer_name`).
   - Tham số `query` có thể là:
     ```json
     {
       "startUrl": "https://www.instagram.com/reels/search/?query=trending",
       "maxItems": 50
     }
     ```
   - **Lưu ý**: Nếu lấy từ danh sách creator cụ thể, thay đổi `query` thành:
     ```json
     {
       "startUrl": "https://www.instagram.com/creator_name/reels/",
       "maxItems": 20
     }
     ```

2. **Node "Set Prompt"**:
   - **Prompt mẫu** để Gemini AI phân tích video:
     ```plaintext
     Analyze this Instagram Reel and provide insights on:
     1. Why is this video viral? (Content, hook, editing style)
     2. What are the key elements that make it engaging?
     3. Suggest improvements for similar videos.
     4. What is the best time to post this type of content?
     ```
   - **Tùy chỉnh prompt** theo nhu cầu của bạn (ví dụ: phân tích âm nhạc, thẻ hashtag, thời lượng video).

3. **Node "Airtable" (Create/Update/Read)**:
   - **Table Name**: Đặt tên bảng trong Airtable (ví dụ: `Viral_Reels_Analysis`).
   - **Fields cần tạo** (nếu chưa có):
     - `Video_URL` (liên kết Reels)
     - `Creator` (tên creator)
     - `Likes` (số like)
     - `Views` (số view)
     - `Analysis` (kết quả từ Gemini AI)
     - `Guideline` (hướng dẫn từ AI)

#### **🔹 Bước 3: Cấu Hình Schedule (Chạy Tự Động)**
- **Node "Schedule Trigger"**:
  - Chọn **thời gian chạy** (ví dụ: **mỗi ngày 8h sáng**).
  - **Lưu ý**: Nếu muốn chạy thủ công, bỏ qua node này và kích hoạt **Execute Workflow Trigger**.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra không có lỗi):
   - Nhấn **"Run Workflow"** và chọn **1-2 video mẫu**.
   - Kiểm tra kết quả trong **Airtable** và **Gemini AI response**.
2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Hợp Với Slack/Telegram**
- **Thêm node "Slack Webhook"** sau khi **Gemini phân tích xong** để thông báo kết quả.
- **Cấu hình**:
  - Tạo **Incoming Webhook** trên Slack.
  - Điền URL vào node **Slack** với nội dung:
    ```json
    {
      "text": "🚀 New Viral Reel Analysis:\n{{ $node["Gemini - Ask Questions"].json["result"] }}"
    }
    ```

### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Thêm node "Google Sheets"** để lưu lịch sử phân tích.
- **Cấu hình**:
  - Tạo sheet mới với các cột: `Date`, `Video_URL`, `Creator`, `Analysis`.
  - Sử dụng node **Google Sheets (Create Row)** sau khi **Airtable update**.

### **3. Tối ưu Prompt cho Kết Quả Chất Lượng**
- **Ví dụ prompt nâng cao**:
  ```plaintext
  Analyze this Reel and provide:
  1. **Content Breakdown**: Script, visuals, music used.
  2. **Engagement Metrics**: Why likes/comments/shares are high.
  3. **Hashtag Strategy**: Best hashtags to use for similar content.
  4. **Posting Time Suggestion**: Best days/hours based on Instagram Insights.
  5. **Competitor Comparison**: How this video compares to top 3 Reels in the same niche.
  ```
- **Lưu ý**: Gemini AI trả lời tốt nhất khi **prompt cụ thể và ngắn gọn**.

### **4. Xử Lý Lỗi Hiện Đang**
| **Lỗi Thường Gặp** | **Giải Pháp** |
|---------------------|---------------|
| **Gemini API limit** | Đăng ký **API Key mới** hoặc tăng limit trong Google Cloud. |
| **Apify không lấy được dữ liệu** | Kiểm tra `startUrl` và `maxItems`, thử lại sau 24h (Instagram có rate limit). |
| **Airtable không update** | Kiểm tra **credentials** và **table name** trong node Airtable. |
| **Video không tải được** | Thay đổi **URL video** trong node **Download File**. |

---

## **📌 Kết Luận**
Workflow **Copy Viral Reels with Gemini AI** là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✔ **Tự động hóa** quá trình phân tích Reels viral.
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược nội dung.
✔ **Lưu trữ dữ liệu** một cách chuyên nghiệp trong Airtable.
✔ **Ra quyết định** dựa trên phân tích AI chính xác.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình credentials** và **prompt**.
3. **Bật Schedule Trigger** để chạy tự động.
4. **Theo dõi kết quả** trong Airtable và áp dụng vào chiến dịch!

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa marketing!** 🚀