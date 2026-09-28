---
title: "🚀 Tự Động Đánh Giá Lead LinkedIn Theo ICP Với Google Sheets, SourceGeek & Gemini AI (Không Cần Code)"
description: "Workflow tự động hóa đánh giá lead LinkedIn dựa trên Ideal Customer Profile (ICP) của doanh nghiệp, kết hợp AI Gemini và SourceGeek để tự động lấy thông tin hồ sơ, tính điểm phù hợp và tạo ra các tin nhắn outreach cá nhân hóa. Giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình tuyển dụng và phát triển lead."
slug: "tieu-dong-danh-gia-lead-linkedin-theo-icp"
tags: [n8n, automation, lead-generation, ai-summarization, sourcegeek, google-sheets, gemini-ai]
keywords: [tự động hóa n8n, đánh giá lead linkedin, icp score, sourcegeek n8n, gemini ai outreach, workflow tự động hóa tuyển dụng]
---

# 🚀 **Tự Động Đánh Giá Lead LinkedIn Theo ICP Với Google Sheets, SourceGeek & Gemini AI**

### **Giải pháp nào giúp các sếp:**
- **Tiết kiệm 80% thời gian** trong việc phân tích hồ sơ LinkedIn thủ công?
- **Tự động tính điểm phù hợp (ICP Score)** của mỗi lead dựa trên tiêu chí doanh nghiệp?
- **Tạo ra tin nhắn outreach cá nhân hóa** để tăng tỷ lệ phản hồi từ lead?
- **Lưu trữ tất cả dữ liệu** trong Google Sheets để theo dõi và phân tích lâu dài?

Nếu câu trả lời là **Có**, thì workflow này chính là giải pháp **tự động hóa 100% không cần code** mà các sếp đang tìm kiếm!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng. Đây là cách duy nhất đảm bảo tính bảo mật và hiệu suất cao cho các tác vụ tự động hóa liên quan đến dữ liệu nhạy cảm như LinkedIn.

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI Gemini)

*Lưu ý:* N8n **không chạy ổn định** trên máy tính cá nhân hoặc cloud miễn phí (như n8n.cloud) khi xử lý nhiều lead đồng thời.
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Không cần phân tích từng hồ sơ LinkedIn thủ công.
✅ **Độ chính xác cao:** AI Gemini tự động so sánh lead với ICP của doanh nghiệp.
✅ **Tin nhắn outreach cá nhân hóa:** AI tạo ra **3 bản tin nhắn** khác nhau cho mỗi lead.
✅ **Lưu trữ dữ liệu toàn diện:** Tất cả thông tin (ICP Score, lý do, tin nhắn) được cập nhật tự động vào Google Sheets.
✅ **Hoạt động liên tục:** Workflow chạy **24/7** khi được tự động hóa trên VPS.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản SourceGeek** (để lấy dữ liệu hồ sơ LinkedIn):
   - [Đăng ký SourceGeek](https://sourcegeek.com/) (miễn phí 7 ngày thử nghiệm).
   - **API Key** từ SourceGeek (tìm trong **Settings > API Keys**).

2. **Google Sheets** với cấu trúc như sau:
   - Một **Sheet** chứa **cột "LinkedIn URL"** (ví dụ: `https://www.linkedin.com/in/nguyenvananh/`).
   - Các cột khác sẽ được tự động thêm sau khi workflow chạy (ICP Score, Reasoning, Outreach Messages).

3. **Google Cloud API Key** (để kết nối với **Google Gemini AI**):
   - [Tạo API Key cho Google Vertex AI](https://console.cloud.google.com/).
   - **Credentials OAuth 2.0** cho Google Sheets (để cập nhật dữ liệu).

4. **N8n Self-hosted** (trên VPS) để chạy workflow ổn định.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13026](https://n8n.io/workflows/13026) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên VPS của các sếp.
3. Nhấn **Import** và chọn file JSON vừa tải.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/13026](https://n8n.io/workflows/13026).
2. Trong **n8n Editor**, nhấn **Import** > **Paste JSON**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình Node "Get data from a linkedin profile" (SourceGeek)**
- **Credentials:** Chọn `sourcegeekCredentialsApi` (đã tạo từ tài khoản SourceGeek).
- **Tham số cần điền:**
  - `url`: **Bắt buộc** là URL LinkedIn của lead (đọc từ Google Sheets).
  - `fields`: Chọn các trường cần lấy (ví dụ: `name, headline, summary, skills, experience`).

#### **B. Cấu hình Node "Google Gemini Chat Model"**
- **Credentials:** Chọn `googlePalmApi` (API Key từ Google Cloud).
- **Prompt mẫu** (cần chỉnh sửa theo ICP của doanh nghiệp):
  ```plaintext
  You are an ICP scoring assistant. Analyze the LinkedIn profile data below and score it from 0-100 based on the following Ideal Customer Profile (ICP):

  **ICP Criteria:**
  - Industry: [Nêu ngành nghề mục tiêu, ví dụ: "Tech Startups"]
  - Job Title: [Ví dụ: "CTO, VP Engineering"]
  - Skills: [Ví dụ: "AI/ML, Cloud Computing, Python"]
  - Experience: [Ví dụ: "5+ years in SaaS product development"]

  **Profile Data:**
  {{{$json}}}

  Return in JSON format:
  {
    "icp_score": 85,
    "reasoning": "The candidate has 7 years in SaaS development and expertise in AI/ML, matching 90% of our ICP criteria.",
    "outreach_messages": [
      "Message 1: 'Hi [Name], I noticed your experience in AI/ML at [Company]. Our startup is looking for a CTO with your background...'",
      "Message 2: 'Your work on [Project] really resonated with me. We’re building a similar solution and would love to connect...'",
      "Message 3: 'I came across your profile and saw your skills in [Skill]. We’re hiring for a [Role] position—would you be open to a quick chat?'"
    ]
  }
  ```

#### **C. Cấu hình Node "Update row in sheet" (Google Sheets)**
- **Credentials:** Chọn `googleSheetsOAuth2Api` (OAuth 2.0 từ Google).
- **Tham số cần điền:**
  - **Sheet Name:** Tên sheet chứa URL LinkedIn.
  - **Range:** `Sheet1!A2:F2` (điều chỉnh theo vị trí dữ liệu).
  - **Values:** Chọn **Dynamic Content** từ node **AI Agent**.

#### **D. Cấu hình Node "Get LinkedIn profile urls from sheet"**
- **Credentials:** `googleSheetsOAuth2Api` (như trên).
- **Tham số cần điền:**
  - **Sheet Name:** Tên sheet chứa URL.
  - **Range:** `Sheet1!A2:A100` (điều chỉnh theo số lượng lead).

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Nhập **1-2 URL LinkedIn** vào Google Sheets.
   - Chọn node **Manual Trigger** và nhấn **Execute Workflow**.
   - Kiểm tra kết quả trong Google Sheets (ICP Score, Reasoning, Outreach Messages).

2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển **Manual Trigger** sang **Active** để workflow chạy tự động khi có dữ liệu mới.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa ICP Score cho doanh nghiệp**
- **Chỉnh sửa Prompt** trong node **Google Gemini Chat Model** để phù hợp với **ICP cụ thể** của doanh nghiệp.
  - Ví dụ: Nếu doanh nghiệp chuyên **e-commerce**, hãy thêm tiêu chí như:
    ```plaintext
    "Industry: E-commerce, Experience: 3+ years in Shopify/BigCommerce, Skills: SEO, Conversion Rate Optimization"
    ```

### **2. Kết hợp với Slack/Telegram để báo cáo kết quả**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** sau node **Update row in sheet** để nhận thông báo khi có lead mới được đánh giá.
- **Cách làm:**
  1. Tạo **Slack Webhook** hoặc **Telegram Bot Token**.
  2. Thêm node **Slack** hoặc **Telegram** vào workflow.
  3. Chọn **Dynamic Content** từ node **AI Agent** để gửi thông báo tự động.

### **3. Lưu log hoạt động để theo dõi**
- Thêm node **Set** hoặc **Code** để lưu **thời gian chạy**, **ICP Score**, và **trạng thái** vào Google Sheets.
- **Mẫu mã Code (n8n):**
  ```javascript
  // Thêm cột "Last Updated" và "Status"
  $node.set("data", {
    ...$node.input,
    "Last Updated": new Date().toISOString(),
    "Status": "Processed Successfully"
  });
  ```

### **4. Chạy workflow định kỳ với **n8n Cron Trigger****
- Thay thế **Manual Trigger** bằng **Cron Trigger** để workflow chạy **hàng ngày/lần tuần** tự động.
- **Cách cấu hình:**
  1. Thêm node **Cron Trigger** vào đầu workflow.
  2. Đặt lịch chạy (ví dụ: `0 0 * * *` = hàng ngày lúc 00:00).

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp đang gặp khó khăn trong việc:
✔ **Tìm kiếm và đánh giá lead LinkedIn** một cách hiệu quả.
✔ **Tự động hóa quá trình outreach** với tin nhắn cá nhân hóa.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược phát triển doanh nghiệp.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản SourceGeek, Google Sheets và API Key**.
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test với 1-2 lead** và **bật Active** để tự động hóa toàn bộ quy trình!

🚀 **N8n không chỉ tự động hóa, mà còn giúp các sếp "ngủ yên" khi biết lead được xử lý chính xác và hiệu quả!**

---
**Cần hỗ trợ thêm?**
- **Join Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/)
- **Hỗ trợ kỹ thuật**: [n8n.io/community](https://n8n.io/community)