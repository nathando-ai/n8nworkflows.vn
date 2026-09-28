---
title: "🤖 Tự Động Chất Lượng Lead Website Bằng AI (OpenAI) + HubSpot + Email Gmail – Không Cần Code!"
description: "Workflow tự động hóa nhận lead từ website, phân tích chất lượng bằng AI, tạo contact/deal trên HubSpot và gửi thông báo email nội bộ – tiết kiệm 80% thời gian cho bộ phận sales!"
slug: "tieu-dong-chat-luong-lead-website-ai-hubspot-gmail"
tags: [n8n, automation, no-code, lead-generation, ai-summarization, hubspot, openai, gmail]
keywords: [n8n workflow lead generation, tự động hóa chất lượng lead, AI phân tích lead, HubSpot CRM tự động, gửi email thông báo sales, tự động hóa website form]
---

# 🚀 **Tự Động Chất Lượng Lead Website Bằng AI + HubSpot + Email – Không Cần Code!**

### **Giải pháp hoàn hảo cho các sếp bán hàng:**
Tại sao phải mất **giờ đồng hồ** để phân tích từng lead từ website, kiểm tra trên HubSpot, và gửi thông báo cho team? **Workflow này tự động hóa toàn bộ quy trình** – từ nhận lead đến phân tích AI, tạo contact/deal trên HubSpot, và gửi email thông báo nội bộ – **không cần viết một dòng code nào!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** cho bộ phận sales: Không cần phân tích lead thủ công.
- **Chất lượng lead cao hơn**: AI phân tích và đánh giá lead theo tiêu chí của doanh nghiệp.
- **Tự động hóa HubSpot**: Tạo contact/deal một cách chính xác, không sai sót.
- **Thông báo nội bộ tự động**: Email gửi ngay khi lead mới được phân tích.
- **Hoạt động 24/7**: Không cần can thiệp người dùng, workflow chạy liên tục.
- **Cá nhân hóa thông báo**: Email bao gồm phân tích AI và gợi ý hành động.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) để phân tích lead bằng AI.
2. **Tài khoản HubSpot** (Private App Token) để tạo contact/deal.
3. **Tài khoản Gmail** (OAuth 2.0) để gửi email thông báo.
4. **Gmail Label** tên **"Deals"** (hoặc tùy chỉnh theo yêu cầu).
5. **Custom Properties** trên HubSpot:
   - `ai_lead_score` (đánh giá từ AI).
   - `ai_urgency` (mức độ khẩn cấp).
   - `ai_fit` (phù hợp với ICP).
   - `ai_summary` (tóm tắt lead).
   - `ai_followup_draft` (gợi ý nội dung follow-up).
6. **Pipeline và Deal Stage ID** trên HubSpot (ví dụ: Pipeline "Hot Leads", Stage "New Lead").
7. **Webhook URL** từ website form (cần thay đổi sau khi import).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15648](https://n8n.io/workflows/15648) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/15648](https://n8n.io/workflows/15648) (chọn **Export as JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON** → **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **14 node**, các sếp cần chú ý cấu hình **các node sau**:

#### **🔹 Node 1: Webhook (nhận lead từ website)**
- **Path**: `hubspot-lead-qualification` (không thay đổi).
- **HTTP Method**: `POST` (không thay đổi).
- **Lưu ý**:
  - Sau khi import, **copy URL webhook** từ node này và **thay thế vào form website**.
  - Ví dụ: Nếu URL webhook là `https://tên-doman-n8n.com/webhook/hubspot-lead-qualification`, thì trong form website cần gửi dữ liệu POST đến URL này.

#### **🔹 Node 3: OpenAI (phân tích lead bằng AI)**
- **Credentials**: Chọn `openAiApi` (đã cấu hình trước).
- **Prompt**: Workflow sử dụng **prompt mặc định** để phân tích lead. Các sếp có thể **tùy chỉnh** trong node **Code (Lead Data + AI Analysis)**:
  ```javascript
  // Ví dụ prompt mặc định (có thể chỉnh sửa trong node Code):
  "Analyze the lead data and provide the following:
  1. Lead Score (1-100)
  2. Urgency Level (Low/Medium/High)
  3. Fit Level (Low/Medium/High)
  4. Summary (2-3 sentences)
  5. Follow-up Draft (suggested email content)"
  ```
- **Lưu ý**:
  - Đảm bảo **API Key OpenAI** được cấu hình đúng trong **Credentials Manager** của n8n.

#### **🔹 Node 6 & 7: HubSpot HTTP Requests (tìm kiếm/tạo contact)**
- **Credentials**: Chọn `hubspotPrivateAppToken` (đã cấu hình trước).
- **API Endpoint**:
  - **Check for existing contact**: `https://api.hubapi.com/crm/v3/objects/contacts/search`
  - **Create HUBSPOT contact**: `https://api.hubapi.com/crm/v3/objects/contacts`
- **Headers**:
  - `Content-Type: application/json`
  - `Authorization: Bearer {hubspotPrivateAppToken}`
- **Lưu ý**:
  - **Thay đổi `properties`** trong request để phù hợp với **custom properties** của HubSpot (như `ai_lead_score`, `ai_urgency`, etc.).
  - **Thay thế `pipelineId` và `dealStageId`** trong node **Create HUBSPOT deal** bằng ID của pipeline và stage trên HubSpot.

#### **🔹 Node 10 & 11: Gmail (gửi email thông báo)**
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước).
- **Node "Send a message"**:
  - **Subject**: `"New Lead: {leadName} - Score: {aiLeadScore}"` (có thể tùy chỉnh).
  - **Body**: Nội dung email bao gồm **phân tích AI** và **gợi ý hành động**.
- **Node "Add label to message"**:
  - **Label**: `"Deals"` (hoặc tùy chỉnh theo yêu cầu).
- **Lưu ý**:
  - Đảm bảo **Gmail OAuth 2.0** được cấu hình đúng trong **Credentials Manager**.
  - **Test gửi email** trước khi kích hoạt workflow.

#### **🔹 Node 14: Respond to Webhook**
- **Response**: Workflow trả về **status code 200** và **thông báo thành công** cho frontend.
- **Lưu ý**:
  - Các sếp có thể **tùy chỉnh response** để phù hợp với form website (ví dụ: trả về JSON với `success: true`).

---
### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Gửi **1 lead mẫu** từ website form đến webhook.
   - Kiểm tra:
     - AI có phân tích lead không?
     - Contact/deal có tạo trên HubSpot không?
     - Email thông báo có gửi được không?
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật switch Active** trên n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi thông báo ngay khi lead mới.
   - Ví dụ: `"New lead detected! Score: {aiLeadScore} - Urgency: {aiUrgency}"`.

2. **Lưu log tự động**:
   - Sử dụng node **Set** hoặc **Code** để lưu **log phân tích lead** vào **Google Sheets** hoặc **Notion**.

3. **Báo cáo định kỳ**:
   - Tạo workflow riêng để **tổng hợp lead trong ngày** và gửi báo cáo email cho team.

4. **Tùy chỉnh AI prompt**:
   - Nếu doanh nghiệp có **ICP (Ideal Customer Profile) riêng**, các sếp có thể **cập nhật prompt** trong node **Code** để AI phân tích phù hợp hơn.

5. **Tích hợp CRM khác**:
   - Thay thế HubSpot bằng **Salesforce** hoặc **Pipedrive** bằng cách thay đổi **API endpoint** và **credentials**.

6. **Hệ thống cảnh báo**:
   - Sử dụng node **If** để **cảnh báo lead có mức độ khẩn cấp cao** (urgency = High) bằng cách gửi email hoặc Slack.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng toàn bộ thời gian** của bộ phận sales để tập trung vào **giao dịch thực sự**, trong khi **AI và tự động hóa** xử lý phần còn lại. **Không cần code, không cần kỹ thuật**, chỉ cần **cấu hình đúng credentials** và **tùy chỉnh một chút**, các sếp đã có một **hệ thống chất lượng lead hoàn hảo**!

### **Bắt đầu ngay!**
1. **Import workflow** từ [n8n.io/workflows/15648](https://n8n.io/workflows/15648).
2. **Cấu hình credentials** (OpenAI, HubSpot, Gmail).
3. **Test với lead mẫu** và **bật workflow**.
4. **Tùy chỉnh** theo nhu cầu của doanh nghiệp!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Hãy tự động hóa ngay hôm nay và để AI làm việc cho bạn!** 🚀