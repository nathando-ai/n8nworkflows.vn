---
title: "🏡 **Tự Động Hóa Thu Gom, Lọc & Phân Loại Lead Bất Động Sản Với WhatsApp, Typeform, Airtable & AI (GPT-4.1-mini)**"
description: "Workflow tự động hóa 100% không code thu thập lead từ WhatsApp, Typeform, Airtable và phân loại, loại bỏ trùng lặp, gán nhiệm vụ cho nhân viên và báo cáo tuần tự. Giúp doanh nghiệp tiết kiệm 20+ giờ/ngày và tăng tỷ lệ chuyển đổi lead thành khách hàng."
slug: "tieu-dong-hoa-lead-bat-dong-san-whatsapp-typeform-airtable"
tags: [n8n, automation, no-code, real-estate, lead-generation, ai-chatbot, airtable, whatsapp-business, gpt-4, gmail, slack]
keywords: [n8n workflow bất động sản, tự động hóa lead bất động sản, AI phân loại lead bất động sản, WhatsApp thu thập lead, Typeform tự động hóa, Airtable CRM tự động, GPT-4.1-mini phân tích lead]
---

# 🚀 **Tự Động Hóa Lead Bất Động Sản: Từ Thu Gom Đến Báo Cáo Tuần Tự**

### **Nỗi Đau Của Các Sếp Bất Động Sản**
Hàng ngày, các sếp bất động sản phải:
- **Làm thủ công** thu thập lead từ WhatsApp, website, Typeform, Facebook Ads...
- **Loại bỏ trùng lặp** lead (thậm chí cùng 1 lead gửi nhiều lần).
- **Phân loại lead** theo khu vực, loại nhà, ngân sách, và ý định mua bán.
- **Gán nhiệm vụ** cho nhân viên theo quy trình round-robin (đảm bảo công bằng).
- **Báo cáo tuần tự** để đánh giá hiệu suất và tối ưu chiến dịch.

**Kết quả?** Tốn **20+ giờ/ngày**, tỷ lệ chuyển đổi thấp, và mất nhiều thời gian cho công việc lặp lại.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ/ngày** với tự động hóa thu thập, lọc và phân loại lead.
- **Loại bỏ trùng lặp 100%** bằng AI + Airtable, tránh double assignment.
- **Phân loại lead chính xác** theo khu vực, loại nhà, ngân sách và ý định mua bán.
- **Gán nhiệm vụ tự động** theo quy trình round-robin, đảm bảo công bằng.
- **Báo cáo tuần tự** tự động gửi qua Gmail với dữ liệu phân tích chi tiết.
- **Tích hợp AI GPT-4.1-mini** để đánh giá chất lượng lead và chuẩn hóa dữ liệu.
- **Mở rộng dễ dàng** với Facebook Ads, Google Ads, hoặc thêm các kênh mới.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| Dịch Vụ               | Thông Tin Cần Thiết                                                                 |
|-----------------------|------------------------------------------------------------------------------------|
| **WhatsApp Business** | - API Access Token (cấp từ Meta Business Suite)                                   |
|                       | - Credential "whatsAppTriggerApi" (cấu hình trong n8n)                            |
| **OpenAI (GPT-4.1-mini)** | - API Key (mua trên [OpenAI Platform](https://platform.openai.com/))               |
|                       | - Credential "openAiApi" (điền vào n8n)                                           |
| **Airtable**          | - API Key (Access Token)                                                          |
|                       | - Base URL và tên bảng (CRM)                                                      |
|                       | - Credential "airtableTokenApi"                                                   |
| **Gmail**             | - OAuth 2.0 Credential (cấu hình trong n8n)                                      |
|                       | - Credential "gmailOAuth2"                                                        |
| **Slack**             | - API Token (cấp từ [Slack API](https://api.slack.com/))                         |
|                       | - Credential "slackApi"                                                           |
| **Typeform**          | - API Key (cấp từ [Typeform Developer](https://developer.typeform.com/))          |
|                       | - Credential "typeformApi"                                                        |

### **2. Cấu Trúc Airtable (CRM)**
- **Bảng chính (Lead Table):**
  - Các trường bắt buộc: `Email`, `First Name`, `Last Name`, `Phone Number`, `Budget Range`, `Property Type`, `Location`, `Intent` (Mua/Bán/Tìm Nhà).
  - Trường bổ sung: `Assigned Agent`, `Status` (Qualified/Not Qualified), `Created At`, `Updated At`.
- **Bảng phụ (Duplicate Logs):**
  - Dùng để lưu trữ lead trùng lặp để theo dõi và phân tích.

### **3. Cấu Hình WhatsApp Business**
- **Cần có số điện thoại WhatsApp Business** đã đăng ký với Meta.
- **Cấu hình Webhook** trong Meta Business Suite để nhận lead từ WhatsApp.
---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/12820) (ấn nút **"Download"**).
2. Trong n8n Editor, nhấn **"Import"** → Chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở n8n Editor → Nhấn **"Create"** → **"Import Workflow"** → Chọn **"Paste JSON"**.
2. Copy toàn bộ nội dung JSON từ [đây](https://n8n.io/workflows/12820) (ấn **"Export"**).
3. Dán vào ô và nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **37 node** và **5 phần quan trọng** cần cấu hình kỹ lưỡng:

#### **🔹 1. Cấu Hình Credentials (Tất Cả Các Node API)**
- **OpenAI (GPT-4.1-mini):**
  - Đi đến **Credentials** → **"Add"** → Chọn **"OpenAI API"** → Điền `API Key`.
  - Gán credential này cho node:
    - `OpenAI Chat Model`
    - `Basic LLM Chain`
    - `Extract Lead Info`
    - `Info Completeness Check`

- **Airtable:**
  - Đi đến **Credentials** → **"Add"** → Chọn **"Airtable API"** → Điền:
    - `API Key` (Access Token).
    - `Base URL` (ví dụ: `https://api.airtable.com/v0/appXXXXXXXXXX`).
  - Gán credential cho tất cả node Airtable:
    - `Search records`, `Get Records`, `Create A Record`, `Create Duplicate record`.

- **WhatsApp:**
  - Đi đến **Credentials** → **"Add"** → Chọn **"WhatsApp"** → Điền:
    - `Phone Number` (số WhatsApp Business).
    - `API Token` (cấp từ Meta Business Suite).
  - Gán credential cho:
    - `WhatsApp Trigger` (node `whatsAppTrigger`).
    - `Send message` (node `whatsApp`).

- **Gmail & Slack:**
  - Cấu hình tương tự như trên, đảm bảo OAuth2 được cấp quyền đầy đủ.

#### **🔹 2. Cấu Hình Airtable (CRM)**
- **Update tên bảng và trường:**
  - Trong node `Search records` và `Get Records`, chỉnh sửa:
    - `Base ID` → ID của Airtable Base của bạn.
    - `Table Name` → Tên bảng chính (ví dụ: `Leads`).
  - Trong node `Create A Record` và `Create Duplicate record`, đảm bảo:
    - `Table Name` = `Leads` (hoặc tên bảng chính).
    - `Fields` phù hợp với cấu trúc CRM của bạn.

#### **🔹 3. Cấu Hình AI (GPT-4.1-mini)**
Workflow sử dụng AI để:
- **Trích xuất thông tin lead** từ tin nhắn WhatsApp.
- **Kiểm tra độ hoàn chỉnh** của lead.
- **Phân loại lead** theo ngân sách, khu vực, và ý định mua bán.
- **Đánh giá chất lượng lead** (Qualified/Not Qualified).

**Lưu ý:**
- Nếu muốn **tùy chỉnh prompt**, chỉnh sửa trong node:
  - `Basic LLM Chain` (trích xuất thông tin).
  - `Info Completeness Check` (kiểm tra độ hoàn chỉnh).
  - `Extract Lead Info` (chuyển đổi tin nhắn thành dữ liệu structured).

#### **🔹 4. Cấu Hình Deduplication (Loại Bỏ Trùng Lặp)**
Workflow tự động:
1. So sánh lead mới với Airtable bằng **email**.
2. Nếu trùng lặp, **lưu vào bảng phụ** và **bỏ qua lead đó**.
3. Nếu mới, **tạo record mới** và **gán nhiệm vụ**.

**Lưu ý:**
- Trong node `Check for Duplicates in CRM`, đảm bảo:
  - `Field to compare` = `Email`.
  - `Airtable Base ID` và `Table Name` chính xác.

#### **🔹 5. Cấu Hình Routing & Assignment (Gán Nhiệm Vụ)**
Workflow sử dụng **quy trình round-robin** để gán lead cho nhân viên:
- **Phân loại lead** theo `Property Type` (nhà riêng, căn hộ, đất nền...).
- **Lưu trữ metadata** trong Airtable về nhân viên được gán.

**Lưu ý:**
- Trong node `Round-Robin Agent Assignment1`, chỉnh sửa:
  - Danh sách nhân viên (ví dụ: `Agent1@email.com`, `Agent2@email.com`).
  - Quy tắc phân loại (ví dụ: `Property Type = "Condo"` → Gán cho nhóm Condo).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run với Dữ Liệu Mẫu:**
   - Gửi một lead mẫu qua **WhatsApp** hoặc **Typeform**.
   - Kiểm tra:
     - Lead có được lưu vào Airtable không?
     - AI có trích xuất thông tin chính xác không?
     - Lead có được gán cho nhân viên không?
     - Slack/Gmail có nhận được thông báo không?

2. **Bật Active Workflow:**
   - Nhấn **"Publish"** → **"Activate"** để workflow chạy 24/7.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tích Hợp Facebook Ads & Google Ads**
- Sử dụng **Facebook Lead Ads** hoặc **Google Ads** để thu thập lead.
- Cấu hình **Webhook** từ Facebook/Google vào node `Typeform Trigger` hoặc `WhatsApp Trigger`.

### **2. Lưu Log & Theo Dõi Hiệu Suất**
- Tạo **bảng Log** trong Airtable để lưu:
  - Thời gian lead được xử lý.
  - Thời gian gán nhiệm vụ.
  - Trạng thái (Qualified/Not Qualified).
- Sử dụng **node `stickyNote`** để ghi chú lỗi hoặc cảnh báo.

### **3. Báo Cáo Chi Tiết Hàng Ngày**
- Chỉnh sửa node `Weekly Report Schedule` để:
  - **Gửi báo cáo hàng ngày** thay vì tuần.
  - **Thêm biểu đồ** bằng cách kết nối với **Google Sheets** hoặc **Power BI**.

### **4. Tích Hợp CRM Khác (Zoho, HubSpot...)**
- Thay thế node Airtable bằng **Zoho CRM** hoặc **HubSpot** bằng cách:
  - Cấu hình **API Key** của Zoho/HubSpot.
  - Chỉnh sửa `Base URL` và `Table Name` trong node Airtable.

### **5. Tự Động Gửi Email Follow-Up**
- Sử dụng **node `gmail`** để:
  - Gửi email tự động cho lead **Not Qualified** với nội dung khuyến nghị.
  - Gửi email **cảm ơn** cho lead đã hoàn thành form.

---
## 📌 **Kết Luận**
Workflow này **giải quyết tất cả vấn đề thủ công** trong quá trình thu thập, lọc và phân loại lead bất động sản:
✅ **Tự động hóa 100%** từ thu thập đến báo cáo.
✅ **Loại bỏ trùng lặp** bằng AI + Airtable.
✅ **Phân loại lead chính xác** theo khu vực, loại nhà, và ý định mua bán.
✅ **Gán nhiệm vụ tự động** theo quy trình round-robin.
✅ **Báo cáo tuần tự** với dữ liệu phân tích chi tiết.

**👉 Hành động ngay!**
1. **Cài đặt n8n trên VPS** để workflow chạy 24/7 (không phụ thuộc vào máy chủ cá nhân).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với lead mẫu** và bật Active.

**🚀 Kết quả?** **Tiết kiệm 20+ giờ/ngày**, tăng tỷ lệ chuyển đổi lead, và tự động hóa toàn bộ quy trình bất động sản!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**📩 Liên hệ với tác giả (nếu cần hỗ trợ):**
- **Email:** buzanalytics@gmail.com
- **LinkedIn:** [Ezema Kingsley Chibuzo](https://www.linkedin.com/in/ezemakingsley/) (Data Analyst & Automation Developer)