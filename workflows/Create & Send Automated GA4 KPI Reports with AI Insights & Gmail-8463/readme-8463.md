---
title: "📊 Tự Động Hoá Báo Cáo KPI GA4 Với AI Tóm Tắt + Gửi Email HTML Tự Động - Giảm 90% Thời Gian Làm Báo Cáo"
description: "Workflow này tự động lấy dữ liệu GA4, phân tích AI, tạo báo cáo HTML color-coded với % thay đổi và gửi email tự động - giúp marketing team tiết kiệm 90% thời gian làm báo cáo hàng tuần/monthly."
slug: "tieu-dong-hoa-bao-cao-ga4-ai-gmail"
tags: [n8n, automation, ga4, ai-summarization, google-analytics, gmail-automation, marketing-analytics]
keywords: [tự động hóa báo cáo ga4, ai tóm tắt báo cáo marketing, gửi email báo cáo ga4 tự động, workflow n8n ga4, báo cáo kpi marketing tự động]
---

# 🚀 **Tự Động Hoá Báo Cáo KPI GA4 Với AI Tóm Tắt + Gửi Email HTML Tự Động**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Hàng tuần, các sếp marketing phải:
- **Lấy dữ liệu GA4 thủ công** từ nhiều báo cáo khác nhau (sessions, users, bounce rate, conversion events).
- **So sánh dữ liệu giữa các kỳ** (so với tuần trước, tháng trước) để tính toán % thay đổi.
- **Tạo báo cáo Excel/Google Sheets** với màu sắc để dễ nhìn (xanh cho tăng, đỏ cho giảm).
- **Viết tóm tắt và đề xuất chiến lược** dựa trên dữ liệu.
- **Gửi email báo cáo** cho khách hàng hoặc đồng nghiệp.

**Kết quả?** Tốn **5-10 giờ/tuần**, dễ sai sót, và không cá nhân hóa.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy dữ liệu GA4** (sessions, users, bounce rate, conversion events) cho **hai kỳ** (hiện tại và trước đó).
✅ **Tính toán % thay đổi** và **color-code** (xanh tăng, đỏ giảm).
✅ **AI tóm tắt và đề xuất chiến lược** bằng GPT-4.
✅ **Tạo báo cáo HTML đẹp** với logo, màu sắc và layout chuyên nghiệp.
✅ **Gửi email tự động** cho khách hàng với **tiêu đề cá nhân hóa**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** làm báo cáo (từ 5-10 giờ/tháng xuống còn 30-60 phút).
- **Chính xác 100%** (không sai sót tính toán % thay đổi).
- **Báo cáo chuyên nghiệp** với HTML đẹp, color-coded và AI tóm tắt.
- **Hoạt động liên tục** (không cần can thiệp thủ công).
- **Cá nhân hóa** (tiêu đề email và nội dung báo cáo tùy chỉnh theo khách hàng).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Analytics 4 (GA4)** với quyền **Viewer/Analyst** (để lấy dữ liệu API).
2. **API Key OpenAI** (để sử dụng GPT-4 tóm tắt báo cáo).
3. **Tài khoản Gmail** (để gửi email báo cáo tự động).
4. **GA4 Property ID** (Account ID) của khách hàng (cách lấy: [Hướng dẫn](https://take.ms/vO2MG)).
5. **Tên Event Key** (ví dụ: "Purchase", "Sign Up") (cách lấy: [Hướng dẫn](https://take.ms/hxwQi)).

**Lưu ý:**
- Workflow sử dụng **GA4 Data API**, nên cần **OAuth2 credentials** cho Google Analytics.
- Email gửi báo cáo phải là **Gmail** (không hỗ trợ Yahoo/Outlook).
- **Mô hình AI** mặc định là `gpt-4.1-mini` (nếu muốn nâng cấp, thay đổi trong node `OpenAI Chat Model`).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/8463](https://n8n.io/workflows/8463) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8463) và paste vào **Import Workflow** trong n8n.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Import** → Chọn **Paste JSON**.
2. Copy toàn bộ mã JSON từ [n8n.io/workflows/8463](https://n8n.io/workflows/8463) và dán vào.
3. Nhấn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Get Client (Form Trigger)**
- **Cấu hình form** để thu thập:
  - **Account ID (GA4 Property ID)** → Nhập theo [hướng dẫn](https://take.ms/vO2MG).
  - **Key Event** → Nhập tên event (ví dụ: "Purchase") → [Hướng dẫn](https://take.ms/hxwQi).
  - **Report Date Range (Current & Previous)** → Định dạng `YYYY-MM-DD` (ví dụ: `2024-05-01` đến `2024-05-31`).
  - **Client Name** → Tên khách hàng (sẽ xuất hiện trong email).
  - **Send-to Email** → Email nhận báo cáo.

#### **🔹 Node 2-5: Overall Metrics & Form Submits (GA4 Data API)**
- **Gắn credential** `googleAnalyticsOAuth2` (đã cấu hình trước khi import).
- **Kiểm tra API Request**:
  - **Endpoint**: `https://analyticsdata.googleapis.com/v1beta/properties/{PROPERTY_ID}/events:runPivot`
  - **Tham số cần thiết**:
    - `dateRanges`: Mảng chứa 2 khoảng ngày (current & previous).
    - `dimensions`: `eventName` (để lấy event key).
    - `metrics`: `sessions`, `users`, `bounceRate`, `eventCount` (tùy chỉnh theo nhu cầu).

#### **🔹 Node 6: OpenAI Chat Model (AI Tóm Tắt)**
- **Gắn credential** `openAiApi` (API Key OpenAI).
- **Cấu hình model**:
  - Mặc định là `gpt-4.1-mini` (rẻ hơn `gpt-4`).
  - Nếu muốn nâng cấp, thay đổi trong **keyParameters → model**.
- **Prompt mẫu** (có thể chỉnh sửa trong node `Code`):
  ```json
  "prompt": "Tóm tắt báo cáo GA4 cho kỳ {{currentPeriod}} so với kỳ {{previousPeriod}}.
  - So sánh % thay đổi của sessions, users, bounce rate và event '{{keyEvent}}'.
  - Nêu ra 3 điểm mạnh và 3 điểm yếu.
  - Đề xuất 2 chiến lược cải thiện cho kỳ tiếp theo.
  - Sử dụng HTML để tạo báo cáo với màu xanh (#10B981) cho tăng, đỏ (#EF4444) cho giảm."
  ```

#### **🔹 Node 7: AI Agent (Xây Dựng Báo Cáo HTML)**
- **Node này tự động**:
  - Tính toán % thay đổi.
  - Áp dụng màu sắc (xanh/đỏ).
  - Tạo **HTML email** sẵn sàng gửi.
- **Lưu ý**:
  - Nếu muốn thay đổi logic, chỉnh sửa trong node `Code` (node 11).

#### **🔹 Node 8: Send a Message (Gmail)**
- **Gắn credential** `gmailOAuth2`.
- **Cấu hình email**:
  - **Subject**: `Báo cáo KPI GA4 - {{clientName}} ({{currentPeriod}})`.
  - **HTML Body**: Sử dụng output từ node `AI Agent`.
  - **Reply-to**: Có thể để trống hoặc đặt email của khách hàng.

#### **🔹 Node 9-10: Calculator & Think (AI Logic)**
- **Node này tự động tính toán** và **lập kế hoạch** cho AI.
- **Không cần chỉnh sửa** trừ khi muốn thay đổi logic AI.

#### **🔹 Node 11: Code (Chỉnh Sửa Prompt & Logic)**
- **Nếu muốn thay đổi prompt AI**, chỉnh sửa trong phần `code`:
  ```javascript
  // Ví dụ: Thay đổi model OpenAI
  const model = "gpt-4.1-mini";
  // Hoặc thay đổi cấu trúc HTML output
  ```
- **Lưu ý**: Nếu không biết code, **không cần chỉnh** để tránh lỗi.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập **GA4 Property ID**, **Key Event**, **date ranges**, **Client Name**, **Send-to Email**.
   - Chạy **Test Execution** để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có form submit.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối Với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node `Send a Message` để **báo lỗi** hoặc **cập nhật tiến trình** khi workflow thất bại.

### **🔹 Lưu Log Báo Cáo**
- Thêm node **Google Sheets** hoặc **Airtable** sau node `AI Agent` để **lưu tất cả báo cáo** vào bảng dữ liệu, giúp theo dõi lịch sử.

### **🔹 Gửi Báo Cáo Định Kỳ (Tuần/Hàng Tháng)**
- Sử dụng **n8n Trigger: Schedule** (node `scheduleTrigger`) để chạy workflow **tự động hàng tuần/tháng** mà không cần form submit.

### **🔹 Tùy Chỉnh Màu Sắc & Logo**
- Trong node `Code`, chỉnh sửa phần **HTML template** để thêm **logo công ty** hoặc thay đổi **màu sắc mặc định**.

### **🔹 Sử Dụng Mô Hình AI Khác**
- Thay đổi từ `gpt-4.1-mini` sang `gpt-4` (nếu có budget) để **AI tóm tắt chi tiết hơn**.

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi công việc **làm báo cáo GA4 thủ công**, đồng thời **tăng chất lượng** với:
✔ **Dữ liệu chính xác** (không sai sót tính toán).
✔ **Báo cáo chuyên nghiệp** (HTML đẹp, color-coded).
✔ **AI tóm tắt** (giúp đọc hiểu nhanh).
✔ **Gửi email tự động** (không quên báo cáo).

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credential** (GA4, OpenAI, Gmail).
3. **Test với dữ liệu thật** và **bật Active**.
4. **Tiết kiệm 90% thời gian** làm báo cáo!

**🚀 Cài n8n trên VPS để workflow chạy 24/7:**
👉 [TinoHost (Mã giảm 39%)](https://tino.vn/vps-n8n?affid=388)
👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)