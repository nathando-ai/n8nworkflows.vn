---
title: "🚀 Tự Động Hóa Email Re-Engage Lead Khó Nhận với AI GPT-4o-mini, Outlook & Google Sheets – Giảm 80% Thời Gian Nurturing"
description: "Workflow tự động hóa hoàn toàn không cần code để phân tích lịch sử email của lead cũ, tổng hợp thông tin, và tạo email re-engage cá nhân hóa với AI GPT-4o-mini. Giúp các sếp tự động hóa quy trình nurturing lead khó nhằn, tăng tỷ lệ chuyển đổi lên 30-50%."
slug: "tieu-dong-hoa-email-re-engage-lead-voi-gpt-4o-mini-outlook-google-sheets"
tags: [n8n, automation, lead nurturing, ai multichannel, google sheets, microsoft outlook, openai, gpt-4o-mini, no-code]
keywords: [tự động hóa email lead, re-engage lead với ai, workflow n8n lead nurturing, gpt-4o-mini tự động hóa, tự động hóa outlook google sheets, cách tự động hóa email cá nhân hóa]
---

# 🚀 **Tự Động Hóa Email Re-Engage Lead Khó Nhận với AI GPT-4o-mini, Outlook & Google Sheets**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp: Lead "Mất Tầm" Trong Quá Trình Nurturing**
Các sếp đã từng gặp phải tình trạng này chưa?
- **Lead cũ** không phản hồi sau nhiều lần gửi email thông thường.
- **Lịch sử tương tác** (email, tin nhắn) bị phân tán, khó tổng hợp.
- **Tạo email cá nhân hóa** mất nhiều thời gian, không hiệu quả.
- **Tỷ lệ chuyển đổi** từ lead cũ thấp do nội dung email không phù hợp.

**Workflow này giải quyết tất cả!** Sử dụng **AI GPT-4o-mini** để phân tích lịch sử email, tổng hợp thông tin, và tự động tạo **email re-engage cá nhân hóa** trong Outlook. **Không cần code, chỉ cần cấu hình!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** trong việc phân tích và tạo email re-engage.
✅ **Tỷ lệ mở email tăng 30-50%** nhờ nội dung cá nhân hóa từ AI.
✅ **Hoạt động tự động 24/7** mà không cần can thiệp thủ công.
✅ **Tối ưu hóa lead scoring** bằng cách phân tích lịch sử tương tác.
✅ **Không cần kỹ năng code** – chỉ cần cấu hình đơn giản.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu danh sách lead).
✔ **Tài khoản Microsoft Outlook** (để gửi email draft).
✔ **API Key OpenAI** (để sử dụng GPT-4o-mini).
✔ **Danh sách lead cũ** (trong Google Sheets với cột `Email`).

---
:::info[CHUẨN BỊ]
**Bước 1: Chuẩn bị Google Sheets**
- **Copy mẫu spreadsheet** từ [đây](https://docs.google.com/spreadsheets/d/1rQD493GNtTWms6GF0Wracu9Yrm0AR0jxwaWdv8eJbUM/copy).
- **Chỉ cần cột `Email`** (các cột khác sẽ được tự động phân tích).
- **Cấu hình OAuth2** trong n8n:
  - Tạo **Google Sheets OAuth2** credential.
  - Chọn sheet đã copy và đặt tên sheet (ví dụ: `Sheet1`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6919](https://n8n.io/workflows/6919).
- **Import vào n8n Editor**:
  - Nhấn `Import` → Chọn file JSON → **Active workflow**.
- **Hoặc copy/paste JSON** vào `Create Workflow` → `Import from JSON`.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **10 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Start Workflow (Manual Trigger)**
- **Không cần thay đổi**, chỉ dùng để kích hoạt workflow thủ công.

##### **🔹 Node 2: Get Stale Leads (Google Sheets)**
- **Chọn sheet** đã copy từ mẫu.
- **Sheet Name**: `Sheet1` (hoặc tên sheet của bạn).
- **Query**: `SELECT * WHERE Email IS NOT NULL` (lấy tất cả lead có email).

##### **🔹 Node 3: Get All Emails from Outlook (Microsoft Outlook)**
- **Operation**: `getAll`.
- **Filters**:
  - `receivedDateTime ge 2025-01-01T00:00:00Z` (lấy email từ ngày 1/1/2025 trở đi).
  - `sender = {{ $json.Email }}` (động từ Sheets).
- **Lưu ý**: Nếu muốn lấy email cũ hơn, thay đổi ngày trong filter.

##### **🔹 Node 4: Combine into One Field (Aggregate)**
- **Chọn fields cần tổng hợp**:
  - `subject`, `body`, `createdDateTime`.
- **Kết quả**: Tất cả email của lead sẽ được gộp thành **1 chuỗi text**.

##### **🔹 Node 5: Convert Object Fields to Text (Code)**
- **Mã JavaScript**:
  ```js
  return [{
    json: {
      text: items.map(item => JSON.stringify(item.json)).join('\\n'),
    },
  }];
  ```
  - **Đảm bảo không có lỗi syntax**, nếu không workflow sẽ crash.

##### **🔹 Node 6: OpenAI Chat Model (GPT-4o-mini)**
- **Thêm API Key OpenAI**:
  - Tạo **OpenAI API credential** trong n8n.
  - Điền `API Key` từ tài khoản OpenAI.
- **Model**: `gpt-4o-mini` (hoặc `gpt-4` nếu muốn chất lượng cao hơn).
- **Prompt mẫu** (nếu cần chỉnh sửa):
  ```
  Analyze the following email conversation history and suggest a personalized re-engagement email.
  Format output as JSON with:
  - email_subject: "Subject line"
  - email_body: "Personalized email content"
  ```

##### **🔹 Node 7: Structured Output Parser**
- **Không cần chỉnh sửa**, node này tự động phân tích output từ OpenAI.

##### **🔹 Node 8: AI Agent - Re-Engage Lead (LangChain Agent)**
- **Không cần cấu hình**, node này tự động kết nối với OpenAI và Structured Parser.

##### **🔹 Node 9: Save Data to Sheets (Google Sheets)**
- **Operation**: `appendOrUpdate`.
- **Chọn sheet** và **range** (ví dụ: `Sheet1!A1:D100`).
- **Columns**:
  - `Email` (tự động lấy từ Sheets).
  - `email_subject` (từ AI).
  - `email_body` (từ AI).
  - `last_updated` (thời gian cập nhật).

##### **🔹 Node 10: Create Draft Email (Microsoft Outlook)**
- **Resource**: `Draft`.
- **Fields**:
  - **To Recipients**: `={{ $('Google Sheets').item.json.Email }}`
  - **Subject**: `={{ $json.output['email subject'] }}`
  - **Body Content**: `={{ $json.output['email body'] }}`
- **Lưu ý**: Đảm bảo **OAuth2 Outlook** đã được cấu hình trước.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **1 lead mẫu** trong Sheets.
  - Nhấn `Run Workflow` để kiểm tra.
- **Active Workflow**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động gửi email sau khi review**:
   - Thêm **node Microsoft Outlook (Send)** sau draft.
   - Sử dụng **Webhook** để kích hoạt khi email đã được review.

2. **Lưu log hoạt động**:
   - Thêm **node Slack/Telegram** để thông báo khi workflow hoàn thành.

3. **Tích hợp với CRM**:
   - Nếu dùng **HubSpot/Salesforce**, thêm node tương ứng để cập nhật lead sau khi re-engage.

4. **Tối ưu hóa prompt OpenAI**:
   - Nếu muốn email **chuyên nghiệp hơn**, chỉnh sửa prompt:
     ```
     You are a professional sales consultant. Write a highly personalized re-engagement email based on the conversation history.
     ```

5. **Lọc lead hiệu quả hơn**:
   - Thêm **node Code** trước khi lấy email từ Outlook để lọc lead có `last_contact < 30 days`.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **nurturing lead thủ công**, đồng thời **tăng tỷ lệ chuyển đổi** nhờ **email cá nhân hóa từ AI**. **Không cần code, chỉ cần cấu hình đơn giản!**

**Hãy áp dụng ngay và xem kết quả trong vòng 24h!**
👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/6919)**
👉 **[Đăng ký VPS để self-host](https://tino.vn/vps-n8n?affid=388)**

---
**Cần hỗ trợ?** Liên hệ:
📧 **Robert Breen** – [robert@ynteractive.com](mailto:robert@ynteractive.com)
🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)