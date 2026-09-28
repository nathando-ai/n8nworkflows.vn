---
title: "🚀 Tự Động Chuyển Bài Đăng LinkedIn thành X (Twitter) với AI Claude, Apify & Airtable - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp chuyển đổi bài đăng LinkedIn thành tweet cá nhân hóa, thread chuyên nghiệp và carousel tự động, tiết kiệm 10+ giờ công/tháng. Kết hợp AI Claude, Apify scraping và Airtable quản lý - hoạt động 24/7."
slug: "tieu-dong-chuyen-doi-linkedin-sang-twitter-voi-ai-claude-apify-airtable"
tags: [n8n, automation, social-media, ai-claude, airtable, twitter-automation, apify-scraping]
keywords: [n8n workflow tự động hóa LinkedIn sang Twitter, AI Claude tự động tweet, Apify scraping LinkedIn, Airtable quản lý nội dung, tự động hóa content marketing, tự động hóa social media]
---

# 🚀 **Tự Động Chuyển Bài Đăng LinkedIn thành X (Twitter) với AI & Airtable**

## **Nỗi Đau Của Các Sếp**
- **Thủ công chuyển đổi nội dung**: Mỗi bài LinkedIn mất 15-30 phút để viết thành tweet hoặc thread, lãng phí thời gian quý giá.
- **Không đồng bộ nội dung**: Bài đăng LinkedIn không được tái sử dụng trên Twitter, gây lãng phí nội dung giá trị.
- **Không cá nhân hóa**: Tweet tự động thường thiếu tone phù hợp với brand hoặc cá nhân.
- **Quản lý nội dung rối loạn**: Không theo dõi trạng thái bài đăng (chờ duyệt, đã tweet, lỗi...).

**Workflow này giải quyết tất cả!** Sử dụng **AI Claude** để chuyển đổi nội dung, **Apify** để lấy bài đăng LinkedIn, và **Airtable** để quản lý - tất cả tự động hóa **100% không cần code**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần viết tweet thủ công.
- **Nội dung cá nhân hóa**: AI Claude chuyển đổi bài LinkedIn thành tone phù hợp với brand.
- **Thread chuyên nghiệp**: Tự động tạo chuỗi tweet (3-7 tweet) từ 1 bài LinkedIn.
- **Quản lý trung tâm**: Airtable theo dõi trạng thái (chờ duyệt, đã tweet, lỗi...).
- **Hoạt động liên tục**: Schedule tự động chạy hàng tuần (Thứ 7) và hàng ngày (12:30).
- **Tweet ngay lập tức**: Nhấp nút "TWEET NOW" trong Airtable để đăng tweet bất kỳ lúc nào.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [Apify](https://console.apify.com/) (để lấy bài đăng LinkedIn).
   - [OpenAI](https://platform.openai.com/) (để xử lý carousel/PDF).
   - [OpenRouter](https://openrouter.ai/) (để sử dụng AI Claude).
   - [Twitter API](https://developer.twitter.com/) (đăng tweet).
   - [Airtable](https://airtable.com/) (quản lý bài đăng và tweet).

2. **Bảng Airtable**:
   - Tạo **3 bảng** trong Airtable:
     - `Config`: Cấu hình URL LinkedIn, ngày tweet, số bài đăng lấy.
     - `LK Posts`: Lưu bài đăng LinkedIn sau khi lấy.
     - `X Tweets`: Lưu tweet đã tạo và trạng thái.
   - **Hoặc sao chép từ mẫu**: [Airtable Template](https://airtable.com/appiS2JpMdnxAS5o4/shrXh9iXTnL9fX63L/tbl7B3JblukFTGrAo/viwgajzRGnydUDjnw).

3. **Cấu hình Webhook**:
   - Cài đặt nút "TWEET NOW" trong Airtable với URL:
     ```plaintext
     https://your-n8n-server-url/webhook/post-tweet?id=RECORD_ID()
     ```

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12847](https://n8n.io/workflows/12847).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **40 node** phức tạp, nhưng chỉ cần chú ý đến các node quan trọng sau:

##### **A. Cấu Hình API & Credentials**
| Node | Yêu Cầu | Ghi Chú |
|------|----------|----------|
| **ScrapeLastPosts** (Apify) | Thêm `apifyApi` (API Key từ Apify) | Dùng actor `A3cAPGpwBEG8RJwse` (giá $2/1k bài đăng). |
| **Claude-4.5-Sonnet** (OpenRouter) | Thêm `openRouterApi` (API Key) | Model: `anthropic/claude-sonnet-4.5`. |
| **ExtractContentFromFile** (OpenAI) | Thêm `openAiApi` (API Key) | Dùng để xử lý carousel/PDF. |
| **PostStandaloneTweet** & **PostReplyTweet** (Twitter) | Thêm `twitterOAuth2Api` (Bearer Token) | Cấu hình từ Twitter Developer Portal. |
| **Airtable** (tất cả node) | Thêm `airtableTokenApi` (API Key) | Lấy từ Airtable → Settings → API. |

##### **B. Cấu Hình Airtable**
- **Bảng `Config`**:
  - Điền `linkedinProfileUrl` (URL LinkedIn cá nhân).
  - Cấu hình `schedule_tweets_days_after_lk` (số ngày chờ trước khi tweet).
  - Cấu hình `max_posts` (số bài đăng lấy mỗi tuần).

- **Bảng `LK Posts`**:
  - Cột `status` phải có giá trị `Pending` (mặc định).

- **Bảng `X Tweets`**:
  - Cột `status` có giá trị `Approved` (để tweet tự động).

##### **C. Cấu Hình Schedule**
- **Weekly_OnSunday**: Chạy vào **nửa đêm Thứ 7** để lấy bài LinkedIn mới.
- **Daily_AtNoon**: Chạy vào **12:30 PM** để tweet bài đã duyệt.

##### **D. Cấu Hình Webhook**
- Node **Webhook_OnPostTweet** phải có URL:
  ```plaintext
  https://your-n8n-server-url/webhook/post-tweet
  ```
- Kết nối với nút "TWEET NOW" trong Airtable (như hướng dẫn trên).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Execute Workflow** và chọn **Daily_AtNoon** (để test tweet mẫu).
  - Kiểm tra Airtable bảng `X Tweets` có xuất hiện tweet mới không.
- **Bật Active**:
  - Sau khi test thành công, chuyển trạng thái workflow thành **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tối ưu AI Claude**:
   - Edit node **ConvertPostIntoTweets** để thay đổi **prompt** phù hợp với brand:
     ```json
     {
       "prompt": "Convert this LinkedIn post into a professional Twitter thread (3-5 tweets). Keep the tone formal but engaging. Include key takeaways and a call-to-action.",
       "system": "You are a content expert specializing in Twitter threads."
     }
     ```

2. **Quản lý log**:
   - Thêm node **Slack/Telegram** để nhận thông báo lỗi:
     ```json
     {
       "type": "n8n-nodes-base.slack",
       "credentials": ["slackApi"],
       "keyParameters": {
         "text": "Workflow failed! Error: {{$json["error"]}}"
       }
     }
     ```

3. **Báo cáo tuần**:
   - Tạo một **Google Sheet** hoặc **Airtable Dashboard** để theo dõi:
     - Số bài LinkedIn lấy.
     - Số tweet đã tweet.
     - Tỷ lệ duyệt.

4. **Kết hợp với Notion**:
   - Lưu tweet đã tweet vào **Notion** bằng node **Notion API**:
     ```json
     {
       "type": "n8n-nodes-base.notion",
       "credentials": ["notionApi"],
       "keyParameters": {
         "page": {
           "title": [{{$node["GetTweet"].json["name"]}}],
           "properties": {
             "Status": "Tweeted",
             "URL": [{{$node["GetTweet"].json["url"]}}]
           }
         }
       }
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào nội dung chất lượng cao hơn, trong khi **AI và tự động hóa** làm việc 24/7. **Bắt đầu ngay** với những bước đơn giản:
1. **Import workflow** từ n8n.io.
2. **Cấu hình API** và Airtable.
3. **Test và bật Active**.

**🚀 Hãy tự động hóa content marketing của mình ngay hôm nay!** Nếu cần hỗ trợ, liên hệ với tác giả [Elodie Tasia](https://n8n.io/workflows/12847) để tùy chỉnh workflow phù hợp với brand của các sếp.