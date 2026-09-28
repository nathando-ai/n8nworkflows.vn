---
title: "🔄 **Hệ Thống Tự Động Khôi Phục Credential & Workflow cho n8n Self-Hosted – Không Cần Code!**"
description: "Giải pháp hoàn toàn tự động hóa khôi phục credential và workflow n8n từ backup, giúp các sếp tiết kiệm thời gian và tránh mất dữ liệu khi chuyển instance hoặc khắc phục lỗi. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tự-dộng-hoá-khôi-phục-credential-workflow-n8n"
tags: [n8n, tự động hóa, self-hosted, backup-restore, credential-management]
keywords: [n8n workflow khôi phục, tự động hóa n8n, backup credential n8n, chuyển instance n8n, khôi phục workflow n8n]
---

# 🔄 **Khôi Phục Credential & Workflow n8n Tự Động – Chuyển Instance Hoàn Toàn An Toàn!**

### **Nỗi Đau Của Các Sếp Khi Khôi Phục n8n**
Các sếp tự host n8n thường gặp phải những tình huống khó khăn khi:
- **Chuyển instance** từ VPS cũ sang mới, nhưng **credential và workflow bị mất** do không có backup hệ thống.
- **Lỗi server** hoặc **xóa nhầm dữ liệu**, khiến phải **tải lại từ đầu** các workflow đã đầu tư thời gian xây dựng.
- **Không biết cách khôi phục** credential (như SMTP, API keys) một cách **an toàn và tự động**, dẫn đến phải nhập lại từ đầu.
- **Sợ mất dữ liệu** khi nâng cấp phiên bản n8n hoặc thay đổi cấu hình.

**Giải pháp?** Một **workflow tự động hóa hoàn toàn** chỉ cần **1 lần setup**, sau đó **khôi phục credential và workflow chỉ với 1 nút bấm** – **không cần code, không cần lo lắng!**

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Khôi phục toàn bộ credential & workflow chỉ trong vài giây** (không cần nhập lại từ đầu).
✅ **Chuyển instance n8n an toàn** giữa các VPS mà **không mất dữ liệu**.
✅ **Hoạt động 24/7 tự động**, không cần can thiệp thủ công.
✅ **Giảm thiểu rủi ro** khi nâng cấp phiên bản hoặc khắc phục lỗi server.
✅ **Dễ dàng backup định kỳ** để bảo vệ dữ liệu.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Backup folder** chứa các file backup credential và workflow.
   - **Đường dẫn mặc định:** `/files/n8n-backups` (có thể thay đổi trong node **Init**).
   - **Cấu trúc folder:**
     ```
     /files/n8n-backups/
     ├── credentials/
     │   └── n8n-credentials.json  (file credential backup)
     └── workflows/
         └── [backup_workflows_YYYYMMDD]/
             ├── workflow1.json
             ├── workflow2.json
             └── ...
     ```
2. **Quá trình khôi phục có 2 tùy chọn:**
   - **Khôi phục credential** (n8n-credentials.json).
   - **Khôi phục workflow** (tất cả hoặc chỉ một số workflow).
3. **Tài khoản email** (để nhận thông báo thành công/lỗi).
4. **N8n Self-Hosted** (không hỗ trợ n8n Cloud).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/9154) (chọn **Export JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/9154) và dán vào **Import Workflow** trong n8n.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Dán toàn bộ mã JSON từ [workflow gốc](https://n8n.io/workflows/9154) vào ô **Paste JSON**.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình các node quan trọng** như sau:

#### **🔹 Node "Start Restore" (Manual Trigger)**
- **Chức năng:** Bắt đầu quá trình khôi phục.
- **Cấu hình:**
  - **JSON Input:**
    ```json
    [
      {
        "credentials": true,
        "workflows": true
      }
    ]
    ```
    - **Giải thích:**
      - `credentials: true` → Khôi phục credential.
      - `workflows: true` → Khôi phục workflow.
      - **Lưu ý:** Nếu chỉ muốn khôi phục credential, đặt `workflows: false`.

#### **🔹 Node "Init" (Code)**
- **Chức năng:** Xác định đường dẫn backup và biến môi trường.
- **Mã cần chỉnh:**
  ```javascript
  const BACKUP_FOLDER = $env.N8N_BACKUP_FOLDER || '/files/n8n-backups';
  const workflows_temp_folder = '_restore_temp';
  const credentials = "n8n-credentials";
  ```
  - **Đường dẫn backup (`BACKUP_FOLDER`):**
    - Nếu backup ở vị trí khác, thay đổi giá trị này (ví dụ: `/backup/n8n`).
  - **Tên folder credential (`credentials`):**
    - Nếu file credential có tên khác (không phải `n8n-credentials.json`), chỉnh sửa ở đây.

#### **🔹 Node "Find Last Backup" (Code)**
- **Chức năng:** Tìm folder backup mới nhất trong `workflows_temp_folder`.
- **Mã mặc định:**
  ```javascript
  const fs = require('fs');
  const path = require('path');

  const backupFolder = $input.all()[0].json.BACKUP_FOLDER;
  const workflowsFolder = path.join(backupFolder, 'workflows');

  const folders = fs.readdirSync(workflowsFolder);
  const latestBackup = folders.reduce((latest, folder) => {
    const folderDate = folder.replace(/[^0-9]/g, '');
    return folderDate > latest ? folder : latest;
  }, '');

  $output.all().set('latestBackup', latestBackup);
  ```
  - **Không cần chỉnh** trừ khi backup có cấu trúc khác.

#### **🔹 Node "Restore Credentials?" & "Restore Workflows?" (If)**
- **Chức năng:** Xác định xem có khôi phục credential/workflow hay không.
- **Cấu hình:**
  - **Node "Restore Credentials?"** sẽ kiểm tra `credentials: true` trong JSON input.
  - **Node "Restore Workflows?"** sẽ kiểm tra `workflows: true` trong JSON input.
  - **Không cần chỉnh** nếu đã cấu hình đúng ở **Start Restore**.

#### **🔹 Node "SUCCESS email" & "SUCCESS email Workflows" (Email Send)**
- **Chức năng:** Gửi email thông báo thành công khi khôi phục.
- **Cấu hình:**
  - **SMTP Credential:** Chọn credential SMTP đã cấu hình trong n8n.
  - **Nội dung email:**
    - **Thành công khôi phục credential:**
      ```
      Subject: [n8n] Credentials đã được khôi phục thành công!
      Body: Các credential đã được khôi phục từ backup: {BACKUP_FOLDER}/credentials/n8n-credentials.json
      ```
    - **Thành công khôi phục workflow:**
      ```
      Subject: [n8n] Workflow đã được khôi phục thành công!
      Body: {COUNT} workflow đã được khôi phục từ backup: {BACKUP_FOLDER}/workflows/{LATEST_BACKUP}
      ```

#### **🔹 Node "ERROR: Find Most Recent Bkp Folder" (Stop & Error)**
- **Chức năng:** Dừng workflow nếu không tìm thấy folder backup.
- **Không cần chỉnh**, nhưng **nên kiểm tra log** nếu workflow dừng bất thường.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Nhấn **Run Workflow** và chọn **JSON Input** như sau:
     ```json
     [
       {
         "credentials": true,
         "workflows": true
       }
     ]
     ```
   - Kiểm tra **log** để đảm bảo không có lỗi.

2. **Bật Active Workflow:**
   - Sau khi test thành công, nhấn **Active** để workflow hoạt động tự động khi được kích hoạt.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Khôi Phục Định Kỳ (Cron Job)**
- **Sử dụng Cron** để chạy workflow hàng ngày để **backup và khôi phục tự động**.
- **Cú pháp Cron cho n8n (Self-Hosted):**
  ```bash
  0 3 * * * cd /path/to/n8n && n8n exec --workflow "Automated Workflow & Credential Restoration" --data '{"credentials": true, "workflows": true}'
  ```
  - **Thời gian chạy:** 3h sáng hàng ngày (thay đổi theo nhu cầu).

### **2. Gửi Log Khôi Phục qua Slack/Telegram**
- **Thêm node Slack/Telegram** sau **SUCCESS email** để nhận thông báo ngay khi khôi phục.
- **Cấu hình:**
  - **Node Slack:** Chọn credential Slack và gửi message:
    ```
    🚀 **n8n Backup Restore Success!**
    - Credentials: ✅ {credentials ? 'Khôi phục' : 'Bỏ qua'}
    - Workflows: ✅ {workflows ? 'Khôi phục' : 'Bỏ qua'}
    - Backup Folder: {BACKUP_FOLDER}
    ```

### **3. Lưu Log Khôi Phục vào Google Sheets**
- **Thêm node Google Sheets** để ghi lịch sử khôi phục.
- **Cấu hình:**
  - **Sheet Name:** `n8n_backup_logs`
  - **Dữ liệu ghi:**
    | Thời gian | Loại Khôi Phục | Thành Công | Lỗi (nếu có) |
    |-----------|----------------|------------|---------------|
    | `{{$now}}` | `{{credentials ? 'Credential' : 'Workflow'}}` | `{{success ? '✅' : '❌'}}` | `{{error || 'Không'}}` |

### **4. Khôi Phục Chỉ Một Số Workflow Chọn Lọc**
- **Sử dụng node `Execute Command` (Filter Workflows):**
  ```bash
  # Lọc workflow có tên bắt đầu bằng "sales_"
  ls /files/n8n-backups/workflows/latest/ | grep 'sales_' > workflows_to_restore.txt
  ```
  - Sau đó, **đọc file này** trong node **Restore Workflows** để chỉ khôi phục workflow cụ thể.

---
## 📌 **Kết Luận**
### **Tại Sao Các Sếp Nên Sử Dụng Workflow Này?**
- **Tiết kiệm thời gian:** Không cần nhập lại credential/workflow từ đầu.
- **An toàn:** Khôi phục **tự động và chính xác**, giảm thiểu lỗi người dùng.
- **Dễ dàng chuyển instance:** Chuyển n8n giữa các VPS mà **không mất dữ liệu**.
- **Hoạt động 24/7:** Khôi phục **một cách tự động** khi cần.

**Hành động ngay!**
1. **Setup backup folder** theo cấu trúc trên.
2. **Import workflow** và **cấu hình** như hướng dẫn.
3. **Test run** và **bật Active**.
4. **Tự động hóa** với Cron hoặc trigger thủ công khi cần.

**🎁 Mã giảm giá VPS cho n8n:**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Bắt đầu tự động hóa khôi phục n8n của mình ngay hôm nay!** 🚀