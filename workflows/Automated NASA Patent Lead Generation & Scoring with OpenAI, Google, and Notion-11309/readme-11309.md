---
title: "🚀 Tự Động Hóa Khám Phá & Đánh Giá Lead Doanh Nghiệp NASA với OpenAI, Google & Notion"
description: "Workflow tự động hóa tìm kiếm, phân tích và đánh giá các startup phù hợp với công nghệ của NASA, tự động soạn thảo email outreach và lưu trữ lead vào Notion - tiết kiệm thời gian cho các bộ phận chuyển giao công nghệ và phát triển kinh doanh."
slug: "tieu-dong-hoa-kham-pha-lead-nasa-voi-openai-google-notion"
tags: [n8n, automation, lead-generation, ai-summarization, tech-transfer, no-code]
keywords: [n8n workflow tự động hóa, tìm kiếm lead NASA, AI phân tích startup, tự động soạn thảo email, Notion CRM, công nghệ không code]
---

# 🚀 **Tự Động Hóa Khám Phá Lead Doanh Nghiệp NASA với AI & Notion**

## **Nỗi Đau Của Các Sếp**
Các bộ phận **Chuyển Giao Công Nghệ (Tech Transfer)** và **Phát Triển Kinh Doanh (Business Development)** của NASA hoặc các tổ chức nghiên cứu phải mất **tuần ngày** để:
✅ **Tìm kiếm thủ công** các startup hoặc doanh nghiệp có thể ứng dụng công nghệ NASA.
✅ **Phân tích từng lead** xem họ có phù hợp với công nghệ của NASA không.
✅ **Soạn thảo email outreach** cá nhân hóa cho từng đối tượng.
✅ **Lưu trữ và theo dõi lead** trong nhiều hệ thống khác nhau.

**Workflow này giải quyết tất cả bằng AI + tự động hóa 100% không cần code!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** tìm kiếm và phân tích lead.
- **Đánh giá chính xác** sự phù hợp giữa công nghệ NASA và startup bằng AI.
- **Email outreach tự động** với nội dung cá nhân hóa.
- **Lưu trữ lead trong Notion** với thông tin chi tiết (đánh giá, liên kết LinkedIn, email, website).
- **Hoạt động liên tục** mà không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản API NASA** (miễn phí tại [api.nasa.gov](https://api.nasa.gov/)).
2. **Tài khoản Apify** (đăng ký tại [apify.com](https://apify.com/)) và **các actor sau**:
   - `google-search-scraper` (tìm kiếm Google).
   - `website-content-crawler` (lấy nội dung website).
3. **API Key OpenAI** (đăng ký tại [openai.com](https://openai.com/)).
4. **Tài khoản Notion** và **Database Lead** với các trường sau:
   - `Company` (Text)
   - `Website` (URL)
   - `LinkedIn` (URL)
   - `Email` (Email)
   - `Score` (Number)
   - `Draft Email` (Text)
   - `NASA Tech` (Text)
5. **Tài khoản n8n** (cài đặt [self-hosted](https://n8n.io/) hoặc dùng [n8n.cloud](https://n8n.io/)).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11309](https://n8n.io/workflows/11309) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Import** để hoàn tất.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/11309](https://n8n.io/workflows/11309).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. Chọn **Import** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Manual Trigger**
- **Không cần chỉnh sửa**, chỉ dùng để kích hoạt workflow thủ công.

#### **🔹 Node 2: Configuration (Set)**
- **Điền `keyword`** (ví dụ: `"quantum computing"`, `"AI satellite"`) để tìm kiếm patent NASA liên quan.
- **Ví dụ**:
  ```json
  {
    "keyword": "AI in space technology"
  }
  ```

#### **🔹 Node 3: NASA Patents API (HTTP Request)**
- **Thay thế URL API** từ:
  ```
  https://api.nasa.gov/search/patents?q={keyword}
  ```
  thành:
  ```
  https://api.nasa.gov/search/patents?q={{ $node["Configuration"].json["keyword"] }}
  ```
- **Thêm Header `X-API-Key`** với API Key NASA của bạn.

#### **🔹 Node 4: Google Search - Find Company (Apify)**
- **Chọn actor**: `google-search-scraper`.
- **Tham số cần điền**:
  - `query`: `{{ $node["NASA Patents API"].json["title"] }} + "company" + "startup"` (tìm kiếm công ty liên quan đến patent).
  - `maxItems`: `5` (lấy 5 kết quả đầu tiên).
- **Lưu ý**: Cần **cài đặt actor** trong tài khoản Apify trước.

#### **🔹 Node 5: Extract Company URL (Code)**
- **Không cần chỉnh sửa**, node này tự động trích xuất URL từ kết quả Google.

#### **🔹 Node 6: Crawl Company Website (Apify)**
- **Chọn actor**: `website-content-crawler`.
- **Tham số cần điền**:
  - `url`: `{{ $node["Extract Company URL"].json["url"] }}`.
  - `selectors`: `["h1", "p", "a"]` (lấy tiêu đề, đoạn văn bản và liên kết).
- **Lưu ý**: Cần **cài đặt actor** trong tài khoản Apify trước.

#### **🔹 Node 7: Analyze Fit & Draft Email (OpenAI)**
- **Chọn model OpenAI**: `gpt-3.5-turbo` (hoặc `gpt-4` nếu có).
- **Prompt mẫu** (có thể chỉnh sửa):
  ```
  Analyze the NASA patent: {{ $node["NASA Patents API"].json["title"] }}
  and the company website: {{ $node["Crawl Company Website"].json["content"] }}.
  Score the fit (1-10) and draft a personalized outreach email.
  ```
- **Lưu ý**: Đảm bảo **API Key OpenAI** đã được cấu hình trong n8n.

#### **🔹 Node 8: High Score Filter (If)**
- **Điều kiện**: `{{ $node["Analyze Fit & Draft Email"].json["score"] }} > 7`.
- **Nếu true**: Tiếp tục lấy LinkedIn và lưu vào Notion.
- **Nếu false**: Bỏ qua lead.

#### **🔹 Node 9: Google Search - Find LinkedIn (Apify)**
- **Chọn actor**: `google-search-scraper`.
- **Tham số cần điền**:
  - `query`: `{{ $node["Extract Company URL"].json["url"] }} + "LinkedIn"`.
  - `maxItems`: `1`.

#### **🔹 Node 10: Create Notion Lead (Notion)**
- **Chọn Database ID** của Notion (đã tạo trước).
- **Tham số cần điền**:
  - `properties`:
    ```json
    {
      "Company": "{{ $node["Extract Company URL"].json["title"] }}",
      "Website": "{{ $node["Extract Company URL"].json["url"] }}",
      "LinkedIn": "{{ $node["Google Search - Find LinkedIn"].json["url"] }}",
      "Email": "{{ $node["Analyze Fit & Draft Email"].json["email"] }}",
      "Score": "{{ $node["Analyze Fit & Draft Email"].json["score"] }}",
      "Draft Email": "{{ $node["Analyze Fit & Draft Email"].json["email"] }}",
      "NASA Tech": "{{ $node["NASA Patents API"].json["title"] }}"
    }
    ```
- **Lưu ý**: Đảm bảo **Database Notion** đã có tất cả trường yêu cầu.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra từng node.
   - Đảm bảo **API Key** và **credentials** đã đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tự Động Hoạt Động Hàng Ngày**
- **Sử dụng Webhook** thay vì **Manual Trigger** để chạy workflow tự động hàng ngày.
- **Cấu hình Cron Job** trên VPS để kích hoạt workflow định kỳ.

### **2. Lưu Log & Theo Dõi Lead**
- **Thêm node `stickyNote`** để ghi log lỗi hoặc thông báo thành công.
- **Kết hợp với Slack/Telegram** để nhận báo cáo tự động.

### **3. Cải Tiến Prompt OpenAI**
- **Định hình prompt** để AI trả về **email dài hơn** hoặc **các gợi ý liên lạc khác**.
- **Ví dụ**:
  ```
  Draft a 3-paragraph email with call-to-action, and suggest 2 alternative contact methods.
  ```

### **4. Lọc Lead Theo Đánh Giá**
- **Thêm node `set`** để **lưu lead có score > 8** vào Notion Database khác (đối tượng ưu tiên).

### **5. Kết Nối với Email Marketing**
- **Export lead từ Notion** vào **Mailchimp/HubSpot** để gửi email tự động.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong **Chuyển Giao Công Nghệ** và **Phát Triển Kinh Doanh** để tập trung vào **đàm phán và hợp tác** thay vì tìm kiếm lead thủ công.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa khám phá lead NASA của bạn!**

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/11309)**
**💬 Có thắc mắc? Hỏi tại [Community n8n](https://community.n8n.io/)**