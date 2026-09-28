---
title: "🤖 **Tự Động Hóa So Sánh Hóa Đơn & Đơn Hàng (PO Matching) Với AI Gemini + Thông Báo Email Tự Động**"
description: "Giải pháp 100% tự động hóa so sánh hóa đơn với đơn đặt hàng (PO) bằng AI Gemini, cập nhật trạng thái thanh toán tự động và gửi thông báo email cho bộ phận tài chính. Giúp các sếp tiết kiệm 10+ giờ/tháng, giảm sai sót và tăng hiệu quả kiểm soát chi phí."
slug: "tự-dộng-hoa-so-sánh-hoa-don-po-matching-ai-gemini"
tags: [n8n, automation, ai-gemini, google-sheets, invoice-processing, email-notification]
keywords: [n8n workflow tự động hóa hóa đơn, so sánh PO với hóa đơn bằng AI, AI Gemini trong n8n, tự động hóa bộ phận tài chính, giảm sai sót hóa đơn]
---

# 🚀 **Tự Động Hóa So Sánh Hóa Đơn & Đơn Hàng (PO Matching) Với AI Gemini + Thông Báo Email Tự Động**

### **🔍 Nỗi Đau Của Các Sếp Trong Bộ Phận Tài Chính**
Hàng ngày, bộ phận tài chính phải:
- **Tìm kiếm và so sánh** hàng trăm hóa đơn với đơn đặt hàng (PO) thủ công → **Tốn thời gian 5-10 giờ/ngày**.
- **Mất nhiều công sức** để tra cứu thông tin chi tiết từ hóa đơn PDF (số lượng, đơn giá, tổng tiền, mã PO...).
- **Sai sót cao** khi so sánh thủ công → Rủi ro thanh toán sai hoặc bị khiếu nại từ nhà cung cấp.
- **Không có báo cáo tự động** → Phải theo dõi từng hóa đơn một, dễ quên hoặc bỏ sót.

**Giải pháp này giúp các sếp:**
✅ **Tự động hóa 100% quy trình** so sánh hóa đơn với PO bằng AI Gemini.
✅ **Cập nhật trạng thái thanh toán** tự động vào Google Sheets.
✅ **Gửi email thông báo** cho bộ phận tài chính khi hóa đơn **không khớp** với PO.
✅ **Tiết kiệm 10+ giờ/tháng** và giảm sai sót đến **90%**.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI Gemini)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**

### **1. Tiết Kiệm Thời Gian & Công Suất**
- **Không cần tra cứu thủ công** trên hóa đơn PDF → AI Gemini tự động **trích xuất số lượng, đơn giá, tổng tiền, mã PO**.
- **So sánh tự động** với dữ liệu PO trong Google Sheets → **Không sai sót** như khi làm thủ công.

### **2. Cập Nhật Trạng Thái Thanh Toán Tự Động**
- Nếu hóa đơn **khớp với PO**, hệ thống **cập nhật trạng thái "Đã thanh toán"** vào bảng Google Sheets.
- Nếu **không khớp**, hệ thống **gửi email cảnh báo** cho bộ phận tài chính để xử lý.

### **3. Giảm Sai Sót & Rủi Ro**
- AI Gemini **xác minh lại** thông tin hóa đơn trước khi so sánh → **Giảm sai sót đến 90%**.
- **Không bỏ sót hóa đơn** nào → Hệ thống **lưu tất cả dữ liệu** vào Google Sheets.

### **4. Hoạt Động 24/7 Mà Không Cần Can Thiệp**
- Workflow **chạy tự động** khi có hóa đơn mới được upload lên Google Drive.
- **Không cần người dùng nhớ bật/tắt** → **Tiết kiệm công sức quản lý**.

---

## 🔧 **Yêu Cầu Cần Thiết**

### **1. Tài Khoản & API Keys Cần Chuẩn Bị**
| **Dịch Vụ**               | **Thông Tin Cần Thiết**                          | **Lưu Ý** |
|---------------------------|--------------------------------------------------|-----------|
| **Google Drive**          | OAuth 2.0 API Key (Google Drive OAuth2)           | Cần **quyền chỉnh sửa** folder chứa hóa đơn. |
| **Google Sheets**         | OAuth 2.0 API Key (Google Sheets OAuth2)          | Cần **quyền chỉnh sửa** bảng PO_DB và Update_Row. |
| **Google Gemini AI**      | API Key (GooglePalmApi)                          | Cần **tài khoản Google Cloud** với API Gemini. |
| **Microsoft Outlook**     | OAuth 2.0 API Key (Microsoft Outlook OAuth2)     | Cần **tài khoản email doanh nghiệp** để gửi thông báo. |

### **2. File & Bảng Dữ Liệu Cần Chuẩn Bị**
- **Google Drive Folder**: Chứa các file hóa đơn PDF (cần **quyền đọc** cho n8n).
- **Google Sheets**:
  - **Bảng PO_DB**: Chứa danh sách đơn đặt hàng (PO) với các cột: `PO_ID`, `Supplier`, `Amount`, `Status`.
  - **Bảng Update_Row**: Chứa thông tin cập nhật trạng thái thanh toán.

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương Pháp 1: Import từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/10123](https://n8n.io/workflows/10123) (chọn **Export as JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn "Import"** → Workflow sẽ được tạo thành công.

#### **Phương Pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/10123](https://n8n.io/workflows/10123).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
3. **Chọn "Import"** → Workflow sẽ được tạo.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Google Drive Trigger**
- **Chọn Folder**: Chỉ định **folder Google Drive** chứa hóa đơn PDF.
- **Event Type**: Chọn **"File created"** (n8n sẽ kích hoạt khi có file mới được upload).

#### **🔹 Node 2: Download File (Google Drive)**
- **File ID**: **Không cần chỉnh** (n8n tự động lấy từ trigger).
- **File Path**: Đảm bảo **quyền đọc** file PDF.

#### **🔹 Node 3: Extract from File (PDF)**
- **File Type**: Chọn **"PDF"**.
- **Output Format**: Chọn **"Text"** (AI Gemini sẽ xử lý dữ liệu văn bản).

#### **🔹 Node 4: Information Extractor (AI Gemini)**
- **Prompt**: **Không cần chỉnh** (AI sẽ tự động trích xuất thông tin từ hóa đơn).
- **Output**: Lấy ra các trường như `Invoice_ID`, `Supplier`, `Amount`, `PO_ID`.

#### **🔹 Node 5: Google Gemini Chat Model (AI Gemini)**
- **Model**: Chọn **"gemini-pro"** (hoặc phiên bản mới nhất).
- **Prompt**: **Không cần chỉnh** (AI sẽ tự động so sánh với PO).
- **Output**: Trả về **các trường khớp/không khớp** giữa hóa đơn và PO.

#### **🔹 Node 6: Switch (Điều Khiển Lộ Trình)**
- **Condition**:
  - Nếu `Amount > 5000` → **Gửi email cảnh báo** (nếu không khớp).
  - Nếu `Amount <= 5000` → **Cập nhật trạng thái tự động**.

#### **🔹 Node 7: PO_DB (Google Sheets Tool)**
- **Sheet Name**: Đặt tên là **PO_DB** (phải khớp với bảng trong Google Sheets).
- **Query**: Lấy dữ liệu PO dựa trên `PO_ID` từ hóa đơn.

#### **🔹 Node 8: Update_Row (Google Sheets Tool)**
- **Sheet Name**: Đặt tên là **Update_Row** (phải khớp với bảng trong Google Sheets).
- **Operation**: Chọn **"Update"** → Cập nhật trạng thái thanh toán.

#### **🔹 Node 9: If (Kiểm Tra Khớp/Không Khớp)**
- **Condition**:
  - Nếu `PO_ID` **không tồn tại** trong PO_DB → **Gửi email cảnh báo**.
  - Nếu `PO_ID` **tồn tại** → **Cập nhật trạng thái "Đã thanh toán"**.

#### **🔹 Node 10: Append Row in Sheet (Google Sheets)**
- **Sheet Name**: Đặt tên là **Invoice_Log** (nếu muốn lưu lịch sử).
- **Data**: Lưu thông tin hóa đơn đã xử lý.

#### **🔹 Node 11: Send a Message (Microsoft Outlook)**
- **Email To**: Điền **email bộ phận tài chính** (ví dụ: `finance@doanhnghiep.com`).
- **Subject**: `"Cảnh báo: Hóa đơn #{{$node["Extract from File"].json["invoice_id"]}} không khớp với PO"`.
- **Body**: Nội dung cảnh báo chi tiết (AI Gemini tự động tạo).

#### **🔹 Node 12: Structured Output Parser (AI Gemini)**
- **Output Format**: Chọn **"JSON"** (để dễ dàng xử lý dữ liệu trong n8n).

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **1 file hóa đơn mẫu**:
   - Upload **1 file PDF hóa đơn** vào Google Drive.
   - Kiểm tra **các email cảnh báo** và **cập nhật Google Sheets**.
2. **Bật Active**:
   - Nhấn **Active** trên workflow → Workflow sẽ **chạy tự động** khi có file mới.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram (Thông Báo Thực Tế)**
- **Thêm Node Slack/Telegram** sau **Node "Send a message" Outlook** để **cảnh báo ngay lập tức** trên kênh team.
- **Cách làm**:
  ```markdown
  - Thêm **Node Slack Webhook** (nếu dùng Slack) hoặc **Node Telegram Bot** (nếu dùng Telegram).
  - Gửi **thông báo rich text** với:
    - Tên hóa đơn.
    - Mã PO.
    - Số tiền.
    - Lỗi (nếu có).
  ```

### **2. Lưu Log Tất Cả Các Hóa Đơn (Dễ Dàng Theo Dõi)**
- **Thêm Node "Append Row in Sheet"** sau **Node "Extract from File"** để **lưu tất cả hóa đơn** vào 1 bảng **Invoice_Log**.
- **Cột cần lưu**:
  - `Invoice_ID`
  - `Supplier`
  - `Amount`
  - `PO_ID`
  - `Status` (Đã khớp/Không khớp)
  - `Timestamp` (Thời gian xử lý)

### **3. Gửi Báo Cáo Định Kỳ (Tuần/Hàng Tháng)**
- **Thêm Node "Google Sheets Tool" (Query)** để **tính tổng số hóa đơn khớp/không khớp**.
- **Gửi email báo cáo** hàng tuần bằng **Node "Microsoft Outlook"** với:
  - **Tổng số hóa đơn đã xử lý**.
  - **Số hóa đơn khớp vs PO**.
  - **Số hóa đơn chưa khớp (cần xử lý)**.
  - **Bảng thống kê** (có thể đính kèm file Excel).

### **4. Tích Hợp Với ERP (SAP, Odoo, QuickBooks)**
- Nếu doanh nghiệp dùng **ERP**, có thể **tích hợp với Node ERP** để:
  - **Cập nhật trạng thái thanh toán** trực tiếp vào hệ thống.
  - **Trích xuất PO tự động** từ ERP thay vì Google Sheets.

---

## 📌 **Kết Luận**

### **🚀 Workflow này giải quyết hoàn toàn các vấn đề:**
✔ **Tự động hóa so sánh hóa đơn vs PO** → **Không cần làm thủ công**.
✔ **AI Gemini trích xuất dữ liệu chính xác** → **Giảm sai sót đến 90%**.
✔ **Cập nhật trạng thái thanh toán tự động** → **Không quên hóa đơn nào**.
✔ **Gửi email cảnh báo** khi hóa đơn **không khớp** → **Bộ phận tài chính xử lý kịp thời**.

### **💡 Lời Khuyên Cuối Cùng**
- **Test workflow với 1-2 hóa đơn mẫu** trước khi áp dụng toàn bộ.
- **Monitor Google Sheets** để đảm bảo dữ liệu cập nhật đúng.
- **Tích hợp Slack/Telegram** để **nhận thông báo ngay lập tức** khi có lỗi.

**👉 Hãy áp dụng ngay workflow này và tiết kiệm **10+ giờ/tháng** cho bộ phận tài chính!**
**📩 Có thắc mắc? Để lại comment bên dưới hoặc liên hệ tôi qua [LinkedIn](https://www.linkedin.com/in/abdulmatheen/).**

---
**🔥 Cảm ơn các sếp đã đọc đến cuối!** 🔥