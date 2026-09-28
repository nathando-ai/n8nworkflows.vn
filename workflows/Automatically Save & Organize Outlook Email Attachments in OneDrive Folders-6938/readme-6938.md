---
title: "📤 Tự Động Lưu & Sắp Xếp Tệp Đính Kèm Email Outlook Vào OneDrive Theo Folder (Không Code)"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp tự động lưu tất cả file đính kèm từ email Outlook vào OneDrive theo folder riêng biệt, tiết kiệm thời gian và tránh mất mát dữ liệu. Hoạt động liên tục 24/7, không cần can thiệp thủ công."
slug: "tu-dong-luu-tep-dinh-kem-outlook-vao-onedrive"
tags: [n8n, automation, Microsoft Outlook, OneDrive, file management, no-code]
keywords: [tự động hóa email Outlook, lưu file đính kèm OneDrive, n8n workflow, tự động hóa văn phòng, lưu trữ cloud tự động]
---

# 🚀 **Tự Động Lưu & Sắp Xếp Tệp Đính Kèm Email Outlook Vào OneDrive Theo Folder**

### **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- **Lọc và tải xuống** file đính kèm từ email Outlook (PDF, Excel, Word, hình ảnh...).
- **Tìm kiếm và sắp xếp** chúng vào các folder OneDrive phù hợp (theo dự án, khách hàng, loại file...).
- **Lo ngại mất mát** dữ liệu khi không lưu trữ hệ thống.

**Workflow này giải quyết tất cả!** Nó **tự động**:
✅ **Nhận biết** email có đính kèm từ Outlook.
✅ **Tạo folder mới** trên OneDrive theo tên email (hoặc tên dự án).
✅ **Tải xuống và lưu trữ** tất cả file đính kèm vào folder tương ứng.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải **lọc và tải xuống** file một cách thủ công.
- **Tránh mất mát dữ liệu**: Tất cả file đính kèm **luôn được lưu trữ hệ thống** vào OneDrive.
- **Sắp xếp logic**: File được **tự động phân loại** vào folder phù hợp (theo tên email, dự án...).
- **Hoạt động liên tục**: Workflow **chạy tự động** mỗi khi có email mới.
- **Dễ dàng mở rộng**: Có thể **kết hợp với Slack/Teams** để thông báo khi có file mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Microsoft** (Outlook + OneDrive) với **quyền truy cập API**.
✔ **Client ID & Secret** của ứng dụng Outlook/OneDrive (cài đặt trong [Azure Portal](https://portal.azure.com/)).
✔ **Thời gian** để cấu hình các **credentials** trong n8n (hướng dẫn chi tiết bên dưới).

---
:::note[LƯU Ý QUAN TRỌNG]
- Workflow **không tự động tạo folder** nếu folder đó đã tồn tại (để tránh trùng lặp).
- **Tên folder mới** sẽ được tạo dựa trên **tiêu đề email** (hoặc có thể tùy chỉnh).
- **Kích thước file lớn** (>2GB) **không được hỗ trợ** (Outlook có giới hạn).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Từ file JSON (khuyến nghị)**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/6938) (nút "Download").
2. Trong **n8n Editor**, nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Xác nhận** và workflow sẽ xuất hiện trên canvas.

**Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn **"From JSON"**.
2. Dán toàn bộ mã JSON từ [đây](https://n8n.io/workflows/6938) (nút "Raw").
3. **Xác nhận** và workflow sẽ được tạo.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **7 node chính**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node 1: Microsoft Outlook Trigger (Giao diện nhận email)**
- **Chọn credentials**:
  - Nhấn **"Add"** → Chọn **"Microsoft Outlook"** → **"Add new credentials"**.
  - Điền:
    - **Client ID** & **Client Secret** (từ [Azure Portal](https://portal.azure.com/)).
    - **Tên tài khoản Outlook** (ví dụ: `sop@gmail.com`).
    - **Scope**: `Mail.ReadWrite` (để đọc email và đính kèm).
  - **Xác nhận** và lưu.

##### **🔹 Node 2: Filter (Lọc email có đính kèm)**
- **Cấu hình**:
  - **Expression**: `$.hasAttachments === true` (lọc chỉ email có file đính kèm).
  - **Nếu không có email nào**, workflow sẽ **dừng lại** (không gây lỗi).

##### **🔹 Node 3: Create Folder (Tạo folder mới trên OneDrive)**
- **Chọn credentials**:
  - Nhấn **"Add"** → Chọn **"Microsoft OneDrive"** → **"Add new credentials"**.
  - Điền:
    - **Client ID** & **Client Secret** (tương tự Outlook).
    - **Tên tài khoản OneDrive** (phải khớp với Outlook).
  - **Key Parameters**:
    - **Folder Name**: `$$.json["email.subject"]` (tạo folder theo tiêu đề email).
    - **Parent Folder Path**: `/` (folder gốc OneDrive).

##### **🔹 Node 4: Upload File OneDrive (Tải file đính kèm lên OneDrive)**
- **Chọn credentials**: Sử dụng cùng **credentials OneDrive** như trên.
- **Key Parameters**:
  - **File Path**: `$$.json["folderPath"]` (đường dẫn folder mới tạo).
  - **File Name**: `$$.json["fileName"]` (tên file đính kèm).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra):
   - Nhấn **"Run Workflow"** với **dữ liệu mẫu** (ví dụ: email có đính kèm PDF).
   - Kiểm tra:
     - Folder có được tạo không?
     - File đính kèm có được tải lên không?
2. **Bật Active**:
   - Sau khi test thành công, **bật switch "Active"** ở góc trên bên phải.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động tạo folder theo dự án**:
   - Thay vì `$$.json["email.subject"]`, các sếp có thể **tùy chỉnh tên folder** bằng cách thêm **thông tin từ email** (ví dụ: `$$.json["email.body"].split("Dự án:")[1]`).

2. **Gửi thông báo khi có file mới**:
   - **Thêm node Slack/Teams** sau **"Upload File OneDrive"** để **báo cáo** khi file được tải lên.

3. **Lưu log hoạt động**:
   - **Thêm node "Sticky Note"** (node thứ 4 trong danh sách) để **ghi lại lịch sử** (tên email, thời gian, file đính kèm).

4. **Xử lý file lớn**:
   - Nếu có file >2GB, các sếp cần **tải xuống trước** bằng Outlook và **tải lên OneDrive thủ công**.

5. **Kết hợp với Power Automate**:
   - Nếu cần **tự động hóa thêm**, các sếp có thể **kết nối n8n với Power Automate** để **xử lý file theo quy trình phức tạp hơn**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **làm thủ công** với email và file đính kèm. Với **cấu hình đơn giản**, nó **hoạt động tự động**, **tránh mất mát dữ liệu** và **sắp xếp logic** tất cả file vào OneDrive.

**🚀 Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình credentials** Outlook và OneDrive.
3. **Bật Active** và **quên đi việc tải file thủ công**!

**💡 Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ với **Michael Gullo** (tác giả workflow) qua [n8n Community](https://community.n8n.io/).

---