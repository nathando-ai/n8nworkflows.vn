---
title: "🚀 Tự Động Hóa Theo Dõi Job Leads Freelance Từ Reddit Sang Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp freelancer và doanh nghiệp theo dõi, lọc và lưu trữ tất cả các cơ hội việc làm từ Reddit vào Google Sheets, tiết kiệm thời gian lên đến 15 giờ/tuần. Hỗ trợ phân tích, tránh trùng lặp và báo cáo định kỳ."
slug: "tieu-doi-job-leads-reddit-sang-google-sheets"
tags: [n8n, automation, lead-generation, freelance, google-sheets, reddit-scraping]
keywords: [tự động hóa reddit, theo dõi job leads, google sheets automation, n8n workflow freelance, scrap job posting reddit]
---

# 🚀 **Tự Động Hóa Theo Dõi Job Leads Freelance Từ Reddit Sang Google Sheets**

### **Giải pháp cho các sếp freelancer: Tiết kiệm 15 giờ/tuần bằng tự động hóa!**
Hàng ngày, các sếp freelancer phải dành nhiều giờ để:
- **Quét thủ công** các subreddit như r/freelance, r/forhire để tìm job leads.
- **Lọc trùng lặp** giữa các bài đăng và bình luận.
- **Ghi chép vào Google Sheets** để theo dõi tiến độ.
- **Nhớ cập nhật** khi có cơ hội mới.

**Workflow này tự động hóa toàn bộ quy trình!** Nó sẽ:
✅ **Scrap** tất cả bài đăng và bình luận liên quan đến việc làm freelance từ Reddit.
✅ **Lọc bỏ** các bình luận của admin/moderator và trùng lặp.
✅ **Lưu trữ** vào Google Sheets với định dạng chuyên nghiệp.
✅ **Chạy tự động** hàng ngày (hoặc theo lịch bạn thiết lập).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không bị giới hạn.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 15 giờ/tuần** bằng việc loại bỏ công việc quét thủ công.
- **Tránh trùng lặp** với hệ thống lọc tự động.
- **Dữ liệu sạch** được lưu vào Google Sheets với định dạng chuẩn.
- **Báo cáo tự động** hàng ngày (hoặc theo lịch).
- **Tăng cơ hội thành công** với việc không bỏ lỡ bất kỳ job lead nào.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Reddit API**:
   - [Đăng ký tại Reddit API](https://www.reddit.com/prefs/apps) để lấy **Client ID** và **Client Secret**.
   - **Note**: Reddit API hiện hỗ trợ **OAuth2**, nhưng workflow này sử dụng **Basic Auth** (có thể cần cập nhật sau).
   - *Lưu ý*: Nếu API bị hạn chế, các sếp có thể sử dụng **proxies** hoặc **VPS** để tránh bị chặn.

2. **Tài khoản Google Sheets**:
   - Một **Google Workspace** hoặc tài khoản cá nhân để lưu trữ dữ liệu.
   - **API Key Google Sheets**:
     - Tạo **Service Account** tại [Google Cloud Console](https://console.cloud.google.com/).
     - Cấp quyền cho **Google Sheets** bằng cách chia sẻ file với email của Service Account (dạng `xxx@xxx.iam.gserviceaccount.com`).

3. **Google Sheet mẫu**:
   - Workflow sẽ tự động tạo cột như: **Tên Job**, **Link Reddit**, **Thời gian Post**, **Tên Người Post**, **Bình luận liên quan** (nếu có).
   - Các sếp có thể **tạo một sheet mới** trước khi chạy workflow để tránh lỗi.

4. **Lịch chạy (Schedule Trigger)**:
   - Workflow sẽ chạy theo **lịch tự động** (ví dụ: hàng ngày lúc 8h sáng).
   - Các sếp có thể điều chỉnh trong **node "Schedule Trigger"**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/6364](https://n8n.io/workflows/6364) và import vào **n8n Editor**.
- **Copy & Paste JSON** từ link trên vào **n8n Editor** (tab "Import").

:::note[Lưu ý]
- **Không chỉnh sửa JSON** nếu chưa hiểu rõ cấu trúc, để tránh lỗi.
- Nếu import từ file, **không mở file JSON bằng Notepad/Word** (sử dụng **VS Code** hoặc **Sublime Text**).
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **3 phần chính** cần cấu hình:

##### **A. Cấu hình Reddit API**
1. **Node "HTTP Request"** (tất cả các node bắt đầu bằng "HTTP Request"):
   - **Method**: `GET`
   - **URL**: `https://oauth.reddit.com/r/freelance/new.json` (hoặc các subreddit khác như `r/forhire`).
   - **Headers**:
     ```
     Authorization: Basic {base64_encoded_client_id:client_secret}
     User-Agent: n8n/1.0
     ```
   - **Thực hiện**:
     - Trộn **Client ID** và **Client Secret** với dấu `:` (ví dụ: `abc123:def456`).
     - Chuyển thành **Base64** (sử dụng [tool online](https://www.base64encode.org/)).
     - Điền vào **Authorization**.

2. **Node "Get many comments FROM multiple POSTS"**:
   - **Subreddit**: Điền `freelance` (hoặc `forhire`).
   - **Limit**: Đặt số lượng bài đăng muốn scrap (ví dụ: `50`).
   - **Fields**: Chọn `id, title, author, created_utc, url`.

##### **B. Cấu hình Google Sheets**
1. **Node "Get present leads"**:
   - **Credentials**: Chọn **Google Sheets** đã cấu hình trước.
   - **Sheet Name**: Điền tên **Google Sheet** muốn lưu dữ liệu (ví dụ: `Job_Leads`).
   - **Range**: Đặt `A1:Z` (hoặc tùy chỉnh theo cột đã tạo).

2. **Node "Add Leads to Google Sheet"**:
   - **Credentials**: Cùng với node trên.
   - **Sheet Name**: Điền tên **Google Sheet** (không đổi).
   - **Range**: Đặt `A1:Z` (hoặc tùy chỉnh).
   - **Value Input Option**: Chọn `RAW`.

##### **C. Cấu hình Lọc & Trừ Lặp**
1. **Node "Filter Unique Leads" (Code Node)**:
   - Mở **Code Editor** và kiểm tra logic lọc:
     ```javascript
     // Kiểm tra nếu lead đã tồn tại trong sheet
     const existingLeads = $input.all().map(item => item.title.toLowerCase());
     const newLeads = $input.all().filter(item =>
         !existingLeads.includes(item.title.toLowerCase())
     );
     return newLeads;
     ```
   - **Lưu ý**: Nếu logic không hoạt động, các sếp có thể **xóa node này** và sử dụng **Google Sheets Filter** thay thế.

2. **Node "Remove Mod Comments" (If Node)**:
   - **Condition**: Kiểm tra `json["data"]["author"]` **không phải là admin/moderator**.
   - **Thực hiện**:
     - Mở **If Node** và chỉnh sửa điều kiện:
       ```json
       {{ $node["Get many comments FROM multiple POSTS"].json["data"]["author"] !== "mod" }}
       ```

##### **D. Cấu hình Schedule Trigger**
- **Node "Schedule Trigger"**:
  - **Type**: Chọn `cron` (ví dụ: `0 8 * * *` để chạy hàng ngày lúc 8h sáng).
  - **Time Zone**: Chọn **Asia/Ho_Chi_Minh** (hoặc khu vực của các sếp).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual test** với **1-2 bài đăng mẫu** để kiểm tra:
     - Dữ liệu có được scrap từ Reddit không?
     - Dữ liệu có được lưu vào Google Sheets không?
     - Có lỗi nào trong **Code Node** hay **If Node** không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.
   - Kiểm tra **Google Sheets** sau 24h để xác nhận dữ liệu tự động cập nhật.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng hiệu suất với nhiều subreddit**:
   - Thay đổi **URL trong "HTTP Request"** để scrap từ nhiều subreddit (ví dụ: `r/webdev`, `r/designjobs`).
   - **Mẹo**: Sử dụng **node "Merge"** để kết hợp dữ liệu từ nhiều subreddit.

2. **Gửi báo cáo định kỳ qua Email/Slack**:
   - Thêm **node "HTTP Request"** để gọi API của **Google Sheets** và gửi **báo cáo hàng tuần** qua **Email** (n8n có node `n8n-nodes-base.email`).
   - **Cách làm**:
     - Sử dụng **node "HTTP Request"** để lấy dữ liệu từ Google Sheets.
     - Thêm **node "Code"** để xử lý dữ liệu thành **PDF/Excel**.
     - Kết nối với **node "Email"** để gửi báo cáo.

3. **Lưu log hoạt động**:
   - Thêm **node "Sticky Note"** để ghi lại lỗi hoặc thông báo.
   - **Cách làm**:
     - Sử dụng **node "Sticky Note"** sau **node "Add Leads to Google Sheet"**.
     - Điền nội dung: `{"status": "success", "count": {{ $node["Add Leads to Google Sheet"].json.length }} }`.

4. **Tự động xóa leads đã hoàn thành**:
   - Thêm **node "Code"** để kiểm tra cột `Status` trong Google Sheets.
   - Nếu `Status = "Done"`, loại bỏ lead khỏi sheet.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp freelancer muốn **tự động hóa việc theo dõi job leads** mà không cần viết code. Với **n8n**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến 15 giờ/tuần.
✔ **Tránh trùng lặp** và **lưu dữ liệu sạch**.
✔ **Chạy tự động** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** và bật **Active**.
3. **Theo dõi Google Sheets** hàng ngày để xem dữ liệu tự động cập nhật.

**Nếu gặp vấn đề**, các sếp có thể:
- **Trả lời comment** dưới bài viết này.
- **Gửi mail** cho tác giả (iamvaar) tại [iamvaar@gmail.com](mailto:iamvaar@gmail.com).

**Chúc các sếp thành công với việc tự động hóa!** 🚀