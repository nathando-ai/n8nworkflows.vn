---
title: "🗄️ Tự Động Hoàn Hảo: Backup Tất Cả Workflow n8n Sang Google Drive Hàng Ngày Với Xóa Tự Động Sau 15 Ngày"
description: "Giải pháp tự động hóa hoàn toàn không cần code để sao lưu toàn bộ workflow n8n hàng ngày lên Google Drive, đồng thời xóa tự động các bản sao lưu cũ hơn 15 ngày để tiết kiệm không gian lưu trữ. Đảm bảo dữ liệu an toàn và hệ thống luôn sẵn sàng hoạt động."
slug: "backup-workflow-n8n-google-drive-daily"
tags: [n8n, automation, devops, google-drive, backup-automation]
keywords: [backup workflow n8n, tự động hóa sao lưu, google drive n8n, xóa tự động backup, lưu trữ an toàn workflow]
---

# 🚀 **Tự Động Sao Lưu Workflow n8n Hàng Ngày Và Xóa Tự Động Sau 15 Ngày**

## **💡 Giải Pháp Cho Nỗi Lo "Làm Sao Lưu Dữ Liệu Workflow n8n An Toàn?"**

Các sếp đã từng gặp phải tình huống **không may xóa nhầm workflow quan trọng**, hoặc **cần sao lưu dữ liệu để chuyển đổi môi trường**? Hoặc thậm chí **không biết cách backup workflow n8n một cách tự động** mà không cần viết code? Đây chính là **nỗi đau lớn** của nhiều người dùng n8n, đặc biệt khi làm việc với nhiều workflow phức tạp.

**Workflow này giải quyết hoàn toàn vấn đề đó** bằng cách:
✅ **Sao lưu toàn bộ workflow n8n hàng ngày** lên Google Drive dưới dạng file `.json` riêng biệt.
✅ **Tạo thư mục theo ngày** để dễ quản lý và phân loại.
✅ **Xóa tự động các bản sao lưu cũ hơn 15 ngày** để tiết kiệm không gian lưu trữ.
✅ **Hoạt động 24/7** mà không cần can thiệp của người dùng.

Kết quả? **Dữ liệu workflow luôn an toàn, dễ truy cập, và hệ thống luôn sẵn sàng khôi phục khi cần.**

---

### **🎯 Kết Quả Các Sếp Nhận Được**

:::tip[**Lợi Ích Cốt Lõi**]
- **An toàn tuyệt đối**: Sao lưu tự động hàng ngày, không lo mất dữ liệu do lỗi người dùng hoặc hệ thống.
- **Tiết kiệm thời gian**: Không cần phải thủ công export workflow mỗi khi cần backup.
- **Quản lý dễ dàng**: Các file backup được tổ chức theo ngày, giúp tìm kiếm và khôi phục nhanh chóng.
- **Tối ưu không gian**: Xóa tự động các bản sao lưu cũ hơn 15 ngày, tránh tình trạng Google Drive bị quá tải.
- **Hoạt động liên tục**: Dù máy tính tắt hoặc n8n offline, workflow vẫn chạy nhờ **self-hosted** trên VPS.
:::

---

### **🔧 Yêu Cầu Cần Thiết**

:::info[**Chuẩn Bị Trước Khi Lên Đồ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền chỉnh sửa và tạo thư mục.
2. **API Key của n8n** (nếu self-hosted) hoặc **URL API của n8n Cloud**.
3. **Thời gian chạy tự động**:
   - **Backup hàng ngày**: Thiết lập tại **4h sáng** (hoặc thời gian phù hợp).
   - **Xóa backup cũ**: Thiết lập tại **4h sáng ngày sau** (hoặc thời gian khác).
4. **Thư mục gốc trong Google Drive** (nếu muốn backup vào thư mục cụ thể).
:::

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/13866](https://n8n.io/workflows/13866).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**

Workflow này bao gồm **13 node** với các chức năng chính sau. Các sếp cần **cấu hình kỹ lưỡng** các node sau:

##### **🔹 Node "Create folder" (Tạo thư mục Google Drive)**
- **Mục đích**: Tạo thư mục mới trong Google Drive với tên theo **ngày hiện tại** (ví dụ: `Backup_2024-05-20`).
- **Cấu hình**:
  - **Resource**: Chọn `folder`.
  - **Folder Name**: Đặt tên tự động bằng `{{ $node["start4h"].json["date"].format("YYYY-MM-DD") }}`.
  - **Parent Folder ID**: Nếu muốn backup vào thư mục cụ thể, điền **ID của thư mục đó** (có thể lấy từ URL Google Drive).
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).

##### **🔹 Node "apiN8N" (Gọi API n8n để lấy workflows)**
- **Mục đích**: Lấy toàn bộ danh sách workflow từ n8n API.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://<your-n8n-instance>/api/v1/workflows` (thay `<your-n8n-instance>` bằng URL của n8n).
  - **Headers**:
    - `Authorization`: `Bearer <your-n8n-api-key>` (nếu self-hosted).
    - **Nếu dùng n8n Cloud**: Thay bằng `Authorization: Bearer <your-n8n-cloud-api-token>`.
  - **Credentials**: Không cần (nếu không dùng OAuth).

##### **🔹 Node "Split" (Chia workflow thành các item riêng biệt)**
- **Mục đích**: Chuyển danh sách workflow từ API thành các item riêng để xử lý từng workflow một.
- **Cấu hình**:
  - **Operation**: Chọn `Split by property` và chọn `items` (trong trường hợp API trả về mảng workflows).

##### **🔹 Node "ConvertToJson" (Chuyển workflow thành file JSON)**
- **Mục đích**: Chuyển mỗi workflow thành file `.json` riêng.
- **Cấu hình**:
  - **Operation**: `toJson`.
  - **File Name**: Đặt tên tự động bằng `{{ $node["Split"].json["name"] }}.json`.

##### **🔹 Node "upload file" (Upload file lên Google Drive)**
- **Mục đích**: Upload file `.json` vừa tạo vào thư mục mới trong Google Drive.
- **Cấu hình**:
  - **Resource**: Chọn `file`.
  - **Folder ID**: Điền **ID của thư mục mới** (lấy từ node `Create folder`).
  - **File Content**: Chọn `File` từ node `ConvertToJson`.
  - **File Name**: Đặt tên tự động bằng `{{ $node["Split"].json["name"] }}.json`.
  - **Credentials**: Chọn `googleDriveOAuth2Api`.

##### **🔹 Node "Delete folder" (Xóa thư mục backup cũ hơn 15 ngày)**
- **Mục đích**: Xóa tự động các thư mục backup cũ hơn 15 ngày.
- **Cấu hình**:
  - **Resource**: Chọn `folder`.
  - **Folder ID**: Lấy từ node `get folder` (node này lấy danh sách tất cả thư mục backup).
  - **Credentials**: Chọn `googleDriveOAuth2Api`.
  - **Lưu ý**: Node `Check date` sẽ tính toán thời gian và chỉ truyền **Folder ID** của các thư mục cũ hơn 15 ngày vào node này.

##### **🔹 Node "Check date" (Kiểm tra tuổi thư mục)**
- **Mục đích**: So sánh ngày tạo thư mục với ngày hiện tại để xác định thư mục nào cần xóa.
- **Cấu hình**:
  - **Operation**: `getTimeBetweenDates`.
  - **Start Date**: `{{ $node["get folder"].json["createdTime"] }}`.
  - **End Date**: `{{ $node["start3h"].json["date"] }}`.
  - **Result Format**: Chọn `days`.

##### **🔹 Node "start4h" và "start3h" (Schedule Trigger)**
- **Mục đích**:
  - `start4h`: Chạy **backup hàng ngày** (ví dụ: 4h sáng).
  - `start3h`: Chạy **xóa backup cũ** (ví dụ: 4h sáng ngày sau).
- **Cấu hình**:
  - **Schedule**: Thiết lập theo **UTC** hoặc **múi giờ** của các sếp.
  - **Example**:
    - `start4h`: `0 4 * * *` (4h sáng hàng ngày).
    - `start3h`: `0 4 * * 1-6` (4h sáng từ thứ 2 đến thứ 7, để tránh xóa vào cuối tuần).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `start4h` để kiểm tra backup.
   - Chạy node `start3h` để kiểm tra xóa thư mục cũ.
2. **Bật Active workflow**:
   - Nhấn **Active** trên tab **Workflow** trong n8n Editor.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**

:::info[**Tối Ưu Hiệu Suất & An Toàn**]
1. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để thông báo khi backup thành công/thất bại.
   - Ví dụ: Sau node `upload file`, thêm node **Slack** để gửi tin nhắn:
     ```json
     {
       "text": "Backup workflows thành công vào ngày {{ $node["start4h"].json["date"].format("YYYY-MM-DD") }}"
     }
     ```

2. **Backup vào thư mục cụ thể**:
   - Thay vì backup vào thư mục gốc của Google Drive, các sếp có thể tạo **một thư mục chuyên dụng** (ví dụ: `n8n_backups`) và đặt **ID của thư mục này** vào node `Create folder`.

3. **Thay đổi thời gian xóa**:
   - Mặc định là **15 ngày**, nhưng các sếp có thể điều chỉnh thành **30 ngày** bằng cách thay đổi node `>15d` thành `>30d`.

4. **Khôi phục workflow từ backup**:
   - Khi cần khôi phục, các sếp chỉ việc **download file `.json`** từ Google Drive và **import vào n8n Editor**.

5. **Backup nhiều instance n8n**:
   - Nếu các sếp quản lý **nhiều instance n8n**, có thể **tạo một workflow riêng** cho mỗi instance và backup vào **thư mục khác nhau** trong Google Drive.
:::

---

### **📌 Kết Luận**

Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **sao lưu và quản lý workflow n8n một cách tự động, an toàn và hiệu quả**. Không cần viết code, không cần lo lắng về mất dữ liệu, và hệ thống luôn sẵn sàng khôi phục khi cần.

**👉 Hãy áp dụng ngay và bảo vệ dữ liệu của mình!**

---
:::note[**Lưu Ý Cuối Cùng**]
- **Self-hosted là lựa chọn tối ưu**: Để workflow chạy 24/7 mà không bị giới hạn, các sếp nên **cài n8n trên VPS**.
- **Google Drive phải có đủ dung lượng**: Đảm bảo tài khoản Google Drive có **dung lượng đủ** để lưu trữ backup.
- **Backup định kỳ**: Nếu muốn tăng tần suất backup (ví dụ: 2 lần/ngày), các sếp có thể thêm **thêm node Schedule Trigger**.
:::

---
**🚀 Cài đặt VPS cho n8n ngay với giá tốt nhất!**
:::info[**Gợi ý Hạ Tầng**]
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::