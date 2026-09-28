---
title: "🔄 **Tự Động Hồi Phục Workflow & Credentials từ FTP: Khôi Phục Toàn Bộ Hệ Thống n8n Mới Chỉ Với 1 Click**"
description: "Workflow này giúp các sếp khôi phục hoàn toàn tất cả workflow và credentials từ kho lưu trữ FTP vào n8n mới hoặc đã bị lỗi, tiết kiệm thời gian và tránh mất dữ liệu quan trọng. Đặc biệt phù hợp cho doanh nghiệp sử dụng n8n self-hosted."
slug: "tieu-dung-ftps-khoi-phuc-workflow-credentials-n8n"
tags: [n8n, automation, backup-restore, ftp, credentials-management, self-hosted]
keywords: [tự động hóa n8n, khôi phục workflow n8n từ ftp, backup credentials n8n, di chuyển workflow n8n, tự động hóa không code]
---

# 🔄 **Khôi Phục Workflow & Credentials từ FTP: Giải Pháp Tự Động Hóa Cho Doanh Nghiệp n8n**

### **Nỗi Đau Của Các Sếp Khi Mất Dữ Liệu Workflow**
Các sếp đã từng gặp phải tình huống nào sau đây?
- **Mất dữ liệu workflow** khi chuyển đổi từ n8n cloud sang self-hosted hoặc ngược lại?
- **Bị lỗi hệ thống** khiến tất cả workflow và credentials bị mất?
- **Không có thời gian** để thủ công khôi phục hàng chục workflow và credential một cách cẩn thận?
- **Sợ mất dữ liệu quan trọng** khi nâng cấp phiên bản n8n?

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách **tự động khôi phục toàn bộ workflow và credentials từ FTP** vào n8n mới hoặc đã bị lỗi, **không cần viết một dòng code nào**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Khôi phục toàn bộ workflow & credentials chỉ trong vài phút** thay vì mất hàng giờ thủ công.
✅ **Tránh mất dữ liệu quan trọng** khi chuyển đổi giữa các phiên bản n8n hoặc máy chủ.
✅ **Tự động hóa hoàn toàn** quá trình khôi phục, giảm thiểu sai sót do con người gây ra.
✅ **Dễ dàng di chuyển workflow** từ n8n cloud sang self-hosted hoặc ngược lại.
✅ **Cấu hình linh hoạt** để chỉ khôi phục workflow hoặc credentials tùy ý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản FTP** chứa file backup của workflow và credentials (định dạng `.json`).
✔ **Credentials FTP** để kết nối với kho lưu trữ (Host, Username, Password, Port).
✔ **Credentials SMTP** (nếu muốn gửi email thông báo kết quả).
✔ **n8n self-hosted** (không hỗ trợ trên n8n cloud).
✔ **File backup** đã được tổ chức theo cấu trúc:
   ```
   /n8n-backups/
   ├── workflows/
   │   ├── workflow1.json
   │   ├── workflow2.json
   │   └── ...
   └── credentials/
       ├── credential1.json
       └── credential2.json
   ```

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải xuống file JSON** từ [n8n.io/workflows/9156](https://n8n.io/workflows/9156) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **phức tạp** vì sử dụng nhiều node logic, các sếp cần chú ý đến các bước sau:

##### **A. Cấu Hình Node "Init" (Bắt buộc)**
Node này **xác định đường dẫn FTP** và cấu trúc tạm thời cho quá trình khôi phục.
```javascript
const FTP_BACKUP_FOLDER = $env.FTP_BACKUP_FOLDER || '/n8n-backups';
const credentials_temp_folder = '-restore-credentials';
const workflows_temp_folder = '-restore-workflows';
const FTPName = 'Tên FTP Server của bạn'; // Thay bằng tên FTP thực tế
const credentials = "n8n-credentials"; // Thường là "n8n-credentials"
```
- **Thay `FTP_BACKUP_FOLDER`** bằng đường dẫn thực tế của folder backup trên FTP.
- **Thay `FTPName`** bằng tên FTP server (ví dụ: `ftp.example.com`).
- **Không thay đổi `credentials_temp_folder` và `workflows_temp_folder`** trừ khi cần.

##### **B. Cấu Hình Node "Start Restore" (Bắt buộc)**
Node này **quản lý việc khôi phục workflow và credentials** thông qua JSON cấu hình.
```json
[
  {
    "credentials": true,  // Khôi phục credentials (true/false)
    "workflows": true     // Khôi phục workflows (true/false)
  }
]
```
- **Nếu chỉ muốn khôi phục workflow**, đặt `"credentials": false`.
- **Nếu chỉ muốn khôi phục credentials**, đặt `"workflows": false`.
- **Lưu ý quan trọng**: **Khôi phục credentials trước** nếu muốn khôi phục workflow hoàn toàn.

##### **C. Cấu Hình Credentials FTP & SMTP (Bắt buộc)**
- **Credentials FTP**:
  - Tạo **credentials FTP** trong n8n với thông tin:
    - Host: `ftp.example.com`
    - Username: `tên_ftp`
    - Password: `mật khẩu_ftp`
    - Port: `21` (hoặc `990` nếu sử dụng FTP Secure)
  - **Gắn credentials này** vào node `List Credentials Folders`, `List Workflows Folder`, `Download Workflow Files`, `Download Credential Files`.

- **Credentials SMTP (nếu gửi email)**:
  - Tạo **credentials SMTP** với thông tin:
    - Host: `smtp.example.com`
    - Port: `587`
    - Username: `tên_email`
    - Password: `mật khẩu_email`
    - From: `tên_email@example.com`
  - **Gắn credentials này** vào node `SUCCESS email Credentials` và `SUCCESS email Workflows`.

##### **D. Node "Find Last Backup" (Bắt buộc)**
Node này **tìm folder backup mới nhất** trên FTP.
- **Không cần chỉnh sửa** nếu cấu hình FTP đúng.
- Nếu gặp lỗi, kiểm tra:
  - **Đường dẫn FTP** có chính xác không?
  - **Credentials FTP** có đúng không?

##### **E. Node "Exclude Current Workflow From Selection" (Bắt buộc)**
Node này **tránh khôi phục workflow hiện tại** (nếu đang chạy).
- **Không cần chỉnh sửa** nếu muốn khôi phục tất cả.
- Nếu muốn **bỏ qua workflow này**, chỉnh sửa code trong node `executeCommand`:
  ```bash
  n8n exec --workflowName "$(jq -r '.name' $json)" --delete
  ```

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `Start Restore` và chọn **Run Once**.
   - Kiểm tra log để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho workflow.
   - **Không quên** kiểm tra email thông báo (nếu cấu hình SMTP).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Khôi Phục**:
   - Thêm node **Slack/Telegram** để nhận thông báo kết quả khôi phục.
   - Ví dụ:
     ```json
     {
       "type": "slackWebhook",
       "credentials": ["slack"],
       "keyParameters": {
         "text": "🔄 Khôi phục workflow & credentials thành công! Thời gian: {{ $json.timestamp }}"
       }
     }
     ```

2. **Khôi Phục Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để khôi phục tự động hàng tháng.
   - Ví dụ:
     ```json
     {
       "type": "n8n-nodes-base.manualTrigger",
       "parameters": {
         "schedule": "0 0 1 * *", // Mỗi tháng ngày 1 lúc 00:00
         "active": true
       }
     }
     ```

3. **Backup Định Kỳ**:
   - **Không chỉ khôi phục**, mà còn **backup định kỳ** workflow và credentials.
   - Sử dụng **n8n FTP Node** để backup tự động:
     ```json
     {
       "type": "ftp",
       "credentials": ["ftp"],
       "keyParameters": {
         "operation": "upload",
         "path": "/n8n-backups/{{ $json.date }}/credentials.json",
         "file": "{{ $json.credentialsFile }}"
       }
     }
     ```

4. **Khôi Phục Chunk Lớn**:
   - Nếu backup quá lớn, **chia nhỏ** thành nhiều folder nhỏ hơn.
   - Ví dụ:
     ```
     /n8n-backups/
     ├── workflows/
     │   ├── 2024/
     │   │   ├── workflow1.json
     │   │   └── workflow2.json
     │   └── 2023/
     └── credentials/
         ├── 2024/
         └── 2023/
     ```

---

### 📌 **Kết Luận**
Workflow này **là giải pháp hoàn hảo** cho các sếp muốn:
✔ **Khôi phục nhanh chóng** workflow và credentials từ FTP.
✔ **Tránh mất dữ liệu** khi chuyển đổi giữa các phiên bản n8n.
✔ **Tự động hóa hoàn toàn** quá trình khôi phục.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình FTP và SMTP** theo hướng dẫn.
3. **Khởi động khôi phục** và **nhận lại toàn bộ hệ thống n8n** như cũ!

**Chia sẻ kinh nghiệm** của mình trong phần comment dưới đây! 🚀