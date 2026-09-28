---
title: "🔍 **Tự Động Xóa Thông Tin Cá Nhân (PII) Trong File CSV Bằng OpenAI - Không Cần Code!**"
description: "Workflow tự động hóa xóa tự động các thông tin cá nhân nhạy cảm (PII) trong file CSV từ Google Drive, sử dụng trí tuệ nhân tạo OpenAI, giúp bảo mật dữ liệu và tuân thủ GDPR, CCPA một cách hiệu quả 24/7."
slug: "tu-dong-xoa-thong-tin-ca-nhan-pii-trong-csv-bang-openai"
tags: [n8n, automation, no-code, ai, google-drive, openai, pii-removal, gdpr, ccpa]
keywords: [tự động hóa n8n, xóa PII trong CSV, OpenAI tự động hóa, bảo mật dữ liệu, GDPR tự động, workflow n8n AI, tự động hóa Google Drive]
---

# 🚀 **Tự Động Xóa Thông Tin Cá Nhân (PII) Trong File CSV Bằng OpenAI - Không Cần Code!**

### **Giải pháp cho các sếp:**
Bạn có bao giờ lo lắng về việc lưu trữ **thông tin cá nhân nhạy cảm** (PII) như số điện thoại, địa chỉ email, hoặc số CMND trong file CSV? Những thông tin này không chỉ vi phạm **GDPR** hay **CCPA**, mà còn gây rủi ro bảo mật nghiêm trọng nếu rò rỉ. Với workflow này, **n8n kết hợp OpenAI** sẽ **tự động phát hiện và xóa** các cột chứa PII trong file CSV, sau đó **tự động upload lại file đã sạch** về Google Drive – **không cần viết một dòng code nào!**

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tự động hóa 100%:** Không cần can thiệp thủ công, workflow chạy **24/7** khi có file CSV mới được upload vào Google Drive.
✅ **Bảo mật dữ liệu:** Xóa **tất cả thông tin cá nhân** (PII) như số điện thoại, email, địa chỉ, ngày sinh, số CMND, v.v. theo yêu cầu GDPR/CCPA.
✅ **Tiết kiệm thời gian:** Thay vì phải **scan từng file thủ công**, AI tự động phân tích và xử lý.
✅ **Tuân thủ pháp lý:** Giúp doanh nghiệp **tránh phạt vi phạm GDPR/CCPA** do lưu trữ PII không an toàn.
✅ **Hoạt động liên tục:** Duy trì **sạch sẽ** tất cả file CSV trong Google Drive mà không cần sự can thiệp của người dùng.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐỘNG**]
Để workflow hoạt động, các sếp cần:
✔ **Tài khoản Google Drive** với quyền **truy cập API** (để workflow có thể **download/upload file**).
✔ **API Key của OpenAI** (đăng ký tại [OpenAI API](https://platform.openai.com/account/api-keys)).
✔ **Folder Google Drive** được **cấu hình trong workflow** để **monitor file CSV mới**.
✔ **File CSV** chứa **cột PII** (ví dụ: `email`, `phone`, `address`, `birthdate`, `id_number`).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/2779](https://n8n.io/workflows/2779) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên **Self-hosted** hoặc **n8n.cloud**).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/2779](https://n8n.io/workflows/2779).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Google Drive Trigger (Khởi động workflow)**
- **Cấu hình:**
  - **Folder ID:** Điền **ID của folder Google Drive** bạn muốn **monitor file CSV mới**.
  - **File Type:** Chọn **CSV**.
  - **Credentials:** Chọn **googleDriveOAuth2Api** (đã cấu hình trước khi import).

#### **🔹 Node 2 & 3: Google Drive (Download) + Extract from File**
- **Google Drive (Download):**
  - **File ID:** Auto lấy từ **Google Drive Trigger**.
  - **Credentials:** **googleDriveOAuth2Api**.
- **Extract from File:**
  - **File Content:** Auto lấy từ node trước.
  - **Format:** Chọn **CSV**.

#### **🔹 Node 4: OpenAI (Xóa PII)**
- **API Key:** Điền **API Key OpenAI** (từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys)).
- **Prompt (gợi ý):**
  ```plaintext
  Analyze the following CSV file and identify all columns containing Personally Identifiable Information (PII).
  Remove all PII columns and return the sanitized CSV data.
  ```
- **Model:** Chọn **gpt-3.5-turbo** (hoặc **gpt-4** nếu có budget).

#### **🔹 Node 5: Merge (Kết hợp dữ liệu)**
- **Auto merge** dữ liệu từ **Extract from File** và **OpenAI** (kết quả sau khi xóa PII).

#### **🔹 Node 6: Upload to Drive (Upload file đã sạch)**
- **File Content:** Lấy từ **Merge**.
- **Folder ID:** Điền **ID folder mục tiêu** (cùng folder hoặc folder khác).
- **File Name:** Auto lấy từ **Get filename** (node sau).
- **Credentials:** **googleDriveOAuth2Api**.

#### **🔹 Node 7 & 8: Get filename & Get result (Lấy thông tin file)**
- **Auto lấy** tên file và kết quả sau khi xử lý từ node trước.

#### **🔹 Node 9: Remove PII columns (Code Custom)**
- **Mã JavaScript (gợi ý):**
  ```javascript
  // Kiểm tra và xóa cột PII theo danh sách
  const piiColumns = ["email", "phone", "address", "birthdate", "id_number"];
  const data = $input.all();

  // Lọc bỏ cột PII
  const sanitizedData = data.map(row => {
    const newRow = { ...row };
    piiColumns.forEach(col => delete newRow[col]);
    return newRow;
  });

  return sanitizedData;
  ```
  - **Lưu ý:** Nếu OpenAI không xóa hết, **cân nhắc chỉnh sửa mã này** để **tự động xóa thêm các cột PII** theo danh sách của doanh nghiệp.

---

### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Upload **1 file CSV mẫu** vào folder Google Drive đã cấu hình.
   - Chạy **Manual Test** trong n8n Editor để kiểm tra kết quả.
2. **Bật Active:**
   - Sau khi **test thành công**, nhấn **Active** để workflow **chạy tự động** khi có file mới.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH LÀM NGOÀI THƯỜNG**]
🔹 **Kết hợp với Slack/Telegram:**
- Thêm **node Slack/Telegram** để **báo cáo kết quả** khi workflow xóa PII thành công.
- **Ví dụ:** `"🚀 File [FILE_NAME] đã được xóa PII thành công! Kết quả tại: [LINK_GOOGLE_DRIVE]"`.
🔹 **Lưu log vào Google Sheets:**
- Sử dụng **node Google Sheets** để **ghi lại lịch sử xử lý** (tên file, thời gian, số cột PII bị xóa).
🔹 **Gửi báo cáo định kỳ:**
- Dùng **node Schedule** (n8n Pro) để **gửi báo cáo tuần/month** về số lượng file đã xử lý.
🔹 **Tự động xóa file gốc sau khi xử lý:**
- Thêm **node Google Drive (Delete)** để **xóa file CSV gốc** sau khi đã upload file sạch.
:::

---

## 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa việc xóa PII trong file CSV**, **tuân thủ GDPR/CCPA**, và **bảo mật dữ liệu** một cách hiệu quả. **Không cần viết code**, chỉ cần **cấu hình API Google Drive và OpenAI**, workflow sẽ **chạy tự động 24/7** khi có file mới.

👉 **Hãy áp dụng ngay để tránh rủi ro pháp lý và tiết kiệm thời gian!**
👉 **Cần hỗ trợ cài đặt VPS cho n8n?** [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với **mã giảm giá VPSN8N (giảm 39%)** hoặc [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
**🚀 Cảm ơn các sếp đã đọc đến cuối!** Nếu có thắc mắc, hãy để lại comment bên dưới. 👇