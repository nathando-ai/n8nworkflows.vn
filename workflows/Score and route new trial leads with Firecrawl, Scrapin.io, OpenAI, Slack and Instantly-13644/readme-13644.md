---
title: "🚀 Tự Động Hóa Chuyển Đổi Lead Tiềm Năng với AI, Scraping & Slack (N8n)"
description: "Workflow tự động hóa 100% không code để đánh giá, phân loại và chuyển đổi lead mới từ form đăng ký thành cơ hội bán hàng cao giá trị. Giúp doanh nghiệp tiết kiệm 300+ giờ/năm và tăng tỷ lệ phản hồi lên 20x so với trung bình ngành."
slug: "tieu-dong-hoa-chuyen-doi-lead-voi-ai-scraping-slack"
tags: [n8n, automation, lead-generation, ai-summarization, sales-intelligence, scraping, slack-integration]
keywords: [n8n workflow lead generation, tự động hóa chuyển đổi lead, scoring lead với AI, scraping website với firecrawl, n8n và openai, tự động hóa bán hàng B2B]
---

# 🚀 **Tự Động Hóa Chuyển Đổi Lead Tiềm Năng với AI, Scraping & Slack (N8n)**

## **🔥 Giới Thiệu: Tự Động Hóa Lead Tiềm Năng Cho Doanh Nghiệp B2B**
Hiện nay, các sếp và đội ngũ marketing/sales phải mất **giờ đồng hồ** để:
- Lọc và đánh giá lead mới từ form đăng ký.
- Xác thực thông tin công ty (website, LinkedIn, số lượng nhân viên).
- Phân loại lead theo độ phù hợp với ICP (Ideal Customer Profile).
- Gửi thông tin cho đội ngũ bán hàng qua Slack/email.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa 100% quá trình** từ nhận lead đến phân loại và chuyển đổi.
✅ **Đánh giá lead bằng AI** (OpenAI) và scraping (Firecrawl) để lấy thông tin chính xác.
✅ **Phân loại lead theo điểm số** (Very High, High, Mid, Low) và chuyển vào các chiến dịch phù hợp.
✅ **Gửi thông báo Slack đẹp mắt** với tất cả thông tin cần thiết cho đội ngũ bán hàng.
✅ **Tránh trùng lặp lead** bằng cách kiểm tra trong CRM (Instantly).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 300+ giờ/năm** cho đội ngũ marketing và sales.
- **Tăng tỷ lệ phản hồi lên 20x** so với trung bình ngành (20.8% vs 1%).
- **Chuyển đổi lead nhanh chóng** với thông tin chính xác từ AI và scraping.
- **Phân loại lead tự động** theo độ phù hợp với ICP, giúp đội ngũ bán hàng tập trung vào lead có giá trị cao nhất.
- **Tránh trùng lặp lead** bằng cách kiểm tra trong CRM (Instantly).
- **Thông báo Slack đẹp mắt** với tất cả thông tin cần thiết (điểm số, thông tin công ty, liên kết LinkedIn, website).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Keys & Credentials:**
   - **OpenAI API Key** (để sử dụng AI Chatbot và Structured Output Parser).
   - **Firecrawl API Key** (để scraping website và lấy thông tin LinkedIn).
   - **Slack API Token** (để gửi thông báo Slack).
   - **Instantly API Key** (để quản lý lead và CRM).
   - **Webhook URL** (để nhận lead từ form đăng ký, Intercom, Webflow, etc.).

2. **Dịch vụ & API:**
   - **Scrapin.io** (để enrich thông tin công ty, có thể thay thế bằng alternative).
   - **Instantly** (CRM để quản lý lead và chiến dịch).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13644](https://n8n.io/workflows/13644).
- **Mở n8n Editor** và chọn **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc copy/paste JSON** từ file vào Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **48 node** và cần cấu hình cẩn thận. Dưới đây là các node quan trọng cần chú ý:

##### **🔹 Node Webhook (Triggers)**
- **Path:** `/new-lead`
- **HTTP Method:** `POST`
- **Lưu ý:** Đảm bảo webhook này được kết nối với nguồn lead (form đăng ký, Intercom, Webflow, etc.).

##### **🔹 Node Firecrawl Scrape (Scraping Website)**
- **API Key:** Điền `firecrawlApi` (từ Credentials).
- **Operation:** `scrape`
- **Lưu ý:** Firecrawl sẽ scraping website để tìm URL LinkedIn của công ty. Nếu website không tồn tại, workflow sẽ tự động bỏ qua.

##### **🔹 Node LinkedIn Agent (AI Enrichment)**
- **Input:** URL LinkedIn của công ty (được lấy từ Firecrawl).
- **Output:** Thông tin công ty như tên, số lượng nhân viên, vị trí HQ, ngành nghề, mô tả.
- **Lưu ý:** Nếu LinkedIn không tồn tại hoặc là profile cá nhân, workflow sẽ bỏ qua.

##### **🔹 Node OpenAI (Scoring & Sanitize Data)**
- **API Key:** Điền `openAiApi` (từ Credentials).
- **Model:** `gpt-5.2` (hoặc thay thế bằng `gpt-4` nếu không có).
- **Lưu ý:**
  - **Normalize Country:** Chuyển "Sheridan, US" → "United States".
  - **Extract Name From Email:** Chuyển `john.smith@company.com` → "John Smith".
  - **Sanitize Description:** Làm sạch mô tả công ty để phù hợp với Slack.

##### **🔹 Node Slack (Send Notification)**
- **API Token:** Điền `slackApi` (từ Credentials).
- **Channel:** Chọn channel Slack để gửi thông báo.
- **Rich Blocks:** Workflow sẽ tự động tạo blocks Slack đẹp mắt với:
  - Email, tên công ty, điểm số, số lượng nhân viên, ngành nghề, mô tả.
  - Nhiều button hành động (Visit LinkedIn, Visit Website).

##### **🔹 Node Instantly (CRM & Campaign Management)**
- **API Key:** Điền `instantlyApi` (từ Credentials).
- **Operation:** `getMany` (kiểm tra lead đã tồn tại) và `addToCampaign` (thêm lead vào chiến dịch).
- **Lưu ý:** Workflow sẽ kiểm tra lead đã tồn tại trong Instantly trước khi thêm vào chiến dịch.

##### **🔹 Node Code (Scoring Logic)**
- **Score Country:** Điểm từ 0-10 dựa trên thị trường.
- **Score Staff Count:** Điểm từ 0-10 dựa trên số lượng nhân viên.
- **Industry Scoring:** Điểm từ 0-10 dựa trên ngành nghề.
- **Algo Score:** Tính điểm tổng hợp (0-100) và phân loại lead (Very High, High, Mid, Low).

##### **🔹 Node If (Routing Based on Score)**
- **Very High (90-100):** Lead có giá trị cao nhất.
- **High (70-89):** Lead có giá trị cao.
- **Mid (50-69):** Lead trung bình.
- **Low (0-49):** Lead có giá trị thấp (có thể bỏ qua hoặc chuyển vào chiến dịch khác).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run Dữ Liệu Mẫu:**
   - Tạo một lead mẫu (ví dụ: `john.doe@company.com` với website `company.com`).
   - Gửi request POST đến webhook (`/new-lead`).
   - Kiểm tra kết quả trong Slack và Instantly.

2. **Bật Active Workflow:**
   - Sau khi test thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logs & Monitoring:**
   - Sử dụng node **StickyNote** để ghi chú và debug.
   - Thêm node **HTTP Request** để log dữ liệu vào Google Sheets hoặc database.

2. **Kết Nối Với CRM Khác:**
   - Thay thế **Instantly** bằng **HubSpot, Salesforce, Pipedrive** bằng cách sử dụng node **HTTP Request** hoặc **CUSTOM** của CRM đó.

3. **Tự Động Gửi Email Báo Cáo:**
   - Sử dụng node **Email** (Gmail/SMTP) để gửi báo cáo hàng tuần về lead mới và điểm số.

4. **Tăng Cường AI với LangChain:**
   - Sử dụng **Agent** và **OutputParserStructured** để cải thiện chất lượng enrichment thông tin.

5. **Tối Ưu Scoring Logic:**
   - Sửa đổi code trong node **Score Country**, **Score Staff Count**, **Industry Scoring** để phù hợp với ICP của doanh nghiệp.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa quá trình chuyển đổi lead từ form đăng ký thành cơ hội bán hàng cao giá trị. Với **AI, scraping, và Slack**, các sếp sẽ tiết kiệm thời gian, tăng tỷ lệ phản hồi và cải thiện hiệu quả bán hàng.

**🚀 Hãy áp dụng ngay và xem kết quả!**
Nếu có vấn đề, liên hệ với tác giả **Brandon Charleson** qua [LinkedIn](https://www.linkedin.com/in/brandon-charleson) hoặc email `brandon@topoffunnel.com`.

---
**💡 Lưu ý cuối cùng:**
- Workflow này **đã được test và chạy sản xuất** trên n8n.
- Đảm bảo **backup workflow** trước khi import.
- **Không cần code** – chỉ cần cấu hình các API key và credentials.