---
title: "📧 **Tự Động Hóa Gửi Email Bulk Cá Nhân Hóa Với File Đính Kèm - Khắc Phục Nỗi Đau Quá Trình Marketing Trùng Lặp & Tốn Thời Gian**"
description: "Workflow này tự động gửi email bulk với nội dung và file đính kèm cá nhân hóa từ Google Sheets, tiết kiệm thời gian cho các sếp marketing lên tới 80% so với làm thủ công. Đảm bảo chính xác, không bị lỗi copy-paste và hoạt động liên tục 24/7."
slug: "tieu-dong-hoa-gui-email-bulk-ca-nhan-hoa"
tags: [n8n, automation, marketing, email marketing, google-sheets, self-hosted]
keywords: [n8n workflow email bulk, tự động hóa gửi email cá nhân hóa, file đính kèm tự động, marketing automation, tiết kiệm thời gian marketing]
---

# 🚀 **Tự Động Hóa Gửi Email Bulk Cá Nhân Hóa Với File Đính Kèm - Giải Pháp Cho Các Sếp Marketing**

### **Nỗi Đau Thực Tế Của Các Sếp Marketing**
Gửi email bulk cho khách hàng hoặc lead là một trong những công việc **tốn thời gian nhất** trong marketing. Các sếp thường phải:
- **Lập danh sách email** từ Google Sheets/Excel và copy-paste từng dòng.
- **Tùy chỉnh nội dung** cho từng người (ví dụ: tên, thông tin cá nhân).
- **Tạo và đính kèm file** (PDF, Word, Excel) riêng cho mỗi người.
- **Gửi email một một** bằng Gmail/Outlook, dễ bị lỗi hoặc quên.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi khách hàng lại nhận được trải nghiệm **không cá nhân hóa** và **chậm trễ**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Workflow này **giải phóng thời gian** và **tăng hiệu quả** cho các sếp marketing bằng cách:
✅ **Tự động hóa 100% quá trình gửi email bulk** – Không cần copy-paste.
✅ **Cá nhân hóa nội dung và file đính kèm** từ Google Sheets (ví dụ: tên, thông tin sản phẩm, file cá nhân).
✅ **Gửi email đồng thời** (batch) mà không bị giới hạn của Gmail.
✅ **Hoạt động liên tục 24/7** – Không phụ thuộc vào giờ làm việc.
✅ **Giảm lỗi** – Không bị quên gửi hoặc sai thông tin như khi làm thủ công.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản SMTP** (để gửi email):
   - Nếu dùng Gmail, cần **App Password** (bật 2FA).
   - Khuyến nghị dùng **SMTP riêng** (ví dụ: SendGrid, Mailgun) để tránh bị chặn.
📌 **Google Sheets** chứa dữ liệu:
   - Cột **Email** (địa chỉ email của người nhận).
   - Cột **Tên** (để cá nhân hóa trong email).
   - Cột **File đính kèm** (link hoặc tên file trong Google Drive/Google Sheets).
📌 **File đính kèm** (nếu lưu trong Google Sheets):
   - File phải được **chuyển thành binary** (n8n sẽ tự động đọc từ Google Sheets).
📌 **n8n Self-hosted** (không dùng n8n Cloud để tránh giới hạn API).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/1514](https://n8n.io/workflows/1514) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **6 node** chính, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Manual Trigger ("On clicking 'execute'")**
- **Chức năng**: Bắt đầu workflow khi nhấn nút "Execute".
- **Lưu ý**: Không cần thay đổi gì, chỉ cần nhấn nút này để chạy.

##### **🔹 Node 2: Spreadsheet File (Đọc Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **Google Sheets** (cần kết nối tài khoản Google).
  - **Sheet Name**: Tên sheet chứa dữ liệu (ví dụ: "Danh sách khách hàng").
  - **Range**: Chọn phạm vi dữ liệu (ví dụ: `A1:D100`).
  - **Output Format**: Chọn **JSON Array** (để n8n xử lý dễ dàng).
- **Lưu ý**:
  - Đảm bảo sheet có **cột Email, Tên, và File đính kèm** (nếu có).
  - Nếu file đính kèm là **link Google Drive**, cần chuyển thành **binary** bằng node sau.

##### **🔹 Node 3: Read Binary File (Đọc File Đính Kèm)**
- **Cấu hình**:
  - **File Path**: Nếu file đính kèm là **tệp trong Google Sheets** (ví dụ: PDF trong ô `D2`), cần sử dụng **node `readBinaryFile`** để đọc file từ URL.
  - **Alternative**: Nếu file đã được **upload lên Google Drive**, sử dụng **Google Drive API** để lấy file.
- **Lưu ý**:
  - Nếu không có file đính kèm, **bỏ qua node này** và chuyển đến **SplitInBatches**.

##### **🔹 Node 4: SplitInBatches (Chia Batch Gửi Email)**
- **Cấu hình**:
  - **Batch Size**: Số email gửi cùng một lúc (ví dụ: **10-20** để tránh bị chặn SMTP).
  - **Output**: Chọn **JSON Array** (để node sau xử lý).
- **Lưu ý**:
  - Nếu không chia batch, email sẽ gửi **từng cái một**, chậm và dễ bị lỗi.

##### **🔹 Node 5: Read Binary File1 (Nếu Có File Đính Kèm)**
- **Cấu hình giống Node 3**, nhưng **áp dụng cho từng batch**.
- **Lưu ý**:
  - Nếu file đính kèm **không thay đổi**, có thể **bỏ node này** và sử dụng file mặc định.

##### **🔹 Node 6: EmailSend (Gửi Email)**
- **Cấu hình**:
  - **Credentials**: Chọn **SMTP** (đã cấu hình trước).
  - **From Email**: Địa chỉ email gửi (ví dụ: `marketing@doanhnghiep.com`).
  - **To Email**: `{$.email}` (đọc từ Google Sheets).
  - **Subject**: `{$.subject}` (ví dụ: `"Xin chào {$.name}, đây là file của bạn"`).
  - **Body**: Nội dung email cá nhân hóa (ví dụ: `"Xin chào {$.name},..."`).
  - **Attachments**: `{$.fileBinary}` (nếu có file đính kèm).
- **Lưu ý**:
  - **Test SMTP** trước để đảm bảo email không bị chặn.
  - **Không dùng Gmail cá nhân** (dễ bị chặn), dùng **SMTP doanh nghiệp** hoặc **SendGrid**.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Execute** để chạy thử với **1-2 email**.
  - Kiểm tra **email nhận được** và **file đính kèm** có đúng không.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** để hoạt động tự động.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node `slack`** để thông báo khi workflow hoàn thành.
   - Ví dụ: `"Workflow gửi email bulk hoàn tất! Tổng số email: {$.length}"`.

2. **Lưu Log Gửi Email**:
   - Thêm **node `set`** để lưu dữ liệu đã gửi vào Google Sheets.
   - Cột mới: `Trạng thái`, `Thời gian gửi`, `Lỗi (nếu có)`.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node `setInterval`** để gửi báo cáo tổng hợp (ví dụ: hàng tuần).
   - Nội dung: `Tổng số email gửi thành công: {$.successCount}`.

4. **Cá Nhân Hóa Nội Dung Email**:
   - Sử dụng **node `template`** để thay đổi nội dung email dựa trên dữ liệu.
   - Ví dụ: Nếu `$.loai_khach_hang = "VIP"`, thì email có nội dung đặc biệt.

---
### **📌 Kết Luận**
Workflow **Tự Động Hóa Gửi Email Bulk Cá Nhân Hóa** là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✔ **Tiết kiệm thời gian** (không cần copy-paste).
✔ **Tăng độ chính xác** (không bị lỗi).
✔ **Cá nhân hóa trải nghiệm** cho khách hàng.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**🚀 Hành động ngay!**
- **Cài n8n Self-hosted** trên VPS để tránh giới hạn Cloud.
- **Import workflow** và **cấu hình SMTP**.
- **Test và bật hoạt động** để tự động hóa email của bạn!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và đánh giá nếu bài hướng dẫn hữu ích!** 🚀