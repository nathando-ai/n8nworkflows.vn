---
title: "🚀 Tự động chấm điểm RSVP sự kiện bằng GPT‑4o‑mini, đồng bộ Leads vào HubSpot & nhận thông báo Slack"
description: "Workflow n8n tự động thu thập RSVP, dùng GPT‑4o‑mini tính điểm tiềm năng, đồng bộ Leads vào HubSpot và gửi cảnh báo Slack ngay lập tức."
slug: "tu-dong-cham-diem-rsvp-hubspot-slack-gpt4o-mini"
tags: [n8n, automation, no-code, lead-generation, ai-summarization, hubspot, slack]
keywords: [n8n workflow, tự động hóa, GPT-4o-mini, HubSpot, Slack, lead scoring]
---

# 🚀 Tự động chấm điểm RSVP sự kiện bằng GPT‑4o‑mini, đồng bộ Leads vào HubSpot & nhận thông báo Slack

Khi tổ chức sự kiện, việc thu thập và đánh giá RSVP (đăng ký tham dự) thường phải làm thủ công: sao chép dữ liệu từ Google Sheet, tính điểm tiềm năng, tạo contact trong CRM và cuối cùng gửi thông báo cho đội sales. Quy trình này tốn thời gian, dễ sai sót và không thể phản hồi nhanh với những lead “nóng”.  

**Workflow này** sẽ tự động hoá toàn bộ chuỗi: nhận RSVP qua webhook → lưu vào Google Sheet → dùng GPT‑4o‑mini (OpenAI) chấm điểm lead → nếu điểm cao thì tạo/ cập nhật contact trong HubSpot → gửi tin nhắn Slack báo cho team ngay lập tức. Tất cả không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Loại bỏ công đoạn sao chép và tính điểm thủ công.  
- **Độ chính xác cao**: GPT‑4o‑mini phân tích nội dung RSVP, đưa ra điểm số dựa trên tiêu chí tùy chỉnh.  
- **Phản hồi nhanh**: Khi lead đạt ngưỡng, Slack thông báo ngay, giúp sales không bỏ lỡ cơ hội.  
- **Dữ liệu đồng bộ**: Leads tự động được tạo/ cập nhật trong HubSpot, luôn luôn “up‑to‑date”.  
- **Hoạt động 24/7**: Workflow chạy liên tục, không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (Self‑hosted hoặc Cloud).  
- **Webhook URL** (được tạo trong n8n, sẽ dùng làm endpoint nhận RSVP).  
- **Google Workspace**: tài khoản có quyền tạo và chỉnh sửa Google Sheet.  
- **OpenAI API Key** (có quyền truy cập GPT‑4o‑mini).  
- **HubSpot API Key / OAuth** (để tạo/ cập nhật contact).  
- **Slack Workspace** + **Incoming Webhook** hoặc **Bot Token** để gửi tin nhắn kênh.  
- (Tùy chọn) **Sticky Note** chỉ để ghi chú trong workflow, không cần credentials.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n > Workflows** → **Import**.  
2. Tải file `score-rsvp-gpt4o-mini-hubspot-slack.json` (được cung cấp ở phần cuối README) **hoặc** copy toàn bộ JSON và dán vào ô **Paste JSON**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node chính và các tham số cần cấu hình:

| Node | Mô tả | Tham số cần điền / Credential |
|------|------|--------------------------------|
| **Webhook** | Nhận dữ liệu RSVP (POST) từ form hoặc công cụ đăng ký. | **HTTP Method**: `POST` <br> **Path**: `/rsvp` (có thể tùy chỉnh). |
| **Google Sheets** | Ghi lại RSVP gốc vào bảng “RSVP Raw”. | **Credential**: Google OAuth <br> **Spreadsheet ID**: ID của file Google Sheet <br> **Sheet Name**: `RawData`. |
| **Set** (Prepare Data) | Định dạng lại dữ liệu (tên, email, nội dung câu trả lời…) để truyền cho OpenAI. | Không cần credential, chỉ mapping các trường. |
| **@n8n/n8n-nodes-langchain.openAi** (GPT‑4o‑mini) | Gửi prompt tới OpenAI, nhận điểm lead (0‑100). | **Credential**: OpenAI API Key <br> **Model**: `gpt-4o-mini` <br> **Prompt**: <br>```text\nBạn là chuyên gia lead scoring. Đánh giá mức độ quan tâm của người đăng ký dựa trên nội dung sau và trả về một số điểm từ 0‑100.\n\nTên: {{ $json["name"] }}\nEmail: {{ $json["email"] }}\nNội dung: {{ $json["message"] }}\n``` |
| **If** (Score Threshold) | Kiểm tra điểm >= 70 (có thể tùy chỉnh). | **Condition**: `{{$json["score"]}} >= 70` |
| **HubSpot** (Create/Update Contact) | Tạo hoặc cập nhật contact trong HubSpot với trường “Lead Score”. | **Credential**: HubSpot API Key/OAuth <br> **Object Type**: `Contact` <br> **Email**: `{{ $json["email"] }}` <br> **Properties**: `firstname`, `lastname`, `lead_score` (điểm). |
| **Slack** (Alert) | Gửi tin nhắn kênh #sales-alerts khi lead đạt ngưỡng. | **Credential**: Slack Bot Token hoặc Incoming Webhook <br> **Channel**: `#sales-alerts` <br> **Message**: <br>```text\n🚀 Lead mới! \n*Tên*: {{ $json["name"] }} \n*Email*: {{ $json["email"] }} \n*Score*: {{ $json["score"] }}\n``` |
| **Sticky Note** | Ghi chú mô tả workflow (không ảnh hưởng tới chạy). | Không cần cấu hình. |

> **⚠️ Lưu ý quan trọng**  
> - Đảm bảo **OpenAI quota** đủ để xử lý số lượng RSVP dự kiến.  
> - Kiểm tra **cấp quyền** của Google Sheet (Editor) và HubSpot (Contacts → Edit).  
> - Khi sử dụng Slack Bot Token, hãy cấp quyền `chat:write` cho bot.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một POST mẫu tới webhook (`https://<your-n8n-domain>/webhook/rsvp`) với payload JSON:  
   ```json
   {
     "name": "Nguyễn Văn A",
     "email": "a.nguyen@example.com",
     "message": "Tôi rất quan tâm tới buổi hội thảo về AI."
   }
   ```  
2. Kiểm tra log từng node trong n8n để xác nhận:  
   - Dữ liệu đã được ghi vào Google Sheet.  
   - GPT‑4o‑mini trả về điểm (ví dụ: 82).  
   - HubSpot tạo contact và Slack nhận tin nhắn.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi email follow‑up**: Thêm node **Email Send** sau node HubSpot để gửi email chào mừng dựa trên điểm.  
- **Lưu log chi tiết**: Dùng node **Google Drive** hoặc **Postgres** để lưu toàn bộ payload + score, phục vụ phân tích sau này.  
- **Đa kênh thông báo**: Thêm node **Telegram** hoặc **Microsoft Teams** để mở rộng kênh cảnh báo.  
- **Dynamic scoring**: Cập nhật prompt trong node OpenAI để phản ánh các tiêu chí mới (ví dụ: “độ ưu tiên dựa trên vị trí địa lý”).  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình xử lý RSVP**, từ việc thu thập, chấm điểm bằng AI, đồng bộ CRM tới việc thông báo nhanh cho đội sales. Không còn mất công sức nhập liệu thủ công, không còn bỏ lỡ lead “nóng”. Hãy triển khai ngay hôm nay, để tập trung vào việc **chốt deal** thay vì quản lý dữ liệu!

---  

**File JSON để import** (đặt tên `score-rsvp-gpt4o-mini-hubspot-slack.json`):

```json
{
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "rsvp",
        "options": {}
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "sheetId": "YOUR_GOOGLE_SHEET_ID",
        "range": "RawData!A1",
        "valueInputMode": "RAW",
        "options": {}
      },
      "name": "Google Sheets",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 1,
      "position": [500, 300],
      "credentials": {
        "googleApi": "Google OAuth"
      }
    },
    {
      "parameters": {
        "values": {
          "string": [
            {
              "name": "name",
              "value": "={{$json[\"name\"]}}"
            },
            {
              "name": "email",
              "value": "={{$json[\"email\"]}}"
            },
            {
              "name": "message",
              "value": "={{$json[\"message\"]}}"
            }
          ]
        },
        "options": {}
      },
      "name": "Set Prepare Data",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [750, 300]
    },
    {
      "parameters": {
        "model": "gpt-4o-mini",
        "prompt": "Bạn là chuyên gia lead scoring. Đánh giá mức độ quan tâm của người đăng ký dựa trên nội dung sau và trả về một số điểm từ 0‑100.\n\nTên: {{ $json[\"name\"] }}\nEmail: {{ $json[\"email\"] }}\nNội dung: {{ $json[\"message\"] }}",
        "temperature": 0,
        "maxTokens": 50,
        "options": {}
      },
      "name": "GPT‑4o‑mini Score",
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1,
      "position": [1000, 300],
      "credentials": {
        "openAiApi": "OpenAI API"
      }
    },
    {
      "parameters": {
        "conditions": {
          "boolean": [
            {
              "value1": "={{$json[\"score\"]}}",
              "operation": "greaterOrEqual",
              "