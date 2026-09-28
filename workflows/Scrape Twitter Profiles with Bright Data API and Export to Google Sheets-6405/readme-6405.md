---
title: "🚀 Tự Động Scrape Dữ Liệu Twitter Tất Tần Tật & Xuất Ra Google Sheets (Không Code!)"
description: "Workflow tự động hóa scrape profile Twitter chi tiết (tweet, user stats, media) bằng Bright Data API và xuất dữ liệu vào Google Sheets với định dạng chuyên nghiệp. Giúp các sếp tiết kiệm 10+ giờ/tháng so với phương pháp thủ công."
slug: "tieu-dong-scrape-twitter-va-xuat-google-sheets"
tags: ["n8n", "automation", "market-research", "bright-data", "google-sheets", "social-media"]
keywords: ["scrape twitter n8n", "tự động hóa scrape twitter", "bright data api n8n", "export twitter data google sheets", "tự động hóa nghiên cứu thị trường"]
---

# 🚀 **Scrape Dữ Liệu Twitter Chi Tiết & Xuất Ra Google Sheets (Không Code!)**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải **tìm hiểu chi tiết về profile Twitter của đối thủ, khách hàng hoặc nhân vật công ty** nhưng lại mất **từ 2-5 giờ** để scrape thủ công? Hoặc phải **lặp đi lặp lại** các công cụ như Phantombuster, Octoparse để lấy dữ liệu không đầy đủ?

**Workflow này sẽ:**
✅ **Scrape toàn bộ dữ liệu tweet** (nội dung, media, hashtags, likes, replies...)
✅ **Lấy thông tin chi tiết về user** (followers, posts, verified status, profile image...)
✅ **Xuất dữ liệu vào Google Sheets** với **cấu trúc chuyên nghiệp**, sẵn sàng phân tích ngay.
✅ **Hoạt động 24/7 tự động**, không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị giới hạn request** của Bright Data, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với phương pháp scrape thủ công.
- **Dữ liệu đầy đủ & chính xác**, bao gồm **tweet, media, user stats, hashtags**.
- **Xuất ra Google Sheets** với **cấu trúc chuẩn**, dễ dàng phân tích bằng Excel/Google Data Studio.
- **Hoạt động tự động**, không cần can thiệp thủ công.
- **Không giới hạn request** (so với các công cụ scrape miễn phí).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (đăng ký tại [brightdata.com](https://brightdata.com/)) và **API Key**.
2. **Google Sheets OAuth 2.0 Credentials** (cài đặt trong n8n).
3. **Google Sheet mới** với **các cột sau** (đã chuẩn bị sẵn trong workflow):
   ```
   id | user_posted | name | description | date_posted | photos | quoted_post | tagged_users | replies | reposts | likes | views | hashtags | followers | posts_count | profile_image_link | following | is_verified | quotes | external_image_urls | videos | external_video_urls | user_id | timestamp
   ```

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6405](https://n8n.io/workflows/6405).
- **Nhấn "Import"** trong n8n Editor.
- **Hoặc copy/paste JSON** vào Editor và nhấn **"Create Workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **7 node chính**, các sếp cần cấu hình như sau:

##### **📥 Node 1: User Input Trigger (formTrigger)**
- **Không cần chỉnh**, dùng để **nhập URL Twitter và ngày range** khi kích hoạt workflow.

##### **🚀 Node 2: Trigger Twitter Scraping (httpRequest)**
- **URL:** `https://api.brightdata.com/scraper/api/v1/scrape`
- **Headers:**
  - `Authorization: Bearer <API_KEY_BRIGHT_DATA>`
  - `Content-Type: application/json`
- **Body (JSON):**
  ```json
  {
    "url": "{{ $node["User Input Trigger"].json["twitter_url"] }}",
    "scraper": "twitter",
    "scraperOptions": {
      "startDate": "{{ $node["User Input Trigger"].json["start_date"] }}",
      "endDate": "{{ $node["User Input Trigger"].json["end_date"] }}"
    }
  }
  ```
  *(Thay thế `twitter_url`, `start_date`, `end_date` từ form input.)*

##### **🔄 Node 3: Monitor Scraping Progress (httpRequest)**
- **URL:** `https://api.brightdata.com/scraper/api/v1/scrape/<SNAPSHOT_ID>/status`
  *(`<SNAPSHOT_ID>` sẽ được trả về từ node trước.)*
- **Headers:**
  - `Authorization: Bearer <API_KEY_BRIGHT_DATA>`
- **Lưu ý:** Node này **kiểm tra trạng thái scrape** (đang chạy hay đã hoàn thành).

##### **⏱️ Node 4: Delay Before Recheck (wait)**
- **Thời gian chờ:** `60000` (1 phút).
- **Lưu ý:** Workflow sẽ **chờ 1 phút** trước khi kiểm tra lại trạng thái scrape.

##### **✅ Node 5: Is Scraping Ready? (if)**
- **Điều kiện:** Kiểm tra `status` trong response Bright Data:
  - **Nếu `status === "ready"`** → Tiến đến node **Fetch Twitter Data**.
  - **Nếu `status === "running"`** → Lặp lại vòng kiểm tra.

##### **📦 Node 6: Fetch Twitter Data (httpRequest)**
- **URL:** `https://api.brightdata.com/scraper/api/v1/scrape/<SNAPSHOT_ID>/data`
  *(`<SNAPSHOT_ID>` từ node trước.)*
- **Headers:**
  - `Authorization: Bearer <API_KEY_BRIGHT_DATA>`
- **Lưu ý:** Node này **lấy toàn bộ dữ liệu tweet** sau khi scrape hoàn thành.

##### **📊 Node 7: Store Twitter Data in Google Sheet (googleSheets)**
- **Chọn Credentials:** `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Operation:** `append` (thêm dữ liệu mới vào sheet).
- **Sheet Name:** Điền tên sheet đã tạo trước.
- **Range:** `Sheet1!A1` (hoặc tùy chỉnh).
- **Lưu ý:**
  - **Cấu trúc dữ liệu phải khớp với cột trong sheet** (đã liệt kê ở trên).
  - **Nếu sheet chưa có dữ liệu**, workflow sẽ **tạo mới các cột tự động**.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với **một URL Twitter mẫu** (ví dụ: `https://twitter.com/ElonMusk`).
2. **Nhấn "Active"** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động scrape định kỳ** bằng **n8n Cron Trigger** (ví dụ: scrape hàng tuần).
2. **Gửi báo cáo tự động** vào Slack/Email khi scrape hoàn thành.
3. **Lưu log scrape** vào Google Drive hoặc Notion để theo dõi lịch sử.
4. **Kết hợp với LLM** (n8n-nodes-ai) để **tóm tắt nội dung tweet** tự động.
5. **Tạo dashboard** từ Google Sheets bằng **Google Data Studio** hoặc **Power BI**.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc scrape thủ công**, giúp **tiết kiệm thời gian, tăng hiệu suất nghiên cứu thị trường** và **cung cấp dữ liệu chi tiết, chính xác**.

**🚀 Hãy áp dụng ngay và bắt đầu scrape Twitter tự động hôm nay!**
*(Nếu có vấn đề, các sếp có thể comment dưới bài viết hoặc liên hệ tôi qua [tên tài khoản].)*

---
**🔹 Cần hỗ trợ cài đặt n8n trên VPS?**
👉 [Hướng dẫn chi tiết cài n8n trên VPS Linux](https://docs.n8n.io/hosting/installation/installation-on-linux/) *(tôi có thể viết bài hướng dẫn riêng nếu các sếp cần!)*