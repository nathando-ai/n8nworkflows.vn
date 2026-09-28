---
title: "🎓 Tự Động Hóa Sinh Lên Chứng Nhận Bằng PDF Từ Google Sheets – Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn sinh ra chứng nhận cá nhân hóa từ Google Sheets, Google Slides sang PDF và gửi qua email tự động. Giúp tiết kiệm thời gian lên tới 90% cho việc cấp chứng nhận, giấy chứng nhận, bằng khen cho sinh viên, nhân viên hoặc khách hàng."
slug: "tieu-dong-hoa-chung-nhan-bang-google-sheets-gmail"
tags: [n8n, automation, google-sheets, google-drive, gmail, no-code, chứng-nhận-bằng]
keywords: [tự động hóa chứng nhận bằng, n8n workflow chứng nhận, tự động hóa bằng khen, sinh chứng nhận bằng PDF, tự động hóa google sheets, tự động hóa google slides]
---

# 🚀 **Tự Động Hóa Sinh Lên Chứng Nhận Bằng PDF – Không Cần Code!**

### **Giải Phóng Tay Các Sếp Từ Việc Tạo Chứng Nhận Bằng Thủ Công!**
Hãy tưởng tượng một tình huống: **Bạn phải tạo hàng chục chứng nhận bằng, giấy chứng nhận hoàn thành khóa học, hoặc bằng khen cho nhân viên/khách hàng** – mỗi chứng nhận đều phải có tên riêng, thiết kế chuyên nghiệp, và gửi qua email. **Thời gian và công sức bạn bỏ ra là vô giá!**

Với **workflow này**, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ bằng một dòng dữ liệu mới trong Google Sheets:
✅ **Tạo chứng nhận bằng PDF cá nhân hóa** từ mẫu Google Slides.
✅ **Gửi tự động qua email** cho người nhận.
✅ **Lưu trữ sạch sẽ** trong Google Drive.
✅ **Không cần viết một dòng code nào!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 90%** so với cách làm thủ công.
- **Chứng nhận chuyên nghiệp** với thiết kế thống nhất từ Google Slides.
- **Tự động hóa hoàn toàn** – không cần nhắc nhở hoặc làm lại.
- **Dữ liệu đồng bộ** giữa Google Sheets, Google Drive và Gmail.
- **Dễ dàng mở rộng** cho nhiều loại chứng nhận khác nhau (bằng khen, chứng chỉ hoàn thành, chứng nhận tham gia).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (đã kết nối với n8n):
   - **Google Sheets** (để lưu danh sách người nhận).
   - **Google Drive** (để lưu mẫu Slides và lưu trữ chứng nhận PDF).
   - **Google Slides** (mẫu chứng nhận có placeholder `[NAME]`).
   - **Gmail** (để gửi chứng nhận qua email).
2. **API Keys & Credentials**:
   - **Google Sheets OAuth 2.0** (để đọc dữ liệu mới).
   - **Google Drive OAuth 2.0** (để copy, download, upload và xóa file).
   - **Google Slides OAuth 2.0** (để thay đổi văn bản trong mẫu).
   - **Gmail OAuth 2.0** (để gửi email tự động).
3. **File mẫu**:
   - **Google Slides template** (có placeholder `[NAME]` để thay thế tên).
   - **Google Sheets** (cột `Name` và `Email` để lưu thông tin người nhận).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/8163](https://n8n.io/workflows/8163) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
Nếu các sếp tự host n8n trên VPS, hãy đảm bảo **cài đặt OAuth 2.0** cho tất cả các dịch vụ Google.
:::

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **📄 Node 1: Google Sheets Trigger**
- **Chọn Sheet ID** của bảng dữ liệu chứa thông tin người nhận (cột `Name` và `Email`).
- **Cấu hình Trigger**:
  - **Watch for changes** (theo dõi thay đổi mới).
  - **Column to watch**: Chọn cột `Name` (hoặc bất kỳ cột nào để kích hoạt workflow).

##### **📁 Node 2 & 3: Copy File (Google Drive) + Replace Text (Google Slides)**
- **Google Drive (Copy file)**:
  - **Source file ID**: ID của **mẫu Google Slides** (đã có placeholder `[NAME]`).
  - **Destination file name**: `<$json["Name"]> Certificate` (để tạo tên file động).
- **Google Slides (Replace text)**:
  - **Presentation ID**: ID của file Slides vừa copy.
  - **Placeholder**: `[NAME]` → Thay thế bằng `$json["Name"]` (tên từ Google Sheets).

##### **📥 Node 4 & 5: Download File (PDF) + Upload File (Google Drive)**
- **Google Drive (Download)**:
  - **File ID**: ID của file Slides đã thay đổi.
  - **Format**: Chọn **PDF** để xuất.
  - **File name**: `<$json["Name"]> Certificate.pdf`.
- **Google Drive (Upload)**:
  - **Destination folder ID**: ID của **thư mục lưu trữ chứng nhận** (cần tạo trước).
  - **File name**: Giữ nguyên tên PDF vừa tạo.

##### **🗑️ Node 6: Delete a File (Google Drive)**
- **File ID**: ID của file Slides **tạm thời** (đã copy và thay đổi).
- **Lý do**: Giảm bớt rác trong Drive, chỉ giữ lại PDF cuối cùng.

##### **✉️ Node 7: Send a Message (Gmail)**
- **To**: `$json["Email"]` (email từ Google Sheets).
- **Subject**: `Your Certificate: $json["Name"]`.
- **Body**: Thêm nội dung tùy chỉnh (ví dụ: *"Chúc mừng bạn đã hoàn thành khóa học!"*).
- **Attachments**: **File PDF** vừa upload vào Google Drive.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Thêm một dòng mới vào **Google Sheets** (cột `Name` và `Email`).
   - Kiểm tra workflow có **sinh ra PDF** và **gửi email** không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để hoạt động 24/7.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM NÂNG CAO]
1. **Thêm Logo & Thông Tin Chi Tiết**:
   - Thêm **logo của doanh nghiệp** vào mẫu Slides.
   - Thêm **mã QR** (tự động sinh từ Google Sheets) vào chứng nhận.
2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Google Sheets** để **tạo báo cáo thống kê** số lượng chứng nhận đã gửi.
3. **Kết Nối Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo khi có chứng nhận mới được sinh ra.
4. **Lưu Log Hoạt Động**:
   - Sử dụng **node StickyNote** để ghi lại lịch sử hoạt động (ai đã nhận chứng nhận, thời gian gửi).
5. **Tự Động Xóa Dữ Liệu Sau Thời Gian**:
   - Kết hợp với **Google Sheets Trigger** để **xóa dữ liệu sau khi gửi email** (tránh trùng lặp).
:::

---
### 📌 **Kết Luận**
**Workflow này không chỉ tiết kiệm thời gian mà còn mang lại sự chuyên nghiệp và tính cá nhân hóa cao cho chứng nhận của các sếp.** Từ bây giờ, **không cần lo lắng về việc tạo chứng nhận bằng tay** – chỉ cần **cập nhật Google Sheets**, hệ thống sẽ tự động làm tất cả!

👉 **Hãy áp dụng ngay và tự động hóa quy trình chứng nhận của mình!**
👉 **Nếu cần hỗ trợ cài đặt n8n trên VPS**, các sếp có thể tham khảo:
🔹 [🎁 Đăng ký VPS TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
🔹 [💻 Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**Chúc các sếp thành công với tự động hóa!** 🚀