---
title: "🚀 Tự Động Hóa Scrape LinkedIn & Gửi Email B2B Tự Động Với AI GPT-4 - Không Cần Code"
description: "Workflow tự động hóa scrape LinkedIn để tìm kiếm leads B2B, tạo email cá nhân hóa bằng GPT-4, đồng bộ dữ liệu vào HubSpot và Gmail, với hệ thống phê duyệt thông qua Google Sheets. Giúp các sếp tiết kiệm 80% thời gian trong outreach và nâng cao tỷ lệ chuyển đổi."
slug: "tieu-dong-hoa-scrape-linkedin-gpt-4-email-b2b"
tags: [n8n, automation, lead-generation, ai-gpt-4, hubspot, gmail, google-sheets, no-code]
keywords: [tự động hóa scrape LinkedIn, workflow n8n leads B2B, AI GPT-4 tạo email cá nhân hóa, tự động hóa outreach, tự động hóa CRM HubSpot]
---

# 🚀 **Scrape LinkedIn & Gửi Email B2B Tự Động Với AI GPT-4 - Không Cần Code**

### **Giải pháp cho các sếp muốn:**
- **Tìm kiếm và lọc leads B2B chất lượng** từ LinkedIn mà không cần scrape thủ công.
- **Tạo email cá nhân hóa** cho từng lead bằng AI GPT-4, không cần viết một dòng nào.
- **Phê duyệt và quản lý leads** một cách dễ dàng qua Google Sheets.
- **Tích hợp CRM HubSpot** để đồng bộ dữ liệu và theo dõi pipeline sales.
- **Gửi email tự động** khi được phê duyệt, tiết kiệm thời gian và nâng cao tỷ lệ mở email.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính ổn định và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc tìm kiếm và gửi email outreach.
- **Tỷ lệ chuyển đổi cao hơn** nhờ email cá nhân hóa được AI tạo ra.
- **Dữ liệu leads được đồng bộ tự động** vào HubSpot, giúp quản lý pipeline hiệu quả.
- **Hệ thống phê duyệt thông minh** qua Google Sheets, giảm rủi ro spam và tối ưu hóa nguồn lực.
- **Hoạt động liên tục 24/7** nhờ tự động hóa, không phụ thuộc vào thời gian làm việc của nhân viên.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API keys:**
   - **Apify API Token** (để scrape LinkedIn).
   - **HubSpot App Token** (để đồng bộ dữ liệu vào CRM).
   - **Google Sheets OAuth2** (để lưu logs và phê duyệt leads).
   - **Gmail OAuth2** (để gửi email tự động).
   - **OpenAI API Key** (để sử dụng GPT-4 tạo email cá nhân hóa).
2. **Google Sheet** riêng để lưu trữ logs và phê duyệt leads (cần chia sẻ quyền cho n8n).
3. **Tài khoản LinkedIn** (để scrape dữ liệu, nhưng không cần login trong workflow).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13007](https://n8n.io/workflows/13007) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **3 phần chính**:
- **Scrape LinkedIn & xử lý leads** (Apify + AI).
- **Phê duyệt leads qua Google Sheets**.
- **Gửi email tự động** (Gmail) hoặc **rewrite email** (nếu bị từ chối).

#### **A. Cấu hình Credentials (BẮT BUỘC)**
| Node | Tham số cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Apify** (`post Apify data scrap`, `Get Apify recent run data`) | `httpHeaderAuth` | Điền **Apify API Token** (tạo tại [Apify](https://apify.com)). |
| **HubSpot** (`HubSpot Company Creator`, `HubSpot Contact Sync`) | `hubspotAppToken` | Điền **HubSpot App Token** (tạo tại [HubSpot Developer](https://developers.hubspot.com/docs/api/private-apps)). |
| **Google Sheets** (`Leads Log`, `Update: Improved Email`) | `googleSheetsOAuth2Api` | Chọn **Google Sheet** chứa logs và chia sẻ quyền cho n8n. |
| **Gmail** (`📤 Send Approved Email`) | `gmailOAuth2` | Đăng nhập và cấp quyền cho n8n. |
| **OpenAI** (`LLM`, `OpenAI Chat Model`) | `openAiApi` | Điền **OpenAI API Key** (tạo tại [OpenAI](https://platform.openai.com/account/api-keys)). |

#### **B. Cấu hình Google Sheet (BẮT BUỘC)**
- **Cột cần có trong Sheet:**
  - `Email` (địa chỉ email của lead).
  - `Status` (Pending/Approved/Rejected).
  - `Company Name`, `Job Title`, `LinkedIn URL` (dữ liệu scrape từ LinkedIn).
  - `Email Draft` (nội dung email AI tạo).
  - `Notes` (ghi chú từ người phê duyệt).
- **Chia sẻ quyền** cho n8n với vai trò **Editor**.

#### **C. Cấu hình AI Prompt (Tùy chọn nâng cao)**
- Trong node **`generate Ai email`** và **`Rejection Email Rewriter`**, các sếp có thể **cập nhật prompt** để AI tạo email phù hợp với **tôn chỉ thương hiệu** của công ty.
  - Ví dụ:
    ```json
    "prompt": "Tạo email cá nhân hóa cho lead {name} tại {company}, với nội dung nhấn mạnh giá trị {value_proposition}. Không sử dụng từ 'sales' hoặc 'offer'."
    ```

#### **D. Cấu hình Webhook (Phê duyệt leads)**
- Khi các sếp **chỉnh sửa status** trong Google Sheets:
  - **Approve** → Email sẽ được gửi tự động.
  - **Reject** → Email sẽ được **rewrite** và cập nhật lại trong Sheet.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền **keyword** (như "Chief Marketing Officer", "Sài Gòn") vào **Lead Campaign Setup** (Form Trigger).
   - Kiểm tra **Leads Log** trong Google Sheets để xác nhận dữ liệu scrape và email AI tạo.
2. **Bật Active** workflow sau khi kiểm tra thành công.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu hóa scrape LinkedIn**
- **Lọc keyword hiệu quả:** Sử dụng từ khóa **niche** (ví dụ: "Founder Startup Saigon" thay vì "Marketing").
- **Bật "Rate Limiting"** trong Apify để tránh bị chặn IP.

### **2. Nâng cao chất lượng email**
- **Cập nhật prompt AI** để email phù hợp với **ngành nghề** của lead.
- **Thêm biến thể email** (ví dụ: email cho CEO khác với email cho Marketing Manager).

### **3. Tích hợp Slack/Telegram để báo cáo**
- Sử dụng **Webhook Slack/Telegram** để nhận thông báo khi:
  - Có **lead mới** được scrape.
  - Email đã được **gửi thành công**.
  - Email bị **từ chối** và cần rewrite.

### **4. Lưu log và báo cáo định kỳ**
- Sử dụng **Google Sheets** để thống kê:
  - Số lượng leads scrape.
  - Tỷ lệ approve/reject.
  - Tỷ lệ mở email (nếu tích hợp Google Analytics).

### **5. Xử lý leads bị từ chối**
- Trong node **`Rejection Email Rewriter`**, AI sẽ **rewrite email** với nội dung mềm mại hơn, ví dụ:
  - **Email gốc (từ chối):** *"Chào {name}, tôi thấy công việc của bạn rất ấn tượng..."*
  - **Email rewrite:** *"Chào {name}, tôi đã nghiên cứu về {company} và thấy công việc của bạn trong lĩnh vực {role} rất thú vị..."*

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** và **quản lý khách hàng** thay vì làm việc thủ công. Với sự kết hợp giữa **scrape LinkedIn, AI GPT-4, HubSpot và Gmail**, các sếp có thể:
✅ **Tìm kiếm leads chất lượng** mà không cần scrape thủ công.
✅ **Tạo email cá nhân hóa** trong giây lát.
✅ **Quản lý pipeline sales** một cách hiệu quả.
✅ **Tăng tỷ lệ chuyển đổi** nhờ nội dung email được tối ưu hóa.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình credentials.
2. **Test với keyword** và kiểm tra kết quả trong Google Sheets.
3. **Bật Active** và bắt đầu tự động hóa outreach của mình!

👉 [Tải workflow này ngay](https://n8n.io/workflows/13007) và bắt đầu **tự động hóa B2B outreach** của bạn! 🚀