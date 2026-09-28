---
title: "📤 Tự Động Lưu Tệp Đính Kèm Gmail Vào Google Drive - Giảm Thời Gian Làm Việc 60%!"
description: "Workflow tự động hóa 100% không code giúp các sếp tự động lưu tất cả các tệp đính kèm từ Gmail vào Google Drive theo thời gian thực, tiết kiệm 40-60% thời gian quản lý email hàng ngày."
slug: "tự-dộng-lưu-tệp-dính-kèm-gmail-google-drive"
tags: [n8n, automation, file-management, gmail, google-drive, no-code]
keywords: [tự động hóa gmail, lưu tệp đính kèm google drive, workflow n8n, tự động hóa email, tiết kiệm thời gian quản lý email]
---

# 🚀 **Tự Động Lưu Tệp Đính Kèm Gmail Vào Google Drive - Không Cần Code!**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Lọc và tải xuống** hàng chục tệp đính kèm từ email (PDF, Excel, Word, hình ảnh...)
- **Tìm kiếm và lưu trữ** chúng vào Google Drive theo cách thủ công, mất **30-60 phút/ngày**.
- **Lo lắng mất tệp** khi không lưu đúng nơi hoặc quên tải xuống.

**Workflow này giải quyết tất cả!** Nó **tự động**:
✅ **Nhận biết** tất cả email mới có tệp đính kèm.
✅ **Lưu trữ** tệp vào **Google Drive** với tên gốc, không bị thay đổi.
✅ **Tiết kiệm 40-60% thời gian** cho công việc quản lý email hàng ngày.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 40-60% thời gian** quản lý email hàng ngày (không cần tải xuống thủ công).
- **Tránh mất tệp**: Tệp đính kèm **tự động** lưu vào Google Drive theo thời gian thực.
- **Tên tệp không bị thay đổi**: Sử dụng tên gốc từ email, không cần chỉnh sửa.
- **Hoạt động liên tục 24/7**: Không phụ thuộc vào thời gian làm việc của cá nhân.
- **Dễ dàng mở rộng**: Có thể kết nối với **Slack/Telegram** để thông báo khi có tệp mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (đã kích hoạt API Gmail).
✔ **Tài khoản Google Drive** (đã kích hoạt API Google Drive).
✔ **Thời gian ~10 phút** để cấu hình workflow.
✔ **Mã giảm giá VPS** (nếu tự host) để tiết kiệm chi phí.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/6466](https://n8n.io/workflows/6466) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **3 node chính**, các sếp cần **cấu hình chính xác** như sau:

##### **🔹 Node 1: Gmail Trigger (Gmail Trigger)**
- **Chọn Credential**:
  - Vào **Credentials** (cột bên trái) → Tạo mới **Gmail OAuth2 API**.
  - Đăng nhập Google, cấp quyền cho API và lưu credential với tên **một cách dễ nhớ** (ví dụ: `Gmail_Account_David`).
- **Cấu hình**:
  - **Polling Interval**: Giá trị mặc định (5 phút) là đủ, có thể giảm xuống **300 giây** (5 phút) để nhanh hơn.
  - **Filter**: Bỏ trống để **nhận tất cả email mới** (hoặc thêm điều kiện như `from:client@example.com`).

##### **🔹 Node 2: If (has Attachments) (Conditional Check)**
- **Điều kiện**: `{{ $json["hasAttachments"] }}` (kiểm tra email có tệp đính kèm hay không).
- **Lưu ý**:
  - Nếu email **không có tệp đính kèm**, workflow sẽ **bỏ qua** và không gây lỗi.
  - **Không cần chỉnh sửa** gì thêm, chỉ cần **bật Active** node này.

##### **🔹 Node 3: Upload to Google Drive (Google Drive)**
- **Chọn Credential**:
  - Vào **Credentials** → Tạo mới **Google Drive OAuth2 API**.
  - Đăng nhập Google, cấp quyền và lưu credential với tên **một cách dễ nhớ** (ví dụ: `Google_Drive_David`).
- **Cấu hình**:
  - **Folder ID**:
    - Tạo **một thư mục mới** trong Google Drive (ví dụ: `Email_Attachments_Archive`).
    - **Copy ID thư mục** từ URL (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp` → `1AbCdEfGhIjKlMnOp`).
    - Điền vào trường **Folder ID** của node Google Drive.
  - **File Name**:
    - Để mặc định: `{{ $node["Gmail Trigger"].json["attachments"][0]["filename"] }}` (sử dụng tên tệp gốc).
    - **Lưu ý**: Nếu email có **nhiều tệp đính kèm**, workflow sẽ **lưu tất cả** vào cùng thư mục.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **một email mẫu** có tệp đính kèm (PDF/Excel/Word...) đến inbox được theo dõi.
  - Kiểm tra **Google Drive** để xác nhận tệp đã được lưu.
- **Bật Active**:
  - Chuyển **switch Active** sang **ON** để workflow chạy **liên tục**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thông báo khi có tệp mới** (Slack/Telegram):
   - Thêm **node Slack/Telegram Webhook** sau node Google Drive để **báo cáo tức thì** khi có tệp mới.
   - Ví dụ: `Tệp mới được lưu: {{ $node["Gmail Trigger"].json["attachments"][0]["filename"] }}`.

2. **Lưu log hoạt động**:
   - Thêm **node Sticky Note** để ghi lại **lịch sử hoạt động** (ví dụ: ngày giờ, tên tệp, email gửi).
   - Có thể kết nối với **Google Sheets** để **báo cáo định kỳ**.

3. **Lọc email theo chủ đề**:
   - Cập nhật **filter** trong node Gmail Trigger để **chỉ lấy email từ khách hàng/đơn hàng** (ví dụ: `from:client@example.com OR subject:"Đơn hàng"`).

4. **Tự động xóa email sau khi lưu**:
   - Thêm **node Gmail** để **xóa email sau khi tệp đã được lưu** (nếu không cần lưu lại email).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **công việc chiến lược** hơn, thay vì mất thời gian trong việc **quản lý email thủ công**. **Chỉ cần 10 phút cấu hình**, workflow sẽ **hoạt động tự động 24/7**, tiết kiệm **40-60% thời gian** hàng ngày.

**Hành động ngay hôm nay!**
1. **Tải workflow** từ [n8n.io/workflows/6466](https://n8n.io/workflows/6466).
2. **Cấu hình Gmail & Google Drive** theo hướng dẫn.
3. **Bật Active** và **nhận email tự động lưu tệp**!

👉 **Cần hỗ trợ?** Liên hệ với tác giả David Olusola qua [david@daexai.com](mailto:david@daexai.com) để **tư vấn cá nhân hóa workflow** cho doanh nghiệp của các sếp!

---