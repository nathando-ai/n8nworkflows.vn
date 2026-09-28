---
title: "🗄️ **Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang Google Drive Với Cấu Trúc Gốc Rễ (Self-Hosted & Cloud)**"
description: "Giải pháp tự động hóa 100% không code để sao lưu toàn bộ cấu trúc thư mục và workflow n8n sang Google Drive, bảo toàn cấu trúc gốc rễ và hoạt động 24/7. Phù hợp cho cả n8n Cloud và Self-Hosted."
slug: "backup-n8n-workflows-google-drive"
tags: [n8n, automation, backup, google-drive, devops, self-hosted]
keywords: [backup n8n workflow, tự động hóa lưu trữ n8n, sao lưu cấu trúc thư mục n8n, google drive n8n, lưu trữ an toàn workflow]
---

# 🚀 **Backup Tất Cả Workflow n8n Sang Google Drive Với Cấu Trúc Gốc Rễ**

## **💡 Giải Pháp Cho Nỗi Lo Lại "Nếu N8n Điện Tử Tắt Hết?"**
Các sếp đã từng gặp phải tình huống **không thể truy cập workflow quan trọng** do lỗi server, cập nhật không đúng cách, hoặc thậm chí là **xóa nhầm cấu trúc thư mục** trong n8n? Hay **không muốn phụ thuộc vào n8n Cloud** mà muốn lưu trữ an toàn trên Google Drive?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Sao lưu toàn bộ cấu trúc thư mục n8n** (bao gồm cả thư mục con) sang Google Drive.
✅ **Tạo bản sao JSON hoàn chỉnh** của từng workflow, **không mất cấu trúc gốc**.
✅ **Chạy tự động theo lịch** (hoặc thủ công) **mỗi ngày/tuần** để đảm bảo dữ liệu luôn mới nhất.
✅ **Phù hợp cho cả n8n Cloud và Self-Hosted** (chỉ cần có API access).
✅ **Không giới hạn API** (khác với Google Sheets, n8n Table hỗ trợ nhiều request hơn).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh phụ thuộc vào n8n Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo toàn 100% cấu trúc thư mục n8n** (không mất mát folder con).
- **Lưu trữ an toàn trên Google Drive**, dễ dàng chia sẻ với team.
- **Không cần code**, chỉ cần cấu hình API và Google Drive OAuth.
- **Chạy tự động hàng ngày** (hoặc theo lịch tùy chọn).
- **Không giới hạn API** (khác với Google Sheets, n8n Table hỗ trợ nhiều request hơn).
- **Khôi phục nhanh chóng** nếu xảy ra lỗi trên n8n.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n** (Cloud hoặc Self-Hosted) với quyền **API access**.
2. **Google Drive OAuth 2.0 API Key** (để tạo folder và upload file).
3. **Thư mục chính trên Google Drive** (ví dụ: `my_n8n_backup`) để lưu backup.
4. **Thời gian ~5-10 phút** để cấu hình lần đầu (sau đó chỉ cần kích hoạt tự động).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13245](https://n8n.io/workflows/13245) hoặc copy/paste JSON vào **n8n Editor**.
- **Chọn "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** (103 nodes) nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

##### **🔹 Node "n8n instance/project access details" (Set)**
- **Cấu hình API n8n**:
  - `n8n_instance_URL`: Điền URL n8n của bạn (không có `/` cuối). Ví dụ:
    ```
    https://myautomations.app.n8n.cloud
    ```
  - `emailOrLdapLoginId`: Email đăng nhập n8n.
  - `password`: Mật khẩu của tài khoản n8n.

##### **🔹 Node "Create backup folder "n8n_backup_folder_structure_ddMMyyyy_HHmmss"" (Google Drive)**
- **Chọn thư mục cha** là thư mục chính đã tạo trước trên Google Drive (ví dụ: `my_n8n_backup`).
- **Không cần đổi tên**, workflow sẽ tự động tạo tên folder backup theo định dạng:
  ```
  n8n_backup_folder_structure_DDMMYYYY_HHmmss
  ```
  (Ví dụ: `n8n_backup_folder_structure_02022026_123343`).

##### **🔹 Node "Schedule Trigger" (Schedule)**
- **Chọn thời gian chạy tự động** (ví dụ: **mỗi ngày 2 giờ sáng**).
- **Hoặc chạy thủ công** bằng cách kích hoạt workflow từ n8n Dashboard.

##### **🔹 Node "Google Drive OAuth2Api" (Credentials)**
- **Đảm bảo đã cấu hình OAuth 2.0** trong n8n với quyền:
  - `drive.file` (đọc/tạo/xóa file).
  - `drive.metadata.readonly` (đọc metadata folder).

##### **🔹 Node "Convert workflow to JSON file" (ConvertToFile)**
- **Không cần chỉnh sửa**, workflow sẽ tự động chuyển đổi JSON workflow thành file uploadable.

##### **🔹 Node "dataTableId \"folders\" & \"workflows\"" (Set)**
- **Không cần thay đổi**, n8n sẽ tự động tạo và quản lý 2 bảng dữ liệu (`folders` và `workflows`) để theo dõi cấu trúc.

---
#### **3. Kích Hoạt ⚡️**
1. **Test run** với **1-2 workflow đơn giản** để kiểm tra cấu trúc backup.
2. **Bật Active workflow** và **chờ kết quả**:
   - Nếu thành công, các sếp sẽ thấy **cấu trúc thư mục n8n được sao lưu hoàn chỉnh** trên Google Drive.
   - **Log lỗi** (nếu có) sẽ hiển thị trong n8n Dashboard.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC CẢNH BÁO & MẶT TRẬN]
- **Không sao lưu workflow đã archived**: Workflow tự động **bỏ qua** workflow đã xóa/archived.
- **Không sao lưu folder trống**: Nếu folder không có workflow nào, nó sẽ **không được tạo** trên Google Drive.
- **Sử dụng n8n Table thay vì Google Sheets**: Vì **Google Sheets có giới hạn API** (60 request/phút), trong khi n8n Table **không giới hạn**.
:::

#### **🔹 Mở Rộng Thêm Slack/Telegram Notifications**
- **Thêm node Slack/Telegram** sau node `Upload file to Google Drive` để **báo cáo thành công/thất bại** mỗi lần backup.
- **Cấu hình webhook** trong Slack/Telegram và kết nối với node `HTTP Request`.

#### **🔹 Lưu Log Lỗi Cho Dễ Dàng Debug**
- **Thêm node `StickyNote`** sau node `Google Drive` để ghi **log lỗi** (nếu có).
- **Kết hợp với Email Notifications** để nhận báo cáo lỗi qua email.

#### **🔹 Tạo Báo Cáo Định Kỳ**
- **Sử dụng node `Schedule Trigger` + `Google Sheets`** để tạo **báo cáo tổng hợp** về số lượng workflow backup mỗi tháng.

#### **🔹 Khôi Phục Nhanh Chóng**
- **Nếu xóa nhầm workflow**, các sếp chỉ cần:
  1. **Tải file JSON** từ Google Drive.
  2. **Import lại** vào n8n.

---

### 📌 **Kết Luận**
Workflow này **giải quyết triệt để** vấn đề **sao lưu an toàn n8n** mà không cần code. Với **cấu trúc thư mục gốc rễ được bảo toàn**, các sếp có thể:
✔ **Yên tâm** khi n8n Cloud bị lỗi.
✔ **Khôi phục nhanh chóng** nếu xảy ra sự cố.
✔ **Chia sẻ backup** với team một cách dễ dàng.

**Hành động ngay!**
1. **Import workflow** và cấu hình API.
2. **Kích hoạt tự động** theo lịch.
3. **Quên mất lo lắng về mất dữ liệu!**

---
**🚀 Cần hỗ trợ kỹ thuật?** Đăng ký **VPS Self-Hosted n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để chạy workflow ổn định 24/7!