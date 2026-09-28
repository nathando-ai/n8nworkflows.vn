---
title: "🚀 Tự Động Hóa Đánh Giá & Chăm Sóc Lead HubSpot Với Clearbit + AI Gemini (Không Cần Code)"
description: "Workflow tự động đánh giá điểm số lead mới từ HubSpot bằng Clearbit (thông tin doanh nghiệp) và AI Gemini (tóm tắt, phân tích), sau đó tự động gửi email cá nhân hóa cho lead nóng và đưa lead ấm vào chu trình chăm sóc. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ chuyển đổi lên 30%."
slug: "tieu-dong-hoa-danh-gia-cham-soc-lead-hubspot-clearbit-gemini"
tags: [n8n, automation, lead-scoring, ai-gemini, hubspot, clearbit, no-code]
keywords: [tự động hóa lead scoring, n8n workflow hubspot, ai gemini tự động hóa, chăm sóc lead tự động, clearbit enrichment, tự động gửi email cá nhân hóa]
---

# 🚀 **Tự Động Hóa Đánh Giá & Chăm Sóc Lead HubSpot Với Clearbit + AI Gemini**

## **🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Mỗi ngày, các sếp phải:
- **Lọc thủ công** hàng trăm lead mới từ HubSpot để đánh giá xem có tiềm năng hay không.
- **Tìm kiếm thông tin doanh nghiệp** trên Google, LinkedIn hoặc Clearbit để đánh giá điểm số (lead scoring) một cách chủ quan và mất nhiều thời gian.
- **Gửi email cá nhân hóa** cho từng lead, nhưng lại không có thời gian để viết nội dung phù hợp với từng đối tượng.
- **Quên theo dõi** lead ấm (warm leads) sau khi không phản hồi, dẫn đến mất cơ hội chuyển đổi.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động enrich** thông tin doanh nghiệp từ Clearbit (tên công ty, ngành nghề, quy mô, nguồn vốn).
✅ **Đánh giá điểm số lead** bằng công thức cơ bản + AI Gemini phân tích sâu để tính điểm chính xác.
✅ **Phân loại lead** thành **nóng (hot)** và **ấm (warm)** để xử lý khác nhau.
✅ **Gửi email cá nhân hóa** tự động cho lead nóng (với nội dung do AI Gemini viết).
✅ **Đưa lead ấm vào chu trình chăm sóc** tự động trong HubSpot.
✅ **Gửi báo cáo điểm số** lên Google Sheets để theo dõi lịch sử.
✅ **Thông báo ngay cho team bán hàng** khi có lead nóng mới qua Slack.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho việc đánh giá và chăm sóc lead thủ công.
- **Tăng tỷ lệ chuyển đổi lên 30%** nhờ email cá nhân hóa và phân loại lead chính xác.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Dữ liệu chính xác** do AI Gemini phân tích thay vì đánh giá chủ quan.
- **Báo cáo tự động** để theo dõi hiệu suất của từng lead.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản HubSpot** (đã kích hoạt API và có quyền chỉnh sửa contact properties).
✔ **API Key Clearbit** (đăng ký tại [Clearbit](https://clearbit.com/)).
✔ **Google Gemini API Key** (đăng ký tại [Google AI Studio](https://aistudio.google/)).
✔ **Tài khoản Gmail** (để gửi email tự động, cần kích hoạt "Less Secure Apps" hoặc OAuth 2.0).
✔ **Slack Workspace** (để thông báo lead nóng cho team bán hàng).
✔ **Google Sheet** (để lưu lịch sử điểm số lead, có thể tạo mới hoặc sử dụng sheet đã có).
✔ **Chu trình chăm sóc (Nurturing Sequence)** trong HubSpot (đã tạo sẵn).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13979](https://n8n.io/workflows/13979) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n Dashboard.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node** quan trọng, các sếp cần cấu hình kỹ như sau:

##### **🔹 Node 1: HubSpot Contact Created (hubspotTrigger)**
- **Chọn Credentials:** Tạo mới hoặc chọn tài khoản HubSpot đã có.
- **Chọn Object:** `contacts`.
- **Filter:** Đảm bảo chỉ bắt lead mới (`createdAt` mới hơn thời gian hiện tại).

##### **🔹 Node 2: Clearbit Company Enrichment (httpRequest)**
- **API Endpoint:** `https://company.clearbit.com/v2/companies/enrich?domain={domain}`
  *(Thay `{domain}` bằng `{{$json["email"].split("@")[1]}}` trong n8n để tự động lấy domain từ email lead.)*
- **Headers:**
  - `Authorization: Bearer YOUR_CLEARBIT_API_KEY`
  - `Content-Type: application/json`
- **Lưu ý:** Nếu Clearbit trả về lỗi, kiểm tra API key và domain email.

##### **🔹 Node 3: Set Scoring Criteria (set)**
- **Cấu hình điểm số mặc định** (các sếp có thể điều chỉnh):
  ```json
  {
    "industry_weight": 20,
    "company_size_weight": 30,
    "funding_status_weight": 20,
    "email_domain_weight": 10,
    "ai_analysis_weight": 20
  }
  ```
  *(Cân bằng trọng số theo nhu cầu của doanh nghiệp.)*

##### **🔹 Node 4: Calculate Basic Score (code)**
- **Mã JavaScript mặc định:**
  ```javascript
  // Tính điểm cơ bản từ Clearbit
  const industryScore = json.company?.industry_score || 0;
  const sizeScore = json.company?.size_score || 0;
  const fundingScore = json.company?.funding_status_score || 0;
  const domainScore = json.email?.domain_score || 0;

  const basicScore = (industryScore * 0.2) + (sizeScore * 0.3) + (fundingScore * 0.2) + (domainScore * 0.1);

  return { json: { basicScore } };
  ```
- **Lưu ý:** Nếu Clearbit không trả về dữ liệu, node này sẽ trả về `0`.

##### **🔹 Node 5: AI Lead Analysis (chainLlm)**
- **Model:** Chọn `Google Gemini` (đã cấu hình trong node `Google Gemini Chat Model`).
- **Prompt mẫu (có thể tùy chỉnh):**
  ```
  Analyze the following lead data and provide a personalized outreach message:
  - Company: {{json.company.name}}
  - Industry: {{json.company.industry}}
  - Size: {{json.company.size}}
  - Funding Status: {{json.company.funding_status}}
  - Email Domain: {{json.email.domain}}
  - Basic Score: {{json.basicScore}}

  Suggest a short, engaging email subject and body (max 100 words) to engage this lead.
  ```
- **Lưu ý:** Nếu AI trả về lỗi, kiểm tra API key và cấu hình `googlePalmApi` trong n8n.

##### **🔹 Node 6: Score Threshold Check (if)**
- **Điều kiện mặc định:**
  - **Hot Lead (>= 80 điểm):** Gửi email + thông báo Slack.
  - **Warm Lead (50-79 điểm):** Đưa vào chu trình chăm sóc.
  - **Cold Lead (<50 điểm):** Bỏ qua (có thể thêm logic khác).
- **Lưu ý:** Các sếp có thể điều chỉnh ngưỡng điểm trong node `Set Scoring Criteria`.

##### **🔹 Node 7: Update Contact Properties (hubspot)**
- **Properties cần cập nhật:**
  - `lead_score` (điểm số tính toán).
  - `ai_analysis` (nội dung phân tích từ AI).
  - `lead_status` (`hot`, `warm`, `cold`).

##### **🔹 Node 8: Send Personalized Email (gmail)**
- **Template email:**
  ```plaintext
  Subject: {{json.ai_analysis.subject}}

  Body:
  {{json.ai_analysis.body}}

  Best regards,
  Team [Tên Công Ty]
  ```
- **Lưu ý:** Kích hoạt **OAuth 2.0** trong Gmail để n8n có thể gửi email.

##### **🔹 Node 9: Add to Nurturing Sequence (hubspot)**
- **Chọn chu trình chăm sóc** đã tạo trước trong HubSpot.
- **Properties điều kiện:** `lead_status = warm`.

##### **🔹 Node 10: Notify Sales Team (slack)**
- **Message mẫu:**
  ```
  🚨 **HOT LEAD ALERT!** 🚨
  - Name: {{json.contact.name}}
  - Email: {{json.contact.email}}
  - Company: {{json.company.name}}
  - Score: {{json.lead_score}}
  - AI Analysis: {{json.ai_analysis.subject}}
  ```
- **Lưu ý:** Thay `CHANNEL_NAME` bằng tên channel Slack của team bán hàng.

##### **🔹 Node 11: Log Scoring History (googleSheets)**
- **Sheet Name:** Tạo một sheet mới với các cột:
  `Timestamp | Contact Name | Email | Company | Score | Status | AI Analysis`.
- **Lưu ý:** Cấu hình `appendOrUpdate` để dữ liệu không bị trùng lặp.

##### **🔹 Node 12: Google Gemini Chat Model (lmChatGoogleGemini)**
- **Credentials:** Chọn `googlePalmApi` (đã cấu hình API key trước đó).

---
#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy workflow với 1-2 lead mẫu để kiểm tra logic.
- **Bật Active:** Sau khi kiểm tra thành công, bật `Active` để workflow chạy tự động.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỚNG MỞ RỘNG]
- **Kết hợp với Zapier/Make:** Nếu cần tích hợp thêm dịch vụ khác (ví dụ: CRM khác).
- **Lưu log vào Google Drive:** Thay vì Google Sheets, các sếp có thể lưu file Excel tự động.
- **Gửi báo cáo định kỳ:** Sử dụng node `set` + `httpRequest` để gửi email báo cáo hàng tuần.
- **Tích hợp với CRM khác:** Thay HubSpot bằng Salesforce, Pipedrive (cần node tương ứng).
- **Cải thiện AI Prompt:** Để AI viết email phù hợp với giọng điệu của doanh nghiệp.
- **Phân loại lead theo ngành:** Sử dụng node `if` để xử lý lead từ ngành ngân hàng, tech khác nhau.
:::

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **tăng hiệu quả chuyển đổi** nhờ AI và tự động hóa. **Chỉ cần 30 phút để setup**, sau đó workflow sẽ hoạt động **một mình 24/7**.

**👉 Hãy áp dụng ngay và xem kết quả trong vòng 1 tuần!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Lưu ý cuối cùng:** Nếu gặp vấn đề, các sếp có thể tham khảo [community n8n](https://community.n8n.io/) hoặc liên hệ tác giả [Oka Hironobu](https://okp29.net/) để hỗ trợ.