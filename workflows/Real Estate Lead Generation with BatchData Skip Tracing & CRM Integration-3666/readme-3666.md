---
title: "🏡 **Tự Động Hóa Tìm Kiếm & Xây Dựng Dữ Liệu Lead Bất Động Sản với Skip Tracing & CRM (n8n)**"
description: "Workflow tự động hóa tìm kiếm, phân tích và xuất dữ liệu lead bất động sản từ BatchData, skip tracing chủ sở hữu, đồng bộ vào CRM (HubSpot) và gửi báo cáo email tự động - tiết kiệm 100% thời gian thủ công cho các sếp bất động sản."
slug: "tieu-dong-hoa-lead-bat-dong-san-skip-tracing-crm"
tags: [n8n, automation, real-estate, lead-generation, skip-tracing, crm-integration]
keywords: [n8n workflow bất động sản, tự động hóa lead bất động sản, skip tracing chủ sở hữu, CRM HubSpot, tìm kiếm nhà đất tự động, xuất dữ liệu Excel]
---

# 🚀 **Tự Động Hóa Lead Bất Động Sản: Từ Tìm Kiếm → Skip Tracing → CRM → Email Tự Động**

## **Nỗi Đau Của Các Sếp Bất Động Sản**
Mỗi ngày, các sếp bất động sản phải:
- **Tìm kiếm thủ công** trên các trang web bất động sản (Zaloan, Batdongsan, BatchData...) để lọc lead phù hợp.
- **Skip tracing chủ sở hữu** bằng cách gọi điện, tra cứu hồ sơ pháp lý hoặc sử dụng dịch vụ trả phí.
- **Nhập liệu vào CRM** (HubSpot, Salesforce...) một cách mệt mỏi, dễ sai sót.
- **Gửi báo cáo hàng ngày** cho team để theo dõi tiến độ.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi lead tiềm năng "chảy mất" vì chậm phản ứng.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình từ tìm kiếm đến CRM, chỉ cần 1 lần cấu hình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo dữ liệu an toàn và không phụ thuộc vào phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** trong việc tìm kiếm và nhập liệu lead.
✅ **Chính xác 100%** với skip tracing tự động (không phụ thuộc vào con người).
✅ **Dữ liệu đồng bộ CRM** (HubSpot, Salesforce, Zoho...) ngay lập tức.
✅ **Báo cáo tự động** gửi email hàng ngày với Excel tóm tắt lead mới.
✅ **Lọc lead chất lượng cao** dựa trên tiêu chí như tỷ lệ sở hữu, tình trạng nợ thuế, hoạt động bán hàng gần đây.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản BatchData API** (để tìm kiếm và skip tracing chủ sở hữu).
   - [Đăng ký BatchData](https://www.batchdata.com/) (miễn phí cho 100 lead/Tháng).
   - **API Key** từ tài khoản BatchData.
2. **Tài khoản CRM** (HubSpot trong ví dụ này, có thể thay thế bằng Salesforce/Zoho).
   - **API Key** và **Credentials** từ CRM.
3. **Tài khoản Email** (Gmail, Outlook...) để gửi báo cáo tự động.
   - **SMTP Credentials** (hoặc sử dụng node `emailSend` với tài khoản Gmail đã kích hoạt "Less Secure Apps").
4. **Google Sheets/Excel Online** (nếu muốn lưu dữ liệu tạm thời trước khi xuất file).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/3666) (chọn "Export").
2. Trên **n8n Editor**, nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/3666) và paste vào **"Import"** → **"From JSON"**.

#### **Phương pháp 2: Copy/Paste JSON**
- Mở **n8n Editor** → **"Import"** → **"From JSON"** → Dán toàn bộ mã JSON từ [workflow gốc](https://n8n.io/workflows/3666).

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **11 node**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

#### **A. Node "Search Properties API" (HTTP Request)**
- **URL:** `https://api.batchdata.com/v1/property/search`
- **Headers:**
  ```json
  {
    "Authorization": "Bearer YOUR_BATCHDATA_API_KEY",
    "Content-Type": "application/json"
  }
  ```
- **Body (JSON):**
  ```json
  {
    "location": "Ho Chi Minh City",
    "property_type": "residential",
    "min_value": 1000000000,
    "max_value": 3000000000,
    "equity_percentage": 30,
    "owner_status": "active"
  }
  ```
  - **Lưu ý:** Thay đổi `location`, `property_type`, `min_value`, `max_value` theo nhu cầu tìm kiếm.

#### **B. Node "Push to CRM" (HubSpot)**
- **Credentials:** Chọn **HubSpot** trong danh sách credentials.
- **API Key:** Nhập **API Key** từ tài khoản HubSpot (tìm tại: **Settings → API Keys**).
- **Endpoint:** Chọn **"Contacts"** (để tạo lead mới).
- **Mapping Data:**
  - `email` → `email`
  - `phone` → `phone`
  - `address` → `address`
  - `property_details` → `custom_properties` (nếu cần thêm trường tùy chỉnh).

#### **C. Node "Email Notification" (EmailSend)**
- **SMTP Config:**
  - **Host:** `smtp.gmail.com` (hoặc SMTP của nhà cung cấp email).
  - **Port:** `587` (hoặc `465` nếu sử dụng SSL).
  - **Username/Password:** Tài khoản email của bạn.
  - **From Email:** Địa chỉ email gửi (ví dụ: `lead-reports@công ty.com`).
- **To Email:** Nhập email của team hoặc bản thân.
- **Subject:** `"Báo cáo Lead Bất Động Sản Hôm Nay - [Ngày Tháng]"`.
- **Body (HTML):**
  ```html
  <p>Xin chào,</p>
  <p>Dưới đây là danh sách lead mới được tìm kiếm tự động:</p>
  <ul>
    {% for lead in $json %}
      <li><strong>Tên Chủ Sở Hữu:</strong> {{ lead.owner_name }}<br>
         <strong>Địa Chỉ:</strong> {{ lead.address }}<br>
         <strong>Giá Trị:</strong> {{ lead.value }} VNĐ</li>
    {% endfor %}
  </ul>
  <p>Tải file Excel chi tiết: <a href="{{ $fileUrl }}">Đây</a></p>
  ```

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Kiểm tra thử):**
   - Nhấn **"Execute"** trên node **"Manual Trigger"** để chạy thử với dữ liệu mẫu.
   - Kiểm tra **CRM** và **email** xem có nhận được lead không.
2. **Bật Schedule Trigger:**
   - Đi đến node **"Daily Schedule"** → Chọn **"Active"** và thiết lập thời gian chạy (ví dụ: **8h sáng hàng ngày**).
3. **Kiểm tra Logs:**
   - Mở **"Logs"** trong n8n để theo dõi lỗi nếu có.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notification:**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
   - Ví dụ: `"🚀 Workflow hoàn thành! Tìm thấy {{ $json.length }} lead mới."`

2. **Lưu Logs vào Google Sheets:**
   - Thêm node **Google Sheets** sau node **"Summarize Results"** để lưu lịch sử chạy workflow.

3. **Tự động Gửi Báo Cáo Cho Team:**
   - Sử dụng node **Google Calendar** để gửi email báo cáo vào thời gian cố định (ví dụ: **mỗi thứ 2 hàng tuần**).

4. **Tối Ưu Tìm Kiếm:**
   - Thêm **tiêu chí lọc thêm** trong node **"Filter Property Results"** (Code):
     ```javascript
     // Ví dụ: Chỉ lấy lead có tỷ lệ sở hữu > 40%
     return $input.all().filter(lead => lead.equity_percentage > 40);
     ```

5. **Kết hợp với AI (LLM) để Tóm Tắt:**
   - Thêm node **LLM (n8n-nodes-ai)** để tự động viết **tóm tắt lead chất lượng cao** trong email.

---

## 📌 **Kết Luận: Áp Dụng Ngay & Tiết Kiệm 100% Thời Gian Thủ Công!**
Workflow này **giải phóng các sếp** khỏi công việc mệt mỏi tìm kiếm và nhập liệu lead bất động sản. Với **tự động hóa từ tìm kiếm → skip tracing → CRM → email**, các sếp có thể:
✔ **Tăng gấp đôi số lead** theo dõi mỗi ngày.
✔ **Tăng chất lượng lead** với lọc tự động.
✔ **Tiết kiệm ngân sách** so với dịch vụ skip tracing trả phí.

**Bước đầu tiên:** Import workflow và **cấu hình BatchData API** ngay hôm nay! Nếu có vấn đề, để lại comment bên dưới, các sếp sẽ được hỗ trợ chi tiết.

---
**#TựĐộngHóaBấtĐộngSản #LeadGeneration #n8nVietnam #CRMAutomation**