---
title: "🧬 **Tự Động Hóa Brand DNA Generator: Tạo Báo Cáo Brand Chi Tiết Từ Dữ Liệu Trực Tuyến (JotForm + Gemini AI + Notion)**"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động thu thập, phân tích và tổng hợp thông tin về Brand DNA từ form JotForm, kết quả tìm kiếm Google, và nội dung website, sau đó lưu vào Notion dưới dạng báo cáo chuyên nghiệp. Giúp tiết kiệm thời gian nghiên cứu lên đến 80% và đảm bảo tính nhất quán trong phân tích brand."
slug: "tieu-dong-hoa-brand-dna-generator-jotform-gemini-notion"
tags: [n8n, automation, no-code, brand-research, ai-summarization, gemini-ai, notion-integration, jotform, serpapi]
keywords: [tự động hóa brand DNA, workflow n8n brand research, gemini AI phân tích brand, lưu báo cáo brand vào Notion, tự động hóa nghiên cứu thị trường, tự động hóa phân tích website]
---

# 🚀 **Tự Động Hóa Brand DNA Generator: Tạo Báo Cáo Brand Chi Tiết Từ Dữ Liệu Trực Tuyến**

Hiện nay, việc xây dựng **Brand DNA** (cốt lõi thương hiệu) thường là một quá trình tốn thời gian, đòi hỏi phải thủ công thu thập thông tin từ website, kết quả tìm kiếm Google, và phân tích nội dung trên nhiều trang web khác nhau. Các sếp phải mất hàng giờ để tổng hợp thông tin về **giá trị cốt lõi, khách hàng mục tiêu (ICP), điểm đau, bằng chứng hỗ trợ (proof points), và giọng điệu thương hiệu**—các yếu tố quan trọng để định hình chiến lược marketing và branding.

**Workflow này giải quyết vấn đề đó bằng cách tự động hóa toàn bộ quy trình:**
- Thu thập dữ liệu từ **form JotForm** (tên công ty và website).
- Tìm kiếm và phân tích **kết quả Google** liên quan đến công ty.
- **Trích xuất thông tin chi tiết** từ website và nội dung tìm kiếm bằng **Gemini AI** (Google’s LLM).
- **Tổng hợp và định dạng** dữ liệu thành một **báo cáo Brand DNA** chuyên nghiệp.
- **Lưu tự động** báo cáo vào **Notion** dưới dạng trang database, sẵn sàng chia sẻ và theo dõi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với phương pháp thủ công.
- **Tính chính xác cao**: AI tự động trích xuất thông tin quan trọng từ nhiều nguồn dữ liệu.
- **Cá nhân hóa**: Mỗi báo cáo Brand DNA được tạo riêng cho từng công ty dựa trên dữ liệu thực tế.
- **Hoạt động liên tục 24/7**: Không cần can thiệp người dùng, chỉ cần submit form là hệ thống tự động xử lý.
- **Dữ liệu sẵn sàng sử dụng**: Báo cáo được lưu vào Notion với định dạng chuyên nghiệp, dễ chia sẻ và theo dõi.
- **Tích hợp AI tiên tiến**: Sử dụng **Gemini 2.0 Flash** (miễn phí) để phân tích và tổng hợp thông tin một cách thông minh.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản JotForm** và **API Key**:
   - Form phải có **hai trường dữ liệu**: `Company Name` và `Company Website`.
   - [Hướng dẫn tạo API Key JotForm](https://www.jotform.com/help/327-How-to-Create-an-API-Token).
2. **API Key SerpAPI** (để tìm kiếm Google tự động):
   - [Đăng ký SerpAPI miễn phí](https://serpapi.com/) (có giới hạn 100 request/ngày).
3. **API Key OpenRouter** (hoặc LLM khác) để kết nối với **Gemini 2.0 Flash**:
   - [Đăng ký OpenRouter](https://openrouter.ai/) (hoặc sử dụng [LangChain](https://www.langchain.com/)).
4. **Token Notion Integration** và **Database ID**:
   - [Tạo token Notion](https://www.notion.so/my-integrations) và [lấy Database ID](https://www.notion.so/help/find-your-database-id).
5. **Notion Database** đã sẵn sàng để lưu báo cáo:
   - Database phải có các thuộc tính phù hợp với cấu trúc Brand DNA (ví dụ: `Company Name`, `Description`, `ICP`, `Pain Points`, etc.).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10617](https://n8n.io/workflows/10617) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** để import:
  ```bash
  n8n import workflow.json --name "Brand DNA Generator"
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node** với các bước logic phức tạp. Dưới đây là **các node quan trọng cần cấu hình kỹ**:

##### **🔹 Node 1: JotForm Trigger**
- **Credentials**: Chọn `jotFormApi` (đã cấu hình trước khi import).
- **Form Configuration**:
  - Chọn form có **hai trường**: `Company Name` và `Company Website`.
  - **Lưu ý**: Nếu form của các sếp có tên trường khác, cần chỉnh sửa **node Code đầu tiên** (node `Code in JavaScript`) để phù hợp.

##### **🔹 Node 2 & 3: Google Search (SerpAPI)**
- **Credentials**: Chọn `serpApi` (đã cấu hình API Key).
- **Parameters**:
  - `q`: `$node["JotForm Trigger"]["json"]["Company Name"]` (tên công ty từ form).
  - `engine`: `google`.
  - `num`: `5` (lấy 5 kết quả tìm kiếm đầu tiên).
  - **Lưu ý**: Nếu kết quả tìm kiếm không đủ, cần tăng `num` hoặc điều chỉnh `q` để chính xác hơn.

##### **🔹 Node 4 & 5: WebpageContentExtractor**
- **Credentials**: Không cần (node này tự động fetch HTML từ URL).
- **Parameters**:
  - `url`: `$node["HTTP Request"]["json"]["url"]` (URL được lấy từ SerpAPI).
  - **Lưu ý**: Nếu website có bảo vệ chống crawl, cần thêm **headers** trong node `HTTP Request` (ví dụ: `User-Agent`).

##### **🔹 Node 6 & 7: Information Extractor (LLM)**
- **Credentials**: Chọn `OpenRouter` (hoặc `LangChain`).
- **Key Parameters**:
  - `model`: `google/gemini-2.0-flash-exp:free` (miễn phí).
  - **Prompt**: Cần tùy chỉnh để phù hợp với mục đích phân tích Brand DNA. Ví dụ:
    ```json
    "prompt": "Analyze the following company website content and extract the following information:\n\n1. Company Description (2-3 sentences)\n2. Ideal Customer Profile (ICP) - Who are they targeting?\n3. Pain Points - What problems does this company solve?\n4. Value Proposition - What makes them unique?\n5. Proof Points - Any customer testimonials, case studies, or awards?\n6. Brand Tone - Is the tone professional, friendly, or authoritative?\n\nFormat the output as a JSON with clear headings."
    ```
  - **Lưu ý**: Nếu prompt không hiệu quả, cần thử lại với các biến thể khác.

##### **🔹 Node 8 & 9: Loop Over Items (splitInBatches)**
- **Parameters**:
  - `batchSize`: `3` (tối ưu hóa cho Gemini AI).
  - **Lưu ý**: Nếu dữ liệu quá lớn, tăng `batchSize` để tiết kiệm thời gian.

##### **🔹 Node 10: Merge Data (Code)**
- **Script**: Node này kết hợp dữ liệu từ nhiều nguồn thành một JSON duy nhất. **Không cần chỉnh sửa** trừ khi cấu trúc dữ liệu thay đổi.

##### **🔹 Node 11 & 12: Create a Database Page (Notion)**
- **Credentials**: Chọn `notion` (đã cấu hình token).
- **Key Parameters**:
  - `databaseId`: ID của database Notion đã tạo sẵn.
  - `properties`: Cần định nghĩa các thuộc tính phù hợp với Brand DNA (ví dụ: `Company Name`, `Description`, `ICP`, etc.).
  - **Lưu ý**: Nếu database của các sếp chưa có, cần tạo trước và lấy `databaseId` từ URL Notion.

##### **🔹 Node 13 & 14: Code in JavaScript (Format Data)**
- **Script**: Node này định dạng dữ liệu JSON thành dạng phù hợp với Notion blocks. **Không cần chỉnh sửa** trừ khi cấu trúc Notion thay đổi.

##### **🔹 Node 15: Set URL (Code)**
- **Script**: Thiết lập URL cho trang Notion mới tạo. **Không cần chỉnh sửa** trừ khi cấu trúc URL thay đổi.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Submit một form mẫu vào JotForm để kiểm tra workflow.
   - Kiểm tra **log** trong n8n để phát hiện lỗi (ví dụ: lỗi API, dữ liệu không hợp lệ).
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt cho AI**:
   - Thử các prompt khác nhau để cải thiện chất lượng phân tích. Ví dụ:
     - Để AI tập trung vào **khách hàng mục tiêu**, thêm câu: `"Focus on the Ideal Customer Profile section."`
     - Để AI trích xuất **bằng chứng hỗ trợ**, thêm: `"Include all customer testimonials and case studies."`
2. **Lưu Log cho Dữ Liệu**:
   - Sử dụng **node StickyNote** để lưu log của mỗi workflow thành công/lỗi. Ví dụ:
     ```json
     {
       "type": "stickyNote",
       "name": "Log Workflow",
       "credentials": ["stickyNote"],
       "parameters": {
         "text": "Workflow executed for {{ $node["JotForm Trigger"]["json"]["Company Name"] }} at {{ $node["JotForm Trigger"]["json"]["timestamp"] }}"
       }
     }
     ```
3. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Slack/Telegram** để thông báo khi có báo cáo Brand DNA mới được tạo. Ví dụ:
     ```json
     {
       "type": "slack",
       "name": "Notify Slack",
       "credentials": ["slack"],
       "parameters": {
         "text": "New Brand DNA Report for {{ $node["JotForm Trigger"]["json"]["Company Name"] }} is ready! 🚀",
         "channel": "#brand-research"
       }
     }
     ```
4. **Tích Hợp với Google Drive**:
   - Sau khi tạo báo cáo Notion, tự động lưu bản PDF vào Google Drive. Ví dụ:
     ```json
     {
       "type": "googleDrive",
       "name": "Save PDF to Drive",
       "credentials": ["googleDrive"],
       "parameters": {
         "file": {
           "content": "{{ $node["Create a Database Page"]["json"]["url"] }}",
           "mimeType": "application/pdf"
         },
         "name": "{{ $node["JotForm Trigger"]["json"]["Company Name"] }}_BrandDNA.pdf"
       }
     }
     ```

---

### 📌 **Kết luận**
Workflow **Brand DNA Generator** là giải pháp **tự động hóa hoàn toàn** để các sếp:
✅ **Tiết kiệm thời gian** lên đến 80% trong việc nghiên cứu Brand.
✅ **Đảm bảo tính nhất quán** với phân tích AI tiên tiến.
✅ **Lưu trữ dữ liệu** một cách chuyên nghiệp vào Notion, sẵn sàng chia sẻ và theo dõi.

**Hành động ngay hôm nay**:
1. Chuẩn bị các **API Key** và **credentials** như hướng dẫn.
2. Import workflow và **cấu hình các node quan trọng**.
3. **Test với một công ty mẫu** và xem kết quả AI tự động tạo báo cáo Brand DNA như thế nào!
4. **Tích hợp thêm Slack/Telegram** để nhận thông báo khi có báo cáo mới.

**Nếu các sếp muốn tối ưu workflow này hơn, có thể:**
- Thử các **model AI khác** (ví dụ: Mistral, Llama) để cải thiện chất lượng phân tích.
- **Tự động hóa thêm** việc gửi báo cáo đến email của các sếp.
- **Tích hợp với CRM** (HubSpot, Salesforce) để cập nhật thông tin Brand vào hệ thống quản lý khách hàng.

**Chúc các sếp thành công trong việc tự động hóa Brand DNA của công ty!** 🚀