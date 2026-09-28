---
title: "🎵 Chuyển YouTube thành MP3 Tự Động: Lưu Trữ Google Drive + Log Google Sheets (Không Code)"
description: "Workflow tự động hóa chuyển đổi video YouTube thành file MP3, lưu trữ trên Google Drive và ghi log chi tiết vào Google Sheets. Giúp tiết kiệm thời gian lên đến 90% khi xử lý hàng loạt video."
slug: "chuyen-youtube-thanh-mp3-tu-dong"
tags: [n8n, automation, youtube-to-mp3, google-drive, google-sheets, rapidapi, no-code]
keywords: [n8n workflow youtube mp3, tự động hóa chuyển đổi video, lưu trữ file google drive, log google sheets, rapidapi youtube]
---

# 🎵 **Chuyển YouTube sang MP3 Tự Động: Lưu Trữ + Log Chi Tiết (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Tốn thời gian** tìm kiếm và chuyển đổi hàng chục video YouTube thành MP3 thủ công?
- **Mất track** các file sau khi tải xuống vì không có hệ thống lưu trữ hoặc ghi log?
- **Không biết** file nào đã được xử lý thành công hoặc gặp lỗi?

Workflow này **giải quyết tất cả** bằng cách tự động hóa toàn bộ quy trình: từ nhận URL YouTube → chuyển đổi → lưu trữ → ghi log chi tiết vào Google Sheets. **Không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Xử lý hàng trăm video chỉ trong vài phút thay vì nhiều giờ.
✅ **Lưu trữ tự động**: Tất cả file MP3 được upload lên Google Drive với tên file rõ ràng.
✅ **Ghi log chi tiết**: Dữ liệu như URL, link tải, kích thước file, thời gian xử lý được ghi vào Google Sheets.
✅ **Hoạt động liên tục**: Workflow chạy 24/7 mà không cần can thiệp thủ công.
✅ **Dễ dàng mở rộng**: Thêm Slack/Telegram để thông báo kết quả hoặc gửi báo cáo định kỳ.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Drive và Google Sheets).
2. **API Key RapidAPI** (để chuyển đổi YouTube thành MP3):
   - Đăng ký tại [RapidAPI](https://rapidapi.com/apidojo/api/youtube-to-mp3-downloader1/) và lấy `x-rapidapi-key`.
   - **Lưu ý**: API này có giới hạn request/month. Các sếp nên kiểm tra tài liệu để tránh bị block.
3. **Google Sheet** đã tạo sẵn với các cột:
   - `URL` (đường link YouTube),
   - `Download Link` (link tải MP3),
   - `File Size (MB)`,
   - `Status` (đang xử lý/done/lỗi),
   - `Timestamp`.
4. **Google Drive** với quyền chỉnh sửa tự động.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6722](https://n8n.io/workflows/6722) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6722) và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** (nếu các sếp đã cài đặt):
  ```bash
  n8n import workflow.json
  ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **9 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **🔹 Node 1: On Form Submission (formTrigger)**
- **Mục đích**: Nhận URL YouTube từ form (có thể là Google Form, Typeform, hoặc form tự tạo).
- **Lưu ý**:
  - Các sếp cần tạo một form với **1 trường input** (ví dụ: `YouTube URL`).
  - **Không cần cấu hình gì thêm** trong node này, chỉ cần kết nối với node tiếp theo.

##### **🔹 Node 2: HTTP Request (httpRequest)**
- **Mục đích**: Gửi yêu cầu POST đến API RapidAPI để chuyển đổi YouTube thành MP3.
- **Cấu hình**:
  - **Method**: `POST`
  - **URL**: `https://youtube-to-mp3-downloader1.p.rapidapi.com/output.php`
  - **Headers**:
    ```
    x-rapidapi-host: youtube-to-mp3-downloader1.p.rapidapi.com
    x-rapidapi-key: [API_KEY_CỦA_BẠN]
    ```
  - **Body** (format `multipart-form-data`):
    ```
    url: ${{$node["On form submission"].json["url"]}}
    ```
  - **Lưu ý**:
    - Thay thế `${{$node["On form submission"].json["url"]}}` bằng **JSON Path** từ node `formTrigger`.
    - Nếu API yêu cầu thêm tham số (ví dụ: `format=mp3`), thêm vào body.

##### **🔹 Node 3: Wait (wait)**
- **Mục đích**: Chờ API hoàn thành việc chuyển đổi (thông thường là 5-30 giây).
- **Cấu hình**:
  - **Time**: `10000` (10 giây). Các sếp có thể điều chỉnh tùy theo tốc độ API.

##### **🔹 Node 4: If (if)**
- **Mục đích**: Kiểm tra trạng thái chuyển đổi (`status: "done"`).
- **Cấu hình**:
  - **Condition**: `${{$json["status"] === "done"}}`
  - **Lưu ý**:
    - API RapidAPI trả về JSON với trường `status`. Nếu `status === "done"`, workflow tiếp tục.

##### **🔹 Node 5 & 6: Google Sheets (googleSheets)**
- **Mục đích**:
  - **Google Sheets1**: Ghi log **trạng thái ban đầu** (URL, thời gian bắt đầu).
  - **Google Sheets**: Ghi log **kết quả cuối cùng** (link tải, kích thước file, trạng thái).
- **Cấu hình chung**:
  - **Credentials**: Chọn `googleApi` (đã cấu hình trước trong n8n).
  - **Sheet Name**: Đặt tên sheet (ví dụ: `YouTube_to_MP3_Logs`).
  - **Range**: `Sheet1!A1` (để ghi từ ô A1).
  - **Data**:
    - **Google Sheets1**:
      ```
      {
        "URL": ${{$node["On form submission"].json["url"]}},
        "Status": "Processing",
        "Timestamp": ${{$node["Wait"].json["date"]}}
      }
      ```
    - **Google Sheets**:
      ```
      {
        "URL": ${{$node["On form submission"].json["url"]}},
        "Download Link": ${{$node["HTTP Request"].json["download_link"]}},
        "File Size (MB)": ${{$node["Code"].json["fileSizeMB"]}},
        "Status": "Done",
        "Timestamp": ${{$node["Wait"].json["date"]}}
      }
      ```
  - **Lưu ý**:
    - Các sếp cần **tạo sẵn Google Sheet** với các cột phù hợp.
    - Đảm bảo **quyền chỉnh sửa tự động** cho Google Drive và Sheets.

##### **🔹 Node 7: Code (code)**
- **Mục đích**: Chuyển đổi kích thước file từ **bytes** sang **MB**.
- **Mã JavaScript**:
  ```javascript
  // Input: ${{$node["HTTP Request"].json["file_size"]}} (bytes)
  // Output: fileSizeMB (MB)
  const fileSizeBytes = $input.all()[0].json.file_size;
  const fileSizeMB = (fileSizeBytes / (1024 * 1024)).toFixed(2);
  return { fileSizeMB };
  ```
- **Lưu ý**:
  - API RapidAPI trả về `file_size` trong bytes. Node này chuyển đổi sang MB để dễ đọc.

##### **🔹 Node 8: Google Drive (googleDrive)**
- **Mục đích**: Upload file MP3 vào Google Drive.
- **Cấu hình**:
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **File Path**: `${{$node["HTTP Request"].json["file_path"]}}` (đường dẫn file MP3 từ API).
  - **Folder**: Chọn thư mục trong Google Drive (ví dụ: `YouTube_MP3_Converted`).
  - **File Name**: `${{$node["On form submission"].json["url"].split('/').pop().replace('.html', '')}}.mp3` (tạo tên file từ URL YouTube).
  - **Lưu ý**:
    - Đảm bảo **quyền upload tự động** cho Google Drive.
    - Nếu file đã tồn tại, node này sẽ **ghi đè** (có thể cấu hình để **không ghi đè** bằng cách kiểm tra trước).

##### **🔹 Node 9: Download MP3 (httpRequest)**
- **Mục đích**: Tải file MP3 từ link trả về của API.
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `${{$node["HTTP Request"].json["download_link"]}}`
  - **Headers**: Không cần thêm (nếu API không yêu cầu).
  - **Lưu ý**:
    - Node này **không thực sự cần thiết** vì file đã được upload lên Google Drive ở node trước.
    - Nếu các sếp muốn **tải xuống file** để sử dụng ngoài Google Drive, có thể giữ lại node này.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhập một URL YouTube vào form và kích hoạt workflow.
   - Kiểm tra:
     - File có được upload lên Google Drive không?
     - Dữ liệu có được ghi vào Google Sheets không?
     - Trạng thái có phải là `"Done"` không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node `slack` hoặc `telegram` để thông báo khi workflow hoàn thành.
   - Ví dụ:
     ```
     {
       "text": "✅ File MP3 đã được chuyển đổi từ: ${{$node["On form submission"].json["url"]}}",
       "attachments": [
         {
           "title": "Chi tiết",
           "fields": [
             { "title": "Link tải", "value": ${{$node["HTTP Request"].json["download_link"]}} },
             { "title": "Kích thước", "value": ${{$node["Code"].json["fileSizeMB"]}} + " MB" }
           ]
         }
       ]
     }
     ```

2. **Lưu Log Lịch Sử**:
   - Thêm node `googleSheets` mới để ghi log **lỗi** (nếu status không phải `"done"`).
   - Ví dụ:
     ```
     {
       "URL": ${{$node["On form submission"].json["url"]}},
       "Status": "Failed",
       "Error": ${{$node["HTTP Request"].json["error"] || "Unknown"}},
       "Timestamp": ${{$node["Wait"].json["date"]}}
     }
     ```

3. **Tự Động Xóa File Tạm**:
   - Sử dụng node `googleDrive` với **action `delete`** để xóa file tạm thời trong quá trình chuyển đổi (nếu API trả về file tạm).

4. **Báo Cáo Định Kỳ**:
   - Sử dụng node `googleSheets` kết hợp với `googleAppsScript` để tạo báo cáo tổng hợp hàng tuần/month.

5. **Cài Đặt API Key Mật**:
   - Thay vì lưu `x-rapidapi-key` trong workflow, các sếp có thể:
     - Sử dụng **n8n Secrets** (đăng ký tài khoản n8n Pro).
     - Tạo biến môi trường (`RAPIDAPI_KEY`) và truy cập trong node HTTP Request:
       ```
       x-rapidapi-key: ${{$env.RAPIDAPI_KEY}}
       ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc chuyển đổi YouTube thành MP3 thủ công. Bằng cách kết hợp **API RapidAPI**, **Google Drive** và **Google Sheets**, nó tự động hóa toàn bộ quy trình và cung cấp **ghi log chi tiết** để theo dõi.

**Hành động ngay**:
1. Import workflow và cấu hình theo hướng dẫn.
2. Tạo form để nhận URL YouTube.
3. Kích hoạt và **xem kết quả trong vài giây**!

Nếu các sếp muốn **tối ưu hóa thêm**, có thể kết hợp với **n8n Webhook** để nhận URL từ ứng dụng khác (ví dụ: Discord, Telegram) hoặc **n8n Cron** để chạy định kỳ.

**Chúc các sếp thành công!** 🚀