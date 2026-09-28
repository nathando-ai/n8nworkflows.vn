---
title: "🤖 Tự Động Xác Minh & Phân Loại Lead Tiềm Năng với GPT-4o, Clearbit & HubSpot (Không Cần Code)"
description: "Workflow tự động hóa 100% AI phân tích lead từ form, enrich dữ liệu công ty bằng Clearbit, đánh giá chất lượng, và tự động phân loại vào HubSpot hoặc yêu cầu review thủ công qua Slack. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lead thành khách hàng."
slug: "tieu-dong-xac-minh-phan-loai-lead-gpt-4o-clearbit-hubspot"
tags: [n8n, automation, no-code, ai-lead-qualification, hubspot, clearbit, slack, gpt-4o]
keywords: [tự động hóa lead qualification, workflow n8n ai, phân loại lead với gpt-4, clearbit enrich data, hubspot automation, slack alert lead]
---

# 🚀 **Tự Động Xác Minh & Phân Loại Lead Tiềm Năng với AI (GPT-4o + Clearbit + HubSpot)**

## **Nỗi Đau Của Các Sếp: "Lead Nhập Nhập Nhưng Không Biết Chọn Đâu?"**
Hàng ngày, các sếp phải:
- **Làm thủ công** phân tích hàng chục lead từ form website, email, hoặc CRM.
- **Mất thời gian** tra cứu thông tin công ty (Clearbit), đánh giá chất lượng lead, và quyết định phân loại.
- **Rủi ro bỏ lỡ** lead chất lượng cao vì quá tải công việc.
- **Không có hệ thống** để tự động cảnh báo team Sales khi lead ưu tiên cao đến.

**Workflow này giải quyết tất cả!** Dùng AI (GPT-4o) phân tích lead, enrich dữ liệu công ty bằng Clearbit, tự động phân loại vào HubSpot (nếu chất lượng cao) hoặc gửi yêu cầu review thủ công qua Slack (nếu cần). **Không cần viết một dòng code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy 24/7 ổn định, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** phân tích lead thủ công.
✅ **Tự động enrich dữ liệu công ty** (Clearbit) để đánh giá chính xác.
✅ **Phân loại lead tự động**:
   - **Score ≥70?** → Thêm vào HubSpot + cảnh báo Sales qua Slack.
   - **Score <70?** → Gửi yêu cầu review thủ công + lưu log vào Airtable.
✅ **AI đánh giá chất lượng lead** (buying intent, urgency, budget, pain points).
✅ **Hoạt động liên tục 24/7** (không phụ thuộc vào nhân viên).
✅ **Tăng tỷ lệ chuyển đổi lead** từ 20-50% (theo Greypillar).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| Dịch vụ               | Thông Tin Cần Thiết                          | Làm thế nào để lấy?                                                                 |
|-----------------------|-----------------------------------------------|--------------------------------------------------------------------------------------|
| **OpenAI (GPT-4o)**   | API Key                                      | [Tạo tài khoản OpenAI](https://platform.openai.com/) → API Keys → Copy API Key.       |
| **Clearbit**          | API Key (HTTP Header Auth)                    | [Đăng ký Clearbit](https://clearbit.com/) → Dashboard → API → Copy API Key.          |
| **HubSpot**           | OAuth2 Credential                             | [Cài đặt OAuth HubSpot](https://developers.hubspot.com/docs/api/private-apps) → Copy. |
| **Slack**             | OAuth2 Credential                             | [Cài đặt Slack App](https://api.slack.com/apps) → Enable OAuth & Copy Credentials.     |
| **Airtable**          | Base ID & Table ID                           | [Tạo Base mới](https://airtable.com/) → Copy `appXXXXXXXXXXXXXX` (Base ID) và `tblYYYYYYYYYYYY` (Table ID). |

#### **2. Cấu Trúc Airtable**
Các sếp cần tạo **bảng "Lead Log"** với các cột sau:
| Tên Cột                  | Loại Dữ liệu | Mô Tả                                                                 |
|--------------------------|--------------|-------------------------------------------------------------------------|
| Name                     | Text         | Tên lead.                                                              |
| Email                    | Text         | Email của lead.                                                        |
| Company                  | Text         | Tên công ty (enrich từ Clearbit).                                       |
| Phone                    | Text         | Số điện thoại (nếu có).                                                |
| Website                  | Text         | Website công ty.                                                       |
| Qualification_Score      | Number       | Điểm từ AI (0-100).                                                    |
| Buying_Intent            | Dropdown     | `high`, `medium`, `low`.                                                |
| Urgency                  | Dropdown     | `immediate`, `this_week`, `this_month`, `exploratory`.                 |
| Budget                   | Dropdown     | `enterprise`, `mid-market`, `small_business`, `unknown`.               |
| AI_Summary               | Multi-line   | Tóm tắt từ AI về lead.                                                 |
| Pain_Points              | Multi-line   | Vấn đề của lead (do AI phân tích).                                    |
| Recommended_Action       | Dropdown     | `immediate_call`, `schedule_demo`, `nurture_sequence`, `disqualify`.   |
| Status                   | Text         | `active`, `review`, `qualified`, `disqualified`.                        |
| Submitted_Date           | Date         | Ngày lead được submit.                                                 |

#### **3. Custom Properties HubSpot**
Các sếp cần tạo **8 thuộc tính mới** trong HubSpot:
| Tên thuộc tính          | Loại Dữ liệu       | Giá trị mặc định          |
|-------------------------|--------------------|----------------------------|
| qualification_score     | Number             | 0                          |
| buying_intent           | Dropdown          | `low`                      |
| urgency_level           | Dropdown          | `exploratory`              |
| budget_indicator        | Dropdown          | `unknown`                  |
| ai_summary              | Multi-line text    | -                          |
| pain_points             | Multi-line text    | -                          |
| recommended_action       | Dropdown          | `nurture_sequence`         |

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tạo workflow mới trong n8n Editor.
**Bước 2:** Import từ file JSON:
- Tải file chính: [Qualify & Route Leads](https://n8n.io/workflows/9162) (nút "Download").
- Tải file sub-workflow: [Clearbit Enrichment Tool](https://n8n.io/workflows/9162#tab=subworkflows) (nút "Download").
**Bước 3:** Cài đặt sub-workflow trước:
1. Tạo workflow mới cho **Clearbit Enrichment Tool**.
2. Import file JSON của sub-workflow.
3. **Bật (Active)** sub-workflow và **copy Workflow ID** từ URL (ví dụ: `https://your-n8n.io/workflow/12345` → ID là `12345`).
4. Dán ID này vào node **"Clearbit Enrichment Tool"** trong workflow chính.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Cấu Hình Slack**
- **Channel Sales**: Right-click channel → **View details** → Copy **Channel ID**.
- **Channel Review**: Lặp lại bước trên cho channel review.
- Trong workflow, thay thế:
  - `REPLACE_WITH_SLACK_SALES_CHANNEL_ID` → Channel ID Sales.
  - `REPLACE_WITH_SLACK_REVIEW_CHANNEL_ID` → Channel ID Review.

##### **B. Cấu Hình Airtable**
- **Base ID**: Copy từ URL Airtable (ví dụ: `https://airtable.com/appXXXXXXXXXXXXXX/tblYYYYYYYYYYYY` → `appXXXXXXXXXXXXXX`).
- **Table ID**: Copy từ URL (phần `tblYYYYYYYYYYYY`).
- Trong node **"Log to Airtable"**, điền:
  - **Base ID**: `appXXXXXXXXXXXXXX`.
  - **Table ID**: `tblYYYYYYYYYYYY`.

##### **C. Cấu Hình HubSpot**
- Trong node **"Add to HubSpot CRM"**, chọn:
  - **Contact Object**: `Contacts`.
  - **Properties**: Chọn các custom properties đã tạo (ví dụ: `qualification_score`, `buying_intent`, ...).
- **Lưu ý**: Nếu lead không có email, workflow sẽ tự động tạo một email giả (ví dụ: `lead+[random]@company.com`) để HubSpot nhận diện.

##### **D. Cấu Hình OpenAI (GPT-4o)**
- Trong node **"OpenAI Chat Model"**, đảm bảo:
  - **Model**: `gpt-4o`.
  - **API Key**: Đã điền trong **Credentials** (OpenAI API).

##### **E. Cấu Hình Webhook**
- Node **"Form Submission"** sử dụng **Webhook** với:
  - **Path**: `lead-intake`.
  - **HTTP Method**: `POST`.
- **Lưu ý**: Các sếp cần **cấu hình form website** gửi dữ liệu POST đến URL webhook này. Ví dụ:
  ```plaintext
  https://your-n8n.io/webhook/lead-intake
  ```
  (URL chính xác sẽ hiển thị khi workflow được bật).

---

#### **3. Kích Hoạt ⚡️**
**Bước 1:** Test run với dữ liệu mẫu:
1. Gửi một lead mẫu qua form (hoặc gọi trực tiếp webhook với JSON mẫu):
   ```json
   {
     "name": "John Doe",
     "email": "john@example.com",
     "phone": "+1234567890",
     "company": "TechCorp",
     "message": "Chúng tôi quan tâm đến dịch vụ của bạn."
   }
   ```
2. Kiểm tra:
   - AI có phân tích lead không?
   - Dữ liệu công ty (Clearbit) có enrich không?
   - Lead có được phân loại đúng không?

**Bước 2:** Bật **Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Kết Nối với CRM Khác**
- Thay thế node HubSpot bằng **Salesforce** hoặc **Pipedrive** bằng cách:
  - Sử dụng node `n8n-nodes-salesforce` hoặc `n8n-nodes-pipedrive`.
  - Cấu hình tương tự như HubSpot.

#### **2. Lưu Log & Báo Cáo Định Kỳ**
- **Node "Log to Airtable"** đã lưu tất cả lead. Các sếp có thể:
  - Tạo **báo cáo hàng tuần** bằng Airtable Automation.
  - Gửi báo cáo qua **Email** hoặc **Slack** bằng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack`.

#### **3. Cải Thiện AI với Prompt Tùy Chỉnh**
- Node **"AI Lead Analysis Agent"** sử dụng GPT-4o với prompt mặc định. Các sếp có thể:
  - **Tùy chỉnh prompt** trong node **"OpenAI Chat Model"** để phù hợp với ngành nghề.
  - Ví dụ: Nếu là dịch vụ SaaS, có thể yêu cầu AI tập trung vào **ROI** và **chuyển đổi**.

#### **4. Xử Lý Lead Trùng Lặp**
- Sử dụng node **"Format Data"** để:
  - Kiểm tra email đã tồn tại trong HubSpot/Airtable.
  - Bỏ qua lead trùng lặp (nếu cần).

#### **5. Cảnh Báo Thông Báo Qua Email**
- Thêm node `n8n-nodes-base.email` sau **"Request Manual Review"** để:
  - Gửi email cảnh báo cho team review khi lead cần kiểm tra.

---

### 📌 **Kết Luận: Áp Dụng Ngay & Tăng Doanh Thu!**
Workflow này **giải phóng thời gian** cho các sếp từ việc phân tích lead thủ công, đồng thời **tăng tỷ lệ chuyển đổi** từ 20-50% (theo Greypillar). **Không cần code, không cần IT**, chỉ cần:
1. **Import workflow** và cấu hình các API key.
2. **Test run** với lead mẫu.
3. **Bật Active** và để AI làm việc 24/7.

**🚀 Hành động ngay!** Tải workflow, cài đặt, và bắt đầu tự động hóa lead của mình. Nếu có vấn đề, hãy để lại comment dưới đây hoặc liên hệ Greypillar qua [đây](https://greypillar.com/).

---
**#TựĐộngHóa #LeadQualification #AIForBusiness #HubSpotAutomation #Clearbit #n8n**