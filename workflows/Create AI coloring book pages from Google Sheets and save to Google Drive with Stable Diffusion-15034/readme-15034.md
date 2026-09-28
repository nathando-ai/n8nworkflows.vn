---
title: "🎨 Tự Động Hoá Sáng Tạo Trang Bảng Vẽ Coloring AI Từ Google Sheets & Lưu Trên Google Drive (Stable Diffusion)"
description: "Workflow này tự động chuyển đổi các chủ đề từ Google Sheets thành trang vẽ coloring AI chất lượng cao, lưu trữ trên Google Drive với tên file tự động hóa và theo dõi tất cả quá trình trong bảng tính. Giúp tiết kiệm 100% thời gian sáng tạo và tối ưu hóa quy trình nội dung AI cho doanh nghiệp."
slug: "tieu-dong-hoa-sang-tao-trang-coloring-ai"
tags: [n8n, automation, no-code, ai-content-creation, stable-diffusion, google-sheets, google-drive]
keywords: [tự động hóa sáng tạo coloring ai, n8n workflow stable diffusion, tự động hóa nội dung từ google sheets, lưu file ai vào google drive, tự động hóa content creation]
---

# 🚀 **Tự Động Hoá Sáng Tạo Trang Bảng Vẽ Coloring AI Từ Google Sheets & Lưu Trên Google Drive**

### **Giải Phóng Tay Các Sếp Từ Quy Trình Sáng Tạo Coloring AI**
Hiện nay, việc tạo ra hàng loạt trang vẽ coloring chất lượng cao để phục vụ cho sách, giáo dục, hoặc marketing là một công việc tốn thời gian và đòi hỏi kỹ năng nghệ thuật. Các sếp thường phải:
- **Tạo thủ công** từng trang vẽ, mất hàng giờ cho mỗi chủ đề.
- **Quản lý không hiệu quả** các file AI sau khi tạo, dẫn đến rối loạn và khó tìm kiếm.
- **Không theo dõi được quá trình** sinh sản, không biết trang nào đã được xử lý, trang nào còn lại.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động chuyển đổi** các chủ đề từ Google Sheets thành trang coloring AI chất lượng cao.
✅ **Lưu trữ tự động** tất cả file vào Google Drive với tên file logic và cấu trúc thư mục.
✅ **Theo dõi toàn bộ quá trình** trong Google Sheets, giúp các sếp biết trang nào đã được xử lý, trang nào còn lại.
✅ **Chỉ cần cập nhật Google Sheets**, workflow sẽ tự động chạy và sinh sản mới mỗi khi có chủ đề mới hoặc cập nhật.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế từng trang coloring thủ công, chỉ cần cập nhật Google Sheets.
- **Chất lượng AI cao**: Sử dụng Stable Diffusion để sinh sản hình ảnh coloring đẹp mắt, phù hợp với mọi chủ đề.
- **Quản lý file tự động**: Tất cả file được lưu vào Google Drive với tên file logic (vd: `Coloring_Page_Thuyền_Biển_2024-05-20.jpg`).
- **Theo dõi toàn bộ quá trình**: Google Sheets ghi lại tất cả trang đã được xử lý, trạng thái, và liên kết file.
- **Hoạt động liên tục**: Có thể chạy hàng tuần hoặc thủ công, phù hợp với quy trình nội dung của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Google Drive).
2. **API Key Hugging Face** (để sử dụng Stable Diffusion).
3. **Bảng tính Google Sheets** với cấu trúc như sau:
   - **Sheet "Themes"**: Danh sách chủ đề coloring (vd: "Thuyền biển", "Cây cối", "Con vật").
   - **Sheet "Coloring Page Config"**: Cấu hình chung như style, kích thước, và trạng thái "pending" (chưa xử lý).
4. **Thư mục Google Drive** để lưu file kết quả (vd: `Coloring_Pages`).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào workspace.
2. Nhấp vào **"Create"** → **"Import Workflow"**.
3. Chọn file JSON hoặc paste JSON từ [đây](https://n8n.io/workflows/15034) (link gốc).
4. Nhấp **"Import"** để hoàn tất.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **14 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Credentials (Tài Khoản)**
- **Google Sheets OAuth2 API**:
  - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/).
  - Tạo **OAuth 2.0 Client ID** và cấp quyền cho Google Sheets.
  - Trong n8n, thêm **credentials** mới với tên `googleSheetsOAuth2Api` và paste **Client ID** và **Client Secret**.
- **Google Drive OAuth2 API**:
  - Tương tự như Google Sheets, tạo credentials mới với tên `googleDriveOAuth2Api`.
- **Hugging Face API**:
  - Đăng ký tài khoản [Hugging Face](https://huggingface.co/) và lấy **API Key**.
  - Trong n8n, thêm credentials mới với tên `huggingFaceApi` và paste **API Key**.

##### **B. Cấu Hình Node Quan Trọng**
1. **Node "Get Themes" (Lấy Chủ Đề)**
   - Chọn **Google Sheets** và chọn sheet `"Themes"`.
   - Đặt **Range** là `"A2:B"` (giả sử cột A là tên chủ đề, cột B là mô tả).
   - Chọn **Credentials**: `googleSheetsOAuth2Api`.

2. **Node "Coloring Page Config" (Cấu Hình Trang Coloring)**
   - Chọn **Google Sheets** và chọn sheet `"Coloring Page Config"`.
   - Đặt **Range** là `"A2:D"` (giả sử cột A là ID, B là tên chủ đề, C là style, D là trạng thái).
   - Chọn **Credentials**: `googleSheetsOAuth2Api`.

3. **Node "Generate Image (huggingface456)" (Sinh Hình AI)**
   - Chọn **HTTP Request** và cấu hình như sau:
     - **Method**: `POST`
     - **URL**: `https://api-inference.huggingface.co/models/stabilityai/stable-diffusion-2-1`
     - **Headers**:
       ```json
       {
         "Authorization": "Bearer YOUR_HUGGINGFACE_API_KEY",
         "Content-Type": "application/json"
       }
       ```
     - **Body**:
       ```json
       {
         "inputs": "prompt: {{ $node["Build Prompt"].json["prompt"] }}",
         "options": {
           "wait_for_model": true
         }
       }
       ```
     - Chọn **Credentials**: `huggingFaceApi`.

4. **Node "Save Coloring Image to Drive" (Lưu File Vào Google Drive)**
   - Chọn **Google Drive** và cấu hình như sau:
     - **Action**: `createFile`
     - **File Name**: `Coloring_Page_{{ $node["Build Prompt"].json["theme"] }}_{{ $node["Build Prompt"].json["date"] }}.jpg`
     - **File Content**: `{{ $node["Generate Image"].json["image"] }}`
     - **Folder ID**: ID của thư mục Google Drive bạn muốn lưu (lấy từ liên kết thư mục).
     - Chọn **Credentials**: `googleDriveOAuth2Api`.

5. **Node "Log Results to Google Sheets" (Ghi Log Vào Google Sheets)**
   - Chọn **Google Sheets** và cấu hình như sau:
     - **Action**: `append`
     - **Sheet Name**: `"Logs"`
     - **Range**: `"A1:F"` (giả sử cột A-F lưu thông tin log).
     - **Data**:
       ```json
       {
         "Theme": "{{ $node["Build Prompt"].json["theme"] }}",
         "Status": "Completed",
         "File Link": "{{ $node["Save Coloring Image to Drive"].json["webContentLink"] }}",
         "Date": "{{ $node["Build Prompt"].json["date"] }}"
       }
       ```
     - Chọn **Credentials**: `googleSheetsOAuth2Api`.

##### **C. Cấu Hình Node "Filter Pending Coloring Tasks" (Lọc Trang Chưa Xử Lý)**
- Trong node **If**, điều kiện phải là:
  ```json
  {{ $json["status"] === "pending" }}
  ```
  (Chỉ cho phép trang có trạng thái "pending" được xử lý).

##### **D. Cấu Hình Node "Run Weekly Coloring Generation" (Chạy Hàng Tuần)**
- Trong node **Schedule Trigger**, đặt thời gian chạy hàng tuần (vd: **Thứ 7 hàng tuần lúc 8h sáng**).

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp vào nút **"Run"** trên node **"Run Manually"** để kiểm tra workflow.
   - Kiểm tra Google Drive và Google Sheets để xác nhận file và log được tạo đúng.
2. **Bật Active Workflow**:
   - Sau khi test thành công, chuyển workflow sang trạng thái **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Cập Nhật Chủ Đề Từ Excel/CSV**:
   - Sử dụng node **Google Sheets** để đọc file Excel/CSV và chuyển dữ liệu vào sheet "Themes" tự động.

2. **Gửi Báo Cáo Định Kỳ Vào Slack/Email**:
   - Thêm node **Slack** hoặc **Email** sau node **"Log Results to Google Sheets"** để thông báo khi có trang mới được tạo.

3. **Tối Ưu Hóa Stable Diffusion**:
   - Thử nghiệm các **prompt khác nhau** trong node **"Build Prompt"** để cải thiện chất lượng hình ảnh.
   - Sử dụng **negative prompt** để loại bỏ các yếu tố không mong muốn (vd: "blurry, low quality").

4. **Lưu Log Chi Tiết Vào Google Sheets**:
   - Thêm cột **"Error Log"** trong sheet "Logs" để ghi lại lỗi nếu workflow bị lỗi.

5. **Tạo Thư Mục Con Tự Động**:
   - Sử dụng node **Google Drive** với **Folder ID** động để tạo thư mục con theo chủ đề (vd: `Coloring_Pages/Thuyền_Biển`).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình sáng tạo coloring AI mà không cần viết code. Với chỉ **vài bước cấu hình**, các sếp có thể:
✔ **Tiết kiệm hàng giờ** sáng tạo hàng tuần.
✔ **Quản lý file AI một cách chuyên nghiệp** với tên file logic và cấu trúc thư mục.
✔ **Theo dõi toàn bộ quá trình** trong Google Sheets, không lo bỏ sót trang nào.

**Hãy áp dụng ngay workflow này và tự động hóa quy trình nội dung AI của doanh nghiệp!** 🚀

---
**🔗 [Tải Workflow JSON](https://n8n.io/workflows/15034) | [Cài Đặt n8n Self-Hosted](https://docs.n8n.io/)**