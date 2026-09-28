---
title: "🗄️ Tự Động Hoàn Chỉnh: Sao Lưu Tất Cả Workflow n8n Về Google Drive Với Hệ Thống Xóa Tự Động (Backup + Cleanup)"
description: "Workflow này tự động sao lưu toàn bộ workflow n8n của các sếp vào Google Drive hàng ngày, đồng thời xóa tự động các bản sao lưu cũ để tiết kiệm không gian và đảm bảo dữ liệu luôn an toàn. Giúp các sếp không phải lo lắng về mất mát dữ liệu khi có sự cố hệ thống."
slug: "tự-dộng-hoàn-chỉnh-sao-lưu-workflow-n8n-google-drive"
tags: [n8n, automation, backup, google-drive, devops, no-code]
keywords: [sao lưu workflow n8n, tự động hóa backup, xóa tự động Google Drive, lưu trữ an toàn workflow, backup hàng ngày]
---

# 🗄️ **Tự Động Hoàn Chỉnh: Sao Lưu Workflow n8n Về Google Drive Với Hệ Thống Xóa Tự Động**

## **🔥 Nỗi Đau Của Các Sếp Khi Sao Lưu Workflow n8n**
Các sếp đã từng gặp phải tình huống nào sau đây?
- **Mất dữ liệu workflow** do lỗi hệ thống, update không đúng cách hoặc xóa nhầm?
- **Phải thủ công sao lưu** hàng ngày, tốn thời gian và dễ quên?
- **Google Drive bị đống đống** các bản sao lưu cũ, không gian bị chiếm dụng không cần thiết?
- **Không biết cách xóa tự động** các bản sao lưu cũ mà vẫn giữ lại những phiên bản quan trọng?

Workflow này **giải quyết tất cả** những vấn đề trên bằng cách:
✅ **Sao lưu tự động** tất cả workflow n8n vào Google Drive **hàng ngày** (hoặc theo lịch bạn thiết lập).
✅ **Xóa tự động** các bản sao lưu cũ, giữ lại chỉ **30 bản sao lưu gần nhất** (bạn có thể điều chỉnh số lượng).
✅ **Tạo cấu trúc gọn gàng** với tên folder theo định dạng `Workflows backup - [ngày-tháng-năm]`.
✅ **Không cần code**, chỉ cần cấu hình vài bước đơn giản.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh gián đoạn do phiên bản miễn phí của n8n.io.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công sao lưu hàng ngày.
- **Dữ liệu an toàn**: Sao lưu tự động hàng ngày, giảm thiểu rủi ro mất mát.
- **Google Drive gọn gàng**: Xóa tự động các bản sao lưu cũ, giữ lại chỉ những phiên bản cần thiết.
- **Cấu trúc rõ ràng**: Mỗi ngày có một folder riêng, dễ quản lý và tìm kiếm.
- **Hoạt động liên tục**: Dùng lịch trình (schedule) để chạy tự động mỗi đêm.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền **quản trị viên** (để tạo folder và upload file).
2. **API Key của n8n** (để workflow có thể lấy danh sách tất cả workflows).
3. **Folder chính trong Google Drive** (để lưu tất cả các bản sao lưu).
4. **Số lượng bản sao lưu muốn giữ lại** (ví dụ: 30 ngày).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/7512](https://n8n.io/workflows/7512) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (chọn **Import Workflow** → **Paste JSON**).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Credentials (Bắt buộc)**
- **Google Drive OAuth2**:
  - Đăng nhập vào Google Drive và cấp quyền cho n8n.
  - Thêm **credentials** mới trong n8n với loại `googleDriveOAuth2Api`.
- **n8n API**:
  - Đăng nhập vào n8n và lấy **API Key** từ **Settings → API**.
  - Thêm **credentials** mới trong n8n với loại `n8nApi`.

##### **B. Cấu Hình Node "CONFIG - Set your variables here"**
Trong node này, các sếp cần điền:
- **`parentFolderId`**: ID của folder chính trong Google Drive (hướng dẫn lấy ID ở phần dưới).
- **`backupsToKeep`**: Số lượng bản sao lưu gần nhất muốn giữ lại (ví dụ: `30` để giữ 30 ngày).

##### **C. Cấu Hình Lịch Trình (Schedule Trigger)**
- Node **Schedule Trigger** được cấu hình mặc định để chạy **mỗi ngày lúc 3h sáng** (bạn có thể thay đổi).
- Nếu muốn chạy **manual**, có thể sử dụng node **Manual Trigger** thay thế.

##### **D. Hướng Dẫn Lấy `parentFolderId`**
1. Mở [Google Drive](https://drive.google.com).
2. Chọn folder muốn dùng làm folder chính (hoặc tạo mới một folder tên `n8n Backups`).
3. Click vào folder → URL trong trình duyệt sẽ hiển thị một chuỗi dài như:
   ```
   https://drive.google.com/drive/folders/1Fs3gg7pSVhbvODJQLcgAfP-V0rCGC_Oc
   ```
4. **`parentFolderId`** là chuỗi sau `folders/` (trong ví dụ trên là `1Fs3gg7pSVhbvODJQLcgAfP-V0rCGC_Oc`).

##### **E. Cấu Hình Node "Sort and isolate old folders" (Code)**
Node này sử dụng **JavaScript** để phân loại folder cũ. Các sếp **không cần chỉnh sửa** nếu muốn sử dụng logic mặc định (xóa folder cũ hơn `backupsToKeep`).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node **Manual Trigger** để kiểm tra workflow có hoạt động không.
   - Kiểm tra Google Drive xem có tạo folder mới không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** cho workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Gửi thông báo Slack/Telegram** khi backup hoàn tất:
  - Thêm node **Slack** hoặc **Telegram Bot** sau node **Upload workflow to Google Drive** để thông báo kết quả.
- **Lưu log vào Google Sheets**:
  - Thêm node **Google Sheets** để ghi lại lịch sử backup (ngày giờ, số lượng workflow, trạng thái).
- **Tự động xóa folder cũ hơn 1 năm**:
  - Thay đổi logic trong node **Code** để xóa folder cũ hơn 365 ngày.
- **Sao lưu workflows chỉ của một team nhất định**:
  - Sử dụng node **Filter** trước node **Get all n8n workflows** để chỉ lấy workflows của team cụ thể.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Sao lưu tự động** workflow n8n hàng ngày.
✔ **Giảm thiểu rủi ro mất dữ liệu**.
✔ **Giảm bớt công việc thủ công**.
✔ **Giúp Google Drive luôn gọn gàng**.

**Hành động ngay hôm nay!**
1. Import workflow vào n8n.
2. Cấu hình credentials và `parentFolderId`.
3. Bật Active và **quên đi lo lắng về mất dữ liệu!**

---
**🚀 Cần hỗ trợ thêm?** Hãy để lại comment bên dưới hoặc liên hệ với chúng tôi qua [Facebook](https://facebook.com/n8n.vn) để được tư vấn chi tiết!