---
title: "🔍 **Tự Động Xây Dựng Danh Sách Leads Tiềm Năng với LeadIQ + Airtable (Không Cần Code!)**"
description: "Workflow tự động hóa 100% AI-driven để tìm kiếm, enrich và lưu trữ leads tiềm năng từ LeadIQ vào Airtable CRM, tiết kiệm thời gian lên đến 80% cho bộ phận marketing và sales. Hỗ trợ tìm kiếm theo tiêu chí chi tiết (vị trí, quy mô, ngành nghề) và enrich thông tin email tự động."
slug: "tieu-dong-xay-dung-danh-sach-leads-leadiq-airtable"
tags: [n8n, automation, lead-generation, ai-chatbot, airtable, leadiq, mistral-ai, tavily, no-code]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm leads, Airtable CRM tự động, LeadIQ API tự động hóa, AI agent cho marketing, danh sách leads tiềm năng]
---

# 🚀 **Tự Động Xây Dựng Danh Sách Leads Tiềm Năng với LeadIQ + Airtable (Không Cần Code!)**

---
### **Nỗi Đau Của Các Sếp Marketing & Sales**
Bạn đã từng phải:
- **Tìm kiếm thủ công** hàng trăm leads trên LinkedIn, Google hay LeadIQ, chỉ để sau đó phải **lọc và enrich** thông tin một cách mệt mỏi?
- **Mất thời gian** viết query phức tạp để lấy dữ liệu từ API LeadIQ?
- **Không biết cách** kết hợp AI để tự động **tìm kiếm, enrich và lưu trữ** leads vào CRM một cách chính xác?
- **Bị giới hạn** số lượng credits của LeadIQ khi làm thủ công, trong khi tự động hóa giúp tiết kiệm chi phí?

**Workflow này giải quyết tất cả!** Sử dụng **AI Agent + LeadIQ API + Airtable**, bạn chỉ cần **gõ một câu prompt đơn giản** (ví dụ: *"Tìm CEO của các startup AI ở New York, 11-50 nhân viên"*), hệ thống sẽ tự động:
✅ **Tìm kiếm leads** theo tiêu chí chi tiết
✅ **Enrich thông tin email** (nếu có)
✅ **Lưu vào Airtable CRM** với cấu trúc sẵn sàng cho sales
✅ **Tối ưu hóa credits** LeadIQ bằng cách tự động hóa

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với làm thủ công (không cần lọc, enrich, hoặc nhập liệu).
- **Dữ liệu chính xác cao**: AI tự động chuyển đổi prompt thành query GraphQL phù hợp với LeadIQ.
- **Enrich email tự động**: Sử dụng Tavily + Mistral AI để tìm kiếm email nếu LeadIQ không có.
- **Lưu trữ sẵn sàng cho sales**: Dữ liệu được tổ chức trong Airtable với cấu trúc CRM chuyên nghiệp.
- **Tối ưu hóa credits**: Hệ thống chỉ tiêu thụ credits LeadIQ khi cần thiết.
- **Hoạt động 24/7**: Không cần can thiệp của con người, workflow chạy tự động sau khi cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LeadIQ**:
   - Đăng ký tại [LeadIQ](https://leadiq.com) và lấy **Secret Base64 API Key**.
   - **Lưu ý**: Workflow sử dụng **GraphQL API** của LeadIQ, nên cần có gói credits đủ để test.

2. **Tài khoản Airtable**:
   - Tạo một **base mới** với template **"Sales CRM"** (tìm trong mục *Templates → Marketing*).
   - **Cấu trúc sheet "Contacts"** phải có các trường:
     - `Name`, `Company`, `Email`, `Title`, `Campaign` (để phân loại leads).
   - **Cấu trúc sheet "Accounts"** (dạng mảng) để lưu thông tin công ty.

3. **Tài khoản Mistral AI**:
   - Đăng ký tại [Mistral AI](https://mistral.ai/) và lấy **API Key**.
   - Workflow sử dụng các model:
     - `open-mistral-7b`
     - `mistral-medium-latest`
     - `mistral-small-latest` (3 node).

4. **Tài khoản Tavily** (tùy chọn, nếu muốn enrich email):
   - Đăng ký tại [Tavily](https://tavily.com/) và lấy **API Key**.

5. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (không dùng phiên bản cloud để tránh giới hạn API).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12562](https://n8n.io/workflows/12562) hoặc copy/paste JSON từ link trên vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor → Nhấn **Import** → Chọn file JSON.
  2. Hoặc nhấn **Create new workflow** → Paste JSON từ link trên.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này phức tạp với **23 nodes**, nhưng chỉ cần chú ý đến các phần sau:

##### **A. Cấu Hình LeadIQ API**
- **Nodes quan trọng**:
  - `LeadIQ Database (Find People)` (type: `httpRequest`)
  - `LeadIQ Database (Find Email)` (type: `httpRequest`)
- **Cách cấu hình**:
  1. Trong mỗi node `httpRequest`, chọn **Method: POST**.
  2. **Headers**:
     - `Authorization: Basic <API_KEY_LEADIQ>` (điền API Key từ LeadIQ).
     - `Content-Type: application/json`.
  3. **URL**: `https://api.leadiq.com/graphql`.
  4. **Body (JSON)**:
     ```json
     {
       "query": "query FlatAdvancedSearch($searchInput: FlatSearchInput!) { flatAdvancedSearch(searchInput: $searchInput) { ... }}"
     }
     ```
     *(Lưu ý: Query GraphQL sẽ được tự động sinh bởi AI Agent, không cần chỉnh tay.)*

##### **B. Cấu Hình Airtable**
- **Nodes quan trọng**:
  - `Airtable: Create Account` (upsert)
  - `Add Contact` (upsert)
  - `Search and Filter Records by Campaign` (search)
  - `Update Record` (update)
- **Cách cấu hình**:
  1. Trong **Credentials**, chọn `airtableTokenApi` (đã cấu hình trước khi import).
  2. **Base ID** và **Sheet Name**:
     - Đặt `baseId` là ID của base Airtable (tìm trong URL: `https://airtable.com/<baseId>`).
     - Đặt `sheetName` là `"Contacts"` (hoặc tên sheet tương ứng).
  3. **Operation**:
     - `upsert`: Thêm hoặc cập nhật nếu tồn tại.
     - `search`: Lọc leads theo campaign.
  4. **Fields cần điền**:
     - `Name`, `Company`, `Email`, `Title`, `Campaign` (trường `Campaign` dùng để phân loại leads).

##### **C. Cấu Hình AI Agent & Mistral**
- **Nodes quan trọng**:
  - `Web Enrichment Agent` (type: `agent`)
  - `Filters Summary Agent` (type: `agent`)
  - `Company-level data preparation` (type: `chainLlm`)
  - `Contact-Level Search Criteria` (type: `chainLlm`)
- **Cách cấu hình**:
  1. Trong **Credentials**, chọn `mistralCloudApi` (đã cấu hình trước khi import).
  2. **Model**:
     - `open-mistral-7b` (dùng cho query GraphQL).
     - `mistral-medium-latest` (dùng cho enrich dữ liệu).
     - `mistral-small-latest` (dùng cho các task nhỏ).
  3. **Prompt Template**:
     - Workflow đã sẵn sàng các **prompt AI** để chuyển đổi input của bạn thành query LeadIQ.
     - Ví dụ: Nếu bạn gõ *"Tìm CTO của startup AI ở SF, 50-200 nhân viên"*, AI sẽ tự động tạo query:
       ```graphql
       query FlatAdvancedSearch($searchInput: FlatSearchInput!) {
         flatAdvancedSearch(searchInput: $searchInput) {
           people {
             name
             company {
               name
             }
             email
             title
           }
         }
       }
       ```

##### **D. Cấu Hình Tavily (Tùy Chọn)**
- Nếu muốn **enrich email** khi LeadIQ không có:
  1. Trong node `Tavily Tool`, điền `tavilyApi` vào Credentials.
  2. **Query Example**:
     ```json
     {
       "query": "Find email for {{contact.name}} at {{contact.company}}",
       "maxResults": 1
     }
     ```

##### **E. Cấu Hình "Manage Number of Leads"**
- **Node `Return an Array for Account`** (type: `code`):
  - Chỉnh dòng code:
    ```javascript
    <input.limit = 5>  // Đặt số leads muốn lấy mỗi lần chạy (mặc định là 1)
    ```
  - **Lưu ý**: Số này ảnh hưởng đến **số credits LeadIQ tiêu thụ**. Đặt số nhỏ (5-10) để test trước.

##### **F. Cấu Hình "Search Filters Summary"**
- **Node `Filters Summary Agent`** (type: `agent`):
  - AI này **tổng hợp các tiêu chí** từ prompt của bạn thành query GraphQL phù hợp.
  - **Không cần chỉnh**, chỉ cần nhập prompt đầu vào.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **Execute Workflow** và nhập một **prompt mẫu**:
     ```
     Tìm Founder của các startup AI ở New York, 11-50 nhân viên, sử dụng Mistral AI
     ```
   - Kiểm tra kết quả trong **Airtable** và **Log n8n**.

2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ `Inactive` sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tạo nhiều Campaign**:
   - Mỗi lần chạy workflow, **đặt tên campaign khác nhau** (ví dụ: `AI_Startup_NYC_2024`).
   - Sử dụng trường `Campaign` trong Airtable để **lọc leads** sau này.

2. **Enrich Email Tự Động**:
   - Nếu LeadIQ không có email, **Tavily** sẽ tìm kiếm và cập nhật vào Airtable.

3. **Lưu Log Cho Audit**:
   - Thêm node **n8n-nodes-base.stickyNote** để ghi lại **lịch sử chạy** và **số credits tiêu thụ**.

4. **Kết Hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** để **báo cáo kết quả** mỗi khi workflow chạy thành công.

5. **Tối Ưu Hóa Credits LeadIQ**:
   - Đặt `<input.limit>` thấp (5-10) để **giảm chi phí** khi test.
   - Sau khi ổn, tăng lên 20-50 để lấy nhiều leads hơn.

6. **Sử Dụng AI Agent Cho Prompt Tự Động**:
   - Nếu muốn **tự động hóa prompt**, thêm node `chatTrigger` với một **AI Agent khác** để sinh prompt từ input của người dùng.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing và sales muốn:
✔ **Tiết kiệm thời gian** lên đến 80% trong việc tìm kiếm và enrich leads.
✔ **Tự động hóa hoàn toàn** từ tìm kiếm đến lưu trữ trong CRM.
✔ **Tối Ưu hóa chi phí** bằng cách kiểm soát credits LeadIQ.

**Bắt đầu ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Nhập một prompt** và xem AI làm việc như thế nào.
3. **Bật Active** và để workflow chạy tự động mỗi khi cần!

**🚀 Hãy tự động hóa sales của bạn hôm nay!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với [GrowSpire](https://growspire.agency) để hỗ trợ chi tiết.

---
**🔗 [Xem video hướng dẫn](https://vimeo.com/1151100805)** (Trailer từ tác giả)