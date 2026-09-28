---
title: "🚀 Tự Động Chuyển RSS Sang Tweet Có Ảnh Và Văn Bản (Miễn Phí) - N8n + AI"
description: "Workflow tự động hóa chuyển đổi bài viết từ RSS thành tweet có hình ảnh và văn bản tóm tắt bằng AI, tiết kiệm thời gian cho các sếp marketing 100% miễn phí với Twitter API v1."
slug: "tieu-dong-chuyen-rss-sang-tweet-co-anh"
tags: [n8n, automation, marketing, ai, twitter-api, rss-to-tweet]
keywords: [n8n workflow tự động hóa, chuyển đổi rss thành tweet, tweet tự động có ảnh, ai marketing, twitter api v1 tự động]
---

# 🚀 **Tự Động Chuyển RSS Sang Tweet Có Ảnh & Văn Bản Tóm Tắt - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Marketing**
Các sếp thường phải:
- **Lọc thủ công** bài viết từ RSS feed để chọn những nội dung hot nhất.
- **Tóm tắt** bài viết dài thành tweet ngắn gọn (không quá 280 ký tự).
- **Tải ảnh** từ bài viết và **nén kích thước** phù hợp với Twitter.
- **Tweet thủ công** mỗi ngày, mất thời gian và dễ bỏ lỡ cơ hội.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy bài viết mới nhất** từ RSS feed.
✅ **Tóm tắt văn bản** bằng AI (OpenRouter).
✅ **Trích xuất ảnh chính** từ bài viết.
✅ **Nén ảnh** và **upload lên Twitter** cùng với tweet tự động.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 giờ/tuần** cho việc tweet thủ công.
- **Tweet chuyên nghiệp** với ảnh đẹp và nội dung tóm tắt chính xác.
- **Tăng tương tác** nhờ bài viết được AI tóm tắt hấp dẫn.
- **Hoạt động liên tục** ngay cả khi các sếp nghỉ ngơi.
- **Miễn phí** (sử dụng Twitter API v1 và mô hình AI miễn phí).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Twitter (X)** và **API Key** của Twitter (v1).
   - [Cách tạo API Key Twitter](https://developer.twitter.com/en/portal/dashboard) (đăng ký với tài khoản cá nhân hoặc doanh nghiệp).
2. **RSS Feed** của blog/news muốn tweet (ví dụ: RSS của TechCrunch, VnExpress, hoặc blog cá nhân).
3. **Mô hình AI miễn phí** (OpenRouter) để tóm tắt bài viết.
   - [Đăng ký OpenRouter](https://openrouter.ai/) (miễn phí với giới hạn request).
4. **VPS Self-hosted n8n** (không dùng n8n.cloud để tránh giới hạn request).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2933) hoặc copy JSON từ editor n8n.
- **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **10 node**, các sếp cần chú ý cấu hình **các node sau**:

##### **A. Node "Get the latest article from the feed" (RSS Feed Read Trigger)**
- **Tham số cần điền:**
  - **Feed URL:** Nhập RSS feed của blog/news (ví dụ: `https://feeds.bbci.co.uk/news/rss.xml`).
  - **Max Items:** Đặt số lượng bài viết lấy mỗi lần (gợi ý: **5**).

##### **B. Node "Fetches the article’s HTML content" (HTTP Request)**
- **Tham số cần điền:**
  - **Method:** `GET`.
  - **URL:** `{json["$url"]}` (được tự động lấy từ RSS feed).
  - **Headers:** Thêm `User-Agent: Mozilla/5.0`.

##### **C. Node "Extracts the main image" (HTML)**
- **Tham số cần điền:**
  - **Selector:** `img[src*="."]` (lấy ảnh có trong thẻ `<img>`).
  - **Attribute:** `src`.

##### **D. Node "AI Agent" (Agent)**
- **Tham số cần điền:**
  - **Prompt:** Sử dụng template mặc định (AI sẽ tự động tóm tắt bài viết).
  - **Model:** Chọn mô hình **OpenRouter** (ví dụ: `mistralai/Mistral-7B-Instruct-v0.1`).

##### **E. Node "OpenRouter Chat Model" (lmChatOpenRouter)**
- **Tham số cần điền:**
  - **API Key:** Nhập API Key từ OpenRouter.
  - **Model:** Chọn mô hình miễn phí (ví dụ: `openai/gpt-3.5-turbo`).
  - **Prompt:** `{json["summary_prompt"]}` (được truyền từ node AI Agent).

##### **F. Node "Upload image to X server with Twitter API v1" (HTTP Request)**
- **Tham số cần điền:**
  - **Method:** `POST`.
  - **URL:** `https://upload.twitter.com/1.1/media/upload.json`.
  - **Headers:**
    - `Authorization: Bearer {twitter_api_key}`.
    - `Content-Type: multipart/form-data`.
  - **Body:**
    - `media_data`: `{json["image_data"]}` (ảnh đã tải từ node "Downloads image").
    - `media_category`: `tweet_image`.

##### **G. Node "Verify tweet constraints" (If)**
- **Tham số cần điền:**
  - **Condition:** Kiểm tra tweet có **dưới 280 ký tự** và **ảnh hợp lệ**.
  - **Nếu sai:** Bỏ qua tweet (không tweet).

##### **H. Node "X" (Twitter)**
- **Tham số cần điền:**
  - **API Key:** Nhập API Key Twitter.
  - **Status:** `{json["tweet_text"]}` (văn bản tweet).
  - **Media IDs:** `{json["media_id"]}` (ID ảnh đã upload).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **"Run Once"** để kiểm tra workflow với 1 bài viết mẫu.
- **Active Workflow:** Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tweet định kỳ:** Sử dụng **n8n Schedule Node** để tweet vào giờ cố định (ví dụ: 8h sáng).
2. **Lưu log tweet:** Kết nối với **Google Sheets** hoặc **Notion** để lưu lịch sử tweet.
3. **Gửi báo cáo Slack:** Sử dụng **Slack Node** để thông báo khi tweet thành công/thất bại.
4. **Tối ưu ảnh:** Sử dụng **node Image Resize** để nén ảnh trước khi upload.
5. **Dùng nhiều RSS feed:** Kết hợp nhiều RSS feed vào 1 workflow bằng **Multi-RSS Trigger**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing, giúp họ **tweet chuyên nghiệp** với nội dung tóm tắt và ảnh đẹp **không cần code**. **Chỉ cần setup 1 lần**, workflow sẽ hoạt động tự động mỗi ngày!

**Hành động ngay:**
1. **Chuẩn bị VPS** (n8n self-hosted) và API keys.
2. **Import workflow** và cấu hình các node quan trọng.
3. **Active workflow** và bắt đầu tweet tự động!

👉 **Bắt đầu tự động hóa marketing của mình ngay hôm nay!** 🚀