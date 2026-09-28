---
title: "💾 **Hệ Thống Backup Tự Động Hóa Workflow n8n: Bảo Vệ Dữ Liệu 24/7 Với Google Drive + GitHub**"
description: "Workflow tự động hóa hoàn toàn không cần code để sao lưu toàn bộ cấu hình workflow n8n lên Google Drive và GitHub, đồng thời gửi thông báo kết quả qua Telegram/Discord. Giúp các sếp yên tâm không sợ mất dữ liệu do lỗi server hoặc xóa nhầm."
slug: "huyet-thuong-backup-workflow-n8n-google-drive-github"
tags: [n8n, automation, backup, google-drive, github, telegram, discord, no-code, version-control]
keywords: [backup workflow n8n, tự động hóa lưu trữ dữ liệu, sao lưu cấu hình n8n, google drive api, github automation, telegram notification, discord alert]
---

# 🚀 **Backup Tự Động Hóa Workflow n8n: Bảo Vệ Dữ Liệu Trước Mọi Thảm Hoạ**

### **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã bao giờ lo lắng về việc:
- **Mất toàn bộ cấu hình workflow** do lỗi server, xóa nhầm hoặc update không đúng cách?
- **Không có bản sao lưu** khi muốn thử nghiệm cấu hình mới mà sợ "đập hỏng" toàn bộ hệ thống?
- **Phải thủ công export/import** mỗi khi cần sao lưu, tốn thời gian và dễ sai sót?

**Workflow này giải quyết tất cả!** Với **sao lưu tự động 2 lần/ngày** lên **Google Drive (cloud) + GitHub (version control)**, các sếp sẽ:
✅ **Yên tâm 100%** dữ liệu không bao giờ mất
✅ **Không cần code** – chỉ cần cấu hình 1 lần là chạy tự động
✅ **Kiểm soát phiên bản** nhờ GitHub (có thể quay lại bất kỳ phiên bản nào)
✅ **Thông báo kết quả** qua Telegram/Discord để biết workflow đã backup thành công

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh phụ thuộc vào n8n.cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật cao**: Dữ liệu sao lưu trên **Google Drive (cloud)** và **GitHub (version control)**.
- **Tiết kiệm thời gian**: Không cần thủ công export/import, chạy tự động **2 lần/ngày**.
- **Không sợ mất dữ liệu**: Nếu server n8n bị lỗi, vẫn có thể khôi phục từ backup.
- **Kiểm soát phiên bản**: GitHub giúp **quay lại bất kỳ phiên bản nào** trước khi update.
- **Thông báo tức thời**: Nhận tin nhắn thành công trên **Telegram/Discord**.
- **Dữ liệu sạch**: Tên file được **lọc bỏ ký tự đặc biệt** để tránh lỗi.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **n8n API Credentials**: Để lấy danh sách workflows từ n8n instance.
   - **Google Drive OAuth2**: Để tạo folder và upload file backup.
   - **GitHub OAuth2**: Để push/pull file backup lên repository.
   - **Telegram Bot API** (tùy chọn): Để nhận thông báo qua Telegram.
   - **Discord Bot API** (tùy chọn): Để nhận thông báo qua Discord.

2. **Thông tin cấu hình**:
   - **GitHub**:
     - `repo_owner`: Tên tài khoản GitHub của bạn.
     - `repo_name`: Tên repository để lưu backup (ví dụ: `n8n-backup`).
     - `repo_path`: Đường dẫn folder trong repo (ví dụ: `n8n-backup/`).
   - **Google Drive**:
     - `gdrive_folder_id`: ID của folder cha trong Google Drive (có thể tạo mới trong workflow).
   - **Telegram** (nếu dùng):
     - `telegram_chat_id`: ID của chat Telegram (có thể lấy bằng bot `@userinfobot`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/8771](https://n8n.io/workflows/8771) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **🔹 Node "Config" (Cấu hình chính)**
- Mở node **"Config"** (type: `set`) và cập nhật các tham số:
  ```json
  {
    "repo_owner": "tên_tài_khoản_github_của_bạn",
    "repo_name": "n8n-backup",
    "repo_path": "n8n-backup/",
    "gdrive_folder_id": "ID_folder_Google_Drive_của_bạn",
    "telegram_chat_id": "123456789" // (nếu dùng Telegram)
  }
  ```
  - **Lấy `gdrive_folder_id`**:
    1. Mở Google Drive.
    2. Tạo 1 folder mới (ví dụ: `n8n_backup`).
    3. Click chuột phải → **Share** → Sao chép link.
    4. Trích xuất ID từ URL: `https://drive.google.com/drive/folders/ID_FOLDER_HERE` → `ID_FOLDER_HERE` là `gdrive_folder_id`.

##### **🔹 Node "Create GDrive Folder"**
- Nếu chưa có folder backup trong Google Drive, node này sẽ **tự động tạo folder mới** với tên:
  `wfBackup - YYYY-MM-DD_HH-mm-ss` (ví dụ: `wfBackup - 2024-05-20_14-30-00`).
- **Không cần chỉnh gì** nếu đã có folder sẵn (điền `gdrive_folder_id` vào node "Config").

##### **🔹 Node "Check if File Exists" (Kiểm tra file trên GitHub)**
- Node này sẽ **kiểm tra file đã tồn tại trên GitHub** trước khi update.
- **Không cần chỉnh** nếu đã cấu hình GitHub OAuth2 đúng.

##### **🔹 Node "Notify: Discord" & "Notify: Telegram" (Thông báo kết quả)**
- **Nếu không muốn thông báo**, các sếp có thể **xóa node này** hoặc **bỏ qua** (node `if` sẽ kiểm tra kết quả).
- **Cấu hình Telegram**:
  1. Tạo bot bằng `@BotFather` trên Telegram.
  2. Sao chép `API Token` và `chat_id` (lấy bằng bot `@userinfobot`).
  3. Điền vào node **"telegramApi"** trong n8n.
- **Cấu hình Discord**:
  1. Tạo bot trên [Discord Developer Portal](https://discord.com/developers/applications).
  2. Sao chép `Bot Token` và `Channel ID` (lấy bằng cách share link channel và trích xuất ID).
  3. Điền vào node **"discordBotApi"** trong n8n.

##### **🔹 Node "Schedule Trigger" (Chạy tự động)**
- Node này **cấu hình chạy 2 lần/ngày** (mặc định là 12 giờ/lần).
- **Không cần chỉnh** nếu muốn giữ mặc định.
- **Nếu muốn thay đổi lịch**, mở node và chỉnh `cron` (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn node **"Manual Trigger"** và nhấn **"Execute"** để kiểm tra workflow.
   - Kiểm tra:
     - File đã được tạo trên Google Drive không?
     - File đã được push lên GitHub không?
     - Có nhận được thông báo Telegram/Discord không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu log chi tiết**:
   - Thêm node **`n8n-nodes-base.telegram`** hoặc **`n8n-nodes-base.discord`** để gửi log lỗi nếu workflow bị crash.
   - Ví dụ: Nếu node `github` lỗi, có thể gửi tin nhắn cảnh báo.

2. **Tự động xóa backup cũ**:
   - Thêm node **`googleDrive`** để xóa folder backup cũ sau 30 ngày (tránh chiếm dung lượng).

3. **Kết hợp với Slack**:
   - Thay vì Telegram/Discord, các sếp có thể dùng **Slack Webhook** để thông báo.

4. **Backup thêm vào Dropbox/OneDrive**:
   - Thêm node **`dropbox`** hoặc **`onedrive`** để sao lưu song song.

5. **Tự động khôi phục từ backup**:
   - Nếu server n8n bị lỗi, các sếp có thể:
     - Tải file `.json` từ GitHub.
     - Import vào n8n mới để khôi phục.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Bảo vệ dữ liệu** của mình một cách tự động.
✔ **Không lo mất cấu hình** workflow do lỗi server.
✔ **Không cần code** – chỉ cần cấu hình 1 lần là chạy tự động.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các API key** và thông tin GitHub/Google Drive.
3. **Bật Active** và **yên tâm** dữ liệu được bảo vệ 24/7!

---
**🚀 Cần hỗ trợ thêm?** Để lại comment hoặc liên hệ qua [n8n Community](https://community.n8n.io/) để được hỗ trợ chi tiết!