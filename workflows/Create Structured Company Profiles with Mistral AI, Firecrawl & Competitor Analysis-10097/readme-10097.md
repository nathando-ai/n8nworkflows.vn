---
title: "🚀 Tự Động Hoá Tạo Báo Cáo Công Ty Cấu Trúc Với AI Mistral, Scraping Deep & Phân Tích Thống Kê Đối Thủ - N8n Workflow"
description: "Workflow này tự động chuyển đổi URL website thành **báo cáo công ty cấu trúc chi tiết** với AI Mistral, scraping deep bằng Firecrawl, và phát hiện đối thủ cạnh tranh thông qua Tavily. Kết quả được lưu trữ trên Supabase và Google Drive, giúp các sếp tiết kiệm thời gian lên đến 80% trong nghiên cứu thị trường và phân tích đối thủ."
slug: "tay-dong-hoa-tao-bao-cao-cong-ty-ai-mistral-firecrawl"
tags: [n8n, automation, ai-summarization, market-research, firecrawl, mistral-ai, competitor-analysis, no-code]
keywords: [n8n workflow scraping website, tự động hóa phân tích công ty, AI Mistral cho nghiên cứu thị trường, Firecrawl deep scraping, lưu trữ dữ liệu Supabase Google Drive]
---

# 🚀 **Tự Động Hoá Tạo Báo Cáo Công Ty Cấu Trúc Với AI + Scraping Deep & Phân Tích Đối Thủ**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải **tìm hiểu chi tiết về đối thủ cạnh tranh** nhưng lại mất nhiều giờ để:
- **Scraping** thông tin từ website (thời gian, công sức, và rủi ro vi phạm chính sách chống bot)?
- **Tóm tắt** thông tin không cấu trúc thành báo cáo dễ đọc?
- **Phân tích** đối thủ mà không biết họ hoạt động trong những lĩnh vực nào, sản phẩm gì, và liên kết với ai?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động scraping** website (cả mode nhanh và deep AI) với **Firecrawl** và **Crawlee**.
✅ **Tạo báo cáo công ty cấu trúc** với **AI Mistral** (tóm tắt, phân loại, và extraxt thông tin chi tiết).
✅ **Phát hiện đối thủ cạnh tranh** thông qua **Tavily AI Agent** (không cần code).
✅ **Lưu trữ dữ liệu** an toàn trên **Supabase** (database) và **Google Drive** (backup JSON).
✅ **Cập nhật liên tục** cho các sếp theo dõi thị trường 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ scraping nhanh)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với phương pháp thủ công.
- **Báo cáo công ty cấu trúc** với thông tin chi tiết: **mục tiêu, sản phẩm, dịch vụ, liên hệ, mạng xã hội, và đối thủ cạnh tranh**.
- **Phân tích đối thủ tự động** (không cần tra cứu thủ công trên Crunchbase hay Google).
- **Dữ liệu an toàn** với **backup JSON** trên Google Drive và **database Supabase** (dễ dàng truy xuất, cập nhật).
- **Scalable** cho nhiều công ty, giúp các sếp **nhận quyết định nhanh chóng** trong chiến lược thị trường.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
| **Tài Khoản/Dịch Vụ**       | **Tham Số Cần Thiết**                          | **Liên Kết Cần Cài Đặt**                          |
|-----------------------------|-----------------------------------------------|---------------------------------------------------|
| **Supabase**                | API Key, Database URL, Table Name            | [Tạo tài khoản Supabase](https://supabase.com/)   |
| **Google Drive**            | OAuth 2.0 Client ID & Secret                 | [Cài đặt API Google Drive](https://developers.google.com/drive/api/v3/quickstart) |
| **Mistral AI Cloud**        | API Key (model: `mistral-small-latest`)       | [Đăng ký API Mistral](https://mistral.ai/)       |
| **Firecrawl**               | API Key (đăng ký miễn phí)                   | [Tạo tài khoản Firecrawl](https://www.firecrawl.dev/) |
| **Tavily (MCP)**            | API Key (để tìm đối thủ cạnh tranh)          | [Đăng ký Tavily](https://www.tavily.com/)         |
| **Google Form (Trigger)**   | Link Form để người dùng nhập URL website    | [Tạo Google Form](https://forms.google.com/)      |

---
:::note[LƯU Ý QUAN TRỌNG]
- **Firecrawl** và **Tavily** là **MCP (Multi-Cloud Provider)**, các sếp cần **cài đặt node `n8n-nodes-mcp`** từ npm:
  ```bash
  npm install n8n-nodes-mcp
  ```
- **Supabase** cần **tạo 3 bảng** (các sếp có thể tự tạo hoặc sử dụng script SQL trong workflow):
  - `company_profiles` (lưu thông tin công ty)
  - `social_media_db` (lưu liên kết mạng xã hội)
  - `keywords` (lưu từ khóa liên quan)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10097](https://n8n.io/workflows/10097) và **import** vào n8n Editor.
- **Copy JSON** từ link trên và **paste** vào n8n Editor (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **2 mode scraping**:
- **Mode 1 (Basic Web Scraper)**: Dùng cho scraping **nhanh** (không cần API).
- **Mode 2 (Deep AI Scraper)**: Dùng **Firecrawl** để scraping **chi tiết** (tốn API credit).

##### **A. Cấu Hình Form Trigger (Bắt Đầu Workflow)**
- Node: **"On form submission"**
  - **Cấu hình Google Form**:
    - Thêm **2 trường**:
      1. **Website URL** (text input)
      2. **Type of Scraping** (dropdown: `1` = Basic, `2` = Deep)

##### **B. Cấu Hình Supabase (Lưu Dữ Liệu)**
- Node: **"Supabase"**, **"Supabase4"**, **"social media db"**, **"keywords"**
  - **Điền tham số**:
    - `Database URL`: `https://<your-project-ref>.supabase.co`
    - `Database Name`: `<your-project-name>`
    - `Table Name`: `<tên bảng>` (ví dụ: `company_profiles`)
    - **Credentials**: API Key từ Supabase Dashboard.

##### **C. Cấu Hình Mistral AI (Tạo Báo Cáo Cấu Trúc)**
- Node: **"Mistral Cloud Chat Model3"**, **"Mistral Cloud Chat Model5"**, **"Mistral Cloud Chat Model6"**
  - **Điền API Key** từ Mistral.
  - **Prompt mẫu** (các sếp có thể tùy chỉnh):
    ```json
    {
      "role": "user",
      "content": "Tóm tắt thông tin công ty từ website {{website_url}} theo cấu trúc JSON sau:
      {
        \"mission\": \"...\",
        \"products\": [\"...\"], \"services\": [\"...\"],
        \"contacts\": {\"email\": \"...\", \"phone\": \"...\"},
        \"social_media\": {\"linkedin\": \"...\", \"twitter\": \"...\"},
        \"competitors\": [\"...\"]
      }"
    }
    ```

##### **D. Cấu Hình Firecrawl (Scraping Deep AI)**
- Node: **"Firecrawl tools1"**, **"Firecrawl list1"**
  - **Điền API Key** từ Firecrawl.
  - **Cấu hình URL scraping**:
    ```json
    {
      "url": "{{$node["On form submission"].json["website_url"]}}",
      "selectors": {
        "mission": "h1, .mission",
        "products": "div.product",
        "contacts": "a.email, a.phone"
      }
    }
    ```

##### **E. Cấu Hình Competitor Analysis (Tavily)**
- Node: **"find competitor"**, **"Web Search tool"**
  - **Prompt Tavily** (tìm đối thủ cạnh tranh):
    ```json
    {
      "query": "Find 5 direct competitors of {{company_name}} in {{industry}} sector",
      "search_engine": "google"
    }
    ```

##### **F. Cấu Hình Lưu Trữ (Google Drive & Supabase)**
- Node: **"Google Drive2"**, **"save to Google Drive1"**, **"save to Supabase"**
  - **Chọn folder** trên Google Drive để lưu backup JSON.
  - **Supabase**: Đảm bảo **table name** khớp với cấu trúc JSON từ Mistral.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhập **URL website mẫu** (ví dụ: `https://example.com`) vào Google Form.
  - Chạy **manual test** trong n8n Editor để kiểm tra kết quả.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật workflow** và **đăng ký trigger** từ Google Form.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Cập Nhật Dữ Liệu**
   - Sử dụng **n8n Cron Trigger** để **scraping lại** website định kỳ (ví dụ: hàng tuần).
   - Cấu hình trong **Settings > Triggers**.

2. **Gửi Báo Cáo Đến Slack/Email**
   - Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** để **báo cáo tự động** khi có kết quả mới.
   - Ví dụ:
     ```json
     {
       "text": "Báo cáo công ty {{company_name}} đã hoàn tất! Kết quả: {{json}}",
       "channel": "#market-research"
     }
     ```

3. **Tạo Dashboard Theo Dõi Đối Thủ**
   - Sử dụng **Supabase + Drizzle** hoặc **Google Data Studio** để **hiển thị bảng điều khiển** theo dõi đối thủ.
   - Cách làm:
     - Trích xuất dữ liệu từ **Supabase** qua **REST API**.
     - Tạo **biểu đồ** cho các chỉ số như: **số lượng đối thủ, từ khóa phổ biến, sản phẩm mới**.

4. **Kết Hợp Với CRM (Salesforce/Zoho)**
   - Sử dụng **node `n8n-nodes-salesforce`** để **cập nhật thông tin công ty** vào CRM tự động.
   - Ví dụ:
     ```json
     {
       "Account": {
         "Name": "{{company_name}}",
         "Website": "{{website_url}}",
         "Industry": "{{industry}}"
       }
     }
     ```

5. **Lưu Log Cho Audit**
   - Thêm **node `n8n-nodes-base.stickyNote`** để **ghi lại lịch sử scraping**.
   - Ví dụ:
     ```json
     {
       "message": "Scraped {{company_name}} at {{timestamp}}",
       "status": "{{$node["Crawl and Scrape"].json["status"]}}"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng phân tích thị trường** cho các sếp. Bằng cách **tự động hóa scraping, phân tích AI, và lưu trữ dữ liệu**, các sếp có thể:
✔ **Nhận báo cáo công ty chi tiết** trong vài giây thay vì nhiều giờ.
✔ **Phát hiện đối thủ cạnh tranh** mà không cần tra cứu thủ công.
✔ **Cập nhật dữ liệu liên tục** để theo dõi thị trường 24/7.

**🚀 Hãy áp dụng ngay workflow này và bắt đầu tự động hóa nghiên cứu thị trường của mình!**
Nếu có vấn đề, các sếp có thể **liên hệ Digital Biz Tech** qua [shilpa.raaju@digitalbiz.tech](mailto:shilpa.raaju@digitalbiz.tech) để hỗ trợ.

---
**🔥 Mẹo cuối:**
- **Optimize Firecrawl API** để tránh bị block: **giảm số lượng request/giây** và **dùng proxy** nếu cần.
- **Tùy chỉnh Mistral Prompt** để phù hợp với **ngành nghề cụ thể** của công ty.