---
title: "🚀 Tự Động Hóa Chuyển Dẫn Lead LinkedIn Sang CRM & Google Sheets - Không Cần Code"
description: "Workflow tự động hóa 100% miễn phí từ n8n.io giúp các sếp tự động chụp leads LinkedIn, đánh giá chất lượng, loại bỏ trùng lặp và đồng bộ hóa liên tục với Google Sheets, HubSpot hoặc Salesforce. Giúp đội ngũ bán hàng tập trung vào leads có tiềm năng cao mà không mất thời gian thủ công."
slug: "tu-dong-hoa-chuyen-dan-lead-linkedin-sang-crm"
tags: [n8n, automation, lead-generation, crm-integration, google-sheets, hubspot, salesforce, ai-summarization]
keywords: [tự động hóa lead LinkedIn, đồng bộ CRM HubSpot, tự động hóa Salesforce, chụp leads LinkedIn, tự động hóa bán hàng, n8n workflow lead generation]
---

# 🚀 **Tự Động Hóa Chụp Lead LinkedIn & Đồng Bộ CRM - Không Cần Code**

## **🔥 Nỗi Đau Của Các Sếp Trong Bán Hàng**
Hàng ngày, đội ngũ bán hàng phải:
✅ **Quét thủ công** danh sách liên hệ mới trên LinkedIn
✅ **Nhập lại** thông tin vào Google Sheets hoặc CRM (HubSpot/Salesforce)
✅ **Loại bỏ trùng lặp** giữa các nguồn dữ liệu
✅ **Đánh giá chất lượng** leads dựa trên hành vi tương tác
✅ **Gửi thông báo** cho đội ngũ bán hàng khi có leads "hot" (có tiềm năng cao)

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc thủ công, trong khi leads tiềm năng bị bỏ qua.

---
### **🎯 Giải Pháp Tự Động Hóa 100% Không Cần Code**
Workflow này **tự động hóa toàn bộ quy trình** từ chụp leads LinkedIn đến đồng bộ hóa với CRM và Google Sheets, giúp các sếp:
✔ **Tiết kiệm 10+ giờ/tuần** cho đội ngũ bán hàng
✔ **Loại bỏ trùng lặp** với hệ thống theo dõi 90 ngày
✔ **Đánh giá tự động** chất lượng leads (Hot/Warm/Cold) dựa trên hành vi tương tác
✔ **Đồng bộ liên tục** với HubSpot, Salesforce hoặc Google Sheets
✔ **Gửi thông báo ngay** cho đội ngũ bán hàng khi có leads tiềm năng

---
### **📌 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản LinkedIn** (đã cấp quyền API)
🔹 **Google Sheets** (đã tạo bảng với cấu trúc cụ thể)
🔹 **CRM** (HubSpot **hoặc** Salesforce - không hỗ trợ cả hai cùng lúc)
🔹 **Slack Webhook** (nếu muốn gửi thông báo)
🔹 **Tài khoản Email SMTP** (nếu muốn gửi email tự động)

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1️⃣ Import Workflow Từ File JSON**
👉 **Bước 1:** Tải workflow từ [n8n.io/workflows/12580](https://n8n.io/workflows/12580) hoặc copy JSON dưới đây.
👉 **Bước 2:** Mở n8n Editor → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.

```json
// (JSON sẽ được cung cấp đầy đủ khi các sếp tải từ n8n.io)
```

### **2️⃣ Cấu Hình Cần Thiết (BẮT BUỘC)**
#### **🔹 Cấu Hình LinkedIn**
- **Node:** `Fetch new LinkedIn connections` & `Fetch post engagement data`
- **Cách làm:**
  1. Tạo **OAuth2 credentials** cho LinkedIn trong n8n (Settings → Credentials → Add → LinkedIn).
  2. Chọn **API Key** và **API Secret** từ [LinkedIn Developer Portal](https://www.linkedin.com/developers/).
  3. Điền vào cả hai node `linkedIn` trong workflow.

#### **🔹 Cấu Hình Google Sheets**
- **Node:** `Append new lead` & `Update existing lead`
- **Cách làm:**
  1. Tạo **Google Sheets** mới với **cấu trúc cột** sau:
     | leadId | fullName | firstName | lastName | email | phone | company | position | headline | location | profileUrl | leadSource | leadTemperature | qualityScore | engagementType | commentText | dateAdded | status | assignedTo | notes | lastUpdated |
  2. Tạo **OAuth2 credentials** cho Google Sheets trong n8n.
  3. Chọn **Google Sheet ID** và **Sheet Name** trong node `googleSheets`.

#### **🔹 Chọn CRM (HubSpot hoặc Salesforce)**
- **Node:** `Create new contact in HubSpot` / `Create new lead in Salesforce`
- **Cách làm:**
  - **HubSpot:**
    1. Tạo **API Key** từ [HubSpot Developer](https://developers.hubspot.com/docs/api/private-apps).
    2. Thêm **credentials** trong n8n với `hubspotApi`.
  - **Salesforce:**
    1. Tạo **Connected App** và lấy **Consumer Key** & **Consumer Secret**.
    2. Thêm **credentials OAuth2** trong n8n với `salesforceOAuth2Api`.

#### **🔹 Cấu Hình Thông Báo (Slack/Email)**
- **Node:** `Send Slack notification` / `Send email notification`
- **Cách làm:**
  - **Slack:**
    1. Tạo **Webhook URL** từ Slack App.
    2. Điền vào node `httpRequest` (Slack).
  - **Email:**
    1. Thêm **SMTP credentials** trong n8n (Settings → Credentials → Add → SMTP).
    2. Chọn **From Email** và **SMTP Server** trong node `emailSend`.

### **3️⃣ Kích Hoạt Workflow**
1. **Test Run:** Chọn **Run Workflow** để kiểm tra dữ liệu mẫu.
2. **Active:** Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động mỗi 15 phút.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
🔹 **Kết hợp với AI:** Sử dụng **n8n-nodes-ai** để tự động phân tích profile LinkedIn và gợi ý comment.
🔹 **Lưu Log:** Thêm node `stickyNote` để ghi lại lịch sử hoạt động của workflow.
🔹 **Báo Cáo Định Kỳ:** Sử dụng **Google Sheets + Apps Script** để tạo báo cáo hàng tuần về leads.
🔹 **Tích Hợp Zoom:** Gửi thông báo khi có leads "Hot" cùng với link cuộc gọi Zoom.

---
## **📌 Kết Luận**
Workflow này **giải phóng đội ngũ bán hàng** khỏi công việc thủ công, giúp họ tập trung vào việc **nắm bắt leads có tiềm năng** mà không mất thời gian nhập liệu. **Chỉ cần 1 lần cấu hình**, workflow sẽ **chạy tự động 24/7**, đồng bộ hóa liên tục với CRM và Google Sheets.

👉 **Hãy thử ngay!** [Tải workflow từ n8n.io](https://n8n.io/workflows/12580) và tự động hóa bán hàng của mình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**🚀 Cần hỗ trợ?** Đăng ký [hỗ trợ từ The AI Squad](https://theaisquad.com) để được tư vấn chi tiết!