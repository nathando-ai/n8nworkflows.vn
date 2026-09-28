---
title: "🚀 Tự Động Hoàn Chỉnh Dữ Liệu CRM HubSpot Với API CompanyEnrich - Nâng Cao Chất Lượng Lead 100% Không Code"
description: "Workflow tự động tra cứu và cập nhật thông tin chi tiết doanh nghiệp (domain, industry, size, contact info...) cho các công ty mới tạo/được cập nhật trong HubSpot, giúp các sếp tiết kiệm 10+ giờ/tháng và nâng cao chất lượng dữ liệu CRM."
slug: "tieu-dong-hoan-chinh-dat-lien-he-hubspot-companyenrich"
tags: [n8n, automation, crm, lead-generation, api-integration, hubspot, companyenrich]
keywords: [tự động hóa hubspot, enrich company data, lead generation no-code, api companyenrich, tự động cập nhật thông tin doanh nghiệp, workflow n8n crm]
---

# 🚀 **Tự Động Hoàn Chỉnh Dữ Liệu CRM HubSpot Với API CompanyEnrich**

## **🔍 Giải quyết vấn đề gì?**
Các sếp đang gặp khó khăn khi:
- **Thủ công tra cứu** thông tin chi tiết của khách hàng (domain, ngành nghề, quy mô, liên hệ...) từ nhiều nguồn khác nhau.
- **Dữ liệu CRM không đầy đủ** → Tốn thời gian để gọi điện, gửi email xác minh.
- **Mất thời gian cập nhật** khi khách hàng mới đăng ký hoặc thông tin thay đổi.
- **Không biết cách tích hợp** API CompanyEnrich (dữ liệu doanh nghiệp toàn cầu) với HubSpot một cách tự động.

**Workflow này giải quyết tất cả!** Nó sẽ:
✅ **Tự động tra cứu** thông tin chi tiết của công ty từ API CompanyEnrich.
✅ **Cập nhật ngay lập tức** vào HubSpot khi có công ty mới hoặc thông tin thay đổi.
✅ **Tiết kiệm 10+ giờ/tháng** cho việc tra cứu và cập nhật thủ công.
✅ **Nâng cao chất lượng lead** với dữ liệu chính xác, cập nhật.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn** quá trình enrich dữ liệu CRM → Không cần code, không cần IT.
- **Dữ liệu chính xác và cập nhật** từ API CompanyEnrich (cập nhật liên tục, không cần tra cứu thủ công).
- **Tiết kiệm thời gian** cho team sales/marketing để tập trung vào bán hàng và chiến lược.
- **Cải thiện chất lượng lead** với thông tin chi tiết (ngành nghề, quy mô, liên hệ...) ngay từ khi khách hàng mới đăng ký.
- **Hoạt động 24/7** nhờ Schedule Trigger, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** với:
   - **Private App** (đã cấp quyền **Company Read/Write**).
   - **App Token** (để kết nối với n8n).
2. **Tài khoản CompanyEnrich** (đăng ký tại [companyenrich.com](https://companyenrich.com/)) và **API Key**.
3. **Dữ liệu công ty trong HubSpot** phải có **domain** (để API CompanyEnrich tra cứu).
4. **N8n Self-hosted** (không dùng phiên bản cloud để đảm bảo hoạt động liên tục).
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11928](https://n8n.io/workflows/11928) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **"Active"** ở góc trên bên phải.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình Schedule Trigger (Lặp lại định kỳ)**
- **Node: "Schedule Trigger"**
  - Thiết lập **thời gian chạy** (ví dụ: hàng ngày 8h sáng).
  - **Lưu ý:** Thời gian này quyết định tần suất cập nhật dữ liệu mới.

#### **🔹 Cấu hình HubSpot Get Companies (Lấy công ty mới/được cập nhật)**
- **Node: "Get recently created/updated companies"**
  - Tham số `7*24*60*60*1000` (7 ngày) **phải được thay đổi** theo nhu cầu:
    - `7` = 7 ngày → Thay thành `1` (1 ngày), `14` (14 ngày), hoặc `30` (30 ngày).
  - **Lưu ý:** Nếu thay đổi, **các công ty cũ** sẽ không được enrich lại.

#### **🔹 Cấu hình CompanyEnrich API Key**
- **Node: "CompanyEnrich - Enrich by Domain" (HTTP Request)**
  - Trong **Headers**, thay thế `YOUR_API_KEY` bằng **API Key** của CompanyEnrich.
  - **Lưu ý:** Nếu không điền đúng, API sẽ trả về lỗi `401 Unauthorized`.

#### **🔹 Cấu hình HubSpot Update Company (Cập nhật dữ liệu enrich)**
- **Node: "HubSpot - Update Company"**
  - **Mapping fields** (đối ứng các trường dữ liệu từ CompanyEnrich với HubSpot):
    - Ví dụ:
      - `companyenrich.industry` → `industry` (HubSpot)
      - `companyenrich.size` → `company_size` (HubSpot)
      - `companyenrich.email` → `email` (HubSpot)
  - **⚠️ Lưu ý:**
    - **Chỉ map 1 giá trị/trường** để tránh lỗi API.
    - Nếu không map, dữ liệu enrich sẽ không được lưu vào HubSpot.

#### **🔹 Xử lý lỗi (On Error Log)**
- **Node: "On Error (Log)"**
  - Nếu enrichment thất bại (ví dụ: domain không tồn tại), workflow sẽ **log lỗi** vào node này.
  - **Không cần chỉnh sửa** trừ khi muốn gửi lỗi đến Slack/Email.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với 1-2 công ty mẫu để kiểm tra:
   - Kiểm tra **domain** có được extract đúng không?
   - **Dữ liệu enrich** có được cập nhật vào HubSpot không?
2. **Bật Active** sau khi test thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Tích hợp với Slack/Telegram để báo cáo lỗi**
- Thêm **node Slack/Telegram Webhook** sau **"On Error (Log)"** để nhận thông báo khi enrichment thất bại.
- **Cách làm:**
  - Tạo **Incoming Webhook** trên Slack/Telegram.
  - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` và cấu hình.

### **🔹 Lưu log enrichment vào Google Sheets/Notion**
- Thêm **node Google Sheets** sau **"On Error (Log)"** để ghi lại tất cả lỗi và thành công.
- **Cách làm:**
  - Tạo **Google Sheet** mới.
  - Thêm node `n8n-nodes-base.googleSheets` và cấu hình sheet tương ứng.

### **🔹 Cập nhật định kỳ báo cáo cho team**
- Sử dụng **node `n8n-nodes-base.email`** để gửi báo cáo hàng tuần về:
  - Số lượng công ty được enrich.
  - Số lượng lỗi (nếu có).
- **Cách làm:**
  - Thêm node `n8n-nodes-base.email` sau **"Merge"** và cấu hình email của team.

### **🔹 Tăng tốc độ với Batch Processing**
- Nếu có **hàng ngàn công ty**, sử dụng **node `splitInBatches`** để chia nhỏ batch và tránh timeout.
- **Cách làm:**
  - Thêm **node `n8n-nodes-base.splitInBatches`** trước **"CompanyEnrich - Enrich by Domain"**.
  - Cấu hình **batch size** (ví dụ: 50 công ty/lần).

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc tra cứu và cập nhật dữ liệu CRM thủ công. Với **API CompanyEnrich**, bạn sẽ có **dữ liệu doanh nghiệp chính xác, cập nhật** ngay từ khi khách hàng mới đăng ký.

**Bắt đầu ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 công ty** để đảm bảo hoạt động.
3. **Bật Active** và **quên đi việc tra cứu thủ công!**

👉 **Nếu cần hỗ trợ**, hãy để lại comment bên dưới hoặc liên hệ với **CompanyEnrich** qua [trang web](https://companyenrich.com/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::