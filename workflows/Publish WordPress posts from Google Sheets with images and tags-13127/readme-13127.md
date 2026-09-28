---
title: "🚀 Tự Động Hóa Bài Viết WordPress Từ Google Sheets: Ảnh + Tags + 1 Click Publish"
description: "Workflow tự động hóa 100% không code chuyển đổi dữ liệu từ Google Sheets sang bài viết WordPress với hình ảnh, tags tự động, và cập nhật trạng thái. Giúp các sếp tiết kiệm 10+ giờ/tháng và duy trì nội dung liên tục 24/7."
slug: "tu-dong-hoa-bai-viet-wordpress-tu-google-sheets"
tags: [n8n, automation, content-marketing, wordpress, google-sheets, no-code]
keywords: [n8n workflow wordpress, tự động hóa bài viết blog, publish từ google sheets, tự động hóa nội dung marketing, tự động hóa wordpress]
---

# 🚀 **Tự Động Hóa Bài Viết WordPress Từ Google Sheets: Ảnh + Tags + 1 Click Publish**

### **Nỗi Đau Của Các Sếp**
Các sếp đang mất thời gian quý báu để:
- **Nhập liệu thủ công** từ Google Sheets sang WordPress (tốn 30-60 phút/bài viết).
- **Quên cập nhật trạng thái** sau khi publish, dẫn đến dữ liệu không đồng bộ.
- **Không tự động xử lý hình ảnh** và tags, buộc phải upload từng file và tạo tags một cách thủ công.
- **Không theo dõi lịch công bố** bài viết, dẫn đến nội dung không được cập nhật kịp thời.

**Workflow này giải quyết tất cả!** Với chỉ **1 lần setup**, các sếp có thể:
✅ **Chuyển đổi dữ liệu từ Google Sheets sang bài viết WordPress tự động** (title, excerpt, nội dung, hình ảnh, tags).
✅ **Tải xuống và upload hình ảnh** từ URL sang WordPress Media.
✅ **Tạo hoặc sử dụng tags** từ hashtags trong Google Sheets.
✅ **Cập nhật trạng thái** từ `READY` → `POSTED` và lưu URL bài viết trong Sheet.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 10+ giờ/tháng cho việc nhập liệu và publish bài viết.
- **Chính xác 100%**: Không sai sót trong quá trình chuyển đổi dữ liệu từ Sheet sang WordPress.
- **Cá nhân hóa nội dung**: Hỗ trợ hình ảnh và tags tự động, giúp bài viết chuyên nghiệp hơn.
- **Hoạt động liên tục**: Workflow chạy tự động khi có dữ liệu mới trong Google Sheets.
- **Dữ liệu đồng bộ**: Trạng thái bài viết và URL luôn được cập nhật trong Sheet.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** với cấu trúc cột như sau:
     | id | status | title | excerpt | body | image_url | hashtags |
     |----|--------|-------|---------|-------|-----------|----------|
   - **Trạng thái `status`** phải là `READY` để workflow xử lý.
   - **Cột `hashtags`** chứa các tags tách bởi dấu `#` (ví dụ: `#marketing #n8n #automation`).

2. **Tài khoản WordPress**:
   - **Trang WordPress** cần kết nối với n8n (sử dụng **Application Password** hoặc **Basic Auth**).
   - **API REST API** của WordPress phải được kích hoạt (mặc định trong WordPress).

3. **Credentials cho n8n**:
   - **Google Sheets OAuth 2.0 API** (để đọc và cập nhật Sheet).
   - **WordPress HTTP Basic Auth** (để publish bài viết và quản lý tags).

4. **File mẫu Google Sheet**:
   - [Mẫu Sheet chuẩn](https://docs.google.com/spreadsheets/d/1lJDeaN75c1hBk0gddsdvbeXDuxDr5Q-NablHRSjvLjQ/edit?gid=0#gid=0) (có thể sao chép và sử dụng).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **Workflow Editor**.
2. Nhấp vào **Import** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/13127)).
3. **Không cần chỉnh sửa** cấu trúc workflow, chỉ cần **cấu hình credentials** như hướng dẫn dưới đây.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **20 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **A. Cấu Hình Credentials**
1. **Google Sheets**:
   - Trong node **"Get row(s) in sheet"** và **"Update row in sheet"**, chọn **credentials** là `googleSheetsOAuth2Api`.
   - Điền **URL của Google Sheet** vào biến `googleSheetUrl` trong node **"Variables"**.

2. **WordPress**:
   - Trong các node sử dụng `httpRequest` (ví dụ: **"Upload $image to WP"**, **"Create new tag"**), chọn **credentials** là `httpBasicAuth`.
   - Điền thông tin sau vào biến trong node **"Variables"**:
     - `wordpressUrl`: URL của trang WordPress (ví dụ: `https://tên-trang.com`).
     - `wordpressUsername` và `wordpressPassword`: Application Password hoặc Basic Auth từ WordPress.

##### **B. Cấu Hình Cột trong Google Sheet**
- **Bắt buộc**: Sheet phải có các cột sau:
  - `id` (dùng để phân biệt bài viết).
  - `status` (phải là `READY` để workflow xử lý).
  - `title`, `excerpt`, `body` (nội dung bài viết).
  - `image_url` (URL hình ảnh, nếu có).
  - `hashtags` (tags tách bởi `#`, ví dụ: `#n8n #automation`).

##### **C. Node Quan Trọng Cần Chú Ý**
1. **Node "If ($image)"**:
   - Nếu cột `image_url` trống, workflow sẽ bỏ qua phần upload hình ảnh.
   - Nếu có hình ảnh, workflow sẽ:
     - Tải xuống từ `image_url` (node **"Load $image as binary"**).
     - Upload lên WordPress Media (node **"Upload $image to WP"**).
     - Gán làm **featured image** cho bài viết.

2. **Node "If ($tags)"**:
   - Nếu cột `hashtags` trống, workflow sẽ bỏ qua phần xử lý tags.
   - Nếu có hashtags, workflow sẽ:
     - **Parse** hashtags thành danh sách tags (node **"Parse $tags"**).
     - **Tìm kiếm tags** đã tồn tại trong WordPress (node **"Get tag_id from WP"**).
     - **Tạo tags mới** nếu chưa có (node **"Create new tag"**).
     - **Lưu ID tags** để gán vào bài viết (node **"Store tag_id"**).

3. **Node "Prepare data"**:
   - Đây là node **Code** chuẩn bị dữ liệu payload cho API WordPress.
   - Các sếp **không cần chỉnh sửa** trừ khi muốn thay đổi cấu trúc bài viết (ví dụ: thêm categories, author).

4. **Node "Update row in sheet"**:
   - Sau khi publish thành công, workflow sẽ cập nhật cột `status` từ `READY` → `POSTED` và thêm cột `post_url` vào Sheet.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Thêm **1 dòng test** trong Google Sheet với `status = READY`.
   - Chạy **Manual Trigger** (node **"When clicking ‘Execute workflow’"**).
   - Kiểm tra:
     - Bài viết có xuất hiện trên WordPress không?
     - Hình ảnh và tags có được gán đúng không?
     - Trạng thái trong Sheet có được cập nhật không?

2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active**.
   - Workflow sẽ tự động chạy mỗi khi có **dòng mới với `status = READY`**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi bài viết được publish thành công.
   - Ví dụ: Sau node **"Publish + update sheet"**, thêm node **Slack Webhook** để gửi tin nhắn:
     ```
     "Bài viết [{{$json.title}}] đã được publish tại: {{ $json.url }}"
     ```

2. **Lưu Log Hoạt Động**:
   - Thêm node **Google Sheets** hoặc **Database** (ví dụ: Airtable) để lưu lịch sử publish.
   - Ví dụ: Tạo một Sheet mới để ghi lại:
     - Ngày giờ publish.
     - Tiêu đề bài viết.
     - Trạng thái thành công/thất bại.

3. **Chỉnh Sửa Thời Gian Publish**:
   - Nếu muốn **chỉnh thời gian publish** (ví dụ: schedule bài viết), các sếp có thể:
     - Sử dụng plugin **WP Schedule** kết hợp với API.
     - Hoặc thêm node **Code** để tính toán thời gian và gửi request publish vào thời điểm mong muốn.

4. **Tự Động Xóa Hình Ảnh Trùng Lặp**:
   - Trong node **"Upload $image to WP"**, các sếp có thể thêm logic kiểm tra hình ảnh đã tồn tại trong Media Library trước khi upload.

5. **Tích Hợp với AI (LLM)**:
   - Sử dụng node **LLM** (ví dụ: OpenAI, Mistral) để:
     - **Tạo excerpt tự động** từ nội dung bài viết.
     - **Tối ưu hóa SEO** cho tiêu đề và nội dung.
     - **Chuyển đổi ngôn ngữ** nếu cần.

---

### 📌 **Kết Luận**
Workflow **"Publish WordPress posts from Google Sheets"** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa toàn bộ quy trình publish** từ Sheet sang WordPress.
✔ **Giảm thiểu sai sót** và tiết kiệm thời gian.
✔ **Duy trì nội dung liên tục** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay!**
1. **Setup VPS** cho n8n (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Thêm 1 dòng test** trong Google Sheet và chạy thử.
4. **Bật Active** và để workflow làm việc 24/7!

**🚀 Cùng tự động hóa nội dung của mình ngay bây giờ!** Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ với [Grigory Frolov](https://n8n.io/workflows/13127) (tác giả của workflow).