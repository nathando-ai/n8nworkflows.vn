---
title: "📊 **Tự Động Hóa Thu Thập Báo Cáo Tuân Thủ (Google Form → Google Drive + MySQL) - Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn thu thập, xử lý và lưu trữ báo cáo tuân thủ từ Google Form sang Google Drive và cơ sở dữ liệu MySQL, tiết kiệm thời gian và giảm thiểu sai sót cho các sếp quản lý."
slug: "tieu-dong-hoa-thu-thap-bao-cao-tuan-thu-google-form-google-drive-mysql"
tags: [n8n, automation, google-forms, google-drive, mysql, no-code, file-management]
keywords: [n8n workflow tự động hóa, thu thập báo cáo tuân thủ, google form google drive mysql, tự động hóa không code, lưu trữ báo cáo tuân thủ]
---

# 🚀 **Tự Động Hóa Thu Thập Báo Cáo Tuân Thủ: Từ Google Form → Google Drive + MySQL**

### **Nỗi Đau Của Các Sếp**
Các sếp quản lý thường phải chịu những vấn đề sau khi thu thập báo cáo tuân thủ thủ công:
- **Tốn thời gian**: Phải kiểm tra, nhập liệu và lưu trữ hàng loạt báo cáo từ nhiều nguồn.
- **Sai sót cao**: Nhập liệu thủ công dễ gây ra lỗi, đặc biệt khi dữ liệu lớn.
- **Không đồng bộ**: Thông tin từ Google Form và tệp đính kèm trên Google Drive không được kết nối tự động.
- **Khó theo dõi**: Không có cơ chế lưu trữ trung tâm để truy xuất nhanh báo cáo cũ.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động:**
✅ **Thu thập** dữ liệu từ Google Form (bao gồm tệp đính kèm).
✅ **Trích xuất** metadata của tệp từ Google Drive.
✅ **Gộp** dữ liệu từ Form và Drive thành một JSON duy nhất.
✅ **Lưu trữ** vào MySQL với cấu trúc chuẩn, sẵn sàng cho báo cáo và phân tích.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần nhập liệu thủ công, giảm thiểu sai sót.
- **Dữ liệu đồng bộ**: Thông tin từ Form và tệp đính kèm được kết nối tự động.
- **Lưu trữ trung tâm**: Tất cả báo cáo được lưu vào MySQL, dễ dàng truy xuất và phân tích.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào thời gian làm việc của nhân viên.
- **Chuẩn hóa dữ liệu**: Các trường dữ liệu được rename và chuẩn hóa trước khi lưu vào MySQL.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google**:
   - **Google Sheets** (đã liên kết với Google Form).
   - **Google Drive** (để lưu tệp đính kèm từ Form).
   - **Google OAuth 2.0 API** (để kết nối với Google Sheets và Drive).
2. **Cơ sở dữ liệu MySQL**:
   - Một bảng `report_logs` với các cột phù hợp (ví dụ: `reporter`, `category`, `timestamp`, `email`, `description`, `folder_id`, `file_name`, `mime_type`).
   - Thông tin kết nối MySQL (host, username, password, database name).
3. **Workflow n8n**:
   - Cài đặt n8n trên máy chủ hoặc VPS (self-hosted).
   - Tạo một **Google Form** liên kết với Google Sheets để thu thập dữ liệu.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Workflows](https://n8n.io/workflows/7765) và tải file JSON.
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
   *Hoặc*:
   - Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7765) và paste vào **Import Workflow** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **6 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **Node 1: Google Sheets Form Trigger**
- **Mục đích**: Theo dõi Google Sheet và kích hoạt workflow khi có dữ liệu mới từ Google Form.
- **Cấu hình**:
  - Chọn **Google Sheets Trigger OAuth2 API** (đã tạo trước đó).
  - Chọn **Google Sheet** liên kết với Form.
  - Chọn **Sheet Name** và **Trigger Row** (ví dụ: `Form Responses 1`).
  - **Lưu ý**: Đảm bảo Google Form đã được cấu hình để gửi dữ liệu vào Sheet này.

##### **Node 2: Extract Google Sheet Data (Function Node)**
- **Mục đích**: Trích xuất dữ liệu từ Sheet và lấy **Google Drive file ID** từ trường `Upload Report File`.
- **Cấu hình**:
  - Mở **Function Node** và chỉnh sửa code như sau (sử dụng **JavaScript**):
    ```javascript
    // Trích xuất các trường cần thiết
    const extractedData = {
      reporter: $input.all().data[0].reporter,
      category: $input.all().data[0].category,
      timestamp: $input.all().data[0].timestamp,
      email: $input.all().data[0].email,
      description: $input.all().data[0].description,
      folder_id: $input.all().data[0].folder_id,
    };

    // Lấy file ID từ URL (nếu có)
    const fileUrl = $input.all().data[0].Upload_Report_File;
    if (fileUrl) {
      const fileId = fileUrl.split('/d/')[1].split('/')[0];
      extractedData.file_id = fileId;
    }

    return extractedData;
    ```
  - **Lưu ý**:
    - Đảm bảo các trường trong Google Form phù hợp với code trên (ví dụ: `Upload Report File` là URL của tệp trên Drive).
    - Nếu trường `folder_id` không có, các sếp có thể bỏ qua hoặc lấy từ `file_id`.

##### **Node 3: Get File Uploaded Metadata (Google Drive Node)**
- **Mục đích**: Lấy metadata của tệp từ Google Drive (tên tệp, loại MIME).
- **Cấu hình**:
  - Chọn **Google Drive OAuth2 API** (đã tạo trước đó).
  - Chọn **Operation**: `download` (để tải metadata).
  - **Key Parameters**:
    - `fileId`: Đặt thành `$node["Extract googlesheet data"].json.file_id` (trích xuất từ node trước).
  - **Lưu ý**:
    - Nếu tệp không có, node này sẽ trả về lỗi. Các sếp có thể thêm **Error Handling** bằng node **Set** hoặc **Function** để xử lý trường hợp này.

##### **Node 4: Merge Sheet & File Data (Merge Node)**
- **Mục đích**: Gộp dữ liệu từ Sheet và Drive thành một JSON duy nhất.
- **Cấu hình**:
  - Chọn **Left Input**: `$node["Extract googlesheet data"].json` (dữ liệu từ Form).
  - Chọn **Right Input**: `$node["Get file uploaded metadata"].json` (metadata từ Drive).
  - **Lưu ý**: Merge Node sẽ tự động kết hợp hai đối tượng JSON.

##### **Node 5: Rename Fields (Set Node)**
- **Mục đích**: Normalize và rename các trường để phù hợp với MySQL.
- **Cấu hình**:
  - Sử dụng **Set Node** để rename các trường như sau:
    ```json
    {
      "fileName": "file_name",
      "mimeType": "mime_type"
    }
    ```
  - **Lưu ý**:
    - Xóa các trường không cần thiết (ví dụ: `Upload_Report_File`, `folder_id` nếu không dùng).
    - Đảm bảo các trường trong MySQL phù hợp với tên mới (ví dụ: `file_name` thay vì `fileName`).

##### **Node 6: Log to MySQL (MySQL Node)**
- **Mục đích**: Lưu dữ liệu vào bảng `report_logs` trong MySQL.
- **Cấu hình**:
  - Chọn **MySQL Credentials** (đã tạo trước đó).
  - Chọn **Database** và **Table**: `report_logs`.
  - **Operation**: `Insert`.
  - **Columns**: Chọn tất cả các trường đã rename (ví dụ: `reporter`, `category`, `file_name`, `mime_type`, ...).
  - **Lưu ý**:
    - Đảm bảo bảng `report_logs` đã được tạo với các cột phù hợp.
    - Nếu bảng chưa có, các sếp có thể tạo bằng SQL:
      ```sql
      CREATE TABLE report_logs (
        id INT AUTO_INCREMENT PRIMARY KEY,
        reporter VARCHAR(255),
        category VARCHAR(255),
        timestamp DATETIME,
        email VARCHAR(255),
        description TEXT,
        file_name VARCHAR(255),
        mime_type VARCHAR(255)
      );
      ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập một bản mẫu vào Google Form để kích hoạt workflow.
   - Kiểm tra các node có hoạt động như mong đợi không (dữ liệu từ Form → Drive → MySQL).
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Schedule Node** để chạy một workflow khác hằng tuần, lấy dữ liệu từ MySQL và gửi báo cáo qua **Email** hoặc **Slack**.

2. **Lưu Log Lịch Sử**:
   - Thêm một **Google Sheets Node** để lưu tất cả dữ liệu vào một Sheet khác, giúp theo dõi lịch sử thay đổi.

3. **Kết Nối với Slack/Telegram**:
   - Sử dụng **Slack/Telegram Node** để thông báo khi có báo cáo mới được thêm vào MySQL.

4. **Xử Lý Lỗi**:
   - Thêm **Error Handling** bằng node **Function** hoặc **Set** để xử lý trường hợp tệp không tồn tại hoặc dữ liệu không đầy đủ.

5. **Tự Động Xóa Tệp Sau Lưu**:
   - Sử dụng **Google Drive Node** với **Operation: `delete`** để xóa tệp sau khi metadata đã được lưu vào MySQL (nếu không cần lưu trữ lâu dài).

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quá trình thu thập, xử lý và lưu trữ báo cáo tuân thủ, giúp các sếp:
✔ **Tiết kiệm thời gian** và giảm thiểu sai sót.
✔ **Có dữ liệu đồng bộ** giữa Form và Drive.
✔ **Lưu trữ trung tâm** dễ dàng truy xuất và phân tích.

**Hành động ngay hôm nay!**
1. Chuẩn bị Google Form, Google Sheets, Google Drive và MySQL.
2. Import workflow và cấu hình theo hướng dẫn.
3. Bật workflow và bắt đầu tự động hóa!

**Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới. Chúc các sếp thành công!** 🚀