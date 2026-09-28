---
title: "🚀 Tự Động Hóa Đánh Giá & Phân Loại Lead Inbound với Claude AI + HubSpot (Không Cần Code)"
description: "Workflow tự động nhận lead từ form, đánh giá chất lượng với AI Claude, phân loại theo lifecycle HubSpot và gửi thông báo tự động cho đội ngũ bán hàng. Giúp các sếp tiết kiệm 8+ giờ/ngày xử lý lead thủ công."
slug: "tieu-dong-hoa-danh-gia-lead-claude-hubspot"
tags: [n8n, automation, lead-scoring, ai-claude, hubspot, no-code, sales-automation]
keywords: [tự động hóa lead scoring, Claude AI với n8n, phân loại lead HubSpot, tự động hóa bán hàng, workflow n8n HubSpot, giảm thời gian xử lý lead]
---

# 🚀 **Tự Động Hóa Đánh Giá Lead Inbound với AI Claude + HubSpot: Từ Form → Deal Trong Vài Giây**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, đội ngũ marketing và bán hàng phải mất **8-10 giờ** để:
- Nhận và nhập liệu lead từ form vào HubSpot.
- Đánh giá thủ công chất lượng lead (hot, warm, cold) dựa trên email, domain, và thông tin công ty.
- Phân loại lead theo lifecycle và gửi thông báo cho sales team.
- Theo dõi và gửi email follow-up cho từng lead.

**Kết quả?** Lead chất lượng bị bỏ qua, thời gian phản hồi chậm, và doanh số bị ảnh hưởng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
- **Tiết kiệm 8+ giờ/ngày** xử lý lead thủ công.
- **Đánh giá lead chính xác** với AI Claude (thay vì con người).
- **Phân loại tự động** lead thành **hot, warm, cold** và gửi thông báo ngay cho sales.
- **Tạo deal tự động** cho lead hot và gửi email follow-up cá nhân hóa.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản HubSpot** (với quyền API access).
2. **API Key Claude (Anthropic)** để đánh giá lead.
3. **Tài khoản Gmail** (để gửi email follow-up).
4. **Tài khoản Slack** (để thông báo cho sales team).
5. **Form nhận lead** (cần cấu hình webhook để gửi dữ liệu vào workflow).

---
### **🚀 Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow từ File JSON**
- Tải file JSON từ [n8n.io/workflows/16011](https://n8n.io/workflows/16011).
- Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
- **Hoặc** copy/paste JSON vào **Import Workflow** trong n8n.

#### **2. Các Bước Cấu Hình Bắt Buộc**
##### **A. Cấu Hình Webhook (Nhận Lead)**
- Node: **"When Lead Submitted"** (Webhook)
- **Path:** `lead-intake`
- **HTTP Method:** `POST`
- **Lưu ý:** Cần cấu hình form nhận lead để gửi dữ liệu POST đến URL webhook này.

##### **B. Cấu Hình HubSpot (API Access)**
- Node: **"Post Lead Score Property"**, **"Post Lead Tier Property"**, **"Upsert Contact"**, **"Create Deal"**
- **Credentials:** `hubspotAppToken`
- **Cách lấy API Key HubSpot:**
  1. Đăng nhập HubSpot → **Settings** → **Integrations** → **API Keys**.
  2. Tạo **Private App Token** và sao chép vào n8n.

##### **C. Cấu Hình Claude AI (Anthropic API)**
- Node: **"Post Lead to Claude AI"**
- **Credentials:** `anthropicApi`
- **Cách lấy API Key Claude:**
  1. Đăng ký tại [Anthropic](https://www.anthropic.com/).
  2. Tạo API Key và sao chép vào n8n.

##### **D. Cấu Hình Gmail (Gửi Email Follow-up)**
- Node: **"Email Hot Lead"**, **"Email Warm Lead"**, **"Email Cold Lead"**
- **Credentials:** `gmailOAuth2`
- **Cách cấu hình:**
  1. Tạo **OAuth2 Client ID** tại [Google Cloud Console](https://console.cloud.google.com/).
  2. Cấu hình trong n8n với **Client ID** và **Client Secret**.

##### **E. Cấu Hình Slack (Thông Báo Sales)**
- Node: **"Notify Sales via Slack"**
- **Credentials:** `slackApi`
- **Cách lấy Token Slack:**
  1. Tạo **Slack App** tại [API Slack](https://api.slack.com/apps).
  2. Sao chép **Bot Token** và **Channel ID** vào n8n.

##### **F. Cấu Hình Node "Set Lead Scoring Params"**
- **Tham số cần chỉnh:**
  - **ICP (Ideal Customer Profile):** Mô tả chi tiết khách hàng lý tưởng (ví dụ: "Doanh nghiệp Fintech có revenue > 10M USD").
  - **Score Thresholds:**
    - **Hot Lead:** Score > 80
    - **Warm Lead:** Score 50-80
    - **Cold Lead:** Score < 50

##### **G. Cấu Hình Node "Setup Web Search Params"**
- **Tham số cần chỉnh:**
  - **Query Template:** Cấu trúc câu hỏi cho Claude (ví dụ: `"Analyze this company: {companyName}, website: {website}, recent news: {news}. Give a lead score between 0-100."`).

---
#### **3. Kích Hoạt Workflow**
- **Test Run:** Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra.
- **Active Workflow:** Sau khi cấu hình xong, bật **Active** để workflow hoạt động 24/7.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Tất Cả Lead**
   - Thêm node **StickyNote** để lưu lịch sử đánh giá lead.
   - **Cách làm:** Thêm node `n8n-nodes-base.stickyNote` sau node **"Parse Claude AI Score"** và cấu hình lưu dữ liệu.

2. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng node **HTTP Request** kết hợp với **Google Sheets** để tự động cập nhật báo cáo lead hàng ngày.

3. **Kết Nối với CRM Khác**
   - Thay thế node HubSpot bằng **Salesforce** hoặc **Pipedrive** bằng cách thay đổi credentials và API.

4. **Cải Tiến AI Scoring**
   - Tối ưu **Prompt** cho Claude để tăng độ chính xác (ví dụ: thêm yêu cầu cụ thể về tiêu chí đánh giá).

---
### **📌 Kết Luận**
Workflow này **giải phóng đội ngũ marketing và sales** khỏi công việc thủ công, giúp tập trung vào **đối thoại và đóng gói deal** thay vì nhập liệu. **Chỉ cần 1 lần cấu hình**, workflow sẽ hoạt động tự động mọi lúc.

**🚀 Hành động ngay:**
1. **Cài n8n Self-hosted** trên VPS để workflow chạy ổn định 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và xem lead được xử lý tự động!

**Nếu cần hỗ trợ thêm**, để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 💡