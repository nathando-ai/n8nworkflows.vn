---
title: "🚀 Tự Động Hóa Tìm Kiếm & Theo Dõi Lead Nha Kỹ Thuật (Dentist) Từ Google Maps - Không Cần Code!"
description: "Workflow tự động hóa tìm kiếm, trích xuất thông tin chi tiết (điện thoại, website, đánh giá, LGBTQ+ friendly) của các nha sĩ tại bất kỳ thành phố nào, loại bỏ lead trùng lặp, và gửi cảnh báo qua Email/Slack. Giúp các sếp tiết kiệm thời gian lên tới 20h/tuần trong việc tìm kiếm lead mới."
slug: "tieu-dong-hoa-tim-kiem-lead-nha-ky-thuat-google-maps"
tags: [n8n, automation, lead-generation, google-maps-scraping, google-sheets, scrapeops, slack, gmail]
keywords: [n8n workflow lead nha ky thuat, tự động hóa tìm kiếm nha sĩ google maps, scrape google maps dentist, lead generation không code, tự động hóa business intelligence]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Theo Dõi Lead Nha Kỹ Thuật (Dentist) Từ Google Maps**

### **Nỗi Đau Của Các Sếp Trong Ngành Y Tế & Dịch Vụ Sức Khỏe**
Các sếp trong ngành nha khoa, y tế hoặc dịch vụ sức khỏe thường phải **tốn thời gian vô cùng nhiều** để:
- **Tìm kiếm thủ công** các nha sĩ, phòng khám tại thành phố mục tiêu trên Google Maps.
- **Trích xuất thông tin chi tiết** như điện thoại, website, đánh giá, địa chỉ, và thậm chí là thông tin về **LGBTQ+ friendly** (nếu cần).
- **Lọc bỏ lead trùng lặp** từ các lần tìm kiếm trước đó.
- **Gửi thông báo mới** cho đội ngũ bán hàng hoặc quản lý thông qua Email/Slack.

**Kết quả?** Thời gian và nguồn lực bị "chôn vùi" trong công việc thủ công, trong khi các lead tiềm năng lại bị bỏ qua hoặc trùng lặp.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Workflow này **giải quyết tất cả những vấn đề trên** bằng cách:
✅ **Tự động hóa tìm kiếm** tất cả các nha sĩ tại bất kỳ thành phố nào chỉ bằng một **form nhập liệu**.
✅ **Trích xuất thông tin chi tiết** (điện thoại, website, đánh giá, địa chỉ, LGBTQ+ friendly) **không cần code**.
✅ **Lọc bỏ lead trùng lặp** so với dữ liệu đã có trong Google Sheets.
✅ **Gửi cảnh báo mới** qua **Email (Gmail)** và **Slack** để đội ngũ bán hàng/quản lý cập nhật ngay lập tức.
✅ **Lưu trữ dữ liệu** vào Google Sheets để theo dõi và phân tích lâu dài.

**Thời gian tiết kiệm:** **Tối thiểu 20h/tuần** (so với cách làm thủ công).

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản và API Key:**
- [ScrapeOps](https://scrapeops.io/app/register/n8n) (để scraping Google Maps).
- **Google Sheets** (để lưu trữ và so sánh lead).
- **Gmail** (để gửi cảnh báo mới).
- **Slack** (để thông báo team).

📌 **Google Sheet mẫu:**
- **Tên file:** `Dentist Leads Tracker`
- **Cột cần thiết:**
  `businessName` | `phone` | `website` | `rating` | `totalReviews` | `address` | `city` | `category` | `mapUrl` | `status` | `checkedAt` | `lgbtqFriendly` | `review1` | `review2` | `review3`
- **Lấy template:** [Google Sheet Mẫu](https://docs.google.com/spreadsheets/d/1HYO6pw9PigmNKzrnmE9s9JcNVSvZAcIHGF1ZJQ9kfks/edit?gid=0#gid=0)

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/11456](https://n8n.io/workflows/11456) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **12 node quan trọng**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Form - City Input (formTrigger)**
- **Mục đích:** Nhận input từ người dùng (tên thành phố).
- **Lưu ý:** Không cần chỉnh sửa, chỉ cần **bật Active** sau khi import.

##### **🔹 Node 2 & 3: ScrapeOps - Google Maps Search & Business Details**
- **Yêu cầu:**
  - Đăng ký **ScrapeOps API** tại [ScrapeOps](https://scrapeops.io/app/register/n8n) và thêm **credentials** với tên `scrapeOpsApi`.
  - Trong **Set Google Maps Configuration**, cập nhật `keyword` (mặc định là "dentist") thành **từ khóa tìm kiếm** của bạn (ví dụ: "orthodontist", "pediatric dentist").
  - **Lưu ý:** ScrapeOps có **limit free tier**, các sếp nên **monitor usage** để không bị giới hạn.

##### **🔹 Node 4 & 5: Parse Business Details & Parse Full Business Info (Code)**
- **Mục đích:** Trích xuất và định dạng dữ liệu từ Google Maps.
- **Lưu ý:** Các sếp **không cần chỉnh sửa** nội dung code (n8n tự động hóa phần này).

##### **🔹 Node 6: Read Previous Entries from Sheet (googleSheets)**
- **Yêu cầu:**
  - Chọn **Google Sheets OAuth2 API** với tên `googleSheetsOAuth2Api`.
  - Chọn **tab Sheet** đã tạo (ví dụ: `Dentist Leads Tracker`).
  - **Lưu ý:** Đảm bảo **quyền truy cập** của API đã được cấp cho Sheet.

##### **🔹 Node 7: Compare With Previous Run (Code)**
- **Mục đích:** So sánh lead mới với dữ liệu cũ để **lọc bỏ trùng lặp**.
- **Không cần chỉnh sửa**, n8n tự động so sánh dựa trên `businessName` và `mapUrl`.

##### **🔹 Node 8: Filter New Leads (if)**
- **Mục đích:** Chỉ giữ lại lead **mới** (không trùng lặp).
- **Không cần chỉnh sửa**, node này tự động **bỏ qua** lead đã tồn tại.

##### **🔹 Node 9: Send Gmail Alert for New Leads (gmail)**
- **Yêu cầu:**
  - Chọn **Gmail OAuth2** với tên `gmailOAuth2`.
  - Cập nhật **người nhận** (ví dụ: `team@company.com`).
  - **Thiết kế Email mẫu:**
    ```html
    <h2>🚨 New Dentist Lead Found in {{ $node["Set Google Maps Configuration"].json["city"] }}!</h2>
    <p><strong>Name:</strong> {{ $json["businessName"] }}</p>
    <p><strong>Phone:</strong> {{ $json["phone"] }}</p>
    <p><strong>Website:</strong> {{ $json["website"] }}</p>
    <p><strong>Rating:</strong> {{ $json["rating"] }}/5</p>
    <p><strong>Map URL:</strong> <a href="{{ $json["mapUrl"] }}">View on Google Maps</a></p>
    ```

##### **🔹 Node 10: Save to Google Sheets (googleSheets)**
- **Yêu cầu:**
  - Chọn **tab Sheet** cùng với Node 6.
  - **Operation:** Chọn `append` (thêm mới vào cuối Sheet).
  - **Lưu ý:** Đảm bảo **cột đầu tiên** trong Sheet là `businessName` để so sánh trùng lặp.

##### **🔹 Node 11: Send a message (slack)**
- **Yêu cầu:**
  - Chọn **Slack API** với tên `slackApi`.
  - Cập nhật **channel** (ví dụ: `#dentist-leads`).
  - **Thiết kế message mẫu:**
    ```markdown
    *🚨 New Dentist Lead in {{ $node["Set Google Maps Configuration"].json["city"] }}!*
    **Name:** {{ $json["businessName"] }}
    **Phone:** {{ $json["phone"] }}
    **Website:** {{ $json["website"] }}
    **Rating:** {{ $json["rating"] }}/5
    **Map:** <{{ $json["mapUrl"] }}|View on Google Maps>
    ```

---
#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhập **tên thành phố** vào Form Trigger và chạy **Manual Test** để kiểm tra workflow.
- **Bật Active:** Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Hóa Thay Vì Form Trigger:**
   - Thay thế **Form Trigger** bằng **Schedule Trigger** (ví dụ: chạy hàng ngày lúc 8h sáng) để **tìm kiếm tự động** mà không cần nhập thủ công.
   - **Cách cấu hình:**
     - Tạo **Schedule Trigger** mới.
     - Chọn **cron expression** (ví dụ: `0 8 * * *` để chạy lúc 8h mỗi ngày).
     - Gán **city** từ một **Google Sheet** hoặc **variable** cố định.

2. **Lưu Log & Theo Dõi Lịch Sử:**
   - Thêm **node `stickyNote`** sau **Save to Google Sheets** để ghi lại **lịch sử chạy** và **status** của workflow.
   - **Mẫu log:**
     ```
     [{{ $node["Date/Time"].date }}] - Scraped {{ $node["ScrapeOps - Google Maps Search"].json.length }} leads in {{ $node["Set Google Maps Configuration"].json["city"] }}.
     ```

3. **Kết Hợp Với CRM (Salesforce/Zoho):**
   - Thay thế **Gmail/Slack** bằng **node Salesforce/Zoho CRM** để **tự động tạo lead** trong hệ thống quản lý bán hàng.
   - **Cách làm:**
     - Thêm **node `salesforce`** sau **Filter New Leads**.
     - Cấu hình **create record** với trường tương ứng (`Name`, `Phone`, `Website`, ...).

4. **Phân Tích Dữ Liệu với Looker Studio:**
   - Kết nối **Google Sheets** với **Looker Studio** để **tạo dashboard** theo dõi:
     - Số lượng lead mới/mỗi ngày.
     - Top 5 nha sĩ có rating cao nhất.
     - Phân bố lead theo thành phố.

5. **Bộ Lọc Lead Theo Đặc Trưng:**
   - Sử dụng **node `code`** sau **Filter New Leads** để **lọc lead** theo tiêu chí:
     - Chỉ giữ lead có **rating > 4.5**.
     - Chỉ giữ lead có **LGBTQ+ friendly = True**.
     - **Ví dụ code:**
       ```javascript
       $node["Filter New Leads"].json = $node["Filter New Leads"].json.filter(lead =>
           lead.rating >= 4.5 && lead.lgbtqFriendly === "Yes"
       );
       ```

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong ngành y tế và dịch vụ sức khỏe, giúp họ **tìm kiếm lead mới hiệu quả hơn 100%**, **tránh trùng lặp**, và **cập nhật team một cách tự động**.

**👉 Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với 1-2 thành phố** để đảm bảo hoạt động ổn định.
3. **Tự động hóa hoàn toàn** bằng **Schedule Trigger** và **CRM integration**.

**🎁 Bonus:** Các sếp có thể **mở rộng** workflow này để tìm kiếm **lead cho các ngành khác** (phòng khám, bác sĩ, spa, gym...) chỉ bằng cách **đổi keyword** trong **Set Google Maps Configuration**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Chúc các sếp thành công với việc tự động hóa lead generation!** 😊