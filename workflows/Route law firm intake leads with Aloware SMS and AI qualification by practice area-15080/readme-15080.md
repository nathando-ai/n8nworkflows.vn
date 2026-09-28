---
title: "🚀 Tự Động Hóa Xử Lý Lời Hỏi Khách Hàng Luật Sư Với SMS + AI & Phân Loại Theo Ngành Hành Pháp Luật"
description: "Workflow tự động hóa nhận, xử lý và phân loại lời hỏi khách hàng luật sư từ website/form, gửi SMS xác nhận, và phân luồng theo ngành hành pháp luật (AI intake cho các trường hợp cao độ ý định, hoặc lịch hẹn cho các trường hợp tiêu chuẩn). Giúp tiết kiệm thời gian lên đến 80% cho bộ phận tiếp nhận khách hàng."
slug: "tieu-dong-hoa-xu-ly-loi-hoi-khach-hang-luat-su"
tags: [n8n, automation, no-code, lead-generation, ai-chatbot, aloware, sms-automation]
keywords: [tự động hóa luật sư, nhận lời hỏi khách hàng, phân loại theo ngành hành pháp luật, SMS tự động, AI intake, Aloware, n8n workflow]
---

# 🚀 Tự Động Hóa Xử Lý Lời Hỏi Khách Hàng Luật Sư Với SMS + AI & Phân Loại Theo Ngành Hành Pháp Luật

### **Giải pháp cho các sếp luật sư:**
Hàng ngày, bộ phận tiếp nhận khách hàng của các công ty luật phải mất **giờ đồng hồ** để:
- Nhận và ghi chép thông tin từ form website hoặc hệ thống intake.
- Gửi SMS xác nhận nhận được lời hỏi.
- Phân loại từng trường hợp theo **ngành hành pháp luật** (Personal Injury, Family Law, Criminal, Immigration, Estate, Business, Real Estate...) để định hướng tiếp theo.
- Giao tiếp với khách hàng để **lịch hẹn hoặc AI intake** tùy theo độ ưu tiên.

**Workflow này tự động hóa toàn bộ quy trình trên, giúp các sếp:**
- **Tiết kiệm 80% thời gian** cho bộ phận tiếp nhận.
- **Tăng trải nghiệm khách hàng** với SMS xác nhận ngay lập tức.
- **Phân loại chính xác** và định hướng khách hàng đến **AI intake** (cho các trường hợp cao độ ý định) hoặc **lịch hẹn** (cho các trường hợp tiêu chuẩn).
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần ghi chép thủ công, gửi SMS hoặc phân loại từng lời hỏi.
- **Chính xác và không sai sót:** AI phân loại theo ngành hành pháp luật theo quy tắc đã thiết lập.
- **Cá nhân hóa:** SMS xác nhận được gửi ngay lập tức với thông tin khách hàng.
- **Hoạt động liên tục:** Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.
- **Tăng doanh thu:** Khách hàng cao độ ý định được định hướng đến **AI intake** ngay lập tức, tăng tỷ lệ chuyển đổi.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Aloware** (hệ thống CRM dành cho luật sư) với:
   - `ALOWARE_API_TOKEN` (API Key từ Aloware).
   - `ALOWARE_LINE_PHONE` (số điện thoại của Aloware để gửi SMS).
   - `ALOWARE_INTAKE_SEQUENCE_ID` (ID của sequence AI intake).
   - `ALOWARE_CONSULT_SEQUENCE_ID` (ID của sequence lịch hẹn).
2. **Tên công ty luật** (`FIRM_NAME`) để personalize SMS.
3. **Form website hoặc hệ thống intake** hiện có (cần cấu hình để gửi dữ liệu POST đến webhook của workflow).
4. **Hai sequence trong Aloware**:
   - **AI Intake Sequence** (cho các trường hợp cao độ ý định).
   - **Consultation Scheduling Sequence** (cho các trường hợp tiêu chuẩn).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào workspace của mình.
2. Nhấp vào **"Create Workflow"** > **"Import Workflow"**.
3. Chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/15080).
4. Nhấp **"Import"** để hoàn tất.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflows này bao gồm **7 node** chính, và các sếp cần chú ý cấu hình sau:

##### **Node 1: Law Firm: New Client Inquiry (Webhook)**
- **Cấu hình:**
  - **Path:** `law-firm-inquiry` (không thay đổi).
  - **HTTP Method:** `POST` (không thay đổi).
- **Lưu ý:**
  - Cần **cấu hình form website hoặc hệ thống intake** để gửi dữ liệu POST đến URL webhook này.
  - URL webhook sẽ được hiển thị khi import workflow thành công.

##### **Node 2: Normalize Inquiry Data (Set)**
- **Cấu hình:**
  - Node này **không cần chỉnh sửa** vì nó tự động định dạng dữ liệu đầu vào (tên, số điện thoại, ngành hành pháp luật, mô tả vụ việc).
  - Nếu dữ liệu đầu vào không chuẩn, các sếp có thể thêm node **Parse JSON** hoặc **Set** để điều chỉnh.

##### **Node 3 & 4: Aloware: Create Client Contact & Aloware: Send Intake SMS (HTTP Request)**
- **Cấu hình:**
  - **Headers:**
    - `Authorization: Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "phone": "{{ $json["phone"] }}",
      "name": "{{ $json["name"] }}",
      "practice_area": "{{ $json["practice_area"] }}",
      "case_description": "{{ $json["case_description"] }}"
    }
    ```
  - **URL:**
    - **Create Client Contact:** `https://api.aloware.com/v1/contacts`
    - **Send Intake SMS:** `https://api.aloware.com/v1/sms/send`
- **Lưu ý:**
  - Thay thế `{{ $variables.ALOWARE_API_TOKEN }}` bằng biến môi trường đã thiết lập trước đó.
  - Thay thế `{{ $json["field"] }}` bằng các trường dữ liệu từ form (ví dụ: `phone`, `name`, `practice_area`).

##### **Node 5: Is High-Intent Practice Area? (If)**
- **Cấu hình:**
  - Node này **phân loại khách hàng** theo ngành hành pháp luật.
  - **Điều kiện:**
    - **True:** Nếu `practice_area` là **Personal Injury, Family, Criminal, hoặc Immigration** (các trường hợp cao độ ý định).
    - **False:** Nếu `practice_area` là **Estate, Business, hoặc Real Estate** (các trường hợp tiêu chuẩn).
  - **Lưu ý:**
    - Các sếp có thể **chỉnh sửa danh sách ngành cao độ ý định** trong node này để phù hợp với chiến lược của công ty.

##### **Node 6 & 7: Aloware: Enroll in AI Intake Sequence & Aloware: Enroll in Consultation Scheduling Sequence (HTTP Request)**
- **Cấu hình:**
  - **Headers:**
    - `Authorization: Bearer {{ $variables.ALOWARE_API_TOKEN }}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "contact_id": "{{ $json["contact_id"] }}",
      "sequence_id": "{{ $variables.ALOWARE_INTAKE_SEQUENCE_ID || $variables.ALOWARE_CONSULT_SEQUENCE_ID }}"
    }
    ```
  - **URL:**
    - **AI Intake Sequence:** `https://api.aloware.com/v1/sequences/{{ $variables.ALOWARE_INTAKE_SEQUENCE_ID }}/enroll`
    - **Consultation Scheduling Sequence:** `https://api.aloware.com/v1/sequences/{{ $variables.ALOWARE_CONSULT_SEQUENCE_ID }}/enroll`
- **Lưu ý:**
  - Thay thế `{{ $variables.ALOWARE_INTAKE_SEQUENCE_ID }}` và `{{ $variables.ALOWARE_CONSULT_SEQUENCE_ID }}` bằng các biến môi trường đã thiết lập.
  - **Node này sẽ chạy tùy thuộc vào kết quả của node If (Node 5).**

---

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấp **"Run Workflow"** và gửi một **dữ liệu mẫu** từ form website hoặc sử dụng **Postman** để gửi POST đến URL webhook.
   - Kiểm tra kết quả trong **Aloware** và **SMS** đã được gửi chưa.
2. **Bật Active:**
   - Sau khi test thành công, nhấp **"Active"** để workflow chạy tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack/Telegram Webhook** để thông báo khi có lời hỏi mới hoặc khi khách hàng được định hướng đến AI intake.

2. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử lời hỏi, giúp theo dõi và phân tích hiệu quả.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng node **Schedule** để chạy workflow hàng ngày và gửi báo cáo tổng hợp về số lượng lời hỏi, tỷ lệ chuyển đổi, và ngành hành pháp luật phổ biến.

4. **Cá nhân hóa SMS:**
   - Thêm biến `{{ $variables.FIRM_NAME }}` vào nội dung SMS để personalize:
     ```
     "Xin chào {{ $json["name"] }}, chúng tôi đã nhận được lời hỏi của bạn về {{ $json["practice_area"] }}. Công ty {{ $variables.FIRM_NAME }} sẽ liên hệ với bạn trong thời gian sớm nhất. Cảm ơn!"
     ```

5. **Xử lý lỗi:**
   - Thêm node **Error Handling** (ví dụ: **n8n-nodes-base.if**) để xử lý trường hợp API Aloware thất bại và gửi thông báo lỗi đến Slack/Email.

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình tiếp nhận khách hàng của các công ty luật, giúp tiết kiệm thời gian, tăng trải nghiệm khách hàng, và tối ưu hóa quy trình phân loại. **Hãy áp dụng ngay để bắt đầu tự động hóa bộ phận tiếp nhận của công ty luật của các sếp!**

👉 **Bắt đầu ngay:** [Tải workflow từ n8n.io](https://n8n.io/workflows/15080) và import vào n8n của mình!