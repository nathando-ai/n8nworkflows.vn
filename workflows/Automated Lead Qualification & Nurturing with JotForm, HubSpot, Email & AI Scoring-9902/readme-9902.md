---
title: "🚀 Tự Động Hóa Xác Minh & Chăm Sóc Khách Hàng (Lead Qualification & Nurturing) với JotForm, HubSpot, Email & AI Scoring"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động nhận, phân loại và chăm sóc khách hàng tiềm năng từ JotForm, đánh giá chất lượng bằng AI, gửi thông báo Slack và email cá nhân hóa, đồng thời cập nhật dữ liệu vào HubSpot và Google Sheets."
slug: "tieu-dong-hoa-xac-minh-cham-soc-khach-hang-ai-scoring"
tags: [n8n, automation, lead-qualification, hubspot, ai-scoring, marketing-automation]
keywords: [n8n workflow tự động hóa, tự động hóa lead qualification, AI đánh giá khách hàng, JotForm HubSpot, tự động hóa chăm sóc khách hàng]
---

# 🚀 Tự Động Hóa Xác Minh & Chăm Sóc Khách Hàng (Lead Qualification & Nurturing) với AI

### 🔍 **Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Làm thủ công** nhập liệu khách hàng từ JotForm vào HubSpot, Google Sheets.
- **Phân loại khách hàng** dựa trên thông tin email, quy mô doanh nghiệp, ngân sách và thời gian phản hồi.
- **Gửi email cá nhân hóa** cho từng lead, mất thời gian và dễ sai sót.
- **Chờ đợi** để Sales và Marketing phản hồi, dẫn đến mất khách hàng tiềm năng.

**Kết quả?** Thời gian phản hồi chậm, tỷ lệ chuyển đổi thấp, và công việc chăm sóc khách hàng trở nên rắc rối.

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động nhận và phân loại** khách hàng tiềm năng từ JotForm trong giây lát.
- **Đánh giá chất lượng lead** bằng AI dựa trên email, quy mô doanh nghiệp, ngân sách và thời gian.
- **Gửi thông báo Slack** ngay lập tức cho Sales (đối với lead nóng) hoặc Marketing (đối với lead ấm/lạnh).
- **Cập nhật tự động** dữ liệu lead vào HubSpot và Google Sheets.
- **Gửi email cá nhân hóa** tự động, tăng tỷ lệ phản hồi.
- **Tiết kiệm thời gian** lên đến **80%** so với làm thủ công.
:::

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 mà không gặp lỗi, các sếp nên cài n8n trên **VPS riêng** (Self-hosted) với tài nguyên ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản JotForm** (để nhận lead từ form).
- **Tài khoản HubSpot** (để lưu trữ và quản lý lead).
- **Tài khoản Google Sheets** (để lưu log và theo dõi lead).
- **Tài khoản Slack** (để gửi thông báo cho Sales/Marketing).
- **SMTP Server** (để gửi email cá nhân hóa, ví dụ: Gmail, SendGrid, Mailgun).
- **API Keys** của các dịch vụ trên (nếu cần).

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ [đây](https://n8n.io/workflows/9902)).
3. Chọn **Create Workflow** để bắt đầu.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **11 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **A. JotForm Trigger**
- **Cấu hình:**
  - Chọn **Form ID** của form JotForm bạn muốn tự động hóa.
  - Chọn **Trigger** là "Form Submission" (khi có submission mới).
  - **Lưu ý:** Đảm bảo form đã được cấu hình đúng các trường cần thiết (email, company size, budget, timeline...).

#### **B. Extract & Format Lead Data (Node `Set`)**
- **Cấu hình:**
  - Map các trường từ JotForm vào biến `leadData` (ví dụ: `{{$json["email"]}}`).
  - **Lưu ý:** Đảm bảo dữ liệu được định dạng chuẩn để AI đánh giá.

#### **C. AI Lead Scoring (Node `Code`)**
- **Cấu hình:**
  - Sử dụng mã JavaScript để tính điểm lead dựa trên các tiêu chí:
    ```javascript
    // Ví dụ mã tính điểm (cần chỉnh sửa theo logic của bạn)
    const score = 0;
    if (leadData.email.includes("@gmail.com")) score += 10;
    if (leadData.companySize > 100) score += 20;
    if (leadData.budget > 10000) score += 30;
    if (leadData.timeline === "immediately") score += 40;
    return { score };
    ```
  - **Lưu ý:** Các sếp cần **chỉnh sửa logic điểm** phù hợp với chiến lược marketing của mình.

#### **D. Route by Lead Quality (Node `If`)**
- **Cấu hình:**
  - Đặt điều kiện phân loại lead:
    - **Hot Lead (Score > 70):** Gửi cho Sales.
    - **Warm Lead (30 < Score ≤ 70):** Gửi cho Marketing.
    - **Cold Lead (Score ≤ 30):** Lưu vào Google Sheets mà không gửi thông báo.

#### **E. Add to HubSpot CRM (Node `HubSpot`)**
- **Cấu hình:**
  - Chọn **Operation = Create**.
  - Map các trường từ `leadData` vào các trường HubSpot tương ứng (ví dụ: `email`, `company`, `lead_score`).
  - **Lưu ý:** Đảm bảo API Key HubSpot được điền chính xác.

#### **F. Log to Google Sheets (Node `Google Sheets`)**
- **Cấu hình:**
  - Chọn **Operation = Append or Update**.
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  - Map `leadData` vào các cột tương ứng.
  - **Lưu ý:** Đảm bảo tài khoản Google Sheets có quyền truy cập vào file.

#### **G. Notify Sales Team (Hot Lead) / Notify Marketing (Warm/Cold) (Node `Slack`)**
- **Cấu hình:**
  - Chọn **Webhook URL** của Slack (tạo từ **Apps > Incoming Webhooks**).
  - Tạo **message template** cá nhân hóa:
    ```json
    {
      "text": "🔥 **Hot Lead Alert!**\nEmail: {{$json["email"]}}\nCompany: {{$json["company"]}}\nScore: {{$json["score"]}}"
    }
    ```
  - **Lưu ý:** Sử dụng **emoji và định dạng** để dễ đọc.

#### **H. Generate Personalized Email (Node `Code`)**
- **Cấu hình:**
  - Sử dụng mã JavaScript để tạo email cá nhân hóa:
    ```javascript
    const emailBody = `
      Chào {{leadData.firstName}},\n
      Tôi là [Tên Bạn], từ [Tên Công Ty].\n
      Tôi thấy [Company Name] của bạn rất phù hợp với giải pháp của chúng tôi. \n
      Với ngân sách {{leadData.budget}} và thời gian {{leadData.timeline}}, chúng tôi có thể hỗ trợ như sau: [Nội dung cá nhân hóa].
      Hãy liên hệ với tôi qua email hoặc gọi số: [Số Điện Thoại].
    `;
    return { emailBody };
    ```
  - **Lưu ý:** Các sếp cần **chỉnh sửa template email** phù hợp với brand.

#### **I. Send Personalized Email (Node `EmailSend`)**
- **Cấu hình:**
  - Chọn **SMTP Server** (ví dụ: Gmail, SendGrid).
  - Điền **From Email**, **To Email** (`{{$json["email"]}}`).
  - Sử dụng `emailBody` từ node trước.
  - **Lưu ý:** Đảm bảo SMTP được cấu hình đúng (username, password, port).

#### **J. Create Daily Summary (Node `Set`)**
- **Cấu hình:**
  - Tạo một biến `dailySummary` để lưu trữ thống kê hàng ngày (ví dụ: số lead, số lead nóng, số lead ấm).
  - **Lưu ý:** Có thể kết hợp với **Google Sheets** để tự động tạo báo cáo.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập một lead mẫu vào JotForm và kiểm tra workflow hoạt động như thế nào.
2. **Bật Active Workflow**:
   - Nhấn **Active** trên n8n Editor để workflow bắt đầu chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Telegram/Email Alerts:** Thay vì Slack, các sếp có thể gửi thông báo qua Telegram hoặc email.
- **Lưu Log Chi Tiết:** Sử dụng **Google Sheets** hoặc **Airtable** để lưu trữ log chi tiết của từng lead.
- **Tự Động Gửi Báo Cáo Hàng Tuần:** Sử dụng **n8n Scheduler** để gửi báo cáo tổng hợp cho Sales/Marketing.
- **Cải Tiến AI Scoring:** Sử dụng **LLM như Mistral AI** để đánh giá lead thông minh hơn (ví dụ: phân tích nội dung email).
- **Tích Hợp CRM Khác:** Thay HubSpot, các sếp có thể sử dụng **Pipedrive** hoặc **Salesforce**.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công, **tăng tỷ lệ chuyển đổi** và **tự động hóa toàn bộ quy trình chăm sóc khách hàng**. Với **AI Scoring**, các sếp có thể **phân loại lead chính xác**, gửi thông báo kịp thời và **tăng doanh thu** hiệu quả.

**Hành động ngay hôm nay!**
1. Import workflow vào n8n.
2. Cấu hình các node theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

👉 [Tải workflow nguyên bản](https://n8n.io/workflows/9902) để bắt đầu!

---