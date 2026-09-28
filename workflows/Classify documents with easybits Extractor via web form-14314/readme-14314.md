---
title: "📄 **Tự Động Hóa Phân Loại Tài Liệu PDF/PNG/JPEG bằng easybits Extractor - Không Cần Code!**"
description: "Giải pháp tự động hóa phân loại tài liệu (hoá đơn y tế, khách sạn, nhà hàng...) bằng AI thông qua form upload và API easybits. Tiết kiệm thời gian, giảm sai sót, hoạt động 24/7."
slug: "tieu-dong-hoa-phan-loai-tai-lieu-bang-easybits"
tags: [n8n, automation, no-code, ai-extraction, easybits, document-classification]
keywords: [n8n workflow phân loại tài liệu, tự động hóa phân loại PDF, AI phân loại hoá đơn, easybits n8n, tự động hóa văn phòng]
---

# 🚀 **Phân Loại Tài Liệu Tự Động bằng Form Upload + AI easybits (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải **quét, phân loại và xử lý hàng trăm tài liệu** như:
- **Hoá đơn y tế** (PDF/PNG)
- **Hoá đơn khách sạn/nha hàng** (PDF/JPEG)
- **Giấy tờ hành chính** (PDF)
- **Báo cáo tài chính** (Excel/PDF)

**Làm thủ công?** Tốn thời gian, dễ sai sót, và không thể hoạt động 24/7. **Cần một giải pháp tự động hóa?** Workflow này giúp **phân loại tài liệu chỉ trong vài giây**, kết nối với **easybits Extractor** (AI phân loại tài liệu tiên tiến) và **không cần viết một dòng code nào!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm 10-20 giờ/tuần** cho việc phân loại tài liệu thủ công.
✅ **Chính xác 95%+** nhờ AI easybits phân loại tự động.
✅ **Hoạt động liên tục 24/7** (không cần người quản lý).
✅ **Cá nhân hóa** theo nhu cầu (ví dụ: phân loại hoá đơn y tế, khách sạn, nhà hàng...).
✅ **Kết nối dễ dàng** với Google Drive, Slack, Email, hoặc hệ thống ERP.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi bắt đầu, các sếp cần:
✔ **Tài khoản easybits Extractor** ([extractor.easybits.tech](https://extractor.easybits.tech)) để tạo **Pipeline ID** và **API Key**.
✔ **VPS tự host n8n** (để workflow chạy 24/7) hoặc sử dụng **n8n Cloud** (miễn phí cho 500 execution/tháng).
✔ **Dịch vụ lưu trữ** (Google Drive, Dropbox, hoặc FTP) để lưu kết quả phân loại (nếu cần).
✔ **Tài khoản Slack/Email** (nếu muốn gửi báo cáo hoặc cảnh báo).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ File JSON 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n Workflow gốc](https://n8n.io/workflows/14314) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

**Cách import:**
1. Mở **n8n Editor** → Nhấn **Import Workflow** (icon 📥).
2. Chọn **Paste JSON** và dán nội dung từ [đây](https://n8n.io/workflows/14314).
3. Nhấn **Import**.

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**

#### **🔹 Bước 1: Tạo Pipeline trên easybits Extractor**
1. **Đăng ký tài khoản** trên [extractor.easybits.tech](https://extractor.easybits.tech).
2. **Tạo một Pipeline mới** và thêm **một trường `document_class`**.
3. **Cấu hình Prompt** (gợi ý dưới đây):
   > *"Phân loại tài liệu vào một trong các danh mục sau:
   > - `medical_invoice` (hoá đơn y tế)
   > - `restaurant_invoice` (hoá đơn nhà hàng)
   > - `hotel_invoice` (hoá đơn khách sạn)
   > - `null` (nếu không xác định được)
   > Trả về **chỉ một label** (không giải thích)."*
4. **Lưu Pipeline** và ghi lại:
   - **Pipeline ID** (ví dụ: `abc123`)
   - **API Key** (tìm trong **Settings** của tài khoản).

#### **🔹 Bước 2: Cấu Hình Node `easybits Extractor for Classification`**
1. Mở **node `easybits Extractor for Classification`** (loại `HTTP Request`).
2. **Thay đổi URL** từ:
   ```
   https://extractor.easybits.tech/api/pipelines/YOUR_PIPELINE_ID
   ```
   thành:
   ```
   https://extractor.easybits.tech/api/pipelines/YOUR_PIPELINE_ID
   ```
   (thay `YOUR_PIPELINE_ID` bằng ID Pipeline của các sếp).
3. **Thêm Authentication (Bearer Token):**
   - Nhấn **Add Credential** → Chọn **Bearer Auth**.
   - Nhập **API Key** từ easybits vào **Token**.
   - Gán credential này cho node này.

#### **🔹 Bước 3: Kiểm Tra & Kích Hoạt Workflow**
1. **Test Run** với một tài liệu mẫu (PDF/PNG/JPEG):
   - Nhấn **Execute Workflow** và upload một file test.
   - Kiểm tra **Output** để xem kết quả phân loại (`medical_invoice`, `restaurant_invoice`, `null`...).
2. **Bật Active** (icon 🟢) để workflow hoạt động tự động.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH MỞ RỘNG WORKFLOW**]
1. **Lưu kết quả vào Google Sheets/Excel**
   - Thêm node **Google Sheets** sau node `easybits Extractor` để ghi kết quả phân loại vào bảng tính.
   - Cấu hình **Sheet Name** và **Range** (ví dụ: `A1:B100`).

2. **Gửi báo cáo qua Slack/Email**
   - Thêm node **Slack Webhook** hoặc **Email** để thông báo khi phân loại thành công/thất bại.
   - Ví dụ: *"Tài liệu [Tên File] đã phân loại thành `medical_invoice`!"*

3. **Lưu tài liệu vào Google Drive**
   - Thêm node **Google Drive** để tự động lưu file đã phân loại vào folder cụ thể (ví dụ: `Hoá đơn Y tế`, `Hoá đơn Khách sạn`).

4. **Xử lý tài liệu chưa phân loại (`null`)**
   - Thêm **Conditional Branch** để chuyển tài liệu chưa phân loại (`document_class = null`) sang một workflow khác để xử lý thủ công.

5. **Tự động xóa file sau phân loại (nếu không cần lưu)**
   - Thêm node **Delete File** sau khi hoàn tất phân loại.
:::

---

### **📌 Kết Luận: Áp Dụng Ngay để Tiết Kiệm Thời Gian!**
Workflow này **giải quyết hoàn toàn vấn đề phân loại tài liệu thủ công** bằng cách kết nối **form upload** với **AI easybits Extractor**, giúp các sếp:
✔ **Tiết kiệm 10-20 giờ/tuần**.
✔ **Giảm sai sót** nhờ AI phân loại chính xác.
✔ **Hoạt động 24/7** mà không cần quản lý.

**Bắt đầu ngay!**
1. **Tải workflow** từ [n8n.io/workflows/14314](https://n8n.io/workflows/14314).
2. **Cấu hình easybits Pipeline** và **API Key**.
3. **Kích hoạt workflow** và chia sẻ form upload cho nhân viên!

---
:::info[**Gợi ý Hạ Tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên **tự host n8n trên VPS** thay vì dùng n8n Cloud (có giới hạn execution).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ ý kiến hoặc câu hỏi về workflow này!** 🚀