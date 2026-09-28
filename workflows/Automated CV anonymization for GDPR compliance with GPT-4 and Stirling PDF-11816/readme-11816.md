---
title: "🔒 **Tự Động Xóa Thông Tin Cá Nhân (PII) Trên CV Theo GDPR Với GPT-4 & Stirling PDF - Chỉ Cần 1 Clic!"**
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp HR xóa triệt để thông tin cá nhân (tên, email, số điện thoại, địa chỉ...) trên CV mà vẫn giữ nguyên kỹ năng, kinh nghiệm và thành tích. Tuân thủ GDPR, tiết kiệm thời gian lên tới 10+ giờ/tuần và giảm thiểu rủi ro pháp lý."
slug: "tieu-dong-xoa-thong-tin-ca-nhan-tren-cv-gdpr"
tags: [n8n, automation, hr-automation, ai-summarization, gdpr-compliance, pdf-processing, openai-gpt4]
keywords: [tự động hóa cv, xóa thông tin cá nhân cv, gdpr cv, workflow n8n hr, gpt-4 anonymize cv, Stirling PDF API]
---

# 🚀 **Tự Động Xóa Thông Tin Cá Nhân Trên CV Theo GDPR Với GPT-4 & Stirling PDF**

### **Nỗi Đau Của Các Sếp HR Hiện Nay**
Mỗi ngày, các sếp HR phải thủ công **quét và xóa thông tin cá nhân (PII)** như tên, email, số điện thoại, địa chỉ trên hàng trăm CV để tuân thủ **GDPR** và bảo mật dữ liệu. Quá trình này:
✅ **Tốn thời gian** (thường mất 5-15 phút cho mỗi CV).
✅ **Mất chính xác** (rủi ro bỏ sót thông tin nhạy cảm).
✅ **Khó bảo mật** (nếu làm thủ công, dễ xảy ra rò rỉ dữ liệu).
✅ **Khó mở rộng** (không thể tự động hóa cho lượng CV lớn).

**Workflow này giải quyết tất cả những vấn đề trên bằng AI + tự động hóa 100% không cần code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và xử lý lượng CV lớn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý **100+ CV/ngày** mà không cần thủ công.
- **Tuân thủ GDPR**: Xóa **triệt để** tất cả thông tin cá nhân (tên, email, số điện thoại, địa chỉ, ngày sinh...) mà **không làm mất** kỹ năng, kinh nghiệm và thành tích.
- **Chất lượng cao**: GPT-4 **hiểu ngữ cảnh** và giữ nguyên **ngôn ngữ, cấu trúc, và ý nghĩa** của CV.
- **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không cần can thiệp.
- **An toàn & bảo mật**: Không lưu trữ dữ liệu nhạy cảm, chỉ xử lý và xóa ngay.
- **Tiết kiệm chi phí**: So với việc thuê nhân viên hoặc sử dụng dịch vụ ngoài.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** với **API Key** (để sử dụng GPT-4 và GPT-4.1-mini).
2. **Tài khoản Stirling PDF** với **Authorization Header** (để chuyển đổi và xử lý file PDF).
3. **Webhook URL** để nhận file CV từ ứng viên (có thể là URL của n8n hoặc một dịch vụ như Zapier/Make).
4. **File mẫu CV** (PDF, DOCX, TXT) để test workflow.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11816](https://n8n.io/workflows/11816) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Workflow Name** (ví dụ: **"CV Anonymization"**).
4. Nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/11816](https://n8n.io/workflows/11816).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **4 node quan trọng** cần cấu hình cẩn thận:

#### **A. Cấu Hình OpenAI (3 Node)**
Tất cả **3 node `OpenAI Chat Model`** (gồm GPT-4 và GPT-4.1-mini) cần:
1. **Tạo credentials OpenAI**:
   - Trên **n8n Editor**, nhấn **Credentials** → **Add** → **OpenAI**.
   - Nhập **API Key** từ tài khoản OpenAI.
   - Lưu và chọn **credentials này** cho tất cả 3 node `OpenAI Chat Model`.

2. **Cấu hình `Basic LLM Chain`**:
   - Node này sử dụng **GPT-4** để xóa PII. Các sếp có thể **tùy chỉnh prompt** trong **system message** để điều chỉnh mức độ anonymization (ví dụ: giữ hoặc xóa ngày sinh).

#### **B. Cấu Hình Stirling PDF (4 Node)**
Tất cả **4 node `httpRequest`** liên quan đến Stirling PDF cần:
1. **Tạo Authorization Header**:
   - Trên mỗi node `httpRequest` (danh sách ở trên), mở **Advanced** → **Headers**.
   - Thêm header:
     ```
     Authorization: Bearer <API_KEY_STIRLING>
     ```
   - Thay `<API_KEY_STIRLING>` bằng **API Key** từ tài khoản Stirling PDF.

2. **Node `PDF → Text1` và `Any File → PDF2`**:
   - Đảm bảo **URL API** của Stirling PDF được điền chính xác (ví dụ: `https://api.stirlingpdf.com/v1/...`).

#### **C. Cấu Hình Webhook 🔗**
1. Node **`Webhook`** nhận file CV từ ứng viên:
   - Đảm bảo **path** (`1faa18ed-f037-48a7-b1ff-ee9975836147`) **không thay đổi**.
   - **HTTP Method** giữ nguyên **POST**.
   - **Credentials**: Chọn **credentials mặc định** (nếu có) hoặc tạo mới.

2. Node **`Respond to Webhook`**:
   - Đảm bảo **status code** trả về là **200 OK** để ứng viên biết file đã được xử lý.

#### **D. Node `If1` (Kiểm tra file)**
- Node này **kiểm tra loại file** trước khi chuyển đổi:
  - Nếu file **không phải PDF**, nó sẽ tự động chuyển đổi sang PDF trước khi xử lý.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với file mẫu**:
   - Upload **1 file CV mẫu** (PDF/DOCX) lên webhook.
   - Kiểm tra **output** trong node `Respond to Webhook` để xem kết quả anonymization.
   - **Kiểm tra**:
     - Thông tin cá nhân (tên, email, số điện thoại) đã được xóa.
     - Kỹ năng, kinh nghiệm và thành tích vẫn được giữ nguyên.

2. **Bật Active Workflow**:
   - Nhấn **Active** trên workflow để nó bắt đầu xử lý tự động.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp với Slack/Telegram để Báo Cáo**
- Sử dụng **node `Slack`** hoặc **`Telegram Bot`** để gửi thông báo khi CV được xử lý thành công/thất bại.
- **Cách làm**:
  1. Thêm node `Slack` sau `Respond to Webhook`.
  2. Cấu hình **webhook URL** của Slack/Telegram.
  3. Tùy chỉnh **message** để báo cáo kết quả.

### **2. Lưu Log Xử Lý CV**
- Sử dụng **node `Google Sheets`** hoặc **`Airtable`** để lưu lịch sử xử lý:
  - Thông tin: **Tên file, ngày xử lý, trạng thái (thành công/thất bại), người gửi**.
- **Cách làm**:
  1. Thêm node `Google Sheets` sau `Respond to Webhook`.
  2. Cấu hình **credentials** và **sheet name**.
  3. Chọn **columns** để lưu dữ liệu.

### **3. Tự Động Gửi CV Anonymized Về Email**
- Sử dụng **node `Email`** (Gmail/SMTP) để gửi CV đã xử lý về email của ứng viên.
- **Cách làm**:
  1. Thêm node `Email` sau `Any File → PDF2`.
  2. Cấu hình **SMTP credentials** và **địa chỉ email** của ứng viên (có thể lấy từ header file).

### **4. Tùy Chỉnh Prompt cho GPT-4**
- Nếu muốn **giữ hoặc xóa thêm thông tin**, chỉnh sửa **system message** trong node `Basic LLM Chain`:
  ```json
  {
    "role": "system",
    "content": "You are a professional CV anonymizer. Remove all personally identifiable information (PII) such as names, emails, phone numbers, addresses, and dates of birth. However, keep job titles, skills, experience, and achievements intact. Output the result in HTML format."
  }
  ```
- **Ví dụ**:
  - Muốn **giữ ngày sinh**, thêm vào prompt: `"Keep the date of birth if it's relevant to the job."`

### **5. Optimize Chi Phí với GPT-4.1-mini**
- Node `OpenAI Chat Model1` và `OpenAI Chat Model2` sử dụng **GPT-4.1-mini** (rẻ hơn GPT-4).
- **Lợi ích**: Giảm chi phí **~80%** so với GPT-4 mà vẫn giữ chất lượng cao.

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc thủ công mệt mỏi, đồng thời **tuân thủ GDPR** một cách an toàn và hiệu quả. Với **AI GPT-4 + tự động hóa n8n**, các sếp có thể:
✅ **Xử lý hàng trăm CV/ngày** mà không cần tăng nhân sự.
✅ **Tránh rủi ro pháp lý** do vi phạm GDPR.
✅ **Tiết kiệm chi phí** so với việc thuê dịch vụ ngoài.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với file mẫu** để đảm bảo hoạt động.
3. **Bật Active** và bắt đầu tự động hóa CV của doanh nghiệp!

---
**💡 Cần hỗ trợ thêm?**
- **Join Cộng đồng n8n Việt Nam** tại [Facebook Group](https://www.facebook.com/groups/n8nvietnam).
- **Đăng ký VPS** để self-host n8n: [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172).