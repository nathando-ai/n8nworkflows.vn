---
title: "🚀 Tự Động Hóa Xác Minh & Soạn Thảo Email LinkedIn Tự Động Với Airtable, Apify & AI Claude (N8N)"
description: "Workflow này tự động lấy dữ liệu từ LinkedIn, phân tích chất lượng lead, và soạn thảo email outreach cá nhân hóa 100% tự động - tiết kiệm 10+ giờ/ngày cho các sếp bán hàng và marketing. Kết hợp AI Claude, Airtable và công cụ web scraping để tối ưu hóa quy trình lead generation."
slug: "tu-dong-hoa-xac-minh-lead-linkedin-voi-airtable-claude"
tags: [n8n, automation, lead-generation, ai-summarization, airtable, linkedin-scraping, claude-ai]
keywords: [n8n workflow lead generation, tự động hóa xác minh lead LinkedIn, AI Claude trong n8n, Airtable + LinkedIn automation, soạn thảo email outreach tự động]
---

# 🚀 **Tự Động Hóa Xác Minh Lead LinkedIn & Soạn Thảo Email Outreach Cá Nhân Hóa**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Bán Hàng & Marketing**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** thông tin trên LinkedIn (profiles, posts, company info) để đánh giá chất lượng lead.
- **Soạn thảo email outreach** một cách chung chung, không cá nhân hóa, dẫn đến tỷ lệ phản hồi thấp.
- **Làm mất thời gian** vào việc phân loại lead (qualified/unqualified) thay vì tập trung vào bán hàng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy dữ liệu** từ LinkedIn (profile, posts, company info) và Airtable.
✅ **Xác minh lead** bằng AI Claude (đánh giá tính phù hợp, mức độ hứng thú).
✅ **Soạn thảo email outreach** cá nhân hóa, sẵn sàng gửi ngay.
✅ **Cập nhật trạng thái lead** trong Airtable (qualified/unqualified/LinkedIn unavailable).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ/ngày** cho việc tìm kiếm và phân tích lead.
- **Tỷ lệ phản hồi cao hơn** nhờ email outreach cá nhân hóa.
- **Dữ liệu lead chính xác** với AI Claude phân tích hành vi, công ty và nội dung LinkedIn.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **GDPR-compliant** (phù hợp với quy định bảo mật EU).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Airtable Account** (để lưu trữ lead và thông tin outreach):
   - Base với bảng `Leads` (cột: `Name`, `Email`, `LinkedIn URL`, `Company`, `Status`, `Message Draft`).
   - Base với bảng `Prompts` (để lưu các template AI Claude).
2. **API Key LinkedIn** (để lấy dữ liệu profile/posts/company):
   - [Lấy API Key LinkedIn](https://www.linkedin.com/developers/) (nếu cần, sử dụng **Lusha API** để lấy email từ LinkedIn URL).
3. **API Key Claude (Anthropic)**:
   - [Đăng ký tại Anthropic](https://www.anthropic.com/) để sử dụng AI Claude Sonnet.
4. **Firecrawl API Key** (để scraping website công ty):
   - [Đăng ký tại Mendable](https://www.mendable.ai/) (hoặc sử dụng node `httpRequest` thay thế).
5. **Credentials trong n8n**:
   - Thiết lập **Airtable**, **Claude**, và **Firecrawl** trong `n8n Credentials`.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/16002](https://n8n.io/workflows/16002) và import vào n8n Editor.
- **Copy/Paste JSON** vào tab `Workflow` trong n8n (đảm bảo đã đăng nhập và có quyền edit).

:::note[**Lưu Ý**]
- **Không** sử dụng phiên bản n8n Community (n8n.io) để chạy workflow này 24/7 (do giới hạn tài nguyên).
- **Cài đặt n8n Self-hosted** trên VPS để đảm bảo ổn định.
:::

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Airtable**
1. **Node `Fetch Leads from Airtable`**:
   - Chọn **Base** và **Table** là `Leads`.
   - Cấu hình **Filter** để lấy lead có `Status = "New"` (hoặc tùy chỉnh theo yêu cầu).
   - **Output**: Dữ liệu lead sẽ được loop qua `Loop Over Leads`.

2. **Node `Save Message to Airtable`**:
   - Chọn **Base** và **Table** là `Leads`.
   - Cấu hình **Update Record** để cập nhật cột `Message Draft` và `Status`.

3. **Node `Fetch Prompt from Airtable`**:
   - Chọn **Base** và **Table** là `Prompts`.
   - Lấy **Prompt Template** cho AI Claude (ví dụ: `Qualification Prompt` và `Redaction Prompt`).

#### **B. Cấu Hình LinkedIn API**
1. **Node `Fetch LinkedIn Profile Info`**:
   - Sử dụng **Lusha API** (hoặc API LinkedIn chính thức) để lấy thông tin profile từ URL.
   - **Headers**:
     ```json
     {
       "Authorization": "Bearer YOUR_LUSHA_API_KEY",
       "Content-Type": "application/json"
     }
     ```
   - **Request Body**:
     ```json
     {
       "url": "{{$node["Loop Over Leads"].json["$.url"]}}"
     }
     ```

2. **Node `Fetch LinkedIn Posts`**:
   - Sử dụng **Graph API LinkedIn** hoặc **Firecrawl** để lấy posts gần đây.
   - **Lưu ý**: LinkedIn có giới hạn API, nên sử dụng **Firecrawl** để scraping an toàn.

3. **Node `Scrape Company Homepage`**:
   - Nếu công ty có trang web, **Firecrawl** sẽ lấy nội dung HTML và chuyển thành Markdown.
   - **Input**: URL công ty từ LinkedIn.
   - **Output**: Dữ liệu sạch sẽ được xử lý bởi `Clean Scraped Markdown`.

#### **C. Cấu Hình AI Claude (Anthropic)**
1. **Node `Claude Sonnet - Qualification`**:
   - **Model**: `claude-2.1` (hoặc `claude-instant-1.2`).
   - **Prompt**:
     ```plaintext
     Analyze the LinkedIn profile and posts of {{$.name}} from {{$.company}}.
     Based on their recent activity, industry trends, and content, assign a qualification score (1-10) and suggest if they are a good fit for our product/service.
     Also, extract key pain points and interests.
     ```
   - **Output Parser**: `Parse Qualification Output` (định dạng JSON).

2. **Node `Claude Sonnet - Redaction`**:
   - **Prompt**:
     ```plaintext
     Based on the lead data, draft a personalized outreach email for {{$.name}}.
     Include:
     - A hook related to their recent posts.
     - A brief introduction about our product.
     - A clear CTA.
     Keep it concise (under 200 words).
     ```
   - **Output Parser**: `Parse Redaction Output`.

#### **D. Cấu Hình Agent AI (LangChain)**
1. **Node `Lead Qualification Agent`**:
   - Kết nối với **Claude** và sử dụng **Output Parser Structured** để phân tích kết quả.
   - **Lưu ý**: Cấu hình **tools** cho agent để lấy dữ liệu từ Airtable và LinkedIn.

2. **Node `Message Drafting Agent`**:
   - Sử dụng kết quả từ `Claude Sonnet - Redaction` để tạo email outreach.
   - **Output**: Email sẵn sàng gửi, được lưu vào Airtable.

#### **E. Cấu Hình Logic If/Else**
1. **Node `If Lead Qualifies`**:
   - Kiểm tra `qualification_score` từ Claude (nếu > 7, lead được đánh giá là `Qualified`).
   - Nếu **không**, chuyển sang `Mark Lead as Not Qualified`.

2. **Node `If LinkedIn Profile Available`**:
   - Kiểm tra nếu LinkedIn URL không trả về dữ liệu, thì **bỏ qua** và đánh dấu `LinkedIn Unavailable`.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Chọn **1 lead mẫu** từ Airtable và chạy `Execute Workflow`.
   - Kiểm tra:
     - Dữ liệu LinkedIn được lấy đúng không?
     - AI Claude phân tích và soạn thảo email có logic không?
     - Airtable được cập nhật trạng thái và email draft không?

2. **Bật Active**:
   - Sau khi test thành công, **bật `Active`** và chọn `Manual Trigger` để chạy khi có lead mới.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Với Slack/Telegram**
- Thêm **node `n8n-nodes-base.slack`** sau `Save Message to Airtable` để thông báo khi có lead mới được xử lý.
- **Example**:
  ```json
  {
    "text": `New lead processed: {{$.name}} ({{$.company}}). Status: {{$.status}}`
  }
  ```

### **2. Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng **node `n8n-nodes-base.set`** để lưu lịch sử vào Airtable.
- **Node `n8n-nodes-base.manualTrigger`** + **node `n8n-nodes-base.schedule`** để chạy báo cáo hàng tuần.

### **3. Cải Tiến Prompt AI**
- **Tối ưu hóa Prompt** cho Claude bằng cách:
  - Thêm **ví dụ cụ thể** về lead đã được xác minh thành công.
  - Yêu cầu AI **tránh lặp lại** thông tin đã có trong profile.

### **4. Sử Dụng Multiple AI Models**
- Thay vì chỉ Claude, kết hợp **GPT-4** (OpenAI) hoặc **Gemini** (Google) để so sánh kết quả.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại, đồng thời **tăng tỷ lệ chuyển đổi lead** nhờ AI và cá nhân hóa. **Chỉ cần 1 lần setup**, workflow sẽ hoạt động tự động 24/7!

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (đăng ký [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm **VPSN8N**).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa lead generation!

---
**🚀 Cần hỗ trợ?** Đăng ký [tư vấn miễn phí](https://n8n.io/community) từ Allan Vaccarizi (tác giả workflow) để tối ưu hóa hiệu quả!