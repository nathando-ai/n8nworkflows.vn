---
title: "📁 Tự Động Hoàn Hảo: Sắp Xếp Tệp Đính Kèm Email vào Google Drive Theo Công Ty & Tháng - Không Cần Code!"
description: "Workflow này tự động lấy tất cả email có đính kèm từ Gmail, phân loại theo công ty (từ Google Sheets) và tháng, sau đó lưu vào Google Drive theo cấu trúc thư mục logic. Giúp các sếp tiết kiệm 10+ giờ/tháng và tránh mất mát dữ liệu quan trọng."
slug: "tieu-dong-hoan-hao-sap-xep-tap-dinh-kem-email-google-drive"
tags: [n8n, automation, google-drive, gmail, google-sheets, no-code]
keywords: [tự động hóa email, sắp xếp đính kèm google drive, workflow n8n gmail, quản lý tài liệu theo công ty, tự động hóa văn phòng]
---

# 🚀 **Tự Động Hoàn Hảo: Sắp Xếp Tệp Đính Kèm Email vào Google Drive Theo Công Ty & Tháng**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hàng ngày, các sếp phải:
- **Lọc và tải xuống** hàng chục email có đính kèm từ Gmail.
- **Tìm kiếm công ty** của người gửi trong danh sách Excel/Google Sheets.
- **Tạo thủ công** thư mục theo tháng (YYYY/MM) và tên công ty trên Google Drive.
- **Đặt tên tệp** một cách rườm rà, dễ gây nhầm lẫn.
- **Lo lắng** về việc mất mát hoặc trùng lặp tệp quan trọng.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp đi lặp lại này. **Workflow này giải quyết tất cả!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** – Workflow chạy tự động, không cần can thiệp.
✅ **Sắp xếp logic** – Tệp được lưu theo **YYYY/MM/Công Ty** (ví dụ: `2024/05/ABC_Corp`).
✅ **Tránh mất mát** – Không còn quên tải xuống hoặc đặt tên sai tệp.
✅ **Cá nhân hóa** – Dùng Google Sheets để **lọc email** theo danh sách công ty đã định.
✅ **Hoạt động liên tục** – Không phụ thuộc vào giờ làm việc của nhân viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail + Google Drive + Google Sheets) với quyền **quản trị viên**.
2. **API Keys OAuth2** cho:
   - **Gmail** (để lấy email có đính kèm).
   - **Google Drive** (để tạo/thuộc thư mục và upload tệp).
   - **Google Sheets** (để lọc công ty từ danh sách whitelist).
3. **Google Sheet Whitelist** (cấu trúc như sau):
   | **email**          | **company**      |
   |--------------------|------------------|
   | `nhanvien1@abc.com`| `ABC Corp`       |
   | `nhanvien2@xyz.com`| `XYZ Limited`    |

   🔗 **Mẫu Google Sheet sẵn sàng**: [Tải bản sao](https://docs.google.com/spreadsheets/d/1tTz9BflstxVL18YG11Ny1eiDj3FcjvtZ619b_bHx8h4/edit?usp=sharing)

4. **Gmail Filter** (để chỉ lấy email có đính kèm và từ công ty trong danh sách):
   - Tạo **filter** với điều kiện:
     - `Has the words`: `invoice receipt` (hoặc từ khóa khác).
     - `Has attachment`.
     - **Apply label**: Tạo một **label** mới (ví dụ: `Auto_Process`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3464](https://n8n.io/workflows/3464).
- **Trên n8n Editor**:
  - Nhấn **Import** → Chọn file JSON vừa tải.
  - Hoặc **copy/paste** toàn bộ JSON vào ô **Import Workflow**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần **cấu hình chính xác** các node sau:

##### **🔹 Node "Gmail Trigger" (gmailTrigger)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
- **Operation**: `get` (lấy email).
- **Filter**:
  - **Label**: Chọn **label** đã tạo trong Gmail Filter (ví dụ: `Auto_Process`).
  - **Limit**: Đặt số lượng email muốn xử lý (ví dụ: `100`).

##### **🔹 Node "Lookup in Sheets" (googleSheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Document ID**: ID của Google Sheet whitelist (tìm trong URL của sheet).
- **Range**: `Sheet1!A2:B` (giả sử dữ liệu bắt đầu từ hàng 2).
- **Output**: Chọn `values` (để lấy danh sách email và công ty).

##### **🔹 Node "Search For Folder" (googleDrive)**
- **Credentials**: Chọn `googleDriveOAuth2Api`.
- **Query**: `mimeType='application/vnd.google-apps.folder' and name contains 'YYYY/MM'` (sau này sẽ được thay đổi bằng node `set`).
- **Limit**: `1`.

##### **🔹 Node "Create Month Folder" (googleDrive)**
- **Credentials**: Chọn `googleDriveOAuth2Api`.
- **Name**: `$node["YYYY/MM"].json["text"]` (tự động lấy từ node `set`).
- **Parent**: Chọn **thư mục cha** (ví dụ: `Root` hoặc thư mục mặc định).

##### **🔹 Node "Create Company Folder" (googleDrive)**
- **Credentials**: Chọn `googleDriveOAuth2Api`.
- **Name**: `$node["Company"].json["company"]` (lấy từ Google Sheets).
- **Parent**: Chọn **thư mục tháng** (`YYYY/MM`).

##### **🔹 Node "Upload To Folder" (googleDrive)**
- **Credentials**: Chọn `googleDriveOAuth2Api`.
- **File**: `$node["Split Up Binary Data1"].json["data"]` (tệp đính kèm).
- **Parent**: Chọn **thư mục công ty** (`YYYY/MM/Công Ty`).

##### **🔹 Node "Split Up Binary Data1" (function)**
- **JavaScript Code** (sử dụng mặc định từ workflow gốc):
  ```javascript
  return {
    json: {
      data: $input.all().data
    }
  };
  ```

##### **🔹 Node "YYYY/MM" (set)**
- **Expression**: `$node["Gmail"].json["date"].split("T")[0].replace(/-/g, "/")` (định dạng ngày thành `YYYY/MM`).

##### **🔹 Node "Company Folder Exists" (if)**
- **Condition**: `$node["Search Company Folder1"].json[0].id != null` (kiểm tra thư mục công ty có tồn tại không).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Once** và chọn **email mẫu** từ Gmail.
   - Kiểm tra:
     - Tệp đính kèm có được upload vào **Google Drive** theo cấu trúc `YYYY/MM/Công Ty` không?
     - Tên tệp có được đặt theo **timestamp** không?
2. **Active Workflow**:
   - Sau khi kiểm tra thành công, **bật Active** và **set cron job** (nếu muốn chạy định kỳ):
     - Ví dụ: `0 9 * * *` (chạy hàng ngày lúc 9h sáng).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Gửi báo cáo định kỳ**:
   - Thêm node **Google Sheets** để ghi log vào sheet theo mẫu:
     | **Email**       | **Company**      | **File Name**      | **Date Processed** |
     |-----------------|------------------|--------------------|--------------------|
     | `abc@test.com`  | `ABC Corp`       | `invoice_20240512.pdf` | `2024-05-12`       |

2. **Kết nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành:
     ```
     "Workflow đã xử lý thành công [X] email vào Google Drive!"
     ```

3. **Lọc email theo từ khóa**:
   - Cập nhật **Gmail Filter** để chỉ lấy email có từ khóa như `invoice`, `contract`, `receipt`.

4. **Tự động xóa email sau khi xử lý**:
   - Thêm node **Gmail** với **operation: delete** để xóa email sau khi upload tệp.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại, đồng thời **giảm thiểu rủi ro mất mát dữ liệu**. **Chỉ cần 10 phút setup**, các sếp sẽ có một hệ thống **tự động hóa hoàn hảo** cho quản lý tài liệu.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các node** theo hướng dẫn.
3. **Bật Active** và **nghỉ ngơi** – công việc sẽ được xử lý tự động!

**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 😊