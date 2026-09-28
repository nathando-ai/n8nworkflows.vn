---
title: "💾 **Tự Động Hoàn Hảo: Backup n8n Workflow Sang Google Drive Với Tính Năng Xóa Tự Động (Hỗ Trợ 24/7)**"
description: "Giải pháp hoàn toàn tự động hóa backup tất cả workflow n8n sang Google Drive theo lịch trình (mặc định 1 giờ/lần), đồng thời xóa tự động các bản sao cũ hơn 7 ngày để tiết kiệm không gian lưu trữ. Phù hợp cho quản trị viên, nhà phát triển và tổ chức cần bảo mật dữ liệu."
slug: "backup-n8n-workflow-google-drive-auto-cleanup"
tags: [n8n, automation, backup, google-drive, devops, no-code, cloud-storage]
keywords: [backup n8n workflow, tự động hóa lưu trữ, Google Drive API, xóa tự động backup, lưu trữ an toàn workflow, n8n self-hosted]
---

# 🚀 **Backup Tự Động Workflow n8n Sang Google Drive Với Xóa Tự Động (Hỗ Trợ 24/7)**

### **Giải pháp hoàn toàn không cần code cho quản trị viên n8n**
Làm thế nào để **bảo vệ toàn bộ workflow n8n** của bạn khỏi mất mát, lỗi hệ thống hoặc thay đổi ngẫu nhiên? Hoặc **không phải lo lắng về việc phải backup thủ công** hàng ngày? **Workflow này sẽ tự động hóa toàn bộ quá trình** với các tính năng:
✅ **Backup theo lịch trình** (mặc định 1 giờ/lần)
✅ **Tạo thư mục duy nhất** với định dạng `n8n_backup_YYYY-MM-DD_HH`
✅ **Lưu trữ từng workflow** dưới dạng file JSON riêng biệt
✅ **Xóa tự động** các backup cũ hơn **7 ngày** (cấu hình được)
✅ **Hỗ trợ 24/7** khi chạy trên VPS riêng (Self-hosted)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì phiên bản cloud. Với VPS, bạn có thể:
- **Chỉnh sửa lịch trình backup** linh hoạt (ví dụ: backup 2 giờ/lần vào giờ làm việc).
- **Tăng tốc độ xử lý** do không bị giới hạn tài nguyên cloud.
- **Bảo mật cao** với quyền truy cập riêng tư.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Hỗ trợ 24/7, SSD, IP Dedicated)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công export/import workflow.
- **Bảo mật tối đa**: Backup tự động hàng giờ, giảm rủi ro mất dữ liệu.
- **Quản lý không gian**: Xóa tự động backup cũ, tránh tốn kém Google Drive.
- **Phục hồi nhanh**: Khôi phục bất kỳ phiên bản workflow cũ nhất định.
- **Hỗ trợ 24/7**: Chạy liên tục trên VPS, không phụ thuộc vào phiên bản cloud.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền chỉnh sửa folder mục tiêu.
2. **API Key của n8n** (Self-hosted) để workflow có thể truy cập dữ liệu.
3. **Folder cha trong Google Drive** (ví dụ: `n8n_Backups`) để lưu trữ backup.
4. **Thời gian backup** (mặc định 1 giờ/lần, có thể điều chỉnh).

---
:::info[CHUẨN BỊ]
- **Google Drive OAuth2 API Credentials**: Tạo trong [Google Cloud Console](https://console.cloud.google.com/).
- **n8n API Key**: Tạo trong **Settings > API** của n8n Self-hosted.
- **Folder mục tiêu**: Chọn folder trong Google Drive để lưu backup (ví dụ: `n8n_Backups`).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/4515](https://n8n.io/workflows/4515) và import vào **n8n Editor**.
- **Copy/paste JSON** từ file vào **Create New Workflow** trong n8n.

:::note[Lưu ý]
- **Không thay đổi cấu trúc** của các node quan trọng (như `n8n`, `Google Drive`, `Schedule Trigger`).
- **Không xóa node `Error Workflow`** (mặc định là `KhpM42Ckgy6qgzCz`), trừ khi bạn đã tạo workflow xử lý lỗi riêng.
:::

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình các node sau**:

| **Node**                          | **Tham số cần chỉnh**                          | **Hướng dẫn**                                                                 |
|-----------------------------------|-----------------------------------------------|-------------------------------------------------------------------------------|
| **Schedule Trigger**              | `Rule` (ví dụ: `0 0 * * *` = hàng giờ)        | Thay đổi lịch trình backup (ví dụ: `0 0 */6 * *` = backup 6 giờ/lần).         |
| **Google Drive Backup Folder**    | `Drive ID` & `Folder ID`                      | Chọn folder cha trong Google Drive (ví dụ: `n8n_Backups`).                     |
| **n8n Node**                      | `n8nApi` (credentials)                        | Điền **API Key** của n8n Self-hosted.                                         |
| **Settings**                      | `Coverage Period` (mặc định: 7)              | Thiết lập số ngày backup được giữ (ví dụ: `30` để giữ 30 ngày).               |
| **Google Drive Upload Workflows** | `Folder ID` (thư mục backup mới)              | Sử dụng **tham chiếu từ node `Google Drive Backup Folder`**.                  |
| **Google Drive Delete**           | `Folder ID` (thư mục cũ)                     | Node này sẽ tự động lấy danh sách folder cũ từ `Coverage Period`.             |

:::tip[Mẹo]
- **Kiểm tra folder ID** trong Google Drive bằng cách mở folder > URL > phần `folder_id=...`.
- **Test run** trước khi kích hoạt: Chọn **Test Tab** để chạy thử với dữ liệu mẫu.
:::

#### **3. Kích hoạt ⚡️**
1. **Test Run**: Chọn **Test Tab** và chạy thử với **1 workflow mẫu**.
2. **Kiểm tra Google Drive**: Đảm bảo backup được tạo thành công.
3. **Bật Active**: Chuyển **Active** sang `ON` trong n8n Editor.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Backup chỉ workflow quan trọng**:
   - Thêm **node `Filter`** sau `n8n` để lọc workflow theo tên/tag (ví dụ: `name == "workflow_important"`).

2. **Gửi thông báo khi backup thất bại**:
   - Sử dụng **node `Slack`** hoặc **`Email`** trong **Error Workflow** để báo lỗi.

3. **Lưu log backup**:
   - Thêm **node `Google Sheets`** để ghi lại lịch sử backup (thời gian, số workflow, trạng thái).

4. **Backup sang nhiều nơi**:
   - Sử dụng **node `Dropbox`** hoặc **`AWS S3`** song song với Google Drive.

5. **Tăng thời gian chờ giữa upload**:
   - Nếu có nhiều workflow, tăng **`Wait` node** từ 3s lên 5s để tránh bị rate limit.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản trị n8n muốn:
✔ **Bảo vệ dữ liệu** khỏi mất mát.
✔ **Tiết kiệm thời gian** với backup tự động.
✔ **Quản lý không gian** với xóa tự động backup cũ.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Kích hoạt** và **quên việc backup thủ công**!
3. **Tối ưu hóa** bằng cách thêm Slack/Email thông báo lỗi.

👉 **[Tải workflow ngay](https://n8n.io/workflows/4515)** và bắt đầu tự động hóa backup của mình!

---
**Cần hỗ trợ thêm?**
- **Liên hệ tác giả**: [daniel@aiautomationpro.org](mailto:daniel@aiautomationpro.org)
- **Hỗ trợ kỹ thuật**: [Diễn đàn n8n](https://community.n8n.io/) hoặc [TinoHost](https://tino.vn/support) (đối với VPS).