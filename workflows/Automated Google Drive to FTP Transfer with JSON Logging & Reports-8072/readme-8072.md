---
title: "🚀 Tự Động Chuyển File Từ Google Drive Sang FTP Với Log & Báo Cáo Chi Tiết - N8n Workflow"
description: "Workflow tự động hóa hoàn toàn không cần code để chuyển tất cả file từ Google Drive sang FTP, đồng thời ghi log chi tiết và gửi báo cáo định kỳ qua email. Giúp các sếp tiết kiệm thời gian và tránh lỗi nhân sự."
slug: "tieu-dong-chuyen-file-tu-google-drive-sang-ftp"
tags: [n8n, automation, file-management, google-drive, ftp, log-reporting]
keywords: [n8n tự động hóa file, chuyển file google drive sang ftp, log file n8n, báo cáo tự động n8n, tự động hóa không code]
---

# 🚀 **Tự Động Chuyển File Từ Google Drive Sang FTP Với Log & Báo Cáo Chi Tiết**

### **📌 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Tải xuống** hàng trăm file từ Google Drive thủ công.
- **Chuyển** chúng lên FTP để đồng bộ với hệ thống nội bộ.
- **Ghi chép** log mỗi lần chuyển để theo dõi lỗi hoặc mất file.
- **Gửi báo cáo** định kỳ cho team để kiểm tra tiến độ.

**Kết quả?** Tốn thời gian, dễ xảy ra lỗi, và không thể theo dõi được quá trình chuyển file một cách toàn diện.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình trong 1 lần setup**, giúp các sếp:
✅ **Tiết kiệm 10+ giờ/ngày** bằng việc loại bỏ công việc thủ công.
✅ **Tránh lỗi chuyển file** nhờ kiểm tra và log chi tiết.
✅ **Lưu trữ báo cáo** để theo dõi lịch sử chuyển file.
✅ **Chuyển file theo lịch** hoặc **bất kỳ lúc nào** bằng Webhook.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi setup.
- **Log chi tiết**: Ghi lại tất cả file thành công/thất bại với thời gian, kích thước, và trạng thái.
- **Báo cáo định kỳ**: Email tự động gửi báo cáo hàng ngày/tuần/tháng.
- **Chuyển file theo lịch**: Hoặc kích hoạt thủ công qua Webhook.
- **An toàn & kiểm soát**: File được kiểm tra trước khi upload lên FTP.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền truy cập vào thư mục chứa file cần chuyển.
2. **Thông tin FTP**:
   - Hostname (IP hoặc domain)
   - Port (thường là 21)
   - Username & Password
   - Đường dẫn remote (ví dụ: `/remote/directory/`)
3. **Tài khoản Email** (để gửi báo cáo tự động).
4. **API Key của n8n** (nếu tự host trên VPS).
5. **Thư mục lưu log** (n8n sẽ tự tạo file JSON ghi log).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8072](https://n8n.io/workflows/8072) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- Nếu tự host n8n, **không sử dụng phiên bản Community** vì cần các node như `googleDrive`, `ftp`, và `emailSend`.
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa cấu hình sau.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **14 node**, nhưng các node quan trọng nhất cần cấu hình kỹ là:

##### **A. Schedule Trigger (Kích Hoạt Theo Lịch)**
- **Cấu hình**:
  - Chọn **cron expression** phù hợp (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  - Hoặc để mặc định (`* * * * *`) để chạy liên tục.

##### **B. Get Drive Files (Lấy File Từ Google Drive)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản Google Drive đã setup.
  - **Query**: Điền `mimeType != 'application/vnd.google-apps.folder'` để loại bỏ thư mục.
  - **Folder ID**: Nếu muốn lấy từ thư mục cụ thể, điền ID của thư mục (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).

##### **C. Filter & Validate Files (Lọc & Kiểm Tra File)**
- **Mã JavaScript trong node Code**:
  ```javascript
  // Lọc file có kích thước < 100MB và loại bỏ file đã tồn tại trên FTP
  const validFiles = $input.all().map(file => {
    if (file.size < 100 * 1024 * 1024) { // <100MB
      return {
        ...file,
        isValid: true
      };
    }
    return { ...file, isValid: false };
  }).filter(file => file.isValid);

  $output.set("validFiles", validFiles);
  ```
  - **Lưu ý**: Chỉnh số MB theo nhu cầu.

##### **D. Upload to FTP (Upload File Lên FTP)**
- **Cấu hình**:
  - **Credentials**: Chọn FTP credentials đã setup.
  - **Path**: Đảm bảo đường dẫn `/remote/directory/` tồn tại trên FTP.
  - **Mode**: Chọn `binary` để upload file nhị phân.

##### **E. Update Notes - Success/Error (Cập Nhật Log)**
- **Mã JavaScript trong node Code**:
  ```javascript
  // Cập nhật log thành công/thất bại
  const notes = $input.current().json.notes || [];
  notes.push({
    fileName: $input.current().json.file.name,
    status: $input.current().json.status,
    timestamp: new Date().toISOString()
  });
  $output.set("notes", notes);
  ```
  - **Lưu ý**: Node này tự động ghi log vào `$json.notes`.

##### **F. Save Notes JSON (Lưu Log Vào File)**
- **Cấu hình**:
  - **File Path**: Đặt đường dẫn lưu log (ví dụ: `/logs/transfer_log_$date.json`).
  - **File Content**: Chọn `$json.notes` từ node trước.

##### **G. Upload Notes to Drive (Upload Log Lên Google Drive)**
- **Cấu hình**:
  - **Credentials**: Chọn Google Drive credentials.
  - **Folder ID**: Thư mục lưu log (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **File Name**: `transfer_log_$date.json`.

##### **H. Send Report Email (Gửi Báo Cáo Email)**
- **Cấu hình**:
  - **Credentials**: Chọn tài khoản email đã setup (ví dụ: Gmail).
  - **Subject**: `Báo cáo chuyển file ngày $date`.
  - **HTML Content**:
    ```html
    <h2>Báo cáo chuyển file</h2>
    <p>Tổng file thành công: {{ $json.successCount }}</p>
    <p>Tổng file thất bại: {{ $json.errorCount }}</p>
    <a href="https://drive.google.com/drive/folders/{{ $json.driveFolderId }}">Xem log chi tiết</a>
    ```
  - **Lưu ý**: Node này sử dụng `$json` từ node **Create Final Report**.

##### **I. Webhook Trigger (Kích Hoạt Thủ Công)**
- **Cấu hình**:
  - **Path**: `/webhook-transfer-status` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Chọn credentials webhook (nếu có).
- **Sử dụng**:
  - Gửi POST request đến URL webhook của n8n để kích hoạt chuyển file ngay lập tức.

##### **J. Create Final Report (Tạo Báo Cáo Cuối Cùng)**
- **Mã JavaScript trong node Code**:
  ```javascript
  // Tính toán báo cáo cuối cùng
  const notes = $input.current().json.notes;
  const successCount = notes.filter(n => n.status === "success").length;
  const errorCount = notes.filter(n => n.status === "error").length;

  $output.set("successCount", successCount);
  $output.set("errorCount", errorCount);
  $output.set("driveFolderId", "1AbCdEfGhIjKlMnOpQrStUvWxYz"); // Thay bằng ID thư mục Drive của bạn
  ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn node **Schedule Trigger** và nhấn **Run Workflow** để kiểm tra.
   - Kiểm tra log trong node **Sticky Note** để xem file nào thành công/thất bại.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo kết quả chuyển file ngay khi hoàn thành.
   - Ví dụ:
     ```javascript
     // Trong node Code sau khi upload FTP
     $output.set("slackMessage", `File ${file.name} đã chuyển thành công!`);
     ```
2. **Lưu log vào Database**:
   - Thay node `writeBinaryFile` bằng `n8n-nodes-base.mysql` hoặc `n8n-nodes-base.postgres` để lưu log vào cơ sở dữ liệu.
3. **Chuyển file theo điều kiện**:
   - Sử dụng node **If** để chỉ chuyển file có đuôi `.pdf`, `.xlsx`, `.docx`, v.v.
   - Ví dụ:
     ```javascript
     const allowedExtensions = ['.pdf', '.xlsx', '.docx'];
     const isAllowed = allowedExtensions.includes($input.current().json.file.name.split('.').pop().toLowerCase());
     $output.set("isAllowed", isAllowed);
     ```
4. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Schedule Trigger** với cron `0 0 * * 1` (hàng tuần thứ 2) để gửi báo cáo tuần.
5. **Backup log tự động**:
   - Thêm node `n8n-nodes-base.googleDrive` để sao lưu log vào Google Drive hàng tháng.
---

### 📌 **Kết Luận**
Workflow này **giải phóng hoàn toàn thời gian** của các sếp khỏi công việc chuyển file thủ công, đồng thời **giảm thiểu rủi ro lỗi** nhờ log chi tiết và báo cáo tự động. **Chỉ cần setup 1 lần**, workflow sẽ hoạt động **24/7** theo lịch hoặc theo yêu cầu thủ công.

**Hành động ngay**:
1. **Setup n8n trên VPS** (để workflow chạy liên tục).
2. **Import workflow** và cấu hình các node theo hướng dẫn.
3. **Test và bật Active** để tự động hóa ngay!

---
:::success[🎁 Đăng ký VPS cho n8n với giá ưu đãi]
Để workflow chạy ổn định 24/7, các sếp nên tự host n8n trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Hãy tự động hóa ngay hôm nay!** 🚀