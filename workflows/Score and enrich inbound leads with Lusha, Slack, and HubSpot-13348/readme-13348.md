---
title: "🚀 Tự Động Hóa & Đánh Giá Lead Inbound với Lusha, Slack & HubSpot - Giúp Các Sếp Tiết Kiệm 100% Thời Gian Chăm Sóc Lead"
description: "Workflow tự động nhận, enrich và phân loại lead inbound theo độ ưu tiên (Hot/Warm/Cold) dựa trên dữ liệu Lusha, gửi thông báo Slack và cập nhật HubSpot một cách tự động - không cần code. Giúp các sếp tập trung vào lead có tiềm năng cao nhất."
slug: "tieu-dong-hoa-lead-scoring-lusha-slack-hubspot"
tags: [n8n, automation, lead-generation, sales-automation, lusha, hubspot, slack, no-code]
keywords: [n8n workflow lead scoring, tự động hóa đánh giá lead, Lusha API n8n, tự động hóa HubSpot Slack, cách tự động nhận lead từ form]
---

# 🚀 **Tự Động Hóa & Đánh Giá Lead Inbound với Lusha, Slack & HubSpot**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp Growth, RevOps hay Sales thường phải mất **giờ đồng hồ** mỗi ngày để:
✅ **Lọc và đánh giá** hàng trăm lead mới từ form đăng ký, landing page hay marketing automation.
✅ **Tra cứu thông tin chi tiết** của lead (độ cao trong công ty, công ty có bao nhiêu nhân viên, ngành nghề phù hợp ICP, số điện thoại, email xác thực).
✅ **Phân loại lead** thành Hot (sẵn sàng mua ngay), Warm (cần outreach), hoặc Cold (cần nurture dài hạn).
✅ **Gửi thông báo** cho đội SDR hoặc cập nhật CRM (HubSpot) một cách thủ công.

**Kết quả?** Thời gian của các sếp bị "chôn vùi" trong công việc lặp lại, trong khi lead có tiềm năng cao bị bỏ qua.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✔ **Tiết kiệm 80% thời gian** trong việc đánh giá và phân loại lead.
✔ **Cập nhật HubSpot tự động** với dữ liệu enrich từ Lusha (độ cao trong công ty, ngành nghề, số điện thoại, email).
✔ **Phân loại lead chính xác** theo độ ưu tiên (Hot/Warm/Cold) dựa trên **điểm số tự động** (lead scoring).
✔ **Nhận thông báo Slack ngay lập tức** khi có lead Hot (sẵn sàng mua) để đội SDR có thể liên hệ kịp thời.
✔ **Tự động gửi lead Warm vào chiến dịch outreach** và lead Cold vào chiến dịch nurture dài hạn.
✔ **Hỗ trợ quyết định** bằng dữ liệu (AI Summarization) về lead có tiềm năng cao nhất.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Lusha** (đăng ký tại [lusha.com](https://www.lusha.com/)) và **API Key** của Lusha.
2. **Tài khoản HubSpot** (CRM) và **API Key** hoặc **OAuth 2.0 Credentials**.
3. **Tài khoản Slack** và **OAuth Token** (để gửi thông báo).
4. **Webhook URL** của workflow (sẽ được cung cấp sau khi import).
5. **Lead Capture Form** (hoặc landing page) được cấu hình gửi dữ liệu đến webhook này (chỉ cần email của lead).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Bước 1: Tải Workflow JSON**
- Tải file JSON từ [n8n.io/workflows/13348](https://n8n.io/workflows/13348) (hoặc copy toàn bộ JSON từ link trên).
- **Lưu ý:** Nếu không tải được, các sếp có thể **copy toàn bộ JSON** từ link trên và paste vào n8n Editor.

#### **Bước 2: Import vào n8n**
- Mở **n8n Editor** (n8n.io hoặc self-hosted).
- Nhấn **Import** (icon "↑" ở góc trên bên trái).
- Chọn **Paste JSON** và dán toàn bộ nội dung JSON từ link trên.
- Nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
#### **🔹 Node 1: New Lead Webhook**
- **Path:** Đã cấu hình là `/lead-scoring` (không cần thay đổi).
- **HTTP Method:** POST (không cần thay đổi).
- **Lưu ý:** Các sếp cần **cấu hình lead capture form** (hoặc landing page) gửi dữ liệu POST đến URL webhook này.
  - **Dữ liệu cần gửi:** Chỉ cần **email** của lead (các sếp có thể thêm dữ liệu khác như tên, công ty, nếu muốn).

#### **🔹 Node 2: Validate Email (Code Node)**
- **Mục đích:** Kiểm tra email có hợp lệ hay không.
- **Lưu ý:** Nếu email không hợp lệ, workflow sẽ **bỏ qua lead** (không enrich hoặc scoring).
- **Không cần chỉnh sửa** (n8n đã tự động validate).

#### **🔹 Node 3: Enrich with Lusha**
- **Cấu hình Lusha:**
  - **API Key:** Điền **API Key** từ Lusha (tìm trong tài khoản Lusha → Settings → API Keys).
  - **Email Field:** Chọn trường `email` từ input (đã cấu hình tự động).
  - **Output Fields:** Chọn tất cả các trường cần enrich (ví dụ: `name`, `job_title`, `company_name`, `company_size`, `phone`, `industry`).
- **Lưu ý:**
  - Nếu Lusha trả về **error**, các sếp cần kiểm tra **API Key** có đúng không.
  - Thời gian enrich ~1-2 giây/lead (tùy tốc độ API Lusha).

#### **🔹 Node 4: Calculate Lead Score (Code Node)**
- **Mục đích:** Tính điểm số lead dựa trên **ICP (Ideal Customer Profile)** của doanh nghiệp.
- **Cấu hình:**
  - **Điểm số mặc định** (các sếp có thể chỉnh sửa trong code):
    ```javascript
    let score = 0;

    // Seniority
    if (jobTitle.includes("VP") || jobTitle.includes("CEO") || jobTitle.includes("CTO")) score += 30;
    else if (jobTitle.includes("Director")) score += 20;
    else if (jobTitle.includes("Manager")) score += 10;

    // Company size
    if (companySize && parseInt(companySize) >= 200) score += 20;

    // Industry match (ví dụ: nếu ICP là SaaS)
    if (industry && industry.includes("SaaS")) score += 15;

    // Direct phone
    if (phone && phone.length > 5) score += 10;

    // Verified email
    if (email && email.includes("@")) score += 5;
    ```
  - **Lưu ý:** Các sếp **cần chỉnh sửa code** để phù hợp với **ICP của riêng mình** (ví dụ: thay "SaaS" thành "Fintech", thay "VP" thành "Head of Product").

#### **🔹 Node 5-11: Phân Loại Lead (If + Slack + HubSpot)**
- **Is Hot Lead? (Score >= 60)**
  - **Slack Alert:** Cấu hình **channel #hot-leads** và **message template** (ví dụ: `🔥 New Hot Lead: {{ $node["Enrich with Lusha"].json()["name"] }} ({{ $node["Enrich with Lusha"].json()["job_title"] }})`).
  - **HubSpot Upsert:** Chọn **Object: Contacts**, **Properties** cần cập nhật (ví dụ: `email`, `name`, `job_title`, `company`, `phone`, `lead_score`).
- **Is Warm Lead? (Score 35-59)**
  - **Slack Notify:** Cấu hình **channel #warm-leads** và **message template**.
  - **HubSpot Upsert:** Cập nhật tương tự như Hot Lead.
- **Cold Lead (<35)**
  - **HubSpot Upsert:** Cập nhật lead vào **chiến dịch nurture** (ví dụ: `nurture_campaign = "Cold Lead"`).

---
### **3. Kích Hoạt ⚡️**
#### **Bước 1: Test Run**
- **Gửi một email mẫu** từ lead capture form đến webhook.
- Kiểm tra:
  - Slack có nhận được thông báo không?
  - HubSpot có cập nhật lead không?
  - Điểm số lead có hợp lý không?

#### **Bước 2: Bật Active**
- Nhấn **Active** trên workflow.
- **Lưu ý:** Nếu workflow bị lỗi, các sếp nên **check log** trong n8n Dashboard.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Hợp với AI Summarization (N8N + LLM)**
- Sử dụng **node AI (n8n-nodes-ai)** để tự động **tóm tắt thông tin lead** từ Lusha (ví dụ: "Lead này là VP Marketing của công ty SaaS có 500 nhân viên, có số điện thoại trực tiếp").
- **Cách làm:**
  - Thêm node **AI (LLM)** sau node **Enrich with Lusha**.
  - Cấu hình **Prompt**:
    ```plaintext
    Summarize this lead in 3 sentences:
    - Name: {{ $node["Enrich with Lusha"].json()["name"] }}
    - Job Title: {{ $node["Enrich with Lusha"].json()["job_title"] }}
    - Company: {{ $node["Enrich with Lusha"].json()["company_name"] }}
    - Company Size: {{ $node["Enrich with Lusha"].json()["company_size"] }}
    - Industry: {{ $node["Enrich with Lusha"].json()["industry"] }}
    - Phone: {{ $node["Enrich with Lusha"].json()["phone"] }}
    ```
  - **Output** sẽ được gửi cùng Slack notification.

### **2. Lưu Log Lead vào Google Sheets (Dành Cho Analytics)**
- Thêm node **Google Sheets** sau node **Calculate Lead Score**.
- Cấu hình:
  - **Sheet Name:** "Lead Logs"
  - **Columns:** `email`, `name`, `job_title`, `company`, `lead_score`, `lead_tier`, `timestamp`.
- **Lợi ích:** Các sếp có thể **theo dõi hiệu suất** của workflow và phân tích lead.

### **3. Gửi Báo Cáo Định Kỳ (Hàng Tuần/Hàng Tháng)**
- Sử dụng **node Schedule** (n8n-nodes-base.schedule) để **tạo báo cáo tổng hợp** về lead trong tuần.
- **Cách làm:**
  - Thêm node **Schedule** (chạy hàng tuần).
  - Sau đó, thêm node **Google Sheets** hoặc **Slack** để gửi báo cáo.
  - **Dữ liệu báo cáo:**
    - Số lượng lead Hot/Warm/Cold.
    - Lead có điểm số cao nhất.
    - Lead được SDR liên hệ nhiều nhất.

### **4. Kết Nối với ZoomInfo (Ngoài Lusha)**
- Nếu Lusha không đủ dữ liệu, các sếp có thể **kết hợp với ZoomInfo** để enrich thêm thông tin.
- **Cách làm:**
  - Thêm node **ZoomInfo** (n8n-nodes-zoominfo) sau node **Enrich with Lusha**.
  - Cấu hình **API Key ZoomInfo** và **email** để enrich.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **lead có tiềm năng cao nhất**, đồng thời **tự động hóa toàn bộ quy trình** từ nhận lead đến phân loại và cập nhật CRM.

**🚀 Hành động ngay:**
1. **Import workflow** vào n8n.
2. **Cấu hình Lusha, HubSpot, Slack**.
3. **Chỉnh sửa lead scoring** phù hợp với ICP của doanh nghiệp.
4. **Test run** và bật Active.

**💡 Lưu ý cuối cùng:**
- Nếu gặp lỗi, **check log** trong n8n Dashboard.
- **Tối ưu hóa lead scoring** theo thời gian để phù hợp với thị trường.
- **Kết hợp với CRM khác** (Salesforce, Pipedrive) nếu cần.

**🎁 Đăng ký VPS TinoHost để self-host n8n 24/7:**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::