---
title: "🗄️ Tự Động Hoàn Hảo: Backup Workflow n8n Sang Google Drive Miễn Phí (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn tự động sao lưu tất cả workflow n8n của các sếp lên Google Drive định kỳ 4 giờ/lần, đảm bảo an toàn dữ liệu và dễ dàng phục hồi. Khắc phục nỗi lo mất dữ liệu khi cập nhật hoặc lỗi hệ thống."
slug: "backup-workflow-n8n-sang-google-drive"
tags: [n8n, automation, devops, google-drive, backup, self-hosted]
keywords: [backup workflow n8n, tự động hóa lưu trữ dữ liệu, sao lưu n8n, Google Drive API, tự động hóa DevOps]
---

# 🚀 **Backup Tất Cả Workflow n8n Sang Google Drive (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng gặp phải tình huống **mất workflow n8n** sau khi cập nhật phiên bản, lỗi server, hoặc thậm chí là **quên sao lưu**? Hoặc phải **tìm kiếm lại logic** của một workflow cũ sau nhiều tháng không sử dụng? Điều này không chỉ **tốn thời gian** mà còn **giảm hiệu quả** của toàn bộ hệ thống tự động hóa.

Với **workflow này**, các sếp sẽ **tự động sao lưu tất cả các workflow n8n** lên Google Drive **mỗi 4 giờ/lần**, đảm bảo:
✅ **Dữ liệu an toàn** – Không phụ thuộc vào hệ thống n8n.
✅ **Phục hồi nhanh** – Khôi phục workflow chỉ trong vài giây.
✅ **Tiết kiệm thời gian** – Không cần làm thủ công.
✅ **Dễ dàng quản lý** – Sắp xếp backup theo ngày tháng.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Sao lưu tự động** tất cả workflow n8n lên Google Drive **mỗi 4 giờ** (cấu hình được thay đổi).
- **Xóa tự động** các folder backup cũ (để tránh tốn dung lượng).
- **Khôi phục nhanh** nếu xảy ra lỗi hệ thống hoặc cập nhật phiên bản.
- **Dễ dàng chia sẻ** với team thông qua Google Drive.
- **Không cần code** – Hoàn toàn **no-code**, chỉ cần cấu hình.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền **create, read, update, delete** (để tạo folder, upload file, xóa folder cũ).
2. **API Key của Google Drive** (cấu hình trong **n8n Credentials**).
3. **n8n Self-hosted** (không thể chạy trên n8n.cloud vì hạn chế API).
4. **Dung lượng Google Drive đủ** để lưu trữ backup (mỗi workflow ~1-2KB).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Từ File JSON**
1. Tải file JSON từ [đây](https://n8n.io/workflows/15724) (hoặc copy từ link trên).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON → **Import**.
3. Workflow sẽ xuất hiện trong danh sách.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Tạo workflow mới.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON từ [đây](https://n8n.io/workflows/15724) → **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình** các node quan trọng sau:

#### **🔹 Node 1: "Scheduled Every 4 Hours" (scheduleTrigger)**
- **Thay đổi lịch chạy** (nếu muốn khác 4 giờ):
  - Mở node → **Schedule** → Chọn **Custom** → Điền biểu thức cron (ví dụ: `0 0 * * *` để chạy hàng ngày 12h đêm).
  - **Gợi ý**:
    - `0 0 */6 * * *` → Chạy mỗi 6 giờ.
    - `0 0 8-18/2 * * *` → Chạy từ 8h đến 18h, mỗi 2 giờ.

#### **🔹 Node 2: "Create Google Drive Folder" (googleDrive)**
- **Tên folder backup** mặc định là `n8n_backup_YYYY-MM-DD_HH-MM-SS`.
- **Các sếp có thể thay đổi** để dễ quản lý:
  - Mở node → **Folder Name** → Điền định dạng mới (ví dụ: `n8n_backup_[teamname]_${$now:yyyy-MM-dd}`).

#### **🔹 Node 3: "Filter by Condition" (filter)**
- **Lọc folder cũ** để xóa (tránh tốn dung lượng).
- **Mặc định**, nó xóa folder có tên chứa `n8n_backup_` và **tuổi > 7 ngày**.
- **Nếu muốn giữ backup lâu hơn**, chỉnh:
  - Mở node → **Condition** → Thay đổi `jsonpath: "$.name"` và điều kiện `olderThan: 7d` thành `olderThan: 30d` (30 ngày).

#### **🔹 Node 4: "Process in n8n1" (n8n)**
- **Nếu các sếp có nhiều workflow**, node này sẽ **lấy tất cả workflow** từ n8n API.
- **Không cần chỉnh gì** nếu muốn backup tất cả.
- **Nếu chỉ backup workflow cụ thể**, chỉnh:
  - Mở node → **URL** → Thêm `?filter[workflowName]=tên_workflow_cần_backup`.

#### **🔹 Node 5: "Upload File to Google Drive" (googleDrive)**
- **Tự động upload** file JSON của workflow vào folder mới tạo.
- **Không cần chỉnh gì** nếu muốn lưu trữ mặc định.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** → Chọn **Manual Trigger Execution** → Nhấn **Execute**.
   - Kiểm tra **Google Drive** có xuất hiện folder backup mới không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[**CÁC TỐT NHẤT CỦA CÁC SẺP**]
1. **Gửi thông báo Slack/Email khi backup thành công**:
   - Thêm node **Slack** hoặc **Email** sau node **Upload File to Google Drive**.
   - Ví dụ: `Tự động backup workflow n8n thành công! Link: [link_google_drive]`.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** để ghi lại lịch sử backup (thời gian, số lượng workflow, trạng thái).

3. **Backup lên nhiều nơi**:
   - Sử dụng **node Google Drive** để backup lên **Dropbox** hoặc **AWS S3** cùng lúc.

4. **Khôi phục workflow từ backup**:
   - Nếu xảy ra lỗi, các sếp chỉ cần:
     - Tải file JSON từ Google Drive.
     - Import vào n8n Editor → **Import** → Chọn file → **Import**.
:::

---

## 📌 **Kết Luận**
**Backup tự động workflow n8n** là **bước quan trọng** để các sếp **tránh mất dữ liệu** và **tăng tính chuyên nghiệp** của hệ thống tự động hóa. Với workflow này:
✔ **Không cần code** – Hoàn toàn **no-code**.
✔ **Chạy tự động** mỗi 4 giờ (cấu hình được thay đổi).
✔ **An toàn dữ liệu** – Sao lưu lên Google Drive.
✔ **Dễ dàng phục hồi** – Khôi phục chỉ trong vài giây.

**Hãy áp dụng ngay** và **ngủ yên tâm** khi biết dữ liệu của mình được bảo vệ!

---
**👉 [Tải workflow ngay](https://n8n.io/workflows/15724) và bắt đầu tự động hóa backup!** 🚀