---
title: "🚀 Tự Động Hóa & Phân Tích Tài Sản Sáng Tạo với ScrapeGraphAI + Google Sheets - Giúp Đội Ngũ Design Tiết Kiệm 20h/Tuần"
description: "Workflow tự động hóa hoàn toàn không cần code giúp phân tích, đánh tag, kiểm tra tuân thủ brand và tổ chức lại tài sản sáng tạo (images, videos, designs) từ upload đến dashboard quản lý. Giúp đội ngũ creative tiết kiệm 20h/tuần và đảm bảo tính nhất quán brand."
slug: "tieu-dong-hoa-phan-tich-tai-san-sang-tao-scrapegraphai"
tags: [n8n, automation, no-code, ai-summarization, creative-workflow, google-sheets, scrapegraphai]
keywords: [tự động hóa tài sản sáng tạo, phân tích hình ảnh bằng AI, quản lý brand asset, tổ chức file design, dashboard creative team, n8n workflow tự động]
---

# 🚀 **Tự Động Hóa & Phân Tích Tài Sản Sáng Tạo với ScrapeGraphAI + Google Sheets**

### **Nỗi Đau Của Đội Ngũ Design & Creative**
Các sếp đang mất **20h/tuần** để:
- **Tìm kiếm và phân loại** hàng ngàn tài sản sáng tạo (images, videos, mockups) trong thư mục hỗn loạn.
- **Đánh tag thủ công** với các tiêu chí như màu sắc, phong cách, mục đích sử dụng, và tuân thủ brand.
- **Kiểm tra tuân thủ brand** cho từng file (màu sắc chính xác, logo, resolution, format file).
- **Tạo cấu trúc thư mục logic** và tên file tiêu chuẩn để dễ tìm kiếm sau này.
- **Cập nhật dashboard** cho team để theo dõi trạng thái và sử dụng hiệu quả.

**Workflow này giải quyết tất cả!** Với **ScrapeGraphAI** (AI phân tích hình ảnh) + **Google Sheets Dashboard**, các sếp sẽ có một hệ thống **tự động hóa 100% không cần code**, giúp:
✅ **Tiết kiệm 20h/tuần** cho team design.
✅ **Đảm bảo tính nhất quán brand** với kiểm tra tự động.
✅ **Tổ chức lại tài sản** theo logic dễ tìm kiếm.
✅ **Cập nhật dashboard** thực thời cho toàn team.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phân tích hình ảnh** bằng AI: Nhận được thông tin chi tiết về màu sắc, phong cách, nội dung, và yếu tố brand trong file.
- **Đánh tag tự động** theo nhiều tiêu chí: Loại file, màu sắc, phong cách, mục đích sử dụng, và tuân thủ brand.
- **Kiểm tra tuân thủ brand** với điểm số và trạng thái phê duyệt tự động.
- **Tổ chức lại thư mục** theo cấu trúc logic: Theo ngày, loại file, và mục đích sử dụng.
- **Dashboard quản lý** trên Google Sheets: Theo dõi tất cả tài sản, trạng thái tuân thủ, và sử dụng hiệu quả.
- **Tiết kiệm thời gian** lên đến **20h/tuần** cho team design.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản ScrapeGraphAI**:
   - [Đăng ký tài khoản miễn phí](https://www.scrapegraphai.com/) và lấy **API Key**.
   - Nếu muốn sử dụng phiên bản Pro (phân tích nâng cao), cần mua gói trả phí.
2. **Google Sheets Dashboard**:
   - Một **Google Sheet** để lưu trữ dữ liệu tài sản (các sếp có thể tạo mới hoặc sử dụng sheet hiện có).
   - **Chia sẻ quyền truy cập** cho workflow với vai trò **"Editor"** (để n8n có thể ghi dữ liệu).
3. **Webhook Endpoint**:
   - Cung cấp **URL webhook** (`/asset-upload`) để các hệ thống upload file (DAM tools, FTP, hoặc ứng dụng nội bộ) gửi dữ liệu.
   - Ví dụ: `https://tên-domain-của-bạn.n8n.cloud/webhook/asset-upload`.
4. **(Tùy chọn) Hệ thống upload file**:
   - Các sếp có thể sử dụng **Google Drive, Dropbox, FTP, hoặc DAM tools** (như Bynder, Canto) để upload file và kích hoạt workflow.
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6640) (ấn "Export" trên canvas).
- **Copy JSON** và dán vào **n8n Editor** (trang `workflows` trên dashboard n8n).
- **Nhấn "Import"** để workflow xuất hiện trên canvas.

:::note[LƯU Ý]
- **Không cần chỉnh sửa code** trong các node `Tag Generator`, `Brand Compliance Checker`, và `Asset Organizer` (n8n đã cung cấp logic sẵn).
- **Cần cấu hình lại các node sau** để phù hợp với môi trường của các sếp:
  - `ScrapeGraphAI Asset Analyzer`
  - `Creative Team Dashboard` (Google Sheets)
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Node `ScrapeGraphAI Asset Analyzer`**
- **Tham số quan trọng**:
  - **API Key**: Điền **API Key** từ tài khoản ScrapeGraphAI.
  - **Asset URL**: Node này sẽ nhận **URL của file** từ node `Asset Upload Trigger`.
  - **Prompt (tùy chọn)**: Nếu muốn điều chỉnh cách AI phân tích, các sếp có thể chỉnh sửa prompt trong node `ScrapeGraphAI Asset Analyzer` (ví dụ: yêu cầu AI tập trung vào yếu tố brand nhất định).

##### **B. Cấu Hình Node `Creative Team Dashboard` (Google Sheets)**
- **Tham số cần điền**:
  - **Google Sheets Credentials**:
    - Chọn **"Add"** và chọn **"Google Sheets"** trong danh sách credentials.
    - Nhập **email Google** và **password** (hoặc sử dụng OAuth 2.0 nếu đã cấu hình trước).
  - **Sheet Name**: Điền tên **Google Sheet** muốn lưu dữ liệu (ví dụ: `"Creative Assets Dashboard"`).
  - **Range**: Điền **tên sheet + phạm vi** (ví dụ: `"Sheet1!A1"`).
  - **Operation**: Đặt là **"appendOrUpdate"** (để cập nhật dữ liệu mới hoặc cập nhật nếu tồn tại).

##### **C. Kiểm Tra Node `Asset Upload Trigger`**
- **Path**: Đảm bảo **path webhook** (`/asset-upload`) khớp với URL các sếp sử dụng.
- **Payload**: Node này cần nhận **JSON** với trường `asset_url` (ví dụ:
  ```json
  {
    "asset_url": "https://example.com/creative-asset.jpg"
  }
  ```
  - Nếu upload từ **Google Drive**, các sếp có thể sử dụng **Google Drive Webhook** hoặc **n8n-nodes-base.googleDrive** để truyền URL file vào workflow.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **request POST** đến webhook với payload mẫu (ví dụ bằng Postman hoặc cURL):
     ```bash
     curl -X POST https://tên-domain-của-bạn.n8n.cloud/webhook/asset-upload \
     -H "Content-Type: application/json" \
     -d '{"asset_url": "https://example.com/test-asset.jpg"}'
     ```
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active**:
   - Chuyển **switch Active** từ **OFF** sang **ON** trên canvas.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết Nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau `Creative Team Dashboard` để thông báo khi có tài sản mới được phân tích hoặc có vấn đề tuân thủ brand.
   - Ví dụ: Nếu `Brand Compliance Checker` trả về **status: "Rejected"**, workflow có thể gửi tin nhắn cảnh báo đến team.

2. **Lưu Log Lịch Sử**:
   - Thêm node **n8n-nodes-base.fileSystem** để lưu **log phân tích** của từng file vào thư mục trên VPS (để theo dõi lịch sử và debug).

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **n8n-nodes-base.googleSheets** để tạo **báo cáo tuần/month** về:
     - Số lượng tài sản mới.
     - Trạng thái tuân thủ brand.
     - Top 5 màu sắc được sử dụng nhiều nhất.
   - Cập nhật báo cáo vào **Google Sheet** hoặc gửi qua email (thêm node **n8n-nodes-base.email**).

4. **Tự Động Xóa File Không Tuân Thủ**:
   - Thêm node **n8n-nodes-base.httpRequest** để gọi API của **Google Drive/Dropbox** và xóa file nếu `Brand Compliance Checker` trả về **status: "Rejected"**.

5. **Tối Ưu Hóa AI**:
   - Nếu muốn **AI phân tích sâu hơn**, các sếp có thể chỉnh sửa **prompt** trong node `ScrapeGraphAI Asset Analyzer` để:
     - Yêu cầu AI **phân tích chi tiết hơn về yếu tố brand**.
     - Loại bỏ các tag không cần thiết.
     - Cập nhật **danh sách màu sắc chính thức** của brand vào prompt.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý đội ngũ design, giúp:
✔ **Tự động hóa 100% quá trình phân tích, đánh tag, và tổ chức tài sản sáng tạo**.
✔ **Đảm bảo tính nhất quán brand** với kiểm tra tự động.
✔ **Tiết kiệm thời gian** lên đến **20h/tuần** cho team.
✔ **Cập nhật dashboard** thực thời để team dễ theo dõi và sử dụng hiệu quả.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.cloud).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Kích hoạt và bắt đầu tự động hóa!**

**Chia sẻ kết quả của các sếp sau khi áp dụng workflow này!** 🚀