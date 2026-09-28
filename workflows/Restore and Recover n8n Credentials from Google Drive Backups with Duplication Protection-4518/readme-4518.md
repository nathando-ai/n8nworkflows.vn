---
title: "🔄 **Khôi Phục & Khôi Tạo Tự Động Credentials n8n Từ Backup Google Drive (Với Bảo Vệ Trùng Lặp)**"
description: "Workflow tự động hóa hoàn toàn không cần code để khôi phục lại tất cả credentials n8n từ các file backup trên Google Drive, đồng thời loại bỏ trùng lặp và đảm bảo dữ liệu chính xác. Giúp các sếp tiết kiệm thời gian và tránh mất mát dữ liệu khi chuyển đổi server hoặc reset n8n."
slug: "khoi-phuc-credentials-n8n-tu-google-drive"
tags: [n8n, automation, devops, google-drive, backup-restore]
keywords: [n8n workflow backup, khôi phục credentials n8n, tự động hóa lưu trữ an toàn, bảo vệ trùng lặp dữ liệu, n8n self-hosted]
---

# 🔄 **Khôi Phục Credentials n8n Từ Backup Google Drive – Không Cần Code**

### **Nỗi Đau Của Các Sếp Khi Khôi Phục Credentials n8n**
Các sếp đã từng gặp phải tình huống này chưa?
- **Reset n8n** vì lỗi server, upgrade phiên bản hoặc bảo trì hệ thống → tất cả credentials (API keys, OAuth tokens, database connections) **mất trắng**.
- **Chuyển đổi server** từ VPS cũ sang mới → phải nhập lại hàng chục credentials một cách thủ công, tốn thời gian và dễ xảy ra lỗi.
- **Backup không đầy đủ** → không biết file nào là mới nhất, dẫn đến trùng lặp hoặc mất dữ liệu quan trọng.

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách:
✅ **Tự động khôi phục** tất cả credentials từ Google Drive (dạng JSON) vào n8n.
✅ **Bảo vệ trùng lặp** bằng cách kiểm tra và bỏ qua credentials đã tồn tại.
✅ **Hoạt động liên tục** 24/7, không cần can thiệp thủ công.
✅ **Chỉnh sửa linh hoạt** cho phù hợp với cấu trúc file backup của các sếp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **chạy ổn định 24/7** và không bị gián đoạn, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**. Với VPS, các sếp có thể:
- **Không phụ thuộc** vào n8n.io (miễn phí) và đảm bảo **dữ liệu không bị xóa** khi n8n.io ngừng dịch vụ.
- **Tùy chỉnh** các workflow theo nhu cầu riêng.
- **Bảo mật cao** hơn với các credentials được lưu trữ an toàn trên máy chủ riêng.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ và ổn định)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
1. **Tiết kiệm thời gian** từ **giờ đồng hồ** xuống **vài phút** khi khôi phục credentials.
2. **Tránh mất mát dữ liệu** nhờ kiểm tra trùng lặp tự động.
3. **Cập nhật liên tục** khi có backup mới trên Google Drive.
4. **Bảo mật cao** với việc không lưu trữ credentials trong n8n.io (nếu self-hosted).
5. **Dễ dàng mở rộng** cho các file backup khác (ví dụ: credentials Slack, Discord, API keys của các dịch vụ khác).

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
#### **1. Tài Khoản & Credentials Cần Thiết**
| Tài Khoản/Dịch Vụ          | Mô Tả                                                                 | Làm Thế Nào Để Lấy?                                                                 |
|----------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **Google Drive**           | Tài khoản Google Drive có quyền truy cập vào folder chứa file backup credentials. | Tạo **OAuth 2.0 Client ID** trong [Google Cloud Console](https://console.cloud.google.com/). |
| **n8n Self-hosted**        | Server n8n đã cài đặt và hoạt động (nếu không, các sếp có thể dùng n8n.io miễn phí). | Cài đặt từ [n8n.io](https://n8n.io/) hoặc sử dụng VPS như hướng dẫn trên.               |
| **File Backup Credentials**| File JSON chứa tất cả credentials cũ (ví dụ: `n8n_credentials_backup_2024.json`). | Tạo file backup bằng cách export từ n8n cũ hoặc sử dụng script `n8n credential:export`. |

#### **2. Cấu Trúc File Backup (Ví Dụ)**
File backup nên có định dạng JSON với cấu trúc như sau:
```json
{
  "credentials": [
    {
      "name": "Slack API Token",
      "value": "xoxb-your-token-here",
      "type": "apiKey"
    },
    {
      "name": "Google Drive OAuth",
      "value": "ya29.your-oauth-token",
      "type": "oauth2"
    }
  ]
}
```

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
**Cách 1: Từ file JSON**
1. Tải file JSON của workflow từ [n8n.io/workflows/4518](https://n8n.io/workflows/4518).
2. Vào **n8n Editor** (trang chủ của n8n).
3. Nhấn **Import** → Chọn file JSON vừa tải.
4. Nhấn **Import Workflow**.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/4518](https://n8n.io/workflows/4518).
2. Vào **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. Nhấn **Import Workflow**.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **7 node quan trọng** cần cấu hình cẩn thận:

##### **A. Node "Google Drive Get Credentials File"**
- **Mục đích**: Lấy danh sách file JSON từ Google Drive để khôi phục.
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã tạo trước đó).
  - **Folder ID**: Điền **ID của folder** chứa file backup (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/FOLDER_ID`).
  - **File Name Pattern**: Điền `*.json` để lấy tất cả file JSON trong folder.
  - **Operation**: Chọn `listFiles`.

##### **B. Node "Convert Files To JSON"**
- **Mục đích**: Chuyển file JSON từ Google Drive thành dữ liệu có thể xử lý.
- **Cấu hình**:
  - **Operation**: Đảm bảo chọn `fromJson`.

##### **C. Node "Check For Skipped Credentials" (IF)**
- **Mục đích**: Kiểm tra credentials đã tồn tại trong n8n để **bỏ qua** và tránh trùng lặp.
- **Cấu hình**:
  - **Condition**: Sử dụng biểu thức:
    ```json
    {{ $json["name"] && !($json["value"] === null) }}
    ```
  - **Nếu true**: Tiến hành khôi phục.
  - **Nếu false**: Bỏ qua (không khôi phục).

##### **D. Node "Restore N8n Credentials"**
- **Mục đích**: Khôi phục credentials vào n8n.
- **Cấu hình**:
  - **Credentials**: Chọn `n8nApi` (credentials của n8n self-hosted).
  - **Resource**: Chọn `credential`.
  - **Payload**:
    ```json
    {
      "name": "{{ $json["name"] }}",
      "value": "{{ $json["value"] }}",
      "type": "{{ $json["type"] }}"
    }
    ```

##### **E. Node "Execute Command Get All Credentials" (Nếu Cần)**
- **Mục đích**: (Nếu các sếp muốn **lấy tất cả credentials hiện tại** trong n8n để so sánh với backup).
- **Cấu hình**:
  - **Command**: `n8n credential:list --format json`.
  - **Output**: Chuyển sang node **Aggregate Credentials** để so sánh.

##### **F. Node "Aggregate Credentials"**
- **Mục đích**: Gộp tất cả credentials từ backup và so sánh với credentials hiện tại.
- **Cấu hình**:
  - **Key**: Chọn `name` (để so sánh trùng lặp).
  - **Operation**: Chọn `aggregate`.

##### **G. Node "Loop Over Items" (Split In Batches)**
- **Mục đích**: Lặp qua từng credentials để khôi phục.
- **Cấu hình**:
  - **Batch Size**: Đặt **10-20** (để tránh quá tải server).

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với một file mẫu:
   - Chọn **On Click Trigger** → Nhấn **Execute**.
   - Kiểm tra **Output** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Đặt **Active** thành `true`.
   - **Lưu workflow**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Tự Động Khôi Phục Mỗi Lần Có Backup Mới**
- **Sử dụng Webhook** (thay thế `On Click Trigger`) để kích hoạt workflow khi có file mới trên Google Drive.
- **Cài đặt Google Drive Webhook** (sử dụng [Google Apps Script](https://developers.google.com/apps-script)) để gửi thông báo khi có file mới.

#### **2. Lưu Log Khôi Phục**
- Thêm node **Slack/Telegram Notification** để thông báo kết quả khôi phục:
  ```json
  {
    "text": `🔄 Khôi phục credentials thành công: {{ $json["name"] }}`
  }
  ```
- Hoặc lưu log vào **Google Sheets** để theo dõi lịch sử.

#### **3. Khôi Phục Cho Các Dịch Vụ Khác**
- **Mở rộng cho Slack/Discord**: Sử dụng node `slack` hoặc `discord` để khôi phục tokens.
- **Khôi phục Database Connections**: Thêm node `mysql`/`postgres` để khôi phục credentials cơ sở dữ liệu.

#### **4. Backup Định Kỳ**
- **Tự động backup credentials** định kỳ (ví dụ: hàng tháng) bằng cách sử dụng workflow khác:
  ```json
  {
    "name": "Backup N8n Credentials to Google Drive",
    "type": "executeCommand",
    "command": "n8n credential:export --format json > /path/to/backup.json"
  }
  ```
- Sau đó upload lên Google Drive bằng node `googleDrive`.

---
### 📌 **Kết Luận**
Workflow này **giải quyết triệt để** vấn đề mất mát credentials khi reset n8n hoặc chuyển đổi server. Với **tự động hóa hoàn toàn**, các sếp không cần lo lắng về việc mất dữ liệu quan trọng và có thể **tích hợp vào quy trình DevOps** một cách an toàn.

**Hành động ngay hôm nay:**
1. **Chuẩn bị** Google Drive và credentials như hướng dẫn.
2. **Import workflow** và **cấu hình** các node quan trọng.
3. **Test run** và **bật Active** để khôi phục dữ liệu.
4. **Tự động hóa** bằng cách kết nối với Webhook hoặc lịch trình định kỳ.

**🚀 Nếu các sếp cần hỗ trợ thêm**, có thể liên hệ với tác giả **Daniel Ng** qua email: [daniel@aiautomationpro.org](mailto:daniel@aiautomationpro.org).

---
**Chúc các sếp thành công với tự động hóa n8n!** 💻✨