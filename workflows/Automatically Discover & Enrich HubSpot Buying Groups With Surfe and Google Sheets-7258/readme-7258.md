---
title: "🚀 Tự Động Hóa Khám Phá & Phân Tích Nhóm Mua Sắm HubSpot Với Surfe + Google Sheets (N8N)"
description: "Giải pháp tự động hóa 100% không code để khám phá, phân tích và cập nhật thông tin chi tiết về nhóm mua sắm (buying groups) từ HubSpot, kết hợp với API Surfe và Google Sheets. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công, đồng thời nâng cao độ chính xác và cá nhân hóa lead."
slug: "tu-dong-hoa-kham-pha-phan-tich-nhom-mua-sam-hubspot-surfe-google-sheets"
tags: [n8n, automation, lead-generation, hubspot, google-sheets, surfe-api, no-code]
keywords: [n8n workflow hubspot, tự động hóa lead generation, phân tích nhóm mua sắm, API Surfe, tự động hóa bán hàng, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Khám Phá & Phân Tích Nhóm Mua Sắm HubSpot Với Surfe + Google Sheets**

### **💡 Giải pháp nào giúp các sếp:**
- **Khám phá** thông tin chi tiết về nhóm mua sắm (buying groups) từ HubSpot một cách tự động?
- **Phân tích** và **cập nhật** dữ liệu liên lạc (email, số điện thoại) của các cá nhân trong nhóm mua sắm?
- **Tích hợp** với Google Sheets để lưu trữ và quản lý dữ liệu một cách hệ thống?
- **Tiết kiệm** đến **80% thời gian** so với cách làm thủ công?

Nếu câu trả lời là **Có**, thì workflow này là **công cụ vàng** cho các sếp bán hàng, marketing hoặc sales development representative (SDR) muốn **tăng cường hiệu quả lead generation** mà không cần viết một dòng code nào!

---

## :::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Dưới đây là một số gợi ý về dịch vụ VPS uy tín với **giá cả hợp lý** và **tốc độ ổn định**:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho workflow phức tạp)

---
## 🎯 **Kết quả các sếp nhận được**

### ✅ **Tiết kiệm thời gian lên đến 80%**
- Không cần **tìm kiếm thủ công** thông tin trên LinkedIn, website công ty hay các nguồn khác.
- **Tự động khám phá** và **cập nhật** dữ liệu liên lạc (email, số điện thoại) của các thành viên trong nhóm mua sắm.

### ✅ **Dữ liệu chính xác và đáng tin cậy**
- Sử dụng **API Surfe**, một trong những công cụ **phân tích lead** hàng đầu, với **tỷ lệ chính xác cao** (95%+).
- **Kết hợp với HubSpot**, đảm bảo dữ liệu đồng bộ và cập nhật liên tục.

### ✅ **Cá nhân hóa và tối ưu hóa quy trình bán hàng**
- **Lưu trữ dữ liệu** vào **Google Sheets**, giúp các sếp **theo dõi và phân tích** hiệu quả hơn.
- **Gửi thông báo tự động** qua Gmail khi có dữ liệu mới, giúp **không bỏ lỡ bất kỳ lead nào**.

### ✅ **Hoạt động liên tục 24/7**
- Workflow **không cần can thiệp thủ công**, hoạt động **tự động** khi có sự kiện mới (ví dụ: deal mới trên HubSpot).

---

## 🔧 **Yêu cầu cần thiết**

Trước khi **import và chạy workflow**, các sếp cần chuẩn bị các **thông tin và credential** sau:

### **1. Tài khoản và API Key**
| **Dịch vụ**       | **Credential cần thiết**                          | **Lưu ý**                                                                 |
|-------------------|---------------------------------------------------|---------------------------------------------------------------------------|
| **HubSpot**       | - API Key (Developer API)                         | [Cài đặt API Key HubSpot](https://developers.hubspot.com/docs/api/private-apps) |
|                   | - App Token (để tạo/update lead)                | [Tạo App Token](https://developers.hubspot.com/docs/api/private-apps)      |
| **Surfe**         | - API Key (Bearer Token)                          | [Đăng ký API Key Surfe](https://www.surfe.com/)                          |
| **Google Sheets** | - OAuth 2.0 API Credential (Service Account)      | [Cài đặt OAuth 2.0](https://developers.google.com/sheets/api/quickstart/python) |
| **Gmail**         | - OAuth 2.0 API Credential (để gửi email tự động)| [Cài đặt OAuth 2.0 Gmail](https://developers.google.com/gmail/api/quickstart/python) |

### **2. Google Sheets**
- **Tạo một bảng Google Sheets** mới để lưu trữ kết quả.
- **Cấu trúc bảng** nên bao gồm các cột như:
  - `Company Name`
  - `Company Domain`
  - `Lead Name`
  - `Email`
  - `Phone`
  - `LinkedIn Profile`
  - `Job Title`

### **3. HubSpot**
- **Chọn một deal** trên HubSpot để workflow bắt đầu khám phá nhóm mua sắm.
- **Đảm bảo deal có thông tin công ty (company) liên quan**.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. **Tải workflow** từ [đây](https://n8n.io/workflows/7258) (nếu có liên kết trực tiếp) hoặc **copy toàn bộ JSON** từ trang workflow.
2. **Mở n8n Editor** trên máy chủ của bạn.
3. **Nhấn "Import"** và **dán JSON** vào.
4. **Chọn "Import"** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [trang workflow](https://n8n.io/workflows/7258).
2. **Mở n8n Editor** → **Nhấn "Import"** → **Dán JSON** → **Chọn "Import"**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node "When clicking ‘Execute workflow’" (Manual Trigger)**
- **Không cần thay đổi gì** nếu các sếp muốn **chạy workflow thủ công**.
- **Nếu muốn tự động hóa**, các sếp cần **thay thế bằng một trigger khác** như:
  - **HubSpot Trigger** (khi có deal mới).
  - **Webhook** (khi nhận được request từ bên ngoài).

#### **🔹 Node "HubSpot Trigger" (hubspotTrigger)**
- **Chọn credential**: `hubspotDeveloperApi`.
- **Cấu hình**:
  - **Object**: `deal` (hoặc `company`, tùy thuộc vào yêu cầu).
  - **Filter**: `is_deal: true` (để chỉ lấy deal mới).

#### **🔹 Node "Search People in Companies" (httpRequest)**
- **Credentials**: `httpBearerAuth` (API Key Surfe).
- **Payload**: Sẽ được tự động chuẩn bị bởi node **"prepare JSON PAYLOAD for Person Search"** (code node).
- **Lưu ý**:
  - **Đảm bảo API Key Surfe** có quyền truy cập đầy đủ.
  - **Domain của công ty** sẽ được lấy từ **deal trên HubSpot**.

#### **🔹 Node "Surfe Bulk Enrichments API" (httpRequest)**
- **Credentials**: `httpBearerAuth` (API Key Surfe).
- **Payload**: Sẽ được chuẩn bị bởi node **"Prepare JSON Payload Enrichment Request"** (code node).
- **Lưu ý**:
  - **Kiểm tra API Key** có hiệu lực không.
  - **Thời gian chờ** (3 giây) giữa các request để tránh bị block.

#### **🔹 Node "HubSpot: Create or Update" (hubspot)**
- **Credentials**: `hubspotAppToken`.
- **Cấu hình**:
  - **Object**: `contact` (để tạo/update lead).
  - **Fields**: Đảm bảo các trường như `email`, `phone`, `jobtitle` được truyền từ Surfe.

#### **🔹 Node "Gmail" (gmail)**
- **Credentials**: `gmailOAuth2`.
- **Cấu hình**:
  - **Chọn template email** (nếu có) hoặc **chọn "Send email"** với nội dung tự động tạo bởi node **"prepare email content"** (code node).
  - **Lưu ý**: **Kiểm tra spam** nếu email không được gửi thành công.

#### **🔹 Node "Google Sheets READ CRITERIAS" (googleSheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Cấu hình**:
  - **Chọn sheet** và **tab** cần đọc.
  - **Range**: `A1:Z1000` (hoặc tùy chỉnh theo yêu cầu).

#### **🔹 Node "Filter: phone AND email" (filter)**
- **Lưu ý**: **Chỉ giữ lại dữ liệu** có cả **email và số điện thoại** để tránh lead không đầy đủ.

---

### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - **Chọn một deal** trên HubSpot.
   - **Chạy workflow** và **kiểm tra kết quả** trên Google Sheets và Gmail.
2. **Bật Active workflow**:
   - **Nhấn "Active"** để workflow bắt đầu hoạt động tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tích hợp với Slack/Telegram để thông báo tức thời**
- **Thêm node Slack/Telegram** sau khi **cập nhật lead thành công** để **thông báo ngay** cho team.
- **Cách làm**:
  - **Thêm node `slack`** (n8n-nodes-base.slack).
  - **Cấu hình webhook Slack** và **gửi thông báo** khi có lead mới.

### **2. Lưu log hoạt động vào Google Sheets**
- **Thêm node `code`** sau khi **cập nhật lead** để **ghi log** vào Google Sheets.
- **Cấu trúc log**:
  - `Date`
  - `Company Name`
  - `Lead Name`
  - `Status` (Success/Failure)
  - `Error (nếu có)`

### **3. Gửi báo cáo định kỳ (hàng tuần/ngày)**
- **Sử dụng node `setInterval`** (n8n-nodes-base.setInterval) để **chạy workflow định kỳ**.
- **Cấu hình**:
  - **Thời gian chạy**: Ví dụ, **mỗi thứ 2 hàng tuần**.
  - **Gửi email báo cáo** tổng hợp từ Google Sheets.

### **4. Kết hợp với Zapier/Integromat (Make) để mở rộng**
- **Nếu cần thêm tính năng**, các sếp có thể **kết nối với Zapier** để:
  - **Gửi lead** vào **CRM khác** (Salesforce, Pipedrive).
  - **Tích hợp với CRM** để **theo dõi tương tác** của lead.

---

## 📌 **Kết luận**

### **🚀 Workflow này giúp các sếp:**
✅ **Tự động hóa** quá trình khám phá và phân tích nhóm mua sắm.
✅ **Tiết kiệm thời gian** lên đến **80%** so với cách làm thủ công.
✅ **Nâng cao độ chính xác** với dữ liệu từ **API Surfe**.
✅ **Cập nhật liên tục** thông tin lead trên **HubSpot và Google Sheets**.

### **💡 Lời khuyên cuối cùng**
- **Test workflow** với **dữ liệu mẫu** trước khi áp dụng cho **dữ liệu thực tế**.
- **Monitor log** để **khắc phục lỗi** nếu có.
- **Cập nhật API Key** khi hết hạn.

**👉 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa bán hàng của mình!** 🚀

---
**📌 Cần hỗ trợ thêm?**
- **Trang chủ Surfe**: [https://www.surfe.com](https://www.surfe.com)
- **GitHub API Examples**: [https://github.com/surfe/api-examples](https://github.com/surfe/api-examples)
- **Hỗ trợ n8n**: [https://n8n.io/community](https://n8n.io/community)