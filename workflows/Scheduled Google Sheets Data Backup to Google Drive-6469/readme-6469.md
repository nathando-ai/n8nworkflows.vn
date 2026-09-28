---
title: "🗄️ Tự Động Hoàn Hảo: Backup Dữ Liệu Google Sheets Sang Google Drive Mỗi Ngày (Không Cần Code)"
description: "Workflow tự động hóa 100% miễn phí sao lưu dữ liệu Google Sheets sang Google Drive hàng ngày với định dạng CSV/XLSX, giúp các sếp bảo vệ dữ liệu quan trọng khỏi mất mát, giảm thiểu rủi ro và dễ dàng phục hồi khi cần. Chỉ cần 5 phút thiết lập!"
slug: "tự-dộng-hoàn-hảo-backup-google-sheets-sang-google-drive"
tags: [n8n, automation, google-sheets, google-drive, backup-data, no-code]
keywords: [backup google sheets, tự động hóa lưu trữ dữ liệu, n8n workflow, sao lưu hàng ngày, google drive automation, miễn phí backup]
---

# 🚀 **Backup Tự Động Google Sheets Sang Google Drive: Bảo Vệ Dữ Liệu Quan Trọng 24/7**

## **💥 Nỗi Đau Của Các Sếp: Dữ Liệu Google Sheets "Mất Tình Cờ" Là Thảm Hoạ!**
Các sếp đã bao giờ lo lắng về những trường hợp sau đây chưa?
- **Sửa sai dữ liệu** trên Google Sheets nhưng không có bản sao lưu, phải mất nhiều giờ để khôi phục?
- **Tài khoản bị hack** hoặc bị xóa ngẫu nhiên, dẫn đến mất mát dữ liệu quan trọng?
- **Cần tra cứu dữ liệu cũ** nhưng không biết cách lấy lại bản gốc?
- **Đơn vị kinh doanh** phụ thuộc vào dữ liệu hàng ngày nhưng chưa có giải pháp sao lưu tự động?

**Giải pháp?** Một **workflow tự động hóa hoàn hảo** chỉ với **3 node** trong n8n, giúp các sếp:
✅ **Sao lưu dữ liệu Google Sheets sang Google Drive** **mỗi ngày** (hoặc theo lịch tự chọn).
✅ **Bảo vệ dữ liệu khỏi mất mát** do sai sót, hacker, hoặc xóa ngẫu nhiên.
✅ **Không cần code**, chỉ cần **5 phút thiết lập**.
✅ **Lưu trữ định kỳ** để phục hồi dữ liệu cũ khi cần.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **An toàn tuyệt đối**: Dữ liệu được sao lưu tự động hàng ngày, không phụ thuộc vào con người.
- **Tiết kiệm thời gian**: Không cần phải thủ công export và upload dữ liệu mỗi ngày.
- **Phục hồi nhanh chóng**: Khi xảy ra lỗi, các sếp chỉ cần **1 click** để khôi phục từ bản sao lưu.
- **Dễ dàng quản lý**: Dữ liệu được lưu trong Google Drive, có thể chia sẻ hoặc tra cứu dễ dàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google** (đã liên kết với Google Sheets và Google Drive).
✔ **Dữ liệu Google Sheets** cần sao lưu (cần **ID của Sheet** và **tên tab**).
✔ **Thư mục Google Drive** để lưu trữ backup (cần **ID của thư mục**).
✔ **n8n Self-hosted** (để workflow chạy 24/7, không bị giới hạn thời gian chạy).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải workflow** từ [đây](https://n8n.io/workflows/6469) (nếu có link JSON).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
3. **Hoặc copy JSON** từ [đây](https://n8n.io/workflows/6469) và **paste** vào **"Import"** → **"From JSON"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Daily Backup Schedule (2 AM)**
- **Lưu ý**: Workflow sẽ chạy **mỗi ngày lúc 2 giờ sáng** (theo giờ máy chủ n8n).
- **Không cần chỉnh sửa** nếu muốn giữ lịch này.

#### **🔹 Node 2: Read Google Sheet Data**
**Bước 1: Thiết lập Credentials**
- **Chọn "Google Sheets OAuth2 API"** (đã tạo trước khi import).
- **Nếu chưa có**, tạo tại:
  - **n8n Dashboard** → **Credentials** → **Add Credential** → Chọn **"Google Sheets OAuth2 API"**.
  - **Cần cấp quyền** cho Google Sheets khi đăng nhập.

**Bước 2: Điền thông tin Google Sheet**
- **Google Sheet ID**: Lấy từ **URL của Sheet** (ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → **1AbCdEfGhIjKlMnOpQrStUvWxYz**).
- **Sheet Name (GID)**: Tên của **tab** cần sao lưu (ví dụ: `Sheet1`, `Dữ liệu Doanh Thu`).

**Bước 3: Chọn định dạng xuất (CSV/XLSX)**
- **Mặc định là CSV** (nhẹ hơn, dễ dàng tra cứu).
- **Nếu muốn Excel**, thay đổi **fileType** thành `xlsx` (tùy chọn).

#### **🔹 Node 3: Upload Backup to Google Drive**
**Bước 1: Thiết lập Credentials**
- **Chọn "Google Drive OAuth2 API"** (đã tạo trước khi import).
- **Nếu chưa có**, tạo tại:
  - **n8n Dashboard** → **Credentials** → **Add Credential** → Chọn **"Google Drive OAuth2 API"**.
  - **Cần cấp quyền** cho Google Drive khi đăng nhập.

**Bước 2: Điền thông tin Google Drive**
- **Google Drive Folder ID**: Lấy từ **URL của thư mục** (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → **1AbCdEfGhIjKlMnOpQrStUvWxYz**).
- **File Name**: **Không cần chỉnh**, workflow sẽ tự động đặt tên như `backup_Sheet1_2024-07-26.csv`.

---

### **3. Kích Hoạt ⚡️**
1. **Bật "Active"** (toggle ở góc trên bên phải).
2. **Test Run** (nút **"Execute Workflow"**) để kiểm tra:
   - Dữ liệu có được đọc từ Google Sheets không?
   - File backup có được tạo và upload lên Google Drive không?
3. **Kiểm tra Google Drive**:
   - File backup sẽ xuất hiện ở **thư mục đã chỉ định** với tên như `backup_Sheet1_2024-07-26.csv`.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Sao Lưu Nhiều Tab Trong Một Sheet**
- **Cách 1**: Tạo **một workflow riêng** cho mỗi tab.
- **Cách 2**: Sử dụng **node "Set"** để **lặp qua nhiều tab** và sao lưu từng tab vào **một file CSV duy nhất**.

### **🔹 2. Gửi Thông Báo Khi Backup Thành Công**
- **Thêm node "Email"** hoặc **"Slack"** sau node **Google Drive** để nhận **email/notification** khi backup hoàn tất.
- **Ví dụ**:
  - Nếu backup thành công → Gửi tin nhắn Slack: **"Backup Sheet1 hoàn tất!"**.
  - Nếu lỗi → Gửi email cảnh báo.

### **🔹 3. Lưu Log Backup Vào Google Sheets**
- **Thêm node "Google Sheets"** sau node **Google Drive** để ghi **lịch sử backup** (ngày giờ, status, file được backup).
- **Cột cần thêm**:
  | Ngày Backup | Status | File Backup | Link File |
  |-------------|--------|-------------|-----------|
  | 2024-07-26  | Thành công | backup_Sheet1_2024-07-26.csv | [Link] |

### **🔹 4. Sao Lưu Nhiều Sheet Sang Một File Excel**
- **Sử dụng node "Google Sheets"** để **đọc tất cả tab** → **Gộp vào một file Excel** bằng **node "Excel"** (nếu cần).
- **Cần thêm node "Excel"** (n8n-nodes-base.excel) để xuất dữ liệu vào định dạng `.xlsx`.

### **🔹 5. Sao Lưu Sang Cloud Khác (Dropbox, OneDrive)**
- **Thay thế node Google Drive** bằng **node Dropbox** hoặc **OneDrive** (n8n có hỗ trợ).
- **Cách làm**:
  1. Tạo **credentials mới** cho Dropbox/OneDrive.
  2. Thay đổi **node Upload Backup** từ Google Drive sang Dropbox/OneDrive.

---

## **📌 Kết Luận: Bảo Vệ Dữ Liệu Hôm Nay, Tránh Đau Đầu Mai!**

Các sếp đã **xem qua workflow này** và thấy **rất đơn giản** phải không?
- **Chỉ 5 phút thiết lập**, **không cần code**.
- **Chạy tự động hàng ngày**, **không lo mất dữ liệu**.
- **Dễ dàng mở rộng** với Slack, email, hoặc lưu log.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Chỉnh sửa credentials** và **thông tin Google Sheet/Drive**.
3. **Bật Active** và **test run** để kiểm tra.
4. **Quên việc backup thủ công** và **yên tâm làm việc**!

**🚀 Nếu các sếp cần hỗ trợ**, có thể liên hệ với tác giả **David Olusola** qua email: **david@daexai.com** (đặc biệt nếu muốn **tối ưu workflow** cho doanh nghiệp lớn).

---
**#TựĐộngHóa #BackupDữLiệu #GoogleSheets #GoogleDrive #n8n #NoCode**