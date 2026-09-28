---
title: "📁 [Tự Động Hóa Sao Chép Nested Folder Google Drive Với Bảo Toàn Quyền Truy Cập - 100% Không Code]"
description: "Workflow này tự động sao chép toàn bộ cấu trúc thư mục Google Drive (bao gồm file và subfolder) cùng với tất cả quyền chia sẻ, metadata và cấu trúc nhánh vô hạn - giải pháp hoàn hảo cho backup, template hoặc di chuyển dữ liệu an toàn mà không cần viết một dòng code."
slug: "tieu-dong-hoa-sao-chep-google-drive-voi-quyen-truy-cap"
tags: [n8n, automation, google-drive, file-management, recursive-workflow]
keywords: [n8n workflow google drive, sao chép thư mục google drive, tự động hóa backup, quyền truy cập google drive, lưu trữ đám mây]
---

# 🚀 **Tự Động Hóa Sao Chép Thư Mục Nested Google Drive Với Bảo Toàn Quyền Truy Cập**

### **Giải pháp hoàn hảo cho các sếp quản lý dữ liệu đám mây**
Bạn đã bao giờ phải mất nhiều giờ để sao chép thủ công một thư mục Google Drive có hàng trăm file và subfolder vô hạn? Hay phải lo lắng về việc mất quyền truy cập khi copy dữ liệu? **Workflow này sẽ giải quyết tất cả những vấn đề đó trong vài phút!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Sao chép toàn bộ cấu trúc thư mục** (tất cả file, subfolder và nested folder) **vô hạn sâu** chỉ với một lần click.
- **Bảo toàn tất cả quyền chia sẻ** (quyền đọc, chỉnh sửa, chia sẻ) của từng file và folder.
- **Giữ nguyên metadata** (người tạo, ngày cập nhật, mô tả...) khi copy.
- **Tiết kiệm thời gian** từ hàng giờ/lần xuống chỉ vài phút.
- **Không cần code** - hoàn toàn tự động hóa với n8n.
- **Dùng cho backup, template, di chuyển dữ liệu** an toàn và chính xác 100%.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive OAuth2**:
   - Cài đặt [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/python) và tạo **OAuth2 Credentials** trong [Google Cloud Console](https://console.cloud.google.com/).
   - **Scope cần thiết**: `https://www.googleapis.com/auth/drive`.

2. **Thông tin thư mục**:
   - **ID thư mục nguồn (Source Folder ID)**: Thư mục bạn muốn sao chép.
   - **ID thư mục đích (Target Parent Folder ID)**: Thư mục cha nơi dữ liệu sẽ được copy vào.
   - **Tên thư mục mới (New Folder Name)**: Tên cho thư mục sao chép (ví dụ: "Backup_Project_X").

3. **Quyền truy cập**:
   - **Đọc** thư mục nguồn.
   - **Ghi** vào thư mục đích.
   - **Quyền admin** để sao chép quyền chia sẻ (nếu cần).
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7402) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **"Active"** ở góc trên bên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **cấu trúc gọi đệ quy (recursive)** để sao chép tất cả thư mục con. Dưới đây là các bước **cần chỉnh sửa bắt buộc**:

##### **A. Cấu hình "Set Configuration" (Node đầu tiên)**
- **Thay đổi các tham số sau** trong node này:
  - `sourceFolderId`: ID thư mục nguồn (lấy từ liên kết Google Drive: `https://drive.google.com/drive/folders/[ID]`).
  - `targetParentFolderId`: ID thư mục cha đích (nơi dữ liệu sẽ được copy vào).
  - `newFolderName`: Tên mới cho thư mục sao chép (ví dụ: `"Backup_${new Date().toISOString().slice(0,10)}"` để tự động thêm ngày).

##### **B. Cấu hình Google Drive OAuth2**
- Trong **n8n Credentials**, tạo một **Google Drive OAuth2** mới:
  - Đăng nhập tài khoản Google.
  - Chọn **Google Drive API** với scope `https://www.googleapis.com/auth/drive`.
  - Lưu credentials và **gán cho tất cả node Google Drive** trong workflow.

##### **C. Kiểm tra node "Check File Has Permissions" và "Check Folder Has Permissions"**
- Các node này sử dụng **logic mặc định** để sao chép quyền. **Không cần chỉnh sửa** trừ khi bạn muốn thay đổi cách xử lý quyền (ví dụ: bỏ qua quyền nhất định).
- Nếu muốn **bỏ qua quyền**, chỉnh sửa code trong node `Prepare File Permissions` và `Prepare Folder Permissions` để trả về `null` thay vì quyền hiện tại.

##### **D. Node "Recursive Call to Self"**
- Node này **gọi lại chính workflow** để xử lý subfolder. **Không cần chỉnh sửa**, nhưng lưu ý:
  - **Tránh vòng lặp vô hạn** nếu không có điều kiện dừng (workflow đã có logic dừng tự động khi không còn folder nào để xử lý).
  - **Tối đa hóa độ sâu** bằng cách điều chỉnh `maxDepth` trong node `Set Configuration` (nếu cần).

#### **3. Kích hoạt ⚡️**
- **Test run** với một thư mục nhỏ để kiểm tra:
  1. Chạy node **"Start Recursive Processing"**.
  2. Kiểm tra **Google Drive** xem dữ liệu đã được copy chưa.
  3. Nếu thành công, **bật Active workflow** để chạy tự động.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[TIPS THỰC TIỆN]
1. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** sau node **"Main Completion"** để nhận thông báo khi sao chép xong.
   - Ví dụ: `https://n8n.io/workflows/7402` có thể kết hợp với node **Slack** để báo cáo kết quả.

2. **Sao chép định kỳ**:
   - Sử dụng **n8n Trigger** (Webhook hoặc Cron) để chạy workflow hàng tuần/month.
   - Ví dụ: Dùng **n8n-nodes-base.cron** để chạy mỗi thứ 7 sáng 8h.

3. **Tối ưu quyền**:
   - Nếu muốn **bỏ qua quyền chia sẻ**, chỉnh sửa code trong node `Prepare File Permissions` và `Prepare Folder Permissions` như sau:
     ```javascript
     // Thay vì:
     return { permissions: $input.all().permissions };
     // Sử dụng:
     return {}; // Bỏ qua quyền
     ```

4. **Sao chép nhiều thư mục cùng lúc**:
   - Tạo một **workflow cha** sử dụng node **Loop** để gọi workflow này cho nhiều thư mục nguồn khác nhau.

5. **Kiểm tra lỗi**:
   - Thêm node **n8n-nodes-base.set** sau mỗi node Google Drive để log lỗi:
     ```json
     {
       "operation": "set",
       "property": "error",
       "value": "$jsonNode.error"
     }
     ```
   - Sau đó kết nối với node **Slack** để báo lỗi.
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa việc sao chép thư mục Google Drive **vô hạn sâu**, **bảo toàn quyền truy cập** và **giữ nguyên metadata** - tất cả **không cần viết một dòng code**. Dùng cho:
✅ **Backup dữ liệu** an toàn.
✅ **Tạo template** cho dự án mới.
✅ **Di chuyển dữ liệu** giữa các thư mục mà không mất quyền.
✅ **Tối ưu thời gian** trong quản lý file đám mây.

**Hãy thử ngay và tiết kiệm hàng giờ công việc thủ công mỗi tuần!** 🚀

---
:::note[CHÚ Ý]
- **Không sao chép thư mục có file quá lớn** (Google Drive có giới hạn 15GB cho một file).
- **Kiểm tra quyền** trước khi chạy để tránh lỗi.
- **Dùng VPS** để workflow chạy 24/7 mà không bị gián đoạn.
:::