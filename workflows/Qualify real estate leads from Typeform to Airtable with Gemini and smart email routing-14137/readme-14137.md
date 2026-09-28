---
title: "🚀 Tự Động Hóa Xác Minh Lead Đất Đai Từ Typeform Sang Airtable Với Gemini AI + Email Tự Động Phân Loại"
description: "Workflow tự động hóa 100% không code giúp các sếp đất đai nhận lead từ Typeform, AI Gemini phân loại lead (cao/midd/low), lưu vào Airtable CRM và gửi email tự động phù hợp. Tiết kiệm 80% thời gian triage thủ công, tăng hiệu quả chuyển đổi 30%."
slug: "tieu-dong-hoa-xac-minh-lead-dat-dai-tu-typeform-sang-airtable-voi-gemini"
tags: [n8n, automation, real-estate, ai-summarization, airtable, gemini-ai, typeform, email-automation]
keywords: [tự động hóa lead đất đai, gemini ai phân loại lead, airtable crm tự động, email marketing tự động hóa, workflow n8n đất đai, tự động hóa typeform]
---

# 🚀 **Tự Động Hóa Xác Minh Lead Đất Đai: Từ Typeform → AI Gemini → Airtable → Email Tự Động**

### **Nỗi Đau Của Các Sếp Đất Đai**
Hàng ngày, các sếp đất đai phải:
- **Làm thủ công** triage hàng trăm lead từ Typeform (điền form, gọi điện, gửi email theo từng trường hợp).
- **Mất thời gian** phân loại lead (cao/midd/low) và cập nhật vào Airtable CRM.
- **Rủi ro sai sót** khi đánh giá lead thủ công, dẫn đến mất lead hoặc chuyển đổi chậm.
- **Không có hệ thống tự động** để gửi email phù hợp với từng loại lead (urgent vs. nurture).

**Workflow này giải quyết tất cả!** Sử dụng **Gemini AI** để phân loại lead chính xác, **Airtable** lưu trữ dữ liệu CRM, và **email tự động** gửi theo mức độ ưu tiên. **Không cần code, chỉ cần copy/paste!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian triage** lead thủ công.
✅ **Phân loại lead chính xác** (cao/midd/low) bằng AI Gemini.
✅ **Lưu trữ tự động** tất cả lead vào Airtable CRM.
✅ **Email tự động** gửi theo mức độ ưu tiên (urgent vs. nurture).
✅ **Tăng hiệu quả chuyển đổi** lên đến 30% so với cách làm thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Typeform** (để nhận lead từ form).
2. **API Key Google Gemini** (hoặc GPT-4o/Claude nếu muốn thay thế).
3. **Airtable Base** với các trường dữ liệu sau:
   - Full Name, Email, Phone, Property Type, Purpose, Location, Budget, Requirements, Submit Date, **Lead Score**, **Intent**, **Timeline**, **Notes**.
4. **SMTP Credentials** (để gửi email từ n8n).
5. **Webhook URL** từ Typeform (sẽ được tạo tự động khi import workflow).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14137) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
##### **A. Webhook (Node: Webhook1)**
- **Không cần thay đổi** URL webhook trong workflow (n8n sẽ tự tạo URL duy nhất).
- **Cần làm:**
  - Copy **URL production** từ node Webhook1 (trong tab "Credentials").
  - Đăng ký vào Typeform:
    - **Typeform → Connect → Webhooks → Add Webhook**
    - Dán URL từ n8n vào và chọn **"POST"** method.

##### **B. Extract Typeform Fields (Node: Extract Typeform Fields1)**
- **Node này** sử dụng **các reference ID** từ Typeform (không phải tên trường).
- **Nếu rebuild form Typeform:**
  - Mở **log execution** của node này (nhấn **"View Execution"**).
  - Tìm **payload test** từ Typeform và sao chép lại **các REF_** mới vào node.
  - Ví dụ:
    ```javascript
    const REF_FULL_NAME = "field_123456789"; // Thay thế bằng REF mới
    ```

##### **C. Google Gemini Chat Model (Node: Google Gemini Chat Model2)**
- **Thêm API Key:**
  - Tạo **credential mới** trong n8n:
    - **Credentials → Add Credential → Google Gemini**
    - Nhập **API Key** từ [Google AI Studio](https://aistudio.google.com/).
  - Gắn credential này vào node **Google Gemini Chat Model2**.

##### **D. Airtable (Node: Save to Airtable2)**
- **Thêm credential Airtable:**
  - **Credentials → Add Credential → Airtable**
  - Nhập **API Key** và chọn **Base ID** của bạn.
- **Cập nhật Table ID:**
  - Mở node **Save to Airtable2** → Tab **"Parameters"**.
  - Thay thế **`your_base_id`** và **`your_table_id`** bằng ID của bảng trong Airtable.

##### **E. Email Send (Node: Priority Email & Nurture Email)**
- **Cập nhật `fromEmail`:**
  - Mở cả hai node **Priority Email** và **Nurture Email**.
  - Thay thế **`fromEmail`** bằng địa chỉ email SMTP của bạn (ví dụ: `no-reply@coban.vn`).
- **Kiểm tra SMTP:**
  - Đảm bảo SMTP đã được cấu hình trong **Credentials → SMTP**.

##### **F. AI Lead Qualifier (Node: AI Lead Qualifier2)**
- **Không cần chỉnh sửa** nếu muốn sử dụng **prompt mặc định**.
- **Nếu muốn thay đổi logic phân loại:**
  - Mở node **Parse AI Output2** → Tab **"Code"**.
  - Thay đổi **các rule scoring** trong đoạn code (ví dụ: điều kiện `if (score === "High")`).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:**
  - Nhấn **"Run Workflow"** và gửi **1 lead test** từ Typeform.
  - Kiểm tra **log execution** để đảm bảo:
    - AI phân loại lead chính xác.
    - Dữ liệu được lưu vào Airtable.
    - Email được gửi đúng.
- **Bật Active:**
  - Sau khi test thành công, chuyển **Workflow Status** từ **"Inactive"** sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Email Cho Lead "Low"**
   - Sau node **High Lead?2**, thêm **1 node IF mới** để phân loại lead "Low" và gửi email riêng.

2. **Lưu Log Tất Cả Các Lead**
   - Thêm **node Slack/Telegram** sau **Save to Airtable2** để thông báo khi có lead mới.

3. **Tự Động Gửi Báo Cáo Hàng Tuần**
   - Sử dụng **node Schedule** (n8n-nodes-base.schedule) để chạy workflow hàng tuần và gửi báo cáo tổng hợp qua email.

4. **Sử Dụng GPT-4o/Claude Thay Vì Gemini**
   - Thay đổi node **Google Gemini Chat Model2** thành **OpenAI Chat** hoặc **Claude Chat** và cập nhật API Key tương ứng.

5. **Tích Hợp CRM Khác**
   - Thay thế node **Airtable** bằng **HubSpot**, **Pipedrive**, hoặc **Zoho CRM** bằng cách thay đổi credential và cấu trúc dữ liệu.

---

### 📌 **Kết Luận**
Workflow này **giải phóng 80% thời gian triage lead** cho các sếp đất đai, đồng thời **tăng hiệu quả chuyển đổi** nhờ AI Gemini phân loại chính xác và email tự động phù hợp. **Không cần code, chỉ cần copy/paste và cấu hình nhanh chóng!**

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với 1 lead** để đảm bảo hoạt động.
3. **Bật Active** và để nó chạy tự động 24/7!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định mà không lo downtime! 🚀