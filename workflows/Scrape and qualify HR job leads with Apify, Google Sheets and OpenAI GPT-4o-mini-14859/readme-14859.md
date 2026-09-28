---
title: "🚀 Tự Động Hóa Tìm Kiếm & Lọc CV Tốt Nhất Cho Việc Làm HR Với Apify + AI GPT-4o-mini (N8n)"
description: "Workflow tự động hóa tìm kiếm, trích xuất và đánh giá chất lượng ứng viên từ các công việc tuyển dụng trên internet, loại bỏ trùng lặp, và sử dụng AI để lọc ra những ứng viên có tiềm năng cao nhất - tiết kiệm 80% thời gian cho bộ phận HR."
slug: "tu-dong-hoa-tim-kiem-loc-cv-hr-apify-ai-gpt4o-mini"
tags: [n8n, automation, lead-generation, ai-summarization, hr-automation, apify, openai]
keywords: [n8n workflow tìm kiếm việc làm, tự động hóa tuyển dụng HR, AI đánh giá ứng viên, Apify scrape job, Google Sheets tự động hóa, GPT-4o-mini tự động hóa]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Lọc CV Tốt Nhất Cho Việc Làm HR Với Apify + AI GPT-4o-mini**

## **🔍 Nỗi Đau Của Bộ Phận HR**
Bộ phận HR thường phải mất **gần 30 giờ/tuần** để:
- Tìm kiếm và trích xuất thông tin tuyển dụng từ nhiều trang web khác nhau.
- Loại bỏ trùng lặp và sắp xếp dữ liệu từ hàng trăm ứng viên.
- Đánh giá thủ công chất lượng ứng viên dựa trên tiêu chí phức tạp (kinh nghiệm, kỹ năng, phù hợp với văn hóa công ty).
- Gửi thông báo cho các ứng viên tiềm năng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa tìm kiếm** từ các trang web tuyển dụng lớn (viết code không cần).
✅ **Loại bỏ trùng lặp** và lưu trữ dữ liệu sạch vào Google Sheets.
✅ **Sử dụng AI GPT-4o-mini** để đánh giá ứng viên theo tiêu chí cá nhân hóa của doanh nghiệp.
✅ **Lọc ra ứng viên chất lượng cao** và gửi thông báo tự động.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** cho bộ phận HR trong việc tìm kiếm và lọc ứng viên.
- **Chất lượng tuyển dụng cao hơn** nhờ AI đánh giá khách quan.
- **Dữ liệu sạch và cập nhật** trong Google Sheets, dễ dàng theo dõi và phân tích.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Cá nhân hóa tiêu chí đánh giá** theo yêu cầu cụ thể của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrape dữ liệu tuyển dụng):
   - [Đăng ký Apify](https://apify.com/) và lấy **API Key**.
   - Cài đặt **n8n-node-apify** (nếu chưa có, thêm trong n8n Community Nodes).
2. **Tài khoản Google Cloud** (để kết nối Google Sheets):
   - [Cài đặt OAuth 2.0](https://developers.google.com/sheets/api/quickstart/python) và lấy **Google Sheets OAuth 2.0 API Key**.
3. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
4. **Google Sheet mẫu** (để lưu trữ dữ liệu):
   - [Mở bản sao Google Sheet](https://docs.google.com/spreadsheets/d/1-7nF5jwil_PenpLfLlqlTdDfBj5q4987drCZj2gkLrQ/edit?usp=sharing) và chia sẻ với n8n.
5. **(Tùy chọn) Tài khoản Gmail** (nếu muốn gửi email thông báo cho ứng viên).
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/14859](https://n8n.io/workflows/14859) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/14859](https://n8n.io/workflows/14859) (chọn **Export as JSON**).
2. Trong n8n Editor, nhấn **Import** > **Paste JSON** và dán vào.
3. Chọn **Create new workflow** và nhấn **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node "When Job Form Submitted" (formTrigger)**
- **Cấu hình:**
  - Chọn **Form Trigger** để bắt đầu workflow khi có dữ liệu từ form.
  - **Lưu ý:** Nếu muốn sử dụng form riêng, thay đổi URL và cấu trúc form trong node này.

#### **🔹 Node "Submit Job Scrape Request" (httpRequest)**
- **Cấu hình:**
  - Thay đổi **URL** thành API của Apify (ví dụ: `https://api.apify.com/v2/act/...`).
  - Điền **API Key** của Apify vào **Headers** (`Authorization: Bearer YOUR_API_KEY`).
  - **Body (JSON):**
    ```json
    {
      "actorId": "your-apify-actor-id",
      "input": {
        "searchTerms": "${{ $json["searchTerms"] }}",
        "maxJobs": 100
      }
    }
    ```
  - **Lưu ý:** Thay `your-apify-actor-id` bằng ID của actor Apify bạn đã tạo.

#### **🔹 Node "Detect Missing Company Names" (firecrawl)**
- **Cấu hình:**
  - Thay đổi **URL** thành URL của trang web bạn muốn scrape (ví dụ: `https://viettalent.vn/jobs`).
  - **Headers** (nếu cần):
    ```json
    {
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    ```
  - **Lưu ý:** Nếu không muốn sử dụng Firecrawl, có thể thay thế bằng **HTTP Request** + **Code Node** để scrape thủ công.

#### **🔹 Node "AI Job Scoring Agent" (openAi)**
- **Cấu hình:**
  - Chọn **Model:** `gpt-4o-mini`.
  - **Prompt mẫu** (có thể tùy chỉnh theo tiêu chí của doanh nghiệp):
    ```plaintext
    Analyze the following job posting and candidate profile. Score the candidate on a scale of 1-10 based on:
    - Relevance to job description (30%)
    - Years of experience (25%)
    - Skills mentioned (25%)
    - Cultural fit (20%)

    Job Posting: ${{ $json["jobDescription"] }}
    Candidate Profile: ${{ $json["candidateProfile"] }}

    Return JSON response with:
    {
      "score": number,
      "reasoning": string,
      "qualified": boolean
    }
    ```
  - **Lưu ý:** Đảm bảo **OpenAI API Key** đã được cấu hình trong **Credentials**.

#### **🔹 Node "Google Sheets" (googleSheets)**
- **Cấu hình chung:**
  - Chọn **Google Sheets OAuth 2.0 API** trong **Credentials**.
  - **Sheet Name:** Đặt tên sheet (ví dụ: `Job_Leads`).
  - **Range:** `Sheet1!A1` (hoặc tùy chỉnh theo cấu trúc sheet).
  - **Lưu ý:**
    - Đảm bảo sheet đã chia sẻ với tài khoản n8n.
    - Cấu trúc sheet phải phù hợp với dữ liệu đầu ra (cột: `JobTitle`, `Company`, `Salary`, `Score`, `Qualified`, ...).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và nhập dữ liệu mẫu vào form (ví dụ: `searchTerms: "Developer"`).
   - Kiểm tra kết quả trong Google Sheets và log của n8n.
2. **Bật Active Workflow:**
   - Sau khi kiểm tra thành công, chuyển **Active** sang **ON**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Kết Nối Slack/Telegram để Thông Báo**
- Thêm **Slack Node** hoặc **Telegram Bot Node** sau node **"Append Qualified Job to Sheets"** để gửi thông báo khi có ứng viên mới được lọc.
- **Cấu hình:**
  - Thêm node **`n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.
  - Gửi tin nhắn mẫu:
    ```json
    {
      "text": "🚀 New qualified job lead found!\nJob: ${{ $json["JobTitle"] }}\nCompany: ${{ $json["Company"] }}\nScore: ${{ $json["Score"] }}/10\nURL: ${{ $json["JobURL"] }}"
    }
    ```

### **2. Lưu Log & Theo Dõi Lịch Sử**
- Thêm **`n8n-nodes-base.code`** sau node **"Append Qualified Job to Sheets"** để lưu log vào Google Sheets hoặc một database khác.
- **Mẫu mã code:**
  ```javascript
  $input.all().forEach((job) => {
    const logEntry = {
      timestamp: new Date().toISOString(),
      jobId: job.id,
      action: "Job qualified",
      details: job
    };
    $output.set(logEntry);
  });
  ```

### **3. Gửi Email Thông Báo Cho Ứng Viên**
- Thêm **`n8n-nodes-base.email`** sau node **"Append Qualified Job to Sheets"** để gửi email tự động cho ứng viên.
- **Cấu hình:**
  - Sử dụng **Gmail API** hoặc **SMTP**.
  - Nội dung email:
    ```html
    <p>Chào <strong>{{ $json["CandidateName"] }}</strong>,</p>
    <p>Chúng tôi đã đánh giá hồ sơ của bạn cho vị trí <strong>{{ $json["JobTitle"] }}</strong> tại <strong>{{ $json["Company"] }}</strong>.</p>
    <p>Điểm số của bạn: <strong>{{ $json["Score"] }}/10</strong> (Đạt tiêu chuẩn: <strong>{{ $json["Qualified"] ? "Có" : "Không" }}</strong>)</p>
    <p>Xin vui lòng liên hệ với chúng tôi nếu có bất kỳ câu hỏi nào.</p>
    ```

### **4. Tự Động Xóa Dữ Liêu Trùng Lặp**
- Thêm **`n8n-nodes-base.code`** trước node **"Append Raw Jobs to Sheets"** để kiểm tra và xóa trùng lặp trước khi lưu.
- **Mẫu mã code:**
  ```javascript
  const existingJobs = $input.all();
  const uniqueJobs = existingJobs.filter((job, index) => {
    return existingJobs.findIndex(j => j.jobId === job.jobId) === index;
  });
  $output.set(uniqueJobs);
  ```

---

## **📌 Kết Luận**
Workflow này **giải phóng bộ phận HR khỏi công việc lặp lại**, giúp tập trung vào việc **phỏng vấn và xây dựng đội ngũ chất lượng**. Với sự kết hợp giữa **Apify (scrape), Google Sheets (lưu trữ), và AI GPT-4o-mini (đánh giá)**, các sếp có thể:
✔ **Tìm kiếm ứng viên nhanh chóng** từ nhiều nguồn.
✔ **Lọc ra ứng viên tiềm năng** một cách chính xác.
✔ **Tự động hóa toàn bộ quy trình** mà không cần viết code.

**🚀 Hãy áp dụng ngay và tiết kiệm thời gian cho bộ phận HR của mình!**

---
:::note[💡 Gợi Ý Nâng Cao]
- **Tùy chỉnh tiêu chí AI:** Thay đổi prompt trong node **`AI Job Scoring Agent`** để phù hợp với tiêu chí tuyển dụng riêng của doanh nghiệp.
- **Kết hợp với CRM:** Gửi dữ liệu ứng viên vào **HubSpot, Salesforce** hoặc **Zoho CRM** để quản lý tiếp theo.
- **Báo cáo tự động:** Sử dụng **Google Data Studio** hoặc **Power BI** để tạo báo cáo từ dữ liệu trong Google Sheets.
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::