---
title: "🚀 Tự Động Hóa Scrape Tin AI Từ Nhiều Nguồn Sang Markdown & Google Drive (Không Cần Code)"
description: "Workflow này tự động scrape tin tức AI từ Google News, Blog OpenAI và các nguồn khác, chuyển đổi thành file Markdown và lưu trữ trên Google Drive hàng ngày. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường và cập nhật thông tin nhanh chóng."
slug: "tieu-dong-hoa-scrape-tin-ai-sang-markdown-google-drive"
tags: [n8n, automation, market-research, ai-research, google-drive, rss-scraping]
keywords: [n8n workflow scrape tin tức AI, tự động hóa nghiên cứu thị trường, chuyển đổi tin tức sang Markdown, lưu trữ tin tức trên Google Drive, RSS.app]
---

# 🚀 **Tự Động Hóa Scrape Tin AI Từ Nhiều Nguồn Sang Markdown & Google Drive**

### **Giải pháp cho các sếp muốn cập nhật tin tức AI hàng ngày mà không tốn thời gian thủ công**
Hàng ngày, các sếp phải mất nhiều thời gian để tra cứu tin tức về AI từ nhiều nguồn khác nhau (Google News, Blog OpenAI, các trang chuyên ngành) để nghiên cứu thị trường. **Workflow này tự động hóa toàn bộ quá trình:**
- Scrape tin tức từ **Google News** và **Blog OpenAI** (hoặc các nguồn RSS khác).
- **Scrape nội dung chi tiết** từ URL bằng API Firecrawl (không cần code).
- **Chuyển đổi thành file Markdown** (định dạng dễ đọc, chia sẻ và lưu trữ).
- **Lưu trữ tự động** trên **Google Drive** với định dạng rõ ràng, sắp xếp theo ngày.

Không cần viết một dòng code nào, chỉ cần **import workflow và cấu hình vài bước**, bạn đã có được một **công cụ nghiên cứu AI 24/7**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công hàng ngày.
- **Dữ liệu chính xác**: Scrape từ nguồn chính thức (Google News, OpenAI).
- **Định dạng chuyên nghiệp**: File Markdown dễ đọc, chia sẻ và lưu trữ.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày (cấu hình lịch).
- **Lưu trữ an toàn**: Tất cả tin tức được lưu trên Google Drive, sắp xếp theo ngày.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản RSS.app** (để lấy feed từ Google News và Blog OpenAI).
   - [Tạo tài khoản miễn phí RSS.app](https://rss.app/) (hoặc sử dụng nguồn RSS khác).
2. **API Key Firecrawl** (để scrape nội dung chi tiết từ URL).
   - [Đăng ký API Firecrawl](https://firecrawl.io/) (miễn phí cho một số lượng scrape hạn chế).
3. **Credentials Google Drive OAuth2**:
   - Cấu hình **Google Drive API** trong n8n để upload file Markdown.
   - Hướng dẫn: [Cài đặt Google Drive OAuth2 trong n8n](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.googleDrive/#credentials).
4. **Credentials HTTP Header Auth** (để kết nối với Firecrawl API).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [link gốc](https://n8n.io/workflows/5416).
- Trong **n8n Editor**, chọn **"Import"** → Chọn file JSON vừa tải.
- Hoặc **copy/paste** nội dung JSON vào ô **"Import from JSON"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **3 phần chính**, các sếp cần cấu hình kỹ lưỡng:

##### **A. Cấu hình nguồn RSS (Google News & Blog OpenAI)**
- **Node `fetch_google_news_feed`** và `fetch_blog_open_ai_feed`:
  - Thay đổi **URL RSS** trong `Method` thành:
    - Google News: `https://news.google.com/rss/search?q=AI&hl=en-US&gl=US&ceid=US:en`
    - Blog OpenAI: `https://blog.openai.com/feed/` (hoặc nguồn RSS khác).
  - Đảm bảo **Method = GET** và **Headers** không thay đổi.

##### **B. Cấu hình API Firecrawl (scrape nội dung chi tiết)**
- **Node `scrape_url`**:
  - **Credentials**: Chọn `httpHeaderAuth` (đã tạo trước khi import).
  - **URL**: `https://api.firecrawl.co/scrape`
  - **Headers**:
    ```
    Authorization: Bearer <API_KEY_FIRECRAWL>
    Content-Type: application/json
    ```
  - **Body (JSON)**:
    ```json
    {
      "url": "{{$json.url}}",
      "render_js": true,
      "render_media": true
    }
    ```
    (Thay `{{$json.url}}` là URL từ tin tức được scrape từ RSS).

##### **C. Cấu hình Google Drive (upload Markdown)**
- **Node `upload_markdown`**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
  - **Folder ID**: Thay bằng **ID thư mục Google Drive** của bạn (tìm trong liên kết thư mục: `https://drive.google.com/drive/folders/<FOLDER_ID>`).
  - **File Name**: `AI_News_${$datetime.date('YYYY-MM-DD')}.md` (định dạng theo ngày).

##### **D. Cấu hình lịch chạy (Schedule Trigger)**
- **Node `google_news_trigger`** và `blog_open_ai_trigger`:
  - Thay đổi **Schedule** thành:
    - **Cron**: `0 0 * * *` (chạy hàng ngày lúc 00:00 giờ Việt Nam).
    - Hoặc chọn **Time Zone** là `Asia/Ho_Chi_Minh`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** cho từng node để kiểm tra kết quả.
   - Kiểm tra file Markdown được tạo ra có nội dung chính xác không.
2. **Bật Active**:
   - Đánh dấu workflow thành **"Active"** để chạy tự động theo lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm nguồn RSS khác**:
   - Sử dụng các nguồn RSS như **Hugging Face Blog**, **DeepLearning.AI**, **AI News** để mở rộng dữ liệu.
2. **Lưu log scrape**:
   - Thêm **node `set`** sau `scrape_url` để lưu URL đã scrape thành công vào Google Sheets.
3. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Slack/Email** để thông báo khi có tin tức mới.
4. **Tự động chia sẻ file Markdown**:
   - Sử dụng **Google Drive API** để chia sẻ file với team hoặc khách hàng.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **cập nhật tin tức AI hàng ngày một cách tự động, chính xác và chuyên nghiệp**. Bằng cách **scrape từ nhiều nguồn**, **chuyển đổi sang Markdown** và **lưu trữ trên Google Drive**, bạn đã có một **công cụ nghiên cứu thị trường AI 24/7** mà không cần viết code.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình các credentials** (RSS, Firecrawl, Google Drive).
3. **Bật Active** và để workflow làm việc cho bạn!

**Cần hỗ trợ?** Đăng ký **VPS n8n** để chạy workflow ổn định 24/7:
👉 [TinoHost (Mã giảm giá: VPSN8N)](https://tino.vn/vps-n8n?affid=388)