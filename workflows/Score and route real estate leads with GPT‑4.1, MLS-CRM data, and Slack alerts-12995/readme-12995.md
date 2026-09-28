---
title: "🚀 Tự Động Hóa & Đánh Giá Lead Đất Đai với GPT-4.1, Dữ Liệu MLS-CRM & Cảnh Báo Slack (AI RAG)"
description: "Workflow tự động hóa 100% không code để đánh giá, phân loại và phân phối lead đất đai từ nhiều nguồn (MLS, CRM, email) với AI GPT-4.1, lưu trữ trong vector database và cảnh báo Slack thời gian thực. Giúp các sếp tiết kiệm 80% thời gian phân tích lead và tăng tỷ lệ chuyển đổi thành công."
slug: "tieu-dong-hoa-lead-dat-dai-voi-gpt-4-1"
tags: [n8n, automation, ai-rag, real-estate, lead-scoring, slack-integration, openai]
keywords: [n8n workflow đất đai, tự động hóa lead đất đai, GPT-4.1 phân loại lead, AI đánh giá lead bất động sản, cảnh báo Slack lead cao cấp, vector database cho lead]
---

# 🚀 **Tự Động Hóa & Đánh Giá Lead Đất Đai với AI GPT-4.1, MLS-CRM và Cảnh Báo Slack**

## **🔍 Nỗi Đau Của Các Sếp Đất Đai Hiện Nay**
Hàng ngày, các sếp bất động sản phải:
- **Lọc hàng trăm lead** từ MLS, CRM, email, và mạng xã hội để tìm ra những cơ hội thực sự.
- **Phân loại lead** theo độ ưu tiên (cao, trung, thấp) dựa trên nhiều tiêu chí phức tạp (tình trạng tài chính, nhu cầu cụ thể, thời gian phản hồi).
- **Phân công lead** cho các agent phù hợp, nhưng lại phải làm thủ công → **tốn thời gian, dễ sai sót và mất cơ hội**.
- **Bỏ lỡ lead cao cấp** vì không có hệ thống cảnh báo tự động (Slack/Email).

**Workflow này giải quyết tất cả!** Sử dụng **AI GPT-4.1** để tự động:
✅ **Đánh giá lead** theo tiêu chí chuyên nghiệp (tình hình tài chính, nhu cầu mua/bán, độ ưu tiên).
✅ **Phân loại lead** thành **cao cấp, trung bình, thấp** với độ chính xác cao.
✅ **Phân phối lead** tự động cho agent phù hợp (vía Slack/Email).
✅ **Lưu trữ lead** trong **vector database** để tra cứu nhanh và phân tích sentiment.
✅ **Cảnh báo Slack** khi có lead cao cấp mới để các sếp phản hồi kịp thời.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** phân tích lead thủ công.
- **Độ chính xác cao** (AI GPT-4.1 đánh giá lead theo tiêu chí chuyên nghiệp).
- **Phân loại tự động** lead thành **cao cấp, trung bình, thấp** với logic AI.
- **Phân phối lead** tự động cho agent phù hợp (vía Slack/Email).
- **Cảnh báo Slack thời gian thực** khi có lead cao cấp mới.
- **Lưu trữ lead** trong **vector database** để tra cứu và phân tích sentiment.
- **Báo cáo tự động** thống kê lead hàng ngày.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản API OpenAI** (để sử dụng GPT-4.1, Embeddings, Sentiment Analysis).
✔ **Tài khoản Slack** (để cảnh báo lead cao cấp).
✔ **Database PostgreSQL** (để lưu trữ lead và dữ liệu phân tích).
✔ **Nguồn lead** từ:
   - **MLS (Multiple Listing Service)** hoặc các portal bất động sản (Zillow, Realtor.com).
   - **CRM** (HubSpot, Salesforce, Pipedrive).
   - **Email/Social Media** (Lead từ form đăng ký, LinkedIn, Facebook).
✔ **Tài khoản Email** (để gửi thông báo phân công lead cho agent).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/12995](https://n8n.io/workflows/12995) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc phiên bản cloud).
3. **Nhấp vào "Import"** → Chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** → Nhấp vào **"Import"** → Chọn **"Paste JSON"**.
3. **Dán JSON** và nhấp **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Schedule Trigger" (Động cơ kích hoạt định kỳ)**
- **Cấu hình thời gian chạy**:
  - **Cron expression**: `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Hoặc**: `*/30 * * * *` (chạy mỗi 30 phút, phù hợp cho lead thời gian thực).

#### **🔹 Node "Fetch Leads from MLS/Portals" & "Fetch Leads from CRM/Email/Social" (Lấy lead từ nhiều nguồn)**
- **Tham số HTTP Request**:
  - **URL**: Điền API endpoint của **MLS** (ví dụ: `https://api.mls.com/leads`) hoặc **CRM** (HubSpot: `https://api.hubapi.com/crm/v3/objects/leads`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (nếu cần)**: JSON request để lấy lead (ví dụ: `{"limit": 100}`).

#### **🔹 Node "OpenAI Model - Enrichment/Routing/Scoring" (AI GPT-4.1)**
- **Cấu hình OpenAI API**:
  - **Credentials**: Chọn `openAiApi` (đã cấu hình trước trong n8n).
  - **Model**: Đảm bảo chọn `gpt-4.1-mini` (hoặc `gpt-4` nếu có budget).
  - **Prompt (cần chỉnh sửa theo nhu cầu)**:
    ```json
    {
      "role": "system",
      "content": "Bạn là một chuyên gia đánh giá lead bất động sản. Hãy phân tích lead theo các tiêu chí sau:\n
      1. Tình hình tài chính (có khả năng mua/bán không?)\n
      2. Nhu cầu cụ thể (mua nhà mới, tái đầu tư, bán nhanh)\n
      3. Độ ưu tiên (cao, trung, thấp)\n
      4. Thời gian phản hồi mong đợi\n
      Trả về kết quả dưới dạng JSON structured:\n
      {\n  \"lead_id\": \"{lead_id}\",\n  \"financial_status\": \"stable/unstable\",\n  \"priority\": \"high/medium/low\",\n  \"next_action\": \"contact/follow-up/ignore\"\n}"
    }
    ```

#### **🔹 Node "Structured Output" (Định dạng kết quả AI)**
- **Chọn schema JSON** phù hợp với tiêu chí đánh giá (ví dụ:
  ```json
  {
    "lead_id": "{{$node["OpenAI Model - Enrichment"].jsonpath("$.lead_id")}}",
    "priority": "{{$node["OpenAI Model - Enrichment"].jsonpath("$.priority")}}",
    "next_action": "{{$node["OpenAI Model - Enrichment"].jsonpath("$.next_action")}}"
  }
  ```

#### **🔹 Node "Notify Slack - High Priority" (Cảnh báo Slack)**
- **Cấu hình Slack**:
  - **Credentials**: Chọn `slackOAuth2Api` (đã cấu hình OAuth2 trong n8n).
  - **Channel**: `#real-estate-leads` (hoặc channel riêng).
  - **Message template**:
    ```json
    {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "*🚨 Lead Cao Cấp Mới!* 🚨\n*ID Lead:* <{{$node["Store Lead in Database"].jsonpath("$.id")}}|{{$node["Store Lead in Database"].jsonpath("$.name")}}>\n*Địa chỉ:* {{$node["Store Lead in Database"].jsonpath("$.address")}}\n*Độ ưu tiên:* {{$node["Structured Output - Routing Decision"].jsonpath("$.priority")}}\n*Hành động cần thực hiện:* {{$node["Structured Output - Routing Decision"].jsonpath("$.next_action")}}"
          }
        },
        {
          "type": "actions",
          "elements": [
            {
              "type": "button",
              "text": {
                "type": "plain_text",
                "text": "Phân công cho Agent"
              },
              "url": "https://your-crm.com/assign?lead_id={{$node["Store Lead in Database"].jsonpath("$.id")}}"
            }
          ]
        }
      ]
    }
    ```

#### **🔹 Node "Store Lead in Database" (Lưu lead vào PostgreSQL)**
- **Cấu hình PostgreSQL**:
  - **Host**: `your-postgres-host`
  - **Database**: `real_estate_leads`
  - **Table**: `leads` (nếu chưa có, tạo bảng với schema:
    ```sql
    CREATE TABLE leads (
      id SERIAL PRIMARY KEY,
      lead_id VARCHAR(255),
      name VARCHAR(255),
      email VARCHAR(255),
      phone VARCHAR(255),
      address TEXT,
      priority VARCHAR(50),
      next_action VARCHAR(100),
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
      updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```
  - **Query**:
    ```sql
    INSERT INTO leads (lead_id, name, email, phone, address, priority, next_action)
    VALUES ('{{$json["lead_id"]}}', '{{$json["name"]}}', '{{$json["email"]}}', '{{$json["phone"]}}', '{{$json["address"]}}', '{{$json["priority"]}}', '{{$json["next_action"]}}')
    ON CONFLICT (lead_id) DO UPDATE SET
      name = EXCLUDED.name,
      email = EXCLUDED.email,
      phone = EXCLUDED.phone,
      address = EXCLUDED.address,
      priority = EXCLUDED.priority,
      next_action = EXCLUDED.next_action,
      updated_at = CURRENT_TIMESTAMP;
    ```

#### **🔹 Node "Aggregate Daily Lead Stats" (Báo cáo thống kê hàng ngày)**
- **Cấu hình**:
  - **Group by**: `priority` (để tính số lead cao, trung, thấp).
  - **Metrics**: `count`, `avg(lead_score)`.
  - **Query**:
    ```sql
    SELECT
      priority,
      COUNT(*) as total_leads,
      AVG(lead_score) as avg_score
    FROM leads
    WHERE created_at >= NOW() - INTERVAL '1 day'
    GROUP BY priority;
    ```

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấp vào **"Execute"** trên node **"Schedule Trigger"** để chạy thử.
   - Kiểm tra **Slack** và **PostgreSQL** để xác nhận lead được lưu và cảnh báo.
2. **Bật Active**:
   - Nhấp vào **"Active"** trên tab **"Workflow"** để workflow chạy tự động theo lịch.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với CRM để phân công tự động**
- Sử dụng **node `emailSend`** để gửi email phân công lead cho agent:
  ```json
  {
    "to": "{{$node["Merge Lead with Agent Data"].jsonpath("$.agent_email")}}",
    "subject": "🚨 Lead Cao Cấp: {{$node["Store Lead in Database"].jsonpath("$.name")}}",
    "html": "<p>Xin chào {{agent_name}},</p><p>Có lead mới cần phân công:</p><ul><li>Tên: {{$node["Store Lead in Database"].jsonpath("$.name")}}</li><li>Địa chỉ: {{$node["Store Lead in Database"].jsonpath("$.address")}}</li><li>Độ ưu tiên: {{$node["Structured Output - Routing Decision"].jsonpath("$.priority")}}</li></ul><p>Hành động cần thực hiện: {{$node["Structured Output - Routing Decision"].jsonpath("$.next_action")}}</p>"
  }
  ```

### **🔹 Lưu log hoạt động vào file CSV**
- Sử dụng **node `set`** để lưu log vào biến:
  ```json
  {
    "log": "{{$json.log || ''}} + \n[{{$node["Schedule Trigger"].jsonpath("$.date")}}] Lead ID: {{$node["Store Lead in Database"].jsonpath("$.lead_id")}} - Priority: {{$node["Structured Output - Routing Decision"].jsonpath("$.priority")}}"
  }
  ```
- Sau đó, sử dụng **node `fileSystem`** để ghi log vào file `logs/lead_activity.csv`.

### **🔹 Tích hợp với Google Sheets/Bitrix24**
- Thay thế **PostgreSQL** bằng **Google Sheets** (node `googleSheets`) hoặc **Bitrix24** (node `bitrix24`) để lưu lead.
- **Cấu hình Google Sheets**:
  - **Sheet Name**: `Real Estate Leads`
  - **Range**: `A1` (đầu tiên của sheet).
  - **Query**:
    ```json
    {
      "values": [
        ["Lead ID", "Name", "Email", "Priority", "Next Action"],
        ["{{$node