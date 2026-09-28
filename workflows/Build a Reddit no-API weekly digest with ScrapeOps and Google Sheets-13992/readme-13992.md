---
title: "📊 Tự Động Hoá Tóm Tắt Tuần Reddit (No-API) Với ScrapeOps & Google Sheets - Giải Pháp Market Research Cho Các Sếp"
description: "Workflow tự động hóa thu thập, xử lý và tổng hợp bài viết top từ các subreddit Reddit hàng tuần, tránh sử dụng API chính thức, đồng thời gửi báo cáo định kỳ qua email hoặc lưu vào Google Sheets. Giúp các sếp tiết kiệm thời gian theo dõi xu hướng thị trường, giảm thiểu công việc thủ công và đảm bảo dữ liệu chính xác, cập nhật 24/7."
slug: "tu-dong-hoa-tom-tat-tuan-reddit-scrapeops-google-sheets"
tags: [n8n, automation, market-research, scrapeops, google-sheets, no-code, email-automation]
keywords: [tự động hóa reddit, scrape reddit no api, market research tự động, tổng hợp bài viết reddit hàng tuần, n8n workflow reddit, tự động hóa google sheets]
---

# 🚀 **Tự Động Hoá Tóm Tắt Tuần Reddit (No-API) Với ScrapeOps & Google Sheets**

Hàng tuần, các sếp phải mất nhiều thời gian để theo dõi xu hướng thị trường, phân tích bài viết hot trên Reddit, và tổng hợp thông tin để ra quyết định. Thay vì phải thủ công vào từng subreddit, tìm kiếm bài viết top, và ghi chép lại dữ liệu, **workflow này tự động hóa toàn bộ quy trình** bằng cách:
- **Thu thập** bài viết top từ các subreddit được chọn (không cần API Reddit chính thức).
- **Xử lý** và enrich dữ liệu với nội dung đầy đủ của bài viết.
- **Deduplicate** tránh trùng lặp với dữ liệu cũ.
- **Tổng hợp** thành báo cáo tuần và gửi qua email hoặc lưu vào Google Sheets.
- **Hoạt động tự động** hàng tuần, không cần can thiệp của con người.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công vào từng subreddit hàng tuần.
- **Dữ liệu chính xác**: Tránh sai sót khi copy-paste hoặc bỏ sót bài viết.
- **Tự động hóa hoàn toàn**: Hoạt động hàng tuần mà không cần can thiệp.
- **Cá nhân hóa**: Chỉ thu thập từ các subreddit quan trọng cho ngành/niche của doanh nghiệp.
- **Báo cáo định kỳ**: Nhận email tổng hợp hoặc dữ liệu trong Google Sheets để phân tích.
- **Không phụ thuộc API**: Không bị giới hạn bởi API Reddit chính thức (có thể bị block hoặc thay đổi).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeOps**:
   - Đăng ký miễn phí tại [ScrapeOps](https://scrapeops.io/app/register/n8n).
   - Lấy **API Key** và thêm vào n8n dưới **Credentials** với tên `scrapeOpsApi`.
2. **Tài khoản Google Sheets**:
   - Tạo hoặc sao chép [mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1rKuVREV4pedie7uAbuEcLvghNrAEeAjIPUBE6cQPleI/edit?usp=sharing) để lưu trữ dữ liệu.
   - Cấu hình **OAuth 2.0** trong n8n với tên `googleSheetsOAuth2Api`.
3. **Tài khoản email** (nếu gửi báo cáo):
   - Cấu hình **SMTP** trong n8n để gửi email tự động (ví dụ: Gmail, Outlook).
4. **Danh sách subreddit** cần theo dõi (ví dụ: `technology`, `startups`, `marketing`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [workflow gốc](https://n8n.io/workflows/13992) hoặc sao chép mã JSON từ trang này.
- Trong n8n Editor, nhấn **Import Workflow** và dán mã JSON vào.
- Hoặc tải file JSON đã download và nhấn **Import** trong giao diện.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần cấu hình các node quan trọng như sau:

##### **A. Cấu hình Credentials**
- **ScrapeOps**:
  - Đi đến **Credentials** → **Add New Credential** → Chọn **ScrapeOps API**.
  - Nhập **API Key** từ ScrapeOps vào trường `apiKey`.
  - Gán credential này cho các node:
    - `ScrapeOps: Fetch Subreddit Listing`
    - `ScrapeOps: Fetch Post Details (JSON)`

- **Google Sheets**:
  - Đi đến **Credentials** → **Add New Credential** → Chọn **Google Sheets OAuth 2.0**.
  - Theo hướng dẫn OAuth để kết nối tài khoản Google.
  - Gán credential này cho các node:
    - `Read Existing Posts from Sheet`
    - `Append New Posts to Sheet`
    - `Append Weekly Digest to Sheet`

- **Email (nếu gửi báo cáo)**:
  - Đi đến **Credentials** → **Add New Credential** → Chọn **Email**.
  - Cấu hình SMTP (ví dụ: Gmail) với:
    - **Host**: `smtp.gmail.com`
    - **Port**: `465` (hoặc `587` cho TLS)
    - **Username** và **Password** (nếu sử dụng ứng dụng mật khẩu).
    - **From Email** và **From Name** (ví dụ: `noreply@doanhnghiep.com`).

##### **B. Cấu hình Node "Configure Subreddits & Week Range" (Code)**
- Mở node này và chỉnh sửa mã JavaScript để cập nhật:
  ```javascript
  // Ví dụ: Cập nhật danh sách subreddit và tuần
  const subreddits = ["technology", "startups", "marketing", "n8n"];
  const weekRange = "week"; // hoặc "month" nếu muốn thu thập tháng
  const sheetId = "YOUR_SHEET_ID"; // Thay bằng ID của Google Sheets
  ```
  - **Lấy `sheetId`** từ URL của Google Sheets (phần sau `/d/` và trước `/edit`).
  - **Danh sách subreddit** là các subreddit bạn muốn theo dõi (ví dụ: `technology`, `startups`).

##### **C. Cấu hình Node "Weekly Schedule Trigger"**
- Mở node này và chỉnh sửa **cron expression** để điều chỉnh thời gian chạy:
  - Mặc định là `0 0 * * 0` (chạy vào thứ 7 lúc 00:00).
  - Các sếp có thể thay đổi thành `0 8 * * 1-5` (chạy hàng ngày lúc 8h) nếu muốn.

##### **D. Kiểm tra Node "Polite Delay (1–3s)"**
- Node này đảm bảo không quá tải server của ScrapeOps. Các sếp có thể điều chỉnh thời gian chờ trong mã JavaScript của node này (nếu cần).

##### **E. Kiểm tra Node "Build Weekly Digest" (Code)**
- Node này tạo báo cáo tuần. Các sếp có thể chỉnh sửa mã để thay đổi cách tổng hợp (ví dụ: thêm tiêu đề, thay đổi định dạng).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra dữ liệu đầu ra.
  - Kiểm tra Google Sheets xem có dữ liệu mới được append không.
  - Nếu gửi email, kiểm tra hộp thư nhận.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng tuần.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node `Append Weekly Digest to Sheet` để thông báo khi có báo cáo mới.
   - Cấu hình trong **Credentials** với token API từ Slack/Telegram.

2. **Lưu Log Dữ liệu**:
   - Thêm node **Google Sheets** hoặc **Database** (ví dụ: Airtable) để lưu lịch sử scraped để phân tích dài hạn.

3. **Tự động Xóa Dữ liệu Cũ**:
   - Thêm node **Google Sheets** với `operation: delete` để xóa dữ liệu cũ sau một thời gian (ví dụ: 6 tháng).

4. **Tùy Chỉnh Báo Cáo**:
   - Sử dụng node **Code** trong `Build Weekly Digest` để thay đổi cách tổng hợp (ví dụ: thêm biểu đồ, thay đổi tiêu đề).

5. **Theo Dõi Subreddit Mới**:
   - Thêm subreddit mới vào danh sách trong node `Configure Subreddits & Week Range` mà không cần chỉnh sửa mã.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc theo dõi xu hướng thị trường trên Reddit mà không cần code hoặc phụ thuộc vào API chính thức. Bằng cách:
- **Thu thập** bài viết top từ các subreddit quan trọng,
- **Xử lý** và enrich dữ liệu,
- **Tổng hợp** thành báo cáo tuần,
- **Gửi tự động** qua email hoặc lưu vào Google Sheets,

các sếp sẽ **tiết kiệm thời gian**, **giảm thiểu sai sót**, và **nhận được dữ liệu cập nhật** mỗi tuần. **Hãy import workflow này ngay hôm nay** và bắt đầu tự động hóa quy trình market research của mình!

---
**🚀 Bắt đầu ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/13992) và cài đặt trên VPS của bạn!