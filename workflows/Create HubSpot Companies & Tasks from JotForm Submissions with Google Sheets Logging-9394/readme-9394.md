---
title: "🚀 Tự Động Hoàn Chỉnh HubSpot & Tạo Nhiệm Vụ Từ Đăng Ký JotForm (Với Google Sheets Log)"
description: "Workflow tự động hóa 100% không code để chuyển đổi dữ liệu từ JotForm thành công ty và nhiệm vụ trên HubSpot, đồng thời ghi log chi tiết vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng và tối ưu hóa quy trình bán hàng/marketing."
slug: "tieu-dong-hoan-chinh-hubspot-tu-jotform"
tags: [n8n, automation, no-code, hubspot, jotform, google-sheets, sales-automation]
keywords: [tự động hóa hubspot, jotform automation, tự động tạo công ty hubspot, ghi log google sheets, workflow n8n marketing]
---

# 🚀 **Tự Động Hoàn Chỉnh HubSpot & Tạo Nhiệm Vụ Từ Đăng Ký JotForm (Với Google Sheets Log)**

### **💡 Nỗi Đau Của Các Sếp**
Các sếp marketing/sales thường phải:
- **Nhập thủ công** dữ liệu từ JotForm vào HubSpot (tốn 10-15 phút/đăng ký).
- **Quên cập nhật** thông tin công ty (đặc biệt là domain) sau khi tạo nhiệm vụ.
- **Không theo dõi** quá trình tự động hóa (không biết có lỗi không?).
- **Lặp lại công việc** khi cần chỉnh sửa thông tin sau này.

**Workflow này giải quyết tất cả!** Chỉ cần 1 lần cấu hình, hệ thống sẽ:
✅ **Tự động tạo công ty** trên HubSpot từ tên công ty trong JotForm.
✅ **Tạo nhiệm vụ** liên quan với thông tin chi tiết (email, LinkedIn, ngân sách marketing...).
✅ **Cập nhật domain** cho công ty trên HubSpot.
✅ **Ghi log toàn bộ quá trình** vào Google Sheets để theo dõi và debug.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần nhập thủ công dữ liệu từ JotForm.
- **Chính xác 100%**: Tự động tạo công ty và nhiệm vụ với thông tin chuẩn hóa.
- **Cập nhật tự động domain**: Không quên bật công ty domain sau khi tạo nhiệm vụ.
- **Theo dõi toàn bộ quá trình**: Google Sheets ghi log chi tiết cho mỗi đăng ký.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp.
- **Giảm lỗi nhân sự**: Tránh sai sót do nhập liệu thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản JotForm**:
   - API Key từ [JotForm Developer Console](https://developer.jotform.com/).
   - Form đã cấu hình với các trường:
     - **Name**, **First Name**, **Last Name**, **Email**, **LinkedIn Profile**, **Company Name**, **Marketing Budget (USD)**, **Domain**, **Any Specific Query**.

2. **Tài khoản HubSpot**:
   - API Key từ [HubSpot Developer Portal](https://developers.hubspot.com/docs/api/private-apps).
   - **Permissions**: Tạo công ty (Companies), tạo nhiệm vụ (Tasks), cập nhật thông tin công ty.

3. **Google Sheets**:
   - File Google Sheets đã tạo với **bảng dữ liệu** để ghi log.
   - **Chuẩn hóa cột**: Cần có cột như `Timestamp`, `Form Submission ID`, `Company Name`, `Status`, `Error (nếu có)`.

4. **N8n Self-hosted**:
   - N8n đã cài đặt trên VPS (không dùng phiên bản cloud).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9394) hoặc copy JSON từ canvas.
- **Mở n8n Editor** → **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** (Active) sau khi import.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình JotForm Trigger**
- **Node**: `JotForm Trigger`
- **Thao tác**:
  - Chọn `jotFormApi` trong **Credentials**.
  - **Test connection** để xác nhận API key đúng.
  - **Lưu ý**: Chỉ chọn **form cụ thể** trong dropdown (không phải tất cả form).

##### **B. Cấu Hình HubSpot**
- **Node 1**: `Create a company1` (type: `hubspot`)
  - **Credentials**: Chọn `hubspotApi`.
  - **Key Parameters**:
    - `resource`: `company` (đã mặc định).
    - **Payload**: Sử dụng dữ liệu từ JotForm (đặc biệt là `companyName`).
  - **Test run**: Gửi một dữ liệu mẫu để kiểm tra tạo công ty thành công.

- **Node 2**: `Create HubSpot Task` (type: `httpRequest`)
  - **Method**: `POST`.
  - **URL**: `https://api.hubapi.com/crm/v3/objects/tasks` (mặc định).
  - **Headers**:
    - `Authorization`: `Bearer {hubspot_api_key}`.
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "properties": {
        "company": "{{ $node["Create a company1"].json[\"result\"][\"id\"] }}",
        "associationCategory": "company",
        "associationValue": "{{ $node["Create a company1"].json[\"result\"][\"id\"] }}",
        "title": "Follow up with {{ $node["JotForm Trigger"].json[\"data\"][\"First Name\"] }} {{ $node["JotForm Trigger"].json[\"data\"][\"Last Name\"] }}",
        "description": "New lead from JotForm: {{ $node["JotForm Trigger"].json[\"data\"][\"Any Specific Query\"] }}",
        "dueDate": "{{ $node["Formating Data"].json[\"dueDate\"] }}",
        "owner": "{{ $node["Formating Data"].json[\"ownerId\"] }}"
      }
    }
    ```
  - **Lưu ý**:
    - Node `Formating Data` (type: `code`) sẽ chuẩn hóa dữ liệu trước khi tạo nhiệm vụ.
    - **Test run** với dữ liệu mẫu để đảm bảo nhiệm vụ được tạo đúng.

##### **C. Cấu Hình Google Sheets Log**
- **Node**: `Storel Logs` (type: `googleSheets`)
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Key Parameters**:
    - `operation`: `appendOrUpdate` (mặc định).
  - **Sheet Name**: Điền tên bảng Google Sheets đã chuẩn bị.
  - **Range**: `Sheet1!A1:Z1000` (hoặc tùy chỉnh).
  - **Data Format**:
    ```json
    {
      "Timestamp": "{{ $node["JotForm Trigger"].json[\"timestamp\"] }}",
      "Form Submission ID": "{{ $node["JotForm Trigger"].json[\"id\"] }}",
      "Company Name": "{{ $node["JotForm Trigger"].json[\"data\"][\"Company Name\"] }}",
      "Status": "Success",
      "Error": ""
    }
    ```
  - **Lưu ý**:
    - Nếu có lỗi, `Status` sẽ tự động thay đổi thành `Failed` và `Error` sẽ ghi chi tiết.

##### **D. Cập Nhật Domain Cho Công Ty**
- **Node**: `Set Company Domain` (type: `httpRequest`)
  - **Method**: `PATCH`.
  - **URL**: `https://api.hubapi.com/crm/v3/objects/companies/{{ $node["Create a company1"].json[\"result\"][\"id\"] }}`.
  - **Headers**:
    - `Authorization`: `Bearer {hubspot_api_key}`.
    - `Content-Type`: `application/json`.
  - **Body (JSON)**:
    ```json
    {
      "properties": {
        "website": "{{ $node["JotForm Trigger"].json[\"data\"][\"Domain\"] }}"
      }
    }
    ```
  - **Lưu ý**:
    - Node `Wait10` (10 giây) trước khi cập nhật domain để tránh rate limit.

##### **E. Node Code (Formating Data)**
- **Mã JavaScript** (cần chỉnh sửa nếu cần):
  ```javascript
  // Chuyển đổi dữ liệu từ JotForm sang định dạng chuẩn cho HubSpot
  const formattedData = {
    dueDate: new Date(Date.now() + 86400000).toISOString(), // Ngày hôm sau
    ownerId: "YOUR_HUBSPOT_OWNER_ID", // Thay bằng ID của người quản lý trong HubSpot
    companyName: $input.all[0].data["Company Name"].trim(),
    email: $input.all[0].data["Email"].trim(),
    linkedin: $input.all[0].data["LinkedIn Profile"],
    budget: $input.all[0].data["Marketing Budget (in USD)"]
  };
  return formattedData;
  ```
  - **Lưu ý**:
    - Thay `YOUR_HUBSPOT_OWNER_ID` bằng ID của người quản lý trong HubSpot (tìm trong `Settings > Users`).
    - **Test run** để đảm bảo dữ liệu được chuẩn hóa đúng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn `JotForm Trigger` → **Run Workflow**.
   - Kiểm tra:
     - Công ty có được tạo trên HubSpot không?
     - Nhiệm vụ có được tạo và liên kết với công ty không?
     - Domain có được cập nhật không?
     - Log trên Google Sheets có ghi dữ liệu không?
2. **Bật Active** nếu tất cả test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau `Storel Logs` để thông báo khi workflow hoàn thành thành công/lỗi.
   - **Ví dụ**:
     ```json
     {
       "text": "✅ New lead processed: {{ $node["JotForm Trigger"].json[\"data\"][\"Company Name\"] }}",
       "username": "n8n HubSpot Bot"
     }
     ```

2. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.googleSheets` để gửi báo cáo tổng hợp hàng tuần về hoạt động của workflow.
   - **Ví dụ**:
     - Tạo một sheet mới mỗi tuần với tổng số công ty/nhiệm vụ được tạo.
     - Gửi email tự động bằng node `email` với dữ liệu từ sheet.

3. **Xử Lý Lỗi Tự Động**:
   - Thêm node `n8n-nodes-base.if` để kiểm tra `Status` trong Google Sheets.
   - Nếu `Status = Failed`, gửi email cảnh báo hoặc gọi API để khắc phục.

4. **Tối Ưu HubSpot API**:
   - Sử dụng node `n8n-nodes-base.wait` giữa các API call để tránh bị rate limit.
   - **Lưu ý**: HubSpot cho phép tối đa 500 request/ngày cho API private apps.

5. **Lưu Trữ Log Dài Hơn**:
   - Thay vì ghi vào Google Sheets, các sếp có thể sử dụng **BigQuery** hoặc **AWS S3** để lưu log dài hạn.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing/sales muốn:
✔ **Tự động hóa** quy trình chuyển đổi lead từ JotForm sang HubSpot.
✔ **Tiết kiệm thời gian** và giảm sai sót do nhập liệu thủ công.
✔ **Theo dõi toàn bộ quá trình** với Google Sheets log chi tiết.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test run** với dữ liệu mẫu để đảm bảo hoạt động ổn định.
3. **Bật Active** và quên đi công việc nhập liệu thủ công!

**Nếu có vấn đề**, các sếp có thể liên hệ với tác giả [Rahi Uppal](https://www.linkedin.com/in/rahiuppal/) trên LinkedIn để hỗ trợ.

---
🚀 **Chúc các sếp thành công với tự động hóa HubSpot!** 🚀