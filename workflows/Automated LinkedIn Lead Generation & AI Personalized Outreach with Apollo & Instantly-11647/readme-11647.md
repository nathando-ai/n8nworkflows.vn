---
title: "🚀 Tự Động Hóa Tìm Kiếm Lead LinkedIn + Gửi Tin Nhắn Cá Nhân Hóa AI - Giảm 90% Thời Gian Outreach"
description: "Workflow tự động hóa tìm kiếm lead LinkedIn từ Apollo, nghiên cứu công ty bằng AI (Tavily), và tạo tin nhắn outreach cá nhân hóa hoàn toàn tự động - không cần code. Giúp các sếp tiết kiệm 10+ giờ/ngày và tăng tỷ lệ phản hồi lên 30%."
slug: "tu-dong-hoa-lead-linkedin-ai-personalized-outreach"
tags: [n8n, automation, lead-generation, ai-personalized, apollo, instantly-ai, tavily, openai]
keywords: [n8n workflow lead linkedin, tự động hóa outreach, apollo scraper n8n, ai tạo tin nhắn cá nhân hóa, instant ai n8n, tavily research]
---

# 🚀 **Tự Động Hóa Tìm Kiếm Lead LinkedIn + Outreach Cá Nhân Hóa AI - Không Cần Code**

## **🔥 Nỗi Đau Của Các Sếp Trong Outreach LinkedIn**
Bạn đã từng:
- **Tốn 5-10 giờ/ngày** để tìm kiếm lead từ LinkedIn, Apollo hay Sales Navigator?
- **Gửi tin nhắn chung chung** mà tỷ lệ phản hồi chỉ ~5-10%?
- **Không biết cách cá nhân hóa** để lead chú ý đến bạn?
- **Phải mua lead từ Apollo** nhưng chất lượng không đảm bảo?

**Workflow này giải quyết tất cả!** Với **AI + Apollo + Instantly**, bạn sẽ:
✅ **Tìm kiếm lead tự động** từ Apollo (không cần nhập thủ công)
✅ **Nghiên cứu công ty** bằng Tavily (AI tìm kiếm thông tin chi tiết)
✅ **Tạo tin nhắn outreach cá nhân hóa** bằng GPT-4 (không copy-paste)
✅ **Gửi tin nhắn tự động** qua Instantly AI (tăng tỷ lệ mở tin nhắn lên 30%+)
✅ **Lưu lead vào Google Sheets** để theo dõi và phân tích

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn free plan.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** (không cần tìm kiếm lead thủ công)
- **Tỷ lệ phản hồi tăng 3x** (tin nhắn cá nhân hóa > 30%)
- **Không phụ thuộc vào API Apollo** (scrape lead tự động)
- **Dữ liệu lead được lưu trữ** trên Google Sheets (theo dõi và phân tích)
- **Hoạt động 24/7** (không cần người làm đêm)
- **Giảm chi phí** (so với mua lead từ Apollo)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Apollo** (để tạo URL tìm kiếm lead)
✔ **API Key của các dịch vụ sau**:
   - [Apify](https://apify.com/) (để scrape lead từ Apollo)
   - [OpenAI](https://platform.openai.com/) (GPT-4.1 & GPT-4.1-mini)
   - [Tavily](https://tavily.com/) (nghiên cứu công ty)
   - [Instantly AI](https://instantly.ai/) (gửi tin nhắn outreach)
✔ **Google Sheet** (để lưu lead và dữ liệu nghiên cứu)
✔ **N8n Workflow Editor** (cài đặt [n8n Cloud](https://n8n.io/) hoặc [Self-hosted](https://docs.n8n.io/))

**💡 Lưu ý:**
- **Apify Actor** đã được cấu hình sẵn trong workflow (không cần mua thêm).
- **Instantly AI** có gói free (500 tin nhắn/ngày), sau đó là $38/tháng.
- **Tavily** miễn phí 100 lead đầu tiên, sau đó $0.08/lead.
- **OpenAI** tính phí theo request (~$0.03/request với GPT-4.1-mini).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11647](https://n8n.io/workflows/11647) (chọn **Export as JSON**).
2. **Mở n8n Editor** → **Import** → Chọn file JSON vừa tải.
3. **Chọn Workspace** (nếu có nhiều workspace) → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải workflow** từ link trên → **Export as JSON**.
2. **Mở n8n Editor** → **Create New Workflow** → **Paste JSON**.
3. **Chọn "Import"** → **Create**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **20 node**, nhưng các bước **quan trọng nhất** cần điều chỉnh:

#### **🔹 Node 1: "On form submission" (formTrigger)**
- **Mục đích:** Nhận input từ form (miêu tả lead bạn muốn tìm).
- **Cấu hình:**
  - **Trigger:** Chọn **"Form Submission"** (nếu muốn người dùng nhập thông tin).
  - **Hoặc:** Bỏ qua node này và **gửi dữ liệu thủ công** vào node **"Loop Over Items"** (splitInBatches).

#### **🔹 Node 2: "Apollo URL Generator" (chainLlm)**
- **Mục đích:** Tạo URL tìm kiếm lead từ Apollo dựa trên input từ form.
- **Cấu hình:**
  - **Input:** Điền **prompt** như:
    ```
    Tạo URL tìm kiếm lead LinkedIn từ Apollo dựa trên mô tả sau:
    {{{ $json["description"] }}}

    URL phải có:
    - Keyword chính: {{{ $json["keyword"] }}}
    - Địa chỉ: {{{ $json["location"] }}}
    - Industry: {{{ $json["industry"] }}}
    - Job title: {{{ $json["job_title"] }}}

    Format URL: https://www.apollo.io/search?query={keyword}&location={location}&industry={industry}&job_title={job_title}
    ```
  - **Model:** Chọn **GPT-4.1** (để đảm bảo độ chính xác).

#### **🔹 Node 3: "Run Apify" (httpRequest)**
- **Mục đích:** Gửi URL Apollo đến Apify để scrape lead.
- **Cấu hình:**
  - **URL:** `https://api.apify.com/v2/actors/jljBwyyQakqrL1wae/runs`
  - **Headers:**
    ```
    Authorization: Bearer {API_KEY_APIFY}
    Content-Type: application/json
    ```
  - **Body (JSON):**
    ```json
    {
      "input": {
        "apolloUrl": "{{$json['url']}}"
      }
    }
    ```
  - **API Key Apify:** Điền vào **Credentials** (n8n → Settings → Credentials → Add → Type: **HTTP Header**).

#### **🔹 Node 4: "Parse Lead Data" (chainLlm)**
- **Mục đích:** Xử lý dữ liệu lead crud từ Apify thành format dễ đọc.
- **Cấu hình:**
  - **Prompt:** Điền:
    ```
    Parse dữ liệu lead từ Apify thành format JSON chuẩn:
    {
      "name": "{{$json['name']}}",
      "email": "{{$json['email']}}",
      "phone": "{{$json['phone']}}",
      "linkedin_url": "{{$json['linkedin_url']}}",
      "company": "{{$json['company']}}",
      "job_title": "{{$json['job_title']}}",
      "location": "{{$json['location']}}"
    }
    ```
  - **Model:** Chọn **GPT-4.1-mini** (để tiết kiệm chi phí).

#### **🔹 Node 5: "Add to Google Sheet" (googleSheets)**
- **Mục đích:** Lưu lead vào Google Sheet.
- **Cấu hình:**
  - **Credentials:** Thêm **Google Sheets** (n8n → Settings → Credentials → Add → Type: **Google Sheets**).
  - **Sheet Name:** Điền tên sheet (ví dụ: **"Leads_LinkedIn"**).
  - **Range:** `A1` (để ghi từ ô A1).
  - **Operation:** Chọn **"Append"** (thêm mới).

#### **🔹 Node 6: "Company Research" (agent)**
- **Mục đích:** Nghiên cứu công ty của lead bằng Tavily.
- **Cấu hình:**
  - **API Key Tavily:** Điền vào **Credentials** (n8n → Settings → Credentials → Add → Type: **Tavily**).
  - **Prompt:** Điền:
    ```
    Nghiên cứu công ty {{{ $json["company"] }}}
    - Trích xuất thông tin:
      - Website chính thức
      - Sản phẩm/dịch vụ chính
      - Mô tả công ty (1-2 câu)
      - Industry
      - Thông tin về CEO/Founder (nếu có)
    ```
  - **Model:** Chọn **GPT-4.1** (để đảm bảo độ chính xác).

#### **🔹 Node 7: "Generate Outreach Message" (chainLlm)**
- **Mục đích:** Tạo tin nhắn outreach cá nhân hóa.
- **Cấu hình:**
  - **Input:** Sử dụng dữ liệu từ **Company Research** và **Lead Data**.
  - **Prompt:** Điền:
    ```
    Tạo tin nhắn outreach cá nhân hóa cho lead {{{ $json["name"] }}} tại {{{ $json["company"] }}}

    Thông tin tham khảo:
    - Job Title: {{{ $json["job_title"] }}}
    - Công ty: {{{ $json["company"] }}}
    - Industry: {{{ $json["industry"] }}}
    - Thông tin công ty: {{{ $json["company_research"] }}}

    Yêu cầu:
    - Tin nhắn phải ngắn gọn (3-5 câu)
    - Nhấn mạnh giá trị của sản phẩm/dịch vụ
    - Kết thúc bằng call-to-action (CTA) rõ ràng
    - Tôn trọng và không spam
    ```
  - **Model:** Chọn **GPT-4.1-mini**.

#### **🔹 Node 8: "Add Lead to Instantly AI" (httpRequest)**
- **Mục đích:** Gửi lead và tin nhắn outreach đến Instantly AI.
- **Cấu hình:**
  - **URL:** `https://api.instantly.ai/v1/campaigns/{CAMPAIGN_ID}/contacts`
  - **Headers:**
    ```
    Authorization: Bearer {API_KEY_INSTANTLY}
    Content-Type: application/json
    ```
  - **Body (JSON):**
    ```json
    {
      "email": "{{$json['email']}}",
      "name": "{{$json['name']}}",
      "message": "{{$json['outreach_message']}}",
      "linkedin_url": "{{$json['linkedin_url']}}"
    }
    ```
  - **API Key Instantly:** Điền vào **Credentials**.

#### **🔹 Node 9: "Limit1" (limit)**
- **Mục đích:** Giới hạn số lead scrape/ngày (tránh bị chặn).
- **Cấu hình:**
  - **Limit:** Đặt số lead tối đa (ví dụ: **50 lead/ngày**).

#### **🔹 Node 10: "Loop Over Items" (splitInBatches)**
- **Mục đích:** Chia lead thành batch để xử lý song song.
- **Cấu hình:**
  - **Batch Size:** Đặt **5-10 lead/lần** (để tránh quá tải API).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Nhập vào form (nếu sử dụng node **formTrigger**) hoặc **gửi manual** vào node **"Loop Over Items"**.
   - Kiểm tra các node quan trọng:
     - **"Apollo URL Generator"** → URL có hợp lệ?
     - **"Run Apify"** → Lead được scrape thành công?
     - **"Company Research"** → Dữ liệu công ty có đầy đủ?
     - **"Generate Outreach Message"** → Tin nhắn có cá nhân hóa?
     - **"Add Lead to Instantly AI"** → Lead có được gửi thành công?

2. **Bật Active Workflow**:
   - Sau khi test thành công, **bật workflow** và **đặt lịch chạy định kỳ** (ví dụ: **1 lần/ngày**).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **🔹 1. Tăng Tỷ Lệ Thành Công với Instantly AI**
- **Chọn gói Instantly AI phù hợp**:
  - **Free (500 tin nhắn/ngày)** → Dùng cho test.
  - **Pro ($38/tháng)** → Cho 5.000 tin nhắn/ngày (tối ưu cho doanh nghiệp).
- **Optimize tin nhắn**:
  - Thêm **CTA rõ ràng** (ví dụ: *"Mời bạn xem demo miễn phí tại [link]"*).
  - **Kết hợp hình ảnh** (nếu Instantly AI hỗ trợ).

### **🔹 2. Lưu Log & Theo Dõi Kết Quả**
- **Thêm node "Set"** sau **"Add Lead to Instantly AI"** để lưu **status** (gửi thành công/thất bại).
- **Tạo Google Sheet mới** để theo dõi:
  - **Tỷ lệ mở tin nhắn**
  - **Tỷ lệ phản hồi**
  - **Chi phí API**

### **🔹 3. Kết Hợp với Slack/Telegram**
- **Thêm node "Webhook"** để nhận thông báo khi:
  - Lead được scrape thành công.
  - Tin nhắn được gửi thành công.
  - Có lỗi xảy ra (ví dụ: API Tavily hết hạn).

### **🔹 4. Tự Động Hóa Nhiều Campaign**