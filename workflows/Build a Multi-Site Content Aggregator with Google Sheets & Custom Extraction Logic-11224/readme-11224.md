---
title: "🌐 **Tự Động Hóa Tham Khảo Nguồn Tin Tức Multi-Site Với Google Sheets & Logic Lọc Tự Động**"
description: "Workflow này tự động thu thập, xử lý và cập nhật nội dung từ nhiều nguồn tin tức khác nhau (Site A, B, C, D...) vào Google Sheets, đồng thời đánh giá độ mới mẻ và phân loại nội dung theo cấp độ. Giúp các sếp tiết kiệm 100% thời gian thủ công trong nghiên cứu thị trường và phân tích nguồn tin."
slug: "tieu-dong-hoa-tham-khao-nuoc-tin-multi-site"
tags: [n8n, automation, market-research, google-sheets, web-scraping, no-code]
keywords: [n8n workflow tự động hóa, thu thập tin tức multi-site, google sheets tự động, logic lọc nội dung mới, web scraping không code, tự động hóa nghiên cứu thị trường]
---

# 🚀 **Tự Động Hóa Tham Khảo Nguồn Tin Tức Multi-Site Với Google Sheets & Logic Lọc Tự Động**

### **Giải pháp cho các sếp:**
Bạn đã từng phải mất hàng giờ mỗi ngày để **thu thập, kiểm tra độ mới mẻ và phân loại nội dung** từ nhiều nguồn tin tức khác nhau? Hay phải **so sánh, đánh giá và lưu trữ** thông tin một cách thủ công? Workflow này sẽ **tự động hóa toàn bộ quy trình**, giúp bạn:
- **Thu thập nội dung** từ nhiều website khác nhau (Site A, B, C, D...) chỉ với một nhấp chuột.
- **Lọc bỏ nội dung cũ** (tùy chỉnh thời gian, ví dụ: >45 ngày).
- **Đánh giá và phân loại** nội dung theo cấp độ (Tier) và trạng thái (mới/ cũ).
- **Cập nhật tự động** vào Google Sheets với định dạng chuẩn, sẵn sàng để phân tích.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần thủ công thu thập từ nhiều website.
✅ **Độ chính xác cao**: Logic lọc tự động bỏ nội dung cũ (>45 ngày).
✅ **Cập nhật liên tục**: Chạy tự động mỗi 4 giờ (hoặc theo lịch).
✅ **Dữ liệu sạch & chuẩn**: Nội dung được **tự động định dạng** và lưu vào Google Sheets.
✅ **Phân loại tự động**: Đánh giá **Tier & Status** (mới/ cũ) cho mỗi bài viết.
✅ **Dễ mở rộng**: Thêm được **bất kỳ website nào** mới vào workflow.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (đã kết nối với n8n via OAuth 2.0).
✔ **2 Sheet Google Sheets** với cấu trúc sau:
   - **"URLs to Process"** (danh sách URL cần thu thập, bao gồm cột `source` để phân loại website).
   - **"Article Feed"** (để lưu kết quả sau khi xử lý).
✔ **API Key của n8n** (nếu self-host).
✔ **Thời gian tối thiểu 10 phút** để cấu hình và test.

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/11224) (hoặc copy JSON từ trang gốc).
2. Trong **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create new workflow**.
2. Chọn **Import** → **Paste JSON** và dán toàn bộ mã JSON từ workflow.
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình chi tiết** các node quan trọng sau:

#### **A. Cấu hình Google Sheets**
1. **Tạo credentials Google Sheets OAuth 2.0**:
   - Trong **n8n**, đi đến **Credentials** → **Add new credential** → Chọn **Google Sheets OAuth 2.0**.
   - Đăng nhập tài khoản Google và cấp quyền cho n8n.
   - Lưu credential với tên **`googleSheetsOAuth2Api`** (để khớp với workflow).

2. **Chỉnh Sheet Name trong các node Google Sheets**:
   - **Node "Read Pending URLs"**:
     - Thay đổi `sheetName` thành tên của **Sheet "URLs to Process"** (ví dụ: `"URLs_to_Process"`).
     - Đảm bảo cột `source` (để phân loại website) tồn tại.
   - **Node "Save to Article Feed"**:
     - Thay đổi `sheetName` thành tên của **Sheet "Article Feed"** (ví dụ: `"Article_Feed"`).
   - **Node "Update URL Status"**:
     - Cùng sheet với "URLs to Process" (để cập nhật trạng thái sau khi xử lý).

#### **B. Cấu hình Source Router (Switch Node)**
- Node **"Source Router"** quyết định **logic extraction** cho mỗi website.
- **Cần thêm/ chỉnh sửa các case** trong `Switch` để khớp với **source** trong Google Sheets:
  - Ví dụ:
    - Nếu `source = "Site A"` → Chuyển đến node **"Extract: Site A"**.
    - Nếu `source = "Site B"` → Chuyển đến node **"Extract: Site B"**.
    - **Nếu không khớp** → Chuyển đến **"Extract: Fallback (Universal)"** (logic mặc định).

#### **C. Cấu hình CSS Selectors cho các Site**
Mỗi website có **logic extraction riêng** (CSS Selectors). Các sếp cần:
1. **Mở DevTools** (F12) trên website cần scrape.
2. **Tìm và sao chép** CSS Selector cho:
   - **Tiêu đề bài viết** (ví dụ: `h1, .post-title`).
   - **Nội dung chính** (ví dụ: `.article-body, .content`).
   - **Ngày đăng** (ví dụ: `.date, .published`).
3. **Điền vào các node HTML Extractor**:
   - Ví dụ, trong node **"Extract: Site A"**:
     - `Selector`: `.article-body` (nội dung).
     - `Selector for date`: `.date` (ngày đăng).

#### **D. Chỉnh logic Freshness Filter**
- Node **"Freshness Filter (45 days)"** kiểm tra độ mới mẻ của bài viết.
- **Cần chỉnh**:
  - `daysThreshold`: Thời gian tối đa cho phép (ví dụ: `45`).
  - `dateSelector`: CSS Selector của ngày đăng (ví dụ: `.date`).

#### **E. Cấu hình Tier & Status**
- Node **"Calculate Tier & Status"** tự động đánh giá:
  - **Tier**: Cấp độ của bài viết (ví dụ: `High`, `Medium`, `Low`).
  - **Status**: `New` (nếu <45 ngày) hoặc `Outdated` (nếu >45 ngày).
- **Cần chỉnh**:
  - Logic trong **Code Node** (nếu cần thay đổi tiêu chí đánh giá).

---
### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **Run Workflow** và chọn **Manual Trigger**.
   - Kiểm tra kết quả trong **Sheet "Article Feed"**.
2. **Bật Schedule Trigger**:
   - Đi đến node **"Schedule (Every 4 Hours)"** → Chọn **Active**.
   - Workflow sẽ chạy **tự động mỗi 4 giờ**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Thêm website mới vào workflow**
- **Bước 1**: Thêm **cột `source` mới** vào Sheet "URLs to Process".
- **Bước 2**: Tạo **node HTML Extractor mới** (ví dụ: **"Extract: Site E"**).
- **Bước 3**: Cập nhật **Source Router (Switch)** để chuyển đến node mới khi `source = "Site E"`.

### **2. Lưu log hoạt động**
- Thêm **node `set`** sau **"Save to Article Feed"** để lưu **thời gian chạy** và **trạng thái thành công/thất bại** vào Sheet.

### **3. Gửi báo cáo định kỳ**
- Sử dụng **node `email`** (n8n-nodes-base.email) để gửi **báo cáo tổng hợp** (ví dụ: số bài viết mới, website có nhiều bài cũ nhất) vào cuối tuần.

### **4. Tối ưu tốc độ**
- Nếu website có **rate limit**, tăng thời gian **Rate Limit (3s)** lên (ví dụ: `5s`).
- Sử dụng **node `splitInBatches`** để chia nhỏ batch nếu có nhiều URL.

### **5. Xử lý lỗi tự động**
- Thêm **node `set`** sau **"Mark as Outdated"** để **ghi lỗi** (ví dụ: `error: "Timeout"`) vào Sheet.

---
## 📌 **Kết luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp trong việc **thu thập, lọc và phân loại tin tức từ nhiều nguồn**. Bằng cách **tự động hóa toàn bộ quy trình**, bạn sẽ:
✔ **Tiết kiệm hàng giờ mỗi ngày** so với cách làm thủ công.
✔ **Nhận dữ liệu chính xác và sạch** sẵn sàng phân tích.
✔ **Cập nhật liên tục** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 website** để đảm bảo logic extraction đúng.
3. **Bật Schedule Trigger** và **quên đi việc thủ công**!

---
**💡 Mẹo cuối:**
Nếu gặp khó khăn trong việc **tìm CSS Selector**, các sếp có thể sử dụng **tool như [Web Scraper](https://webscraper.io/)** hoặc **Chrome Extension [Scraper](https://chrome.google.com/webstore/detail/scraper-mozilla-addon/jnhgnonknehpejjnehehllkliplmbmhn)** để giúp đỡ.

**Chúc các sếp thành công!** 🚀