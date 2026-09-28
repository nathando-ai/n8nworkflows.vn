---
title: "🤖 Kết nối Retell Voice Agent với Hàm Tùy Chỉnh bằng n8n: Tự Động Hóa Trải Nghiệm Hỗ Trợ Khách Hàng Thực Tế"
description: "Workflow này cho phép các sếp kết nối Retell Voice Agent với logic tùy chỉnh trong n8n thông qua Custom Functions, tự động xử lý yêu cầu khách hàng (đặt phòng, cập nhật CRM, trả lời AI) và trả về phản hồi động trong thời gian thực. Giúp tiết kiệm 80% thời gian hỗ trợ và nâng cao trải nghiệm khách hàng."
slug: ket-noi-retell-voice-agent-voi-n8n
tags: [n8n, automation, retell-ai, voice-agent, custom-functions, ai-agent, no-code]
keywords: [n8n workflow retell, tự động hóa hỗ trợ khách hàng, kết nối retell với n8n, custom function retell, tự động hóa thoại AI, giải pháp hỗ trợ khách hàng không code]
---

# 🚀 Kết Nối Retell Voice Agent với Hàm Tùy Chỉnh trong n8n: Tự Động Hóa Hỗ Trợ Khách Hàng Thực Tế

### 🎯 **Nỗi Đau Của Các Sếp**
Hiện nay, khi khách hàng gọi điện để đặt phòng, đặt vé hoặc yêu cầu hỗ trợ, đội ngũ hỗ trợ phải:
- **Lắng nghe và ghi lại thông tin thủ công** (rủi ro sai sót cao).
- **Tìm kiếm thông tin trên nhiều hệ thống** (CRM, booking engine, database) để trả lời chính xác.
- **Phản hồi chậm** do phải chuyển đổi giữa nhiều tab và công cụ.
- **Không thể cá nhân hóa** trải nghiệm theo từng khách hàng.

**Kết quả?** Thời gian phản hồi kéo dài, khách hàng mất niềm tin, và chi phí nhân sự tăng cao.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
- **Tự động hóa 100% quy trình hỗ trợ** qua Retell Voice Agent, giảm thời gian phản hồi xuống **giây chứ không phải phút**.
- **Trả lời khách hàng chính xác và động** bằng cách kết nối với API, CRM, hoặc AI (LLM) trong thời gian thực.
- **Cập nhật thông tin ngay lập tức** vào hệ thống (ví dụ: xác nhận đặt phòng, thêm khách hàng vào CRM).
- **Tiết kiệm 80% thời gian** của đội ngũ hỗ trợ, chuyển hướng họ sang công việc có giá trị cao hơn.
- **Nâng cao trải nghiệm khách hàng** với phản hồi tự động, cá nhân hóa và không cần chờ đợi.

---
### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Retell AI** (đăng ký tại [retellai.com](https://www.retellai.com/)).
2. **Một Retell Voice Agent** có **Custom Function** trong flow hội thoại (sẵn sàng để import từ [template này](https://drive.google.com/file/d/1rAcsNz-f8SyuOxO0VJ_84oPscYFpir4-/view?usp=sharing)).
3. **URL Webhook của n8n** (sẽ được tạo khi import workflow).
4. **(Tùy chọn)** API Key hoặc credentials để kết nối với:
   - Hệ thống booking (ví dụ: Booking.com, Airbnb API).
   - CRM (HubSpot, Salesforce, Zoho).
   - API dữ liệu (Google Sheets, Airtable, hoặc LLM như Mistral AI, GPT-4).
5. **Sẵn sàng test** với một cuộc gọi mẫu hoặc chatbot để kiểm tra logic.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### 1. **Import Workflow từ File JSON**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/3805](https://n8n.io/workflows/3805) hoặc copy JSON dưới đây.
- **Bước 2:** Mở **n8n Editor** (trên máy chủ tự host hoặc n8n.cloud) và chọn **Import Workflow**.
- **Bước 3:** Dán JSON vào và nhấn **Import**.

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "hotel-retell-template",
        "httpMethod": "POST"
      },
      "name": "Webhook",
      "type": "webhook",
      "typeVersion": 1,
      "disabled": false,
      "statusCode": 200,
      "responseData": "",
      "wildcard": false
    },
    {
      "parameters": {},
      "name": "Respond to Webhook",
      "type": "respondToWebhook",
      "typeVersion": 1,
      "disabled": false
    },
    {
      "parameters": {
        "property": "",
        "values": {
          "json": {
            "response": "= $input.all()"
          }
        },
        "options": {}
      },
      "name": "[Replace me!] Set response",
      "type": "set",
      "typeVersion": 1,
      "disabled": false
    }
  ],
  "connections": [
    {
      "element": "webhook",
      "structure": "main",
      "connection": "main",
      "type": "direct",
      "from": "webhook",
      "to": "[Replace me!] Set response"
    },
    {
      "element": "[Replace me!] Set response",
      "structure": "main",
      "connection": "main",
      "type": "direct",
      "from": "[Replace me!] Set response",
      "to": "Respond to Webhook"
    }
  ]
}
```

#### 2. **Cấu Hình Cần Thay Đổi (BẮT BUỘC)**
Sau khi import, các sếp phải **cấu hình node `[Replace me!] Set response`** để xử lý logic tùy chỉnh. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu Hình Webhook (Node "Webhook")**
- **Đã tự động tạo** khi import, không cần chỉnh sửa.
- **URL Webhook** sẽ là: `https://[your-n8n-instance].app.n8n.cloud/webhook/hotel-retell-template`
  *(Thay `[your-n8n-instance]` bằng tên máy chủ của bạn, ví dụ: `https://n8n.agentstudio.com/webhook/hotel-retell-template`)*

##### **B. Thay Đổi Logic trong Node "Set"**
Node này **trả về phản hồi** cho Retell Voice Agent. Các sếp có thể:
1. **Trả về dữ liệu gốc** (giản đơn):
   - Để mặc định `response: = $input.all()` (trả về toàn bộ dữ liệu nhận được từ Retell).
   - Ví dụ: Nếu Retell gửi dữ liệu `{ "name": "John", "room": "Deluxe" }`, n8n sẽ trả về chính dữ liệu đó.

2. **Xử lý logic tùy chỉnh** (phức tạp):
   - **Thêm node LLM** (ví dụ: Mistral AI, GPT-4) để sinh phản hồi động:
     ```plaintext
     - Thêm node `n8n-nodes-ai.mistral` (hoặc `n8n-nodes-ai.openai`).
     - Cấu hình Prompt:
       ```
       "Tôi là trợ lý hỗ trợ khách hàng. Dữ liệu khách hàng là: {{ $input.all() }}.
       Hãy trả lời ngắn gọn và thân thiện để xác nhận đặt phòng thành công."
       ```
     - Kết nối node LLM với node `Set` để lấy phản hồi từ AI.
   - **Kết nối với API** (ví dụ: kiểm tra sẵn phòng):
     ```plaintext
     - Thêm node `n8n-nodes-base.httpRequest` để gọi API Booking.com.
     - Xử lý phản hồi API và trả về kết quả cho node `Set`.
     ```
   - **Cập nhật CRM** (ví dụ: thêm khách hàng vào HubSpot):
     ```plaintext
     - Thêm node `n8n-nodes-base.httpRequest` để gọi API HubSpot.
     - Gửi dữ liệu khách hàng vào CRM.
     ```

##### **C. Cấu Hình Node "Respond to Webhook"**
- Node này **chỉ định phản hồi cuối cùng** gửi về Retell.
- **Không cần chỉnh sửa** nếu đã cấu hình node `Set` đúng.

---
#### 3. **Kích Hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một request POST đến URL Webhook với dữ liệu JSON mẫu:
     ```json
     {
       "name": "John Doe",
       "room": "Deluxe",
       "checkin": "2024-12-15",
       "checkout": "2024-12-18",
       "callId": "abc123"
     }
     ```
   - Kiểm tra phản hồi từ node `Respond to Webhook` trong n8n Editor.

2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active** trên n8n Editor.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### 1. **Kết Nối với Slack/Telegram để Log**
- Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node `Set` để:
  ```plaintext
  - Gửi thông báo log mỗi khi Custom Function được gọi.
  - Ví dụ: `{"callId": "{{ $json.callId }}", "action": "Booking confirmed", "time": "{{ $now.toISOString() }}"}`
  ```

#### 2. **Tạo Báo Cáo Định Kỳ**
- Thêm node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.airtable` để:
  ```plaintext
  - Lưu tất cả yêu cầu hỗ trợ vào bảng Google Sheets.
  - Ví dụ: Dữ liệu sẽ tự động cập nhật mỗi khi có cuộc gọi mới.
  ```

#### 3. **Sử Dụng AI để Phân Loại Yêu Cầu**
- Thêm node `n8n-nodes-ai.mistral` để phân loại yêu cầu khách hàng:
  ```plaintext
  - Prompt:
    ```
    "Phân loại yêu cầu sau đây thành một trong các loại: đặt phòng, hủy phòng, yêu cầu dịch vụ, khiếu nại.
    Dữ liệu: {{ $input.all() }}."
    ```
  - Kết nối với logic khác nhau dựa trên kết quả phân loại.
  ```

#### 4. **Tích Hợp với Calendar (Google Calendar, Outlook)**
- Thêm node `n8n-nodes-base.googleCalendar` để:
  ```plaintext
  - Tự động tạo sự kiện cho khách hàng (ví dụ: check-in, check-out).
  - Ví dụ: Nếu khách hàng đặt phòng, hệ thống sẽ tự động thêm sự kiện vào lịch của họ.
  ```

---
### 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** để các sếp:
✅ **Tự động hóa hoàn toàn** quy trình hỗ trợ khách hàng qua Retell Voice Agent.
✅ **Kết nối với AI, API, CRM** để trả lời động và chính xác.
✅ **Tiết kiệm thời gian và chi phí** cho đội ngũ hỗ trợ.

**Bước tiếp theo:**
1. **Import workflow** và cấu hình URL Webhook trong Retell.
2. **Thêm logic tùy chỉnh** (LLM, API, CRM) vào node `Set`.
3. **Test và deploy** để tự động hóa hỗ trợ khách hàng ngay hôm nay!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ thêm?** Liên hệ với [Agent Studio](mailto:hello@agentstudio.io) để phân tích chi tiết cho Retell Agent của bạn! 🚀