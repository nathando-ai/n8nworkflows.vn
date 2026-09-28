---
title: "🚀 Tự Động Hóa Tạo Lead Chất Lượng & Bài Script Gọi Lạnh với LinkedIn, OpenAI & Sales Navigator - Không Cần Code!"
description: "Workflow tự động hóa 37 node giúp các sếp tìm kiếm, đánh giá AI, và tạo danh sách lead chất lượng từ LinkedIn, đồng thời tự động sinh bài script gọi lạnh cá nhân hóa - tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoa-tao-lead-chat-luong-va-bai-script-goi-lanh"
tags: [n8n, automation, lead-generation, multimodal-ai, sales-navigator, openai, google-sheets]
keywords: [n8n workflow lead generation, tự động hóa tìm kiếm lead LinkedIn, AI đánh giá công ty, bài script gọi lạnh tự động, Sales Navigator API, Ghost Genius API]
---

# 🚀 **Tự Động Hóa Tạo Lead Chất Lượng & Bài Script Gọi Lạnh với LinkedIn, OpenAI & Sales Navigator**

### **Giải pháp cho các sếp bán hàng, marketing, và team sales:**
Bạn có bao giờ phải mất **giờ đồng hồ** để tìm kiếm công ty tiềm năng trên LinkedIn, đánh giá xem họ phù hợp với chiến lược bán hàng của mình, sau đó viết bài script gọi lạnh cá nhân hóa cho từng lead? **Workflow này sẽ tự động hóa toàn bộ quy trình đó trong vài phút!**

Dù bạn là **trưởng phòng bán hàng**, **quản lý marketing**, hay **doanh nhân startup**, việc tự động hóa tìm kiếm lead và tạo script gọi lạnh sẽ giúp bạn:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Tăng chất lượng lead** với AI đánh giá công ty dựa trên dữ liệu thực tế.
✅ **Cá nhân hóa script gọi lạnh** cho từng lead, tăng tỷ lệ thành công gọi điện.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn tài nguyên của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow 37 node này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tìm kiếm và lọc lead** từ LinkedIn Sales Navigator với **AI đánh giá tự động** (đánh giá độ phù hợp, tiềm năng, và mức độ hoạt động của công ty).
- **Tránh trùng lặp lead** bằng cách kiểm tra danh sách công ty đã tồn tại trong Google Sheets.
- **Tự động sinh script gọi lạnh cá nhân hóa** cho từng lead, dựa trên thông tin công ty và vị trí của người quyết định.
- **Lưu trữ lead chất lượng** vào Google Sheets với **đánh giá AI** và trạng thái (đã gọi, chưa gọi, tiềm năng cao).
- **Hoạt động tự động hàng ngày** (cấu hình lịch trình) mà không cần can thiệp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn Sales Navigator** (để truy cập API Ghost Genius).
2. **API Key của Ghost Genius** (để tìm kiếm công ty và nhân viên trên LinkedIn).
3. **Tài khoản OpenAI** (để sử dụng AI đánh giá và sinh script gọi lạnh).
4. **Google Sheets** (để lưu trữ danh sách công ty, lead, và cấu hình workflow).
5. **Credentials cho n8n**:
   - `openAiApi` (API Key OpenAI).
   - `googleSheetsOAuth2Api` (OAuth 2.0 cho Google Sheets).

---
:::note[CHUẨN BỊ FILE CẦN THIẾT]
- **Tạo một bản sao của Google Sheet mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1j8AHiPiHEXVOkUhO2ms-lw1Ygu1eWIWW-8Qe1OoHpCo/edit?usp=sharing) và cấu hình các sheet sau:
  - **Settings**: Cấu hình tham số tìm kiếm (ví dụ: ngành nghề, số lượng nhân viên, vị trí).
  - **Companies**: Lưu trữ danh sách công ty đã tìm kiếm và đánh giá.
  - **Leads**: Lưu trữ lead chất lượng và script gọi lạnh.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7140](https://n8n.io/workflows/7140) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --nodeInputs
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **3 phần chính**: Tìm kiếm công ty, đánh giá AI, và tạo lead. Dưới đây là các node quan trọng cần cấu hình:

##### **A. Cấu hình tìm kiếm công ty (LinkedIn)**
- **Node: "Search Companies" (httpRequest)**
  - **URL**: `https://api.ghostgenius.fr/v1/companies/search`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_GHOST_GENIUS_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "query": "{{$node["Get Settings"].json["search_query"]}}",
      "limit": 100,
      "page": 1
    }
    ```
  - **Lưu ý**:
    - Thay `YOUR_GHOST_GENIUS_API_KEY` bằng API Key của bạn.
    - Tham số `search_query` lấy từ **Google Sheets (Settings sheet)**. Ví dụ:
      ```
      "Growth Marketing Agency AND (11 employees:50 employees) AND location:Vietnam"
      ```
    - **Giới hạn**: Mỗi request chỉ lấy tối đa **100 công ty/trang** (tối đa 1000 công ty/100 trang). Để tránh bị chặn, chia nhỏ tìm kiếm theo quốc gia hoặc ngành nghề.

- **Node: "Get Company Info" (httpRequest)**
  - **URL**: `https://api.ghostgenius.fr/v1/companies/{{$node["Search Companies"].json.data.id}}`
  - **Headers**: Giống như trên, với API Key Ghost Genius.

##### **B. Cấu hình AI đánh giá và sinh script**
- **Node: "AI Company Scoring" (openAi)**
  - **Model**: Chọn `gpt-4` hoặc `gpt-3.5-turbo` (tùy thuộc vào ngân sách).
  - **Prompt mẫu** (có thể chỉnh sửa trong **Settings sheet**):
    ```
    Analyze the following company data and score it from 1 to 10 based on:
    1. Industry relevance (50%)
    2. Company size (30%)
    3. LinkedIn engagement (20%)
    Data: {{$node["Get Company Info"].json}}
    Return JSON with:
    - score: number
    - reasons: array of strings
    ```
  - **Lưu ý**:
    - Đảm bảo **Settings sheet** có cột `ai_prompt` để chỉnh sửa prompt.
    - Kiểm tra **API Key OpenAI** trong credentials của n8n.

- **Node: "Make the perfect request" (openAi)**
  - **Model**: Chọn `gpt-4` (để sinh script gọi lạnh chất lượng).
  - **Prompt mẫu**:
    ```
    Generate a personalized cold call script for a sales representative to contact the decision maker at {{$node["Get Profile details"].json.company_name}}. Include:
    1. Introduction (name, title, company)
    2. Pain points based on company data
    3. Value proposition
    4. Call to action
    Data: {{$node["Get Profile details"].json}}
    ```
  - **Lưu ý**:
    - Node này hoạt động sau khi tìm được **nhân viên quyết định** (decision maker).

##### **C. Cấu hình Google Sheets**
- **Node: "Check If Company Exists" (googleSheets)**
  - **Sheet Name**: `Companies`
  - **Range**: `A2:Z` (để kiểm tra trùng lặp).
  - **Query**: `SELECT * WHERE LinkedIn_ID = "{{$node["Get Company Info"].json.id}}"`
  - **Lưu ý**: Nếu công ty đã tồn tại, workflow sẽ **bỏ qua** để tránh trùng lặp.

- **Node: "Add Company to CRM" (googleSheets)**
  - **Sheet Name**: `Companies`
  - **Operation**: `append`
  - **Row**: Thêm dữ liệu công ty mới vào sheet, bao gồm:
    - `LinkedIn_ID`, `Name`, `Score` (từ AI), `Status` (tạm thời: `pending`).

- **Node: "Lead(s) found" (googleSheets)**
  - **Sheet Name**: `Leads`
  - **Operation**: `appendOrUpdate`
  - **Row**: Lưu lead chất lượng (score ≥ 7) và script gọi lạnh.

##### **D. Cấu hình lịch trình (Schedule Trigger)**
- **Node: "Schedule Trigger"**
  - **Cron Expression**: `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Lưu ý**:
    - **Giới hạn LinkedIn Sales Navigator**: 2,500 kết quả/ngày. Workflow này **không nên xử lý quá 100 công ty/ngày** để tránh bị chặn.
    - Sử dụng **node "Limit"** để điều chỉnh số lượng công ty xử lý.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **manual trigger** (`Start` node) với dữ liệu mẫu để kiểm tra.
   - Kiểm tra **Google Sheets** xem có lead nào được sinh ra không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** và để nó hoạt động tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa tìm kiếm**:
   - Chia nhỏ tìm kiếm theo **ngành nghề** hoặc **quốc gia** để tránh bị giới hạn của LinkedIn.
   - Ví dụ: Tìm kiếm **500 công ty/ngày** thay vì 1000 để an toàn.

2. **Lưu log hoạt động**:
   - Thêm **node "stickyNote"** để ghi lại lỗi hoặc trạng thái của workflow.
   - Ví dụ: `Workflow ran at {{$node["Schedule Trigger"].date}} with {{$node["Search Companies"].json.total}} companies found.`

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node "googleSheets"** để tạo **báo cáo hàng tuần** về số lead sinh ra, tỷ lệ chuyển đổi, và công ty có score cao nhất.

4. **Kết hợp với Slack/Telegram**:
   - Thêm **node "httpRequest"** để gửi thông báo khi có lead mới được sinh ra:
     ```json
     {
       "url": "https://api.telegram.org/botYOUR_BOT_TOKEN/sendMessage",
       "method": "POST",
       "body": {
         "chat_id": "YOUR_CHAT_ID",
         "text": "New lead found: {{$node["Lead(s) found"].json.name}} (Score: {{$node["Lead(s) found"].json.score}})"
       }
     }
     ```

5. **Cập nhật AI prompt**:
   - Thử nghiệm với **prompt khác** để cải thiện chất lượng script gọi lạnh. Ví dụ:
     - Thêm **ví dụ thực tế** trong prompt.
     - Yêu cầu AI **tránh từ ngữ quá bán hàng** để tránh bị chặn điện thoại.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quy trình tìm kiếm lead và gọi lạnh** mà không cần viết một dòng code. Bằng cách kết hợp **LinkedIn Sales Navigator**, **AI OpenAI**, và **Google Sheets**, bạn sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào bán hàng thực tế.
✔ **Tăng tỷ lệ thành công gọi điện** với script cá nhân hóa.
✔ **Quản lý lead một cách chuyên nghiệp** với hệ thống đánh giá AI.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi bật chế độ tự động.
3. **Cập nhật Settings sheet** để phù hợp với chiến lược bán hàng của bạn.

🚀 **Chúc các sếp thành công với chiến dịch tìm kiếm lead mới!** 🚀