---
title: "🚀 Tự Động Hóa & Đánh Giá Lead Tự Động Với Clearbit, Trello & Mattermost (Không Cần Code)"
description: "Workflow tự động hóa lấy, enrich, đánh giá và phân loại lead từ form/CRM sang Trello và Mattermost, giúp các sếp tiết kiệm 10+ giờ/ngày và tăng hiệu quả bán hàng 30%."
slug: "tieu-dong-hoa-lead-clearbit-trello-mattermost"
tags: [n8n, automation, lead-generation, crm-automation, trello-integration, clearbit, mattermost]
keywords: [n8n workflow lead scoring, tự động hóa lead generation, enrich lead với clearbit, phân loại lead trello, tự động hóa bán hàng, workflow n8n cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa & Đánh Giá Lead Tự Động: Từ Form → Trello → Sales (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp đang mất **10+ giờ/ngày** để:
- **Lấy dữ liệu lead** từ form, CRM hoặc website.
- **Tra cứu thông tin công ty** (Clearbit) cho mỗi lead.
- **Đánh giá chất lượng lead** dựa trên nhiều tiêu chí (số nhân viên, ngành nghề, email hợp lệ...).
- **Phân loại lead** vào Trello (Qualified/Unqualified/Needs Research).
- **Gửi thông báo** cho đội bán hàng và team Ops khi có lead mới.

**Kết quả?** Lead trôi nổi, thông tin không đồng bộ, và đội bán hàng phải làm việc với **dữ liệu không đầy đủ** → **tỷ lệ chuyển đổi thấp** và **tốn thời gian quá nhiều**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** với tự động hóa lấy và enrich lead.
- **Đánh giá lead chính xác** dựa trên **Clearbit** (thông tin công ty, email, ngành nghề).
- **Phân loại tự động** vào Trello (Qualified → Sales, Unqualified → Nurture, Needs Research → Ops).
- **Thông báo tức thời** cho đội bán hàng và team Ops trên **Mattermost**.
- **Dữ liệu đồng bộ** trên Trello (single source of truth).
- **Cập nhật hàng ngày** (không cần can thiệp thủ công).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **API Key Clearbit** (để enrich lead với thông tin công ty).
   - 👉 [Đăng ký miễn phí Clearbit](https://clearbit.com/) (có giới hạn 1000 request/month).
2. **Trello API Key** (để tạo card cho lead).
   - 👉 [Tạo Trello API Key](https://trello.com/app-key).
3. **Mattermost OAuth2 Credentials** (để gửi thông báo).
   - 👉 [Cấu hình OAuth2 Mattermost](https://docs.mattermost.com/develop/oauth2.html).
4. **Board & List ID trên Trello**:
   - **Board ID** (ID của board Trello chứa lead).
   - **3 List ID** (đối ứng với:
     - **Qualified Leads** (lead chất lượng cao).
     - **Unqualified Leads** (lead không phù hợp).
     - **Needs Research** (lead cần tra cứu thêm).
5. **Channel ID Mattermost** (để gửi thông báo).
6. **HTTP Credentials cho CRM/API form** (nếu lấy lead từ form/CRM).
   - Ví dụ: API của **Typeform, Jotform, HubSpot, Airtable...**
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/12751](https://n8n.io/workflows/12751) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/12751) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **15 node** quan trọng, các sếp cần **cấu hình kỹ** các node sau:

##### **A. Node "Fetch New Leads" (HTTP Request)**
- **Tham số cần điền:**
  - **URL:** API endpoint của form/CRM (ví dụ: `https://api.jotform.com/submissions`).
  - **Headers:**
    - `Authorization: Bearer {API_KEY_CRM}` (nếu cần).
    - `Content-Type: application/json`.
  - **Query Parameters:**
    - `limit=100` (lấy 100 lead mới nhất).
  - **Lưu ý:** Nếu lấy từ **Airtable**, thay đổi URL thành `https://api.airtable.com/v0/{BASE_ID}/{TABLE_NAME}`.

##### **B. Node "Enrich with Clearbit" (HTTP Request)**
- **Tham số cần điền:**
  - **URL:** `https://person.clearbit.com/v1/enrich?email={email}`.
  - **Headers:**
    - `Authorization: Bearer {CLEARBIT_API_KEY}`.
    - `Content-Type: application/json`.
  - **Lưu ý:**
    - **Tối đa hóa request** bằng cách **split leads** (node `Split In Batches`).
    - **Bật "Continue On Fail"** để workflow không ngừng khi Clearbit trả về lỗi.

##### **C. Node "Calculate Lead Score" (Code)**
- **Logic scoring mặc định:**
  ```javascript
  // Điểm mặc định (có thể chỉnh sửa)
  const scoringRules = {
    "company.employees": (value) => value > 50 ? 20 : value > 10 ? 10 : 0,
    "company.funding": (value) => value > 1000000 ? 30 : value > 500000 ? 20 : 0,
    "email.isValid": () => 10,
    "company.industry": (value) => value === "Tech" ? 15 : 0,
    "company.alexaRank": (value) => value < 10000 ? 15 : 0
  };
  ```
  - **Cách chỉnh sửa:**
    - Mở node **Code** → Sửa `scoringRules` theo tiêu chí của doanh nghiệp.
    - Ví dụ: Nếu **ngành Tech** là ưu tiên, tăng điểm cho `company.industry === "Tech"`.

##### **D. Node "Create Trello Card" (Trello)**
- **Tham số cần điền:**
  - **Board ID:** `{BOARD_ID_TRELLO}` (đã chuẩn bị trước).
  - **List ID:**
    - **Qualified:** `{LIST_ID_QUALIFIED}`.
    - **Unqualified:** `{LIST_ID_UNQUALIFIED}`.
    - **Needs Research:** `{LIST_ID_NEEDS_RESEARCH}`.
  - **Card Name:** `{{ $node["Fetch New Leads"].json["email"] }} - Score: {{ $node["Calculate Lead Score"].json["score"] }}`.
  - **Card Description:** (Dữ liệu enrich + score).
    ```json
    {
      "rawData": "{{ $node["Fetch New Leads"].json }}",
      "enrichedData": "{{ $node["Merge Lead & Enrichment"].json }}",
      "score": "{{ $node["Calculate Lead Score"].json["score"] }}",
      "qualified": "{{ $node["IF Qualified?"].json["qualified"] }}"
    }
    ```

##### **E. Node "Notify Sales Team" & "Notify Ops" (Mattermost)**
- **Tham số cần điền:**
  - **Channel ID:** `{CHANNEL_ID_MATTERMOST}` (Sales hoặc Ops).
  - **Message Template:**
    - **Sales:**
      ```json
      {
        "text": "🚀 **New Qualified Lead!** 🚀",
        "attachments": [
          {
            "title": "{{ $node["Fetch New Leads"].json["email"] }}",
            "text": "Score: {{ $node["Calculate Lead Score"].json["score"] }}",
            "fields": [
              { "title": "Company", "value": "{{ $node["Merge Lead & Enrichment"].json["company.name"] }}", "short": true },
              { "title": "Industry", "value": "{{ $node["Merge Lead & Enrichment"].json["company.industry"] }}", "short": true }
            ]
          }
        ]
      }
      ```
    - **Ops (khi enrich thất bại):**
      ```json
      {
        "text": "⚠️ **Enrichment Failed** ⚠️",
        "attachments": [
          {
            "title": "{{ $node["Fetch New Leads"].json["email"] }}",
            "text": "Clearbit không enrich được lead này. Vui lòng tra cứu thủ công!",
            "fields": [
              { "title": "Raw Data", "value": "{{ $node["Fetch New Leads"].json }}", "short": false }
            ]
          }
        ]
      }
      ```

##### **F. Node "Daily Lead Check" (Schedule Trigger)**
- **Tham số mặc định:** Chạy **mỗi ngày lúc 9h sáng** (có thể chỉnh sửa).
- **Lưu ý:** Đảm bảo **n8n chạy 24/7** trên **VPS** (không dùng phiên bản free).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để gửi thông báo nhanh hơn Mattermost.
   - Ví dụ: Khi lead **Qualified**, gửi tin nhắn Slack với link Trello card.

2. **Lưu log vào Google Sheets/Notion:**
   - Thêm node **Google Sheets** hoặc **Notion API** để lưu lịch sử lead.
   - Cấu hình như sau:
     ```json
     {
       "sheetName": "Lead Log",
       "range": "A2:D",
       "values": [
         ["Email", "Score", "Status", "Date"],
         ["{{ $node["Fetch New Leads"].json["email"] }}", "{{ $node["Calculate Lead Score"].json["score"] }}", "{{ $node["IF Qualified?"].json["qualified"] }}", "{{ $node["Daily Lead Check"].json["date"] }}"]
       ]
     }
     ```

3. **Gửi báo cáo định kỳ cho CEO:**
   - Thêm node **Email (SendGrid/Outlook)** để gửi báo cáo hàng tuần:
     - **Tiêu đề:** "Báo cáo Lead Hàng Tuần - Ngày {{ $node["Daily Lead Check"].json["date"] }}"
     - **Nội dung:**
       ```markdown
       - **Total Leads:** {{ $node["Split Leads"].json["totalItems"] }}
       - **Qualified:** {{ $node["IF Qualified?"].json["qualifiedCount"] }}
       - **Unqualified:** {{ $node["IF Qualified?"].json["unqualifiedCount"] }}
       - **Needs Research:** {{ $node["Fallback Score"].json["count"] }}
       ```

4. **Tăng cường scoring với AI (LLM):**
   - Thêm node **LLM (n8n-nodes-base.llm)** để đánh giá lead bằng **ChatGPT/Google Vertex AI**.
   - Ví dụ:
     ```json
     {
       "model": "gpt-3.5-turbo",
       "prompt": "Analyze this lead: {{ $node["Merge Lead & Enrichment"].json }}. Is this a good fit for our product? Give a score (0-100).",
       "temperature": 0.7
     }
     ```
   - Sau đó, **trừ/bổ sung điểm** vào score hiện tại.

5. **Tự động gửi email follow-up:**
   - Thêm node **SendGrid/Outlook** để gửi email tự động cho lead **Qualified**:
     ```json
     {
       "to": "{{ $node["Fetch New Leads"].json["email"] }}",
       "subject": "👋 Chào {{ $node["Merge Lead & Enrichment"].json["company.name"] }}!",
       "html": "<p>Chúng tôi đã nhận được lead của bạn và đánh giá cao chất lượng!</p><p>Đội bán hàng của chúng tôi sẽ liên hệ trong vòng 24h.</p>"
     }
     ```
:::

---
### **📌 Kết Luận: Áp Dụng Ngay & Tăng Hiệu Quả Bán Hàng!**
Workflow này **giải quyết toàn bộ quy trình lead generation** từ **lấy dữ liệu → enrich → đánh giá → phân loại → thông báo** **tự động**, **không cần code**.

**Kết quả:**
✅ **Tiết kiệm 10+ giờ/ngày** cho team marketing/sales.
✅ **Lead chất lượng cao** được ưu tiên đầu tiên.
✅ **Dữ liệu đồng bộ** trên Trello và Mattermost.
✅ **Team Ops được thông báo kịp thời** khi có lead cần tra cứu.

**Bước đầu tiên:** **Cài đặt n8n trên VPS** (để workflow chạy 24/7) và **import workflow** từ [n8n.io/workflows/12751](https://n8n.io/workflows/12751).

**🎁 Mã giảm giá VPS cho n8n:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

**Hành động ngay:** **Cấu hình workflow, bật chạy và xem lead tự động được phân loại!** 🚀
```

---
**Lưu ý cuối cùng:**
- **Test workflow với dữ liệu mẫu** trước khi bật **Active**.
- **Monitor log** trong n8n để đảm bảo không có lỗi.
- **Cập nhật API Key** nếu Clearbit/Trello/Mattermost thay đổi.