---
title: "🎥 **Chuyển Đổi Video LinkedIn Sang MP4 Tự Động + Lưu Trên Google Drive & Sheets - Không Cần Code!**"
description: "Workflow n8n tự động chuyển đổi video LinkedIn thành định dạng MP4, lưu trên Google Drive với quyền chia sẻ công khai, đồng thời ghi log thất bại vào Google Sheets. Giúp tiết kiệm thời gian và tối ưu hóa quy trình content creation cho các sếp marketing, creator hoặc team nội dung."
slug: "chuyen-doi-video-linkedin-sang-mp4-voi-n8n"
tags: [n8n, automation, content-creation, google-drive, google-sheets, rapidapi]
keywords: [n8n workflow video LinkedIn, tự động hóa chuyển đổi video, lưu video Google Drive, log thất bại Google Sheets, RapidAPI LinkedIn]
---

# 🚀 **Tự Động Chuyển Đổi Video LinkedIn Sang MP4 + Lưu Trên Google Drive & Sheets**

### **Nỗi Đau Của Các Sếp**
Các sếp marketing, creator hoặc team nội dung thường phải mất **thời gian quý báu** để:
- **Tìm kiếm** video LinkedIn chất lượng cao từ các nhà lãnh đạo, chuyên gia hoặc đối thủ cạnh tranh.
- **Chuyển đổi** định dạng video từ LinkedIn (thường là MP4 nhưng không phải lúc nào cũng tải được) sang MP4 chuẩn để sử dụng trong các bài viết, email marketing hoặc video tutorial.
- **Lưu trữ** và **chia sẻ** video một cách hiệu quả trên Google Drive, nhưng lại phải **làm thủ công** mỗi lần, dễ gây lỗi và mất thời gian.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể:
✅ **Tự động** chuyển đổi video LinkedIn thành MP4 trong giây lát.
✅ **Lưu trữ** video trên Google Drive với **quyền chia sẻ công khai** (để dễ dàng embed vào blog, email hoặc chia sẻ trên mạng xã hội).
✅ **Ghi log thất bại** vào Google Sheets để theo dõi và xử lý lại sau.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần phải tải video thủ công từ LinkedIn và chuyển đổi định dạng.
- **Chất lượng ổn định**: Sử dụng API RapidAPI để đảm bảo video được tải và chuyển đổi chính xác.
- **Chia sẻ dễ dàng**: Video được lưu trên Google Drive với quyền **Anyone with the link can view**, giúp embed vào blog hoặc chia sẻ trên mạng xã hội một cách nhanh chóng.
- **Theo dõi thất bại**: Tất cả các lỗi chuyển đổi được ghi log vào Google Sheets, giúp các sếp **xử lý lại** sau hoặc **tìm nguyên nhân** để cải thiện.
- **Hoạt động 24/7**: Workflow chạy tự động khi có yêu cầu, không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive & Sheets**:
   - **Google Drive OAuth 2.0 API Key**: Để upload và chia sẻ file.
   - **Google Sheets API Key**: Để ghi log thất bại.
   - **Folder Google Drive**: Để lưu trữ video MP4 (cần chia sẻ folder này với n8n để workflow có quyền upload).
   - **Sheet Google Sheets**: Để ghi log các URL thất bại (cần định nghĩa các cột: `URL`, `Drive_URL`).

2. **API Key RapidAPI**:
   - **RapidAPI LinkedIn Video Downloader API**: Để lấy link download video từ LinkedIn.
   - **Trang web đăng ký**: [RapidAPI - LinkedIn Video Downloader](https://rapidapi.com/apidojo/api/linkedin-video-downloader/)
   - **Mã API Key**: Mỗi tài khoản RapidAPI sẽ có một API Key riêng (được sử dụng trong node `HTTP Request` để gọi API).

3. **Tài khoản n8n**:
   - Workflow này chạy trên **n8n Self-hosted** (không thể chạy trên n8n.cloud miễn phí).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON**: [Download workflow từ n8n.io](https://n8n.io/workflows/6837) (ấn nút "Download").
- **Import vào n8n**:
  1. Mở **n8n Editor** trên VPS.
  2. Nhấn **Import** (icon "Upload") và chọn file JSON đã tải.
  3. Hoặc copy toàn bộ JSON từ file và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **🔹 Node 1: On Form Submission**
- **Mục đích**: Hiển thị form cho người dùng nhập **URL video LinkedIn**.
- **Cấu hình**:
  - Thêm một **field tên là `URL`** (loại input là `text`).
  - **Không cần chỉnh sửa gì khác**.

##### **🔹 Node 2 & 4: HTTP Request (Fetch & Download MP4)**
- **Mục đích**:
  - Node 2: Gọi API RapidAPI để lấy link download video.
  - Node 4: Tải video MP4 từ link được trả về.
- **Cấu hình**:
  - **Node 2 (`HTTP Request` - Fetch)**:
    - **Method**: `POST`
    - **URL**: `https://linkedin-video-downloader.p.rapidapi.com/getVideo`
    - **Headers**:
      ```
      {
        "content-type": "application/json",
        "x-rapidapi-key": "[API_KEY_RAPIDAPI]",  // Thay bằng API Key của bạn
        "x-rapidapi-host": "linkedin-video-downloader.p.rapidapi.com"
      }
      ```
    - **Body**:
      ```json
      {
        "url": "{{ $node["On form submission"].json["URL"] }}"
      }
      ```
  - **Node 4 (`HTTP Request` - Download)**:
    - **Method**: `GET`
    - **URL**: `{{ $node["HTTP Request"].json["media_url"] }}` (lấy từ response của node 2).
    - **Headers**:
      ```
      {
        "accept": "application/json"
      }
      ```
    - **Response Format**: Chọn `Binary` (để tải file MP4).

##### **🔹 Node 5 & 6: Google Drive (Upload & Set Permission)**
- **Mục đích**: Upload video MP4 vào Google Drive và chia sẻ với quyền công khai.
- **Cấu hình**:
  - **Node 5 (`Upload To Google Drive`)**:
    - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).
    - **Folder ID**: Nhập **ID của folder** bạn muốn lưu video (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[FOLDER_ID]`).
    - **File Name**: `{{ $node["On form submission"].json["URL"].split("/").pop() }}.mp4` (tên file tự động từ URL).
    - **File Content**: Chọn `{{ $node["Download mp4"].binary }}`.
  - **Node 6 (`Google Drive Set Permission`)**:
    - **Credentials**: Chọn `googleDriveOAuth2Api`.
    - **File ID**: `{{ $node["Upload To Google Drive"].json["id"] }}`.
    - **Permission**: Chọn `Anyone with the link can view`.

##### **🔹 Node 3: If (Check Error)**
- **Mục đích**: Kiểm tra nếu API trả về lỗi, workflow sẽ **dừng lại** và ghi log vào Sheets.
- **Cấu hình**:
  - **Condition**: `{{ $node["HTTP Request"].json["error"] }}` (nếu có `error`, workflow đi theo **False Path**).
  - **False Path**:
    1. **Node 7 (`Wait`)**:
       - Thời gian chờ: `5000` (5 giây) để tránh ghi log quá nhanh.
    2. **Node 8 (`Google Sheets Append Row`)**:
       - **Credentials**: Chọn `googleApi`.
       - **Sheet Name**: Tên sheet bạn muốn ghi log (ví dụ: `Failed_Conversions`).
       - **Row Data**:
         ```
         {
           "URL": "{{ $node["On form submission"].json["URL"] }}",
           "Drive_URL": "N/A"
         }
         ```

##### **🔹 Node 8: Google Sheets Append Row**
- **Mục đích**: Ghi log URL thất bại vào Google Sheets.
- **Cấu hình**:
  - **Spreadsheet ID**: Lấy từ liên kết Google Sheets (ví dụ: `https://docs.google.com/spreadsheets/d/[SPREADSHEET_ID]/edit`).
  - **Sheet Name**: Tên sheet (ví dụ: `Failed_Conversions`).
  - **Row Data**: Như đã cấu hình ở trên.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Nhập một **URL video LinkedIn** vào form.
  2. Nhấn **Run Workflow** để kiểm tra.
  3. Kiểm tra:
     - Video có được tải xuống và upload lên Google Drive không?
     - File có quyền chia sẻ công khai không?
     - Nếu có lỗi, Sheet có ghi log không?
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active** để chạy tự động khi có form submission.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chia sẻ video trên Slack/Telegram**:
   - Sau khi upload thành công, thêm node **Slack/Telegram** để thông báo link video cho team.
   - **Cách làm**:
     - Thêm node `Slack Webhook` hoặc `Telegram Bot` sau node `Google Drive Set Permission`.
     - Gửi thông báo với `webViewLink` từ node `Google Drive Set Permission`.

2. **Lưu log thành công**:
   - Thêm node `Google Sheets Append Row` vào **True Path** của node `If` để ghi log thành công.
   - **Row Data**:
     ```
     {
       "URL": "{{ $node["On form submission"].json["URL"] }}",
       "Drive_URL": "{{ $node["Google Drive Set Permission"].json["webViewLink"] }}",
       "Status": "Success"
     }
     ```

3. **Xử lý video dài**:
   - Nếu video dài, có thể thêm node `Wait` giữa `Download mp4` và `Upload To Google Drive` để tránh timeout.

4. **Tự động tạo folder mới**:
   - Sử dụng node `Google Drive Create Folder` để tự động tạo folder mới cho mỗi tháng/năm.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì làm thủ công. Với **n8n**, các sếp có thể:
✔ **Tự động hóa** quy trình chuyển đổi video từ LinkedIn.
✔ **Lưu trữ** và **chia sẻ** video một cách hiệu quả.
✔ **Theo dõi** tất cả các lỗi để cải thiện chất lượng.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa content creation của mình!** 🚀

---
**🔗 [Xem workflow gốc trên n8n.io](https://n8n.io/workflows/6837)**
**📌 [Cài đặt VPS cho n8n Self-hosted](https://tino.vn/vps-n8n?affid=388)** (Mã giảm giá: **VPSN8N**)