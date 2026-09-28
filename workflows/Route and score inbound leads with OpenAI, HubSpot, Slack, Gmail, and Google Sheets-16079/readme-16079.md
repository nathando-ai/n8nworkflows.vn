---
title: "🚀 Tự Động Hóa & Đánh Giá Lead Inbound Với AI (OpenAI), HubSpot, Slack, Gmail & Google Sheets – Giảm Thời Gian Triage 90%"
description: "Workflow tự động nhận, đánh giá, phân loại và chuyển giao lead mới đến sales rep phù hợp ngay lập tức, giảm thiểu công việc thủ công và tối ưu hóa quy trình bán hàng. Sử dụng AI để tạo email outreach cá nhân hóa, tránh trùng lặp và theo dõi toàn bộ quá trình trên Google Sheets."
slug: "tieu-dong-hoa-lead-inbound-voi-openai-hubspot"
tags: [n8n, automation, lead-generation, ai-multimodal, hubspot, slack, gmail, google-sheets, openai]
keywords: [tự động hóa lead inbound, n8n workflow, phân loại lead bằng AI, HubSpot automation, Slack notification, email outreach tự động, Google Sheets logging]
---

# 🚀 **Tự Động Hóa & Đánh Giá Lead Inbound Với AI: Giảm Thiểu Công Việc Triage Cho Sales Team**

Bạn đã bao giờ phải mất **giờ đồng hồ** mỗi ngày để phân loại, đánh giá và chuyển giao lead mới cho các sales rep? Hay phải lo lắng rằng một số lead **trùng lặp** hoặc **không phù hợp** sẽ bị bỏ qua? Với workflow này, các sếp sẽ **tự động hóa toàn bộ quy trình**, từ nhận lead đến phân loại, đánh giá bằng AI, và chuyển giao ngay lập tức đến sales rep phù hợp – **không cần viết một dòng code nào!**

Workflow này kết hợp **OpenAI (AI Multimodal)**, **HubSpot**, **Slack**, **Gmail** và **Google Sheets** để:
✅ **Nhận và kiểm tra** lead mới từ form hoặc CRM.
✅ **Đánh giá lead** dựa trên nguồn, kích thước công ty và tín hiệu ý định.
✅ **Tránh trùng lặp** bằng kiểm tra HubSpot.
✅ **Phân loại và chuyển giao** lead đến sales rep đúng vùng miền và độ ưu tiên.
✅ **Tạo email outreach cá nhân hóa** bằng AI (OpenAI).
✅ **Gửi thông báo Slack** và **email** cho rep cùng với bản nháp email.
✅ **Lưu log toàn bộ quá trình** trên Google Sheets để báo cáo.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** của sales team trong việc triage lead thủ công.
- **Chuyển giao lead ngay lập tức** đến rep phù hợp, không để lead "ngủ" trong hệ thống.
- **Tránh trùng lặp lead** bằng kiểm tra HubSpot tự động.
- **Email outreach cá nhân hóa** bằng AI, tăng tỷ lệ mở và phản hồi.
- **Theo dõi toàn bộ quá trình** trên Google Sheets, dễ dàng báo cáo và phân tích.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản và API Key**:
  - **HubSpot**: Tài khoản Developer và API Key (tạo tại [HubSpot Developer Portal](https://developers.hubspot.com/)).
  - **Slack**: Token OAuth và Channel ID (tạo tại [Slack API](https://api.slack.com/)).
  - **Gmail**: Tài khoản Google và OAuth 2.0 Client ID (tạo tại [Google Cloud Console](https://console.cloud.google.com/)).
  - **Google Sheets**: File Google Sheets và ID Sheet (tạo tại [Google Sheets](https://sheets.google.com/)).
  - **OpenAI**: API Key (tạo tại [OpenAI Platform](https://platform.openai.com/)).
  - **Webhook URL**: URL của n8n để nhận lead (cấu hình tại **Webhook — Inbound Lead**).
- **Tham số cấu hình**:
  - **Tên Sheet Google**: Điền vào node **Google Sheets — Log Lead**.
  - **Tên Channel Slack**: Cập nhật trong tất cả node **Slack**.
  - **Địa chỉ email mặc định**: Để gửi email outreach (cấu hình tại **Gmail — Email Rep with Draft**).
  - **Bản nháp email mẫu**: Cập nhật tại **HTTP — Draft Outreach Email** (nếu cần).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Workflow](https://n8n.io/workflows/16079) và tải file JSON.
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON tải xuống.
   *Hoặc*:
   - Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/16079) (nhấn **Export**).
   - Trong **n8n Editor**, nhấn **Import** → **Paste JSON**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **19 node** quan trọng, các sếp cần chú ý cấu hình sau:

#### **A. Webhook — Inbound Lead**
- **Path**: Đảm bảo giữ nguyên `inbound-lead`.
- **HTTP Method**: POST (không thay đổi).
- **Credentials**: Không cần thêm (n8n sẽ tự động nhận request).

#### **B. Validate Payload (Code Node)**
- **Lógica**: Kiểm tra các trường bắt buộc như `name`, `email`, `source`, `companySize`.
- **Nếu thiếu trường**: Workflow sẽ trả về **400 Bad Request** (node **Respond 400 — Bad Request**).

#### **C. Normalise Lead Data (Set Node)**
- **Cấu hình**:
  - Đảm bảo các trường như `name`, `email`, `source`, `region`, `companySize` được định nghĩa rõ ràng.
  - Thêm trường `leadScore` (sẽ được tính toán sau).

#### **D. Score & Route Lead (Code Node)**
- **Lógica**: Đánh giá lead dựa trên:
  - **Nguồn lead** (ví dụ: `organic`, `paid`, `referral`).
  - **Kích thước công ty** (`small`, `medium`, `large`).
  - **Tín hiệu ý định** (ví dụ: `email_opened`, `website_visited`).
- **Cách cập nhật**:
  - Mở node **Score & Route Lead** → **Edit Code**.
  - Sửa logic để phù hợp với quy tắc đánh giá của doanh nghiệp (ví dụ:
    ```javascript
    const score = {
      "organic": 10,
      "paid": 15,
      "referral": 20,
      "small": 5,
      "medium": 10,
      "large": 15
    };
    const leadScore = score[lead.source] + score[lead.companySize];
    $input.all = { ...$input.all, leadScore };
    ```
  - Lưu và kiểm tra lại logic.

#### **E. HubSpot — Check Duplicate**
- **Credentials**: Chọn tài khoản HubSpot đã cấu hình trước.
- **Operation**: Giữ nguyên `search`.
- **Query**: Cấu hình để tìm kiếm theo `email` (trường mặc định).
  - Ví dụ:
    ```json
    {
      "property": "email",
      "value": "{{$json.email}}"
    }
    ```

#### **F. Merge Duplicate Flag (Code Node)**
- **Lógica**: Kiểm tra kết quả từ HubSpot:
  - Nếu có kết quả (`results.length > 0`), đặt `isDuplicate = true`.
  - Nếu không, đặt `isDuplicate = false`.

#### **G. Slack — Duplicate Warning**
- **Credentials**: Chọn tài khoản Slack đã cấu hình.
- **Channel**: Điền tên channel (ví dụ: `#sales-alerts`).
- **Message Template**: Cập nhật nội dung cảnh báo trùng lặp (ví dụ:
  ```
  *⚠️ Duplicate Lead Detected!*
  Lead với email **{{$json.email}}** đã tồn tại trong HubSpot. Vui lòng kiểm tra lại.
  ```

#### **H. Hot or Warm? (If Node)**
- **Điều kiện**: Phân loại lead dựa trên `leadScore`:
  - **Hot**: `leadScore >= 30` (lead ưu tiên cao).
  - **Warm**: `leadScore >= 15` (lead trung bình).
  - **Cold**: `leadScore < 15` (lead thấp).

#### **I. HubSpot — Upsert Contact**
- **Credentials**: Chọn tài khoản HubSpot.
- **Properties**: Cập nhật các trường cần tạo/ cập nhật (ví dụ: `name`, `email`, `source`, `companySize`, `leadScore`).
- **Operation**: Giữ nguyên `upsert`.

#### **J. HTTP — Draft Outreach Email (OpenAI)**
- **Credentials**: Chọn `httpHeaderAuth` (nếu đã cấu hình).
- **URL**: Đảm bảo là API endpoint của OpenAI (ví dụ: `https://api.openai.com/v1/chat/completions`).
- **Headers**:
  - `Authorization: Bearer {{$credentials.openai.apiKey}}`.
  - `Content-Type: application/json`.
- **Body (Prompt)**:
  Cập nhật prompt để AI tạo email outreach cá nhân hóa. Ví dụ:
  ```json
  {
    "model": "gpt-4",
    "messages": [
      {
        "role": "system",
        "content": "Bạn là một chuyên gia bán hàng AI. Tạo email outreach cá nhân hóa cho lead mới."
      },
      {
        "role": "user",
        "content": "Lead: {{$json.name}}, Email: {{$json.email}}, Công ty: {{$json.company}}, Nguồn: {{$json.source}}, Địa khu: {{$json.region}}, Điểm lead: {{$json.leadScore}}"
      }
    ],
    "temperature": 0.7
  }
  ```

#### **K. Gmail — Email Rep with Draft**
- **Credentials**: Chọn tài khoản Gmail đã cấu hình.
- **To**: Địa chỉ email của sales rep (cần định nghĩa trong logic **Score & Route Lead**).
- **Subject**: Cập nhật chủ đề email (ví dụ: `📩 Lead mới: {{$json.name}} (Điểm: {{$json.leadScore}})`).
- **Body**: Sử dụng kết quả từ OpenAI (trường `response` trong node **HTTP — Draft Outreach Email**).

#### **L. Google Sheets — Log Lead**
- **Credentials**: Chọn tài khoản Google Sheets.
- **Sheet ID**: Điền ID Sheet của file Google Sheets (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
- **Range**: Điền tên sheet và phạm vi (ví dụ: `Sheet1!A1`).
- **Data**: Đảm bảo các trường như `name`, `email`, `source`, `leadScore`, `isDuplicate`, `assignedRep`, `date` được append.

#### **M. Respond to Webhook**
- **Message**: Cập nhật nội dung phản hồi cho người gửi lead (ví dụ:
  ```
  {
    "status": "success",
    "message": "Lead đã được nhận và xử lý thành công!",
    "leadId": "{{$json.id}}"
  }
  ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một lead mẫu đến **Webhook — Inbound Lead** (ví dụ bằng Postman hoặc form test).
   - Kiểm tra các node liên quan (Slack, Gmail, HubSpot, Google Sheets) để đảm bảo hoạt động đúng.
2. **Bật Active**:
   - Nhấn **Active** trên workflow trong n8n Editor.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Zapier/Integromat**: Nếu lead đến từ nhiều nguồn (ví dụ: Facebook Lead Ads, LinkedIn), sử dụng Zapier để chuyển lead đến Webhook của n8n.
- **Lưu log lỗi**: Thêm node **Slack — Error Alert** để báo cáo lỗi nếu workflow gặp vấn đề.
- **Báo cáo định kỳ**: Sử dụng **Google Sheets + Apps Script** để tạo báo cáo tự động về lead mới, lead trùng lặp, và tỷ lệ chuyển đổi.
- **Cập nhật động AI**: Nếu sử dụng OpenAI, cập nhật prompt để AI học hỏi từ phản hồi của sales team.
- **Phân loại lead theo vùng miền**: Cập nhật logic trong **Score & Route Lead** để phân loại lead theo vùng miền (ví dụ: `Vietnam`, `USA`, `Europe`).
- **Gửi email nhắc nhở**: Thêm node **Gmail** để gửi email nhắc nhở cho rep nếu lead không được xử lý trong 24h.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quy trình nhận, đánh giá và chuyển giao lead cho sales team, **giảm thiểu công việc thủ công** và **tăng hiệu quả bán hàng**. Với sự hỗ trợ của **AI (OpenAI)**, lead sẽ được **đánh giá chính xác** và **email outreach cá nhân hóa**, giúp tăng tỷ lệ chuyển đổi.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình các credentials.
2. **Test với lead mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và theo dõi kết quả trên Slack, Gmail và Google Sheets.

Nếu các sếp cần hỗ trợ thêm về **cấu hình cụ thể** hoặc **cập nhật logic**, hãy liên hệ với **iTechNotion** (tác giả của workflow) qua [website](https://itechnotion.com/) hoặc [LinkedIn](https://linkedin.com/in/avkashkakdiya).

---
:::note[CHÚ Ý]
- Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
- **Không sử dụng phiên bản miễn phí** của n8n.io (có giới hạn node và lưu trữ).
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::