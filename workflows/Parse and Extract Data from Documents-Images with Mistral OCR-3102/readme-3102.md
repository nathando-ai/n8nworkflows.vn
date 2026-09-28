---
title: "🔍 **Tự Động Học OCR & Trích Xuất Dữ Liệu Từ Tài Liệu PDF & Ảnh Với Mistral AI (Không Cần Code!)**"
description: "Workflow tự động hóa sử dụng Mistral OCR để trích xuất nội dung từ PDF và ảnh thành markdown, phân loại và phân tích cảm xúc tài liệu chỉ với 1 click. Giúp các sếp tiết kiệm thời gian và nâng cao hiệu quả xử lý tài liệu hàng loạt."
slug: "tieu-dung-mistral-ocr-trong-n8n"
tags: [n8n, automation, ai, ocr, mistral-ai, google-drive, no-code]
keywords: [n8n workflow mistral ocr, tự động hóa trích xuất dữ liệu từ pdf, ocr tự động hóa, mistral ai n8n, giải pháp xử lý tài liệu không code]
---

# 🚀 **Tự Động Học OCR & Trích Xuất Dữ Liệu Từ Tài Liệu PDF & Ảnh Với Mistral AI**

### **Nỗi Đau Của Các Sếp Khi Xử Lý Tài Liệu**
Hàng ngày, các sếp phải mất thời gian quý báu để:
- **Quét và chuyển đổi** hàng trăm trang PDF/ảnh thành văn bản.
- **Tìm kiếm thông tin cụ thể** trong tài liệu dài, mất nhiều thời gian soạn thảo.
- **Phân loại và phân tích** nội dung tài liệu (ví dụ: hợp đồng, báo cáo) để đưa ra quyết định nhanh chóng.
- **Chính xác thấp** khi sử dụng các công cụ OCR truyền thống, dẫn đến sai sót trong dữ liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động trích xuất** nội dung từ PDF và ảnh thành **markdown** (sẵn sàng sử dụng).
✅ **Phân tích và phân loại** tài liệu (ví dụ: xác định loại hợp đồng, cảm xúc trong văn bản).
✅ **Hoạt động 24/7** trên nền tảng n8n self-hosted, không phụ thuộc vào thời gian làm việc.
✅ **Giá rẻ** với chi phí chỉ **$0.001/trang** (Mistral OCR).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Giải Pháp**                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| **Tiết kiệm thời gian**    | Trích xuất 100+ trang PDF/ảnh chỉ trong **vài giây** thay vì nhiều giờ.       |
| **Chính xác cao**         | Mistral OCR xử lý **markdown** (sạch sẽ, không lỗi OCR truyền thống).         |
| **Phân loại tự động**     | Xác định loại tài liệu (hợp đồng, báo cáo, email...) và **phân tích cảm xúc**. |
| **Hoạt động liên tục**   | Workflow chạy **24/7** trên VPS, không cần can thiệp thủ công.               |
| **Giá thành thấp**       | Chi phí **$0.001/trang** (rẻ hơn nhiều so với dịch vụ OCR khác).              |

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key Mistral Cloud**:
   - Đăng ký tại [Mistral Cloud](https://mistral.ai/) và lấy **API Key**.
   - Thêm **credentials** trong n8n với tên: `mistralCloudApi`.
   - **Lưu ý**: Workflow **chỉ hoạt động với Mistral Cloud API** (không hỗ trợ Mistral API khác).

2. **Tài Khoản Google Drive OAuth2**:
   - Cài đặt **Google Drive API** và tạo **OAuth2 credentials**.
   - Thêm **credentials** trong n8n với tên: `googleDriveOAuth2Api`.

3. **Tài Liệu PDF/Ảnh trên Google Drive**:
   - Đăng tải tài liệu cần xử lý lên **Google Drive** (các sếp có thể chia sẻ link công khai hoặc sử dụng **signed URL** cho tài liệu riêng tư).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1**: Tải file JSON của workflow từ [n8n.io/workflows/3102](https://n8n.io/workflows/3102).
**Bước 2**: Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON đã tải.
**Hoặc**:
- Copy toàn bộ JSON từ file và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **hai cách xử lý tài liệu**:
- **Cách 1: Tài Liệu Công Khai (Public URL)**
  - Sử dụng khi tài liệu đã được chia sẻ công khai trên Google Drive.
  - **Node quan trọng**:
    - **Import PDF** / **Import Image**: Chọn **Google Drive OAuth2Api** và điền **link công khai** của file.
    - **Mistral DOC OCR** / **Mistral IMAGE OCR**: Sử dụng **URL công khai** để Mistral xử lý.

- **Cách 2: Tài Liệu Riêng Tư (Private URL - Signed URL)**
  - Sử dụng khi tài liệu **không muốn chia sẻ công khai**.
  - **Node quan trọng**:
    - **Mistral Upload** / **Mistral Upload1**: Upload file lên **Mistral Cloud** (tự động tạo **signed URL**).
    - **Mistral DOC OCR** / **Mistral IMAGE OCR**: Sử dụng **signed URL** để Mistral xử lý.
    - **Lưu ý**:
      - Các sếp cần **điền API Key Mistral Cloud** vào **credentials** `mistralCloudApi`.
      - **Signed URL** sẽ tự động tạo sau khi upload file.

#### **3. Kích Hoạt Workflow ⚡️**
**Bước 1**: **Test Run** với một file mẫu:
- Chọn **Manual Trigger** và chạy workflow với **file PDF/ảnh** đã chuẩn bị.
- Kiểm tra kết quả ở **node "Document Understanding"** (nội dung trích xuất) và **"Document Mis-Understanding?"** (phân tích cảm xúc).

**Bước 2**: Sau khi kiểm tra thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram để báo cáo kết quả**:
   - Thêm **node Slack/Telegram** sau **node "Document Understanding"** để tự động gửi kết quả trích xuất qua chat.

2. **Lưu log kết quả vào Google Sheets**:
   - Sử dụng **node Google Sheets** để ghi lại **tên file, ngày xử lý, kết quả phân tích** vào bảng tính.

3. **Tự động xử lý hàng loạt tài liệu**:
   - Sử dụng **node "List Files" (Google Drive)** để lấy danh sách file mới và **loop** qua workflow cho từng file.

4. **Phân loại tài liệu theo loại**:
   - Sau khi trích xuất, sử dụng **node "Document Mis-Understanding?"** để phân loại tài liệu (ví dụ: hợp đồng, báo cáo, email) và **chuyển hướng** đến workflow xử lý khác.

5. **Cài đặt cron job để chạy định kỳ**:
   - Nếu các sếp muốn **xử lý tự động hàng ngày**, có thể cài đặt **cron job** trên VPS để kích hoạt workflow vào giờ nhất định.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa trích xuất và phân tích tài liệu** mà không cần viết code. Với **Mistral OCR**, các sếp sẽ:
✔ **Tiết kiệm thời gian** lên đến **90%** trong việc xử lý tài liệu.
✔ **Nâng cao chính xác** với kết quả **markdown sạch sẽ**.
✔ **Phân loại và phân tích** tài liệu một cách **tự động và hiệu quả**.

**Hãy import workflow này ngay hôm nay và bắt đầu tự động hóa công việc của mình!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/3102)**
**📧 Liên hệ tác giả (Jimleuk) để hỗ trợ cá nhân hóa: [hello@jimle.uk](mailto:hello@jimle.uk)**