---
title: "📊 Tự Động Hóa Báo Cáo Google Business + Tóm Tắt AI sang Slack & Email (Miễn Code)"
description: "Workflow này tự động thu thập dữ liệu Google Business (impressions, reviews, CTR), so sánh tuần này vs tuần trước và trung bình 12 tuần, sau đó tạo báo cáo AI và gửi thông báo định kỳ sang Slack và email. Giúp các sếp tiết kiệm 10+ giờ/tháng và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "tieu-dong-hoa-bao-cao-google-business-ai-slack-email"
tags: [n8n, automation, google-business, ai-summary, slack, email, google-sheets, no-code]
keywords: [tự động hóa báo cáo google business, workflow n8n google business, báo cáo reviews google business, tự động hóa email báo cáo tuần, ai tổng hợp báo cáo doanh nghiệp]
---

# 🚀 **Tự Động Hóa Báo Cáo Google Business + Tóm Tắt AI sang Slack & Email (Miễn Code)**

---
## **💡 Bạn đang gặp vấn đề gì?**
- **Thủ công thu thập báo cáo Google Business** mất **10+ giờ/tháng**?
- **Không biết cách so sánh tuần này vs tuần trước** để đánh giá hiệu quả?
- **Báo cáo reviews rải rác** không có tổng quan về **trend 12 tuần**?
- **Không biết cách gửi báo cáo tự động** sang Slack và email cho đội ngũ?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập dữ liệu** (impressions, reviews, CTR) từ Google Business API
✅ **So sánh tuần này vs tuần trước + trung bình 12 tuần**
✅ **Tạo tóm tắt AI** bằng OpenAI (GPT-5) về **tình hình tổng quan, reviews, và impressions**
✅ **Gửi báo cáo định kỳ** sang **Slack (tổng hợp + cá nhân)** và **email tuần**
✅ **Lưu tất cả dữ liệu** vào Google Sheets để theo dõi dài hạn

---
### **🎯 Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** (không cần thu thập thủ công)
- **Báo cáo chính xác** (so sánh tuần này vs tuần trước + trend 12 tuần)
- **Tóm tắt AI tự động** (không cần viết báo cáo bằng tay)
- **Gửi báo cáo tự động** sang Slack và email (không quên)
- **Dữ liệu lưu trữ** trong Google Sheets để phân tích dài hạn
- **Cá nhân hóa** (báo cáo riêng cho mỗi doanh nghiệp)
:::

---
## **🔧 Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
### **1. Google Sheet Danh sách Doanh nghiệp**
👉 [**Tải mẫu Google Sheet**](https://docs.google.com/spreadsheets/d/1u-87I9CUywZwiy9oDTUkMrVSADzeojk2UTTJRs3YOGY/edit?usp=sharing)
- **Cách sử dụng:**
  1. **Nhấp File → Make a copy** để sao chép
  2. **Thêm một hàng cho mỗi doanh nghiệp** của bạn
  3. **Cột bắt buộc:**
     - `Company Name` (Tên doanh nghiệp)
     - `Google Business ID` (ID của Google Business Profile)
     - `Slack Channel` (VD: `#brads-service-center`)
     - `Slack Recipients` (danh sách Slack IDs, cách nhau bởi dấu phẩy)
     - `Email Recipients` (danh sách email nhận báo cáo tuần, cách nhau bởi dấu phẩy)

### **2. Google Business API Credential**
- **Tạo một dự án Google Cloud** với **Business Profile API** được kích hoạt:
  1. Truy cập [Google Cloud Console](https://console.cloud.google.com/)
  2. Tạo **mới một dự án**
  3. Kích hoạt **Google Business Profile API**
  4. Tạo **OAuth 2.0 Client ID** (dùng cho n8n)
- **Cấu hình trong n8n:**
  - **Node:** `googleBusinessProfileOAuth2Api`
  - **Tham số:**
    - `Client ID` & `Client Secret` (từ Google Cloud)
    - `Refresh Token` (lấy từ quá trình OAuth)

### **3. Google Sheets Credential**
- **Thêm credential OAuth2 trong n8n** để đọc/writing vào Google Sheet:
  - **Node:** `googleSheetsOAuth2Api`
  - **Cấu hình:**
    - Chọn **Google Sheets** trong n8n
    - Kích hoạt quyền đọc/giới thiệu

### **4. Slack Credential**
- **Thêm credential OAuth2 trong n8n** để gửi tin nhắn:
  - **Node:** `slackOAuth2Api`
  - **Quyền cần thiết:**
    - `chat:write` (gửi tin nhắn)
    - `users:read` (đọc thông tin người dùng)
    - `channels:read` (đọc kênh Slack)

### **5. Email Credential (Tùy chọn nhưng khuyến nghị)**
- **Gmail OAuth2** (nếu gửi email qua Gmail):
  - **Node:** `gmailOAuth2`
  - **Cấu hình:**
    - Kích hoạt **Less Secure Apps** (nếu cần) hoặc sử dụng **OAuth 2.0**
- **Hoặc SMTP** (nếu dùng server email riêng)

---
## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9290](https://n8n.io/workflows/9290)
- **Cách import:**
  1. Mở **n8n Editor**
  2. Nhấp **Import Workflow** → Chọn file JSON
  3. **Hoặc copy/paste JSON** vào **Import Workflow** (nếu file quá lớn)

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** vì sử dụng **OpenAI (GPT-5), Google Business API, và nhiều node code**. Dưới đây là **các bước chỉnh sửa quan trọng**:

#### **🔹 1. Cấu hình Google Sheets**
- **Node:** `Read Companies` (googleSheets)
  - **Tham số:**
    - `Sheet Name`: Đặt tên sheet trong Google Sheet của bạn (VD: `Doanh nghiệp`)
    - `Range`: `Sheet1!A:F` (đảm bảo bao gồm tất cả cột cần thiết)

#### **🔹 2. Cấu hình Google Business API**
- **Node:** `Get Impression data` (httpRequest)
  - **URL:** `https://mybusiness.googleapis.com/v4/accounts/{accountId}/locations/{locationId}/stats:query`
  - **Headers:**
    - `Authorization: Bearer {access_token}`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "dateRange": {
        "startDate": "2024-01-01",
        "endDate": "2024-01-07"
      },
      "dimensions": ["IMPRESSIONS", "CLICKS", "VIEWERS"],
      "metrics": ["IMPRESSIONS", "CLICKS"]
    }
    ```
  - **Lưu ý:** `{accountId}` và `{locationId}` sẽ được lấy từ **Google Business ID** trong Google Sheet.

#### **🔹 3. Cấu hình OpenAI (GPT-5)**
- **Node:** `OpenAI Chat Model`, `OpenAI Chat Model2`, `OpenAI Chat Model4` (lmChatOpenAi)
  - **Tham số:**
    - `Model`: Chọn `gpt-5` (nếu có) hoặc `gpt-4` (nếu không)
    - `API Key`: Điền vào `openAiApi` credential trong n8n
    - **Prompt mẫu (cần chỉnh sửa):**
      ```plaintext
      Tóm tắt báo cáo tuần này cho doanh nghiệp {companyName}:
      - So sánh impressions tuần này vs tuần trước: {impressionsComparison}
      - Tổng quan reviews: {reviewsSummary}
      - Đánh giá tổng thể: {overallRating}
      Viết một đoạn văn ngắn (3-4 câu) tổng kết tình hình và đề xuất hành động.
      ```
  - **Lưu ý:** Các biến `{impressionsComparison}`, `{reviewsSummary}`, `{overallRating}` sẽ được cung cấp từ **node code** trước đó.

#### **🔹 4. Cấu hình Slack & Email**
- **Node:** `All-companies Slack`, `Per Company Slack`, `Per company email` (gmail)
  - **Slack:**
    - **Channel/Recipient:** Lấy từ `Slack Channel` trong Google Sheet
    - **Message Format:** Sử dụng **Slack Blocks** để định dạng đẹp
  - **Email:**
    - **From:** Đặt tên người gửi (VD: "Google Business Pulse <noreply@domain.com>")
    - **Subject:** "Báo cáo tuần {weekStartDate} - {weekEndDate}"

#### **🔹 5. Node Code (cần kiểm tra)**
Workflow này sử dụng **nhiều node code** để:
- **Tính toán tuần hiện tại vs tuần trước** (`Build Week Window`, `Build last week window`)
- **Flatten dữ liệu** (`Flatten`, `Flatten 12-week`)
- **Tóm tắt reviews** (`Summarize Weekly Reviews`, `map and summarize last 12 weeks reviews`)
- **Merge dữ liệu** (`Merge2`, `Join All`, `Merge One Liners`)

**Lưu ý:**
- **Không chỉnh sửa code** nếu không hiểu JavaScript (n8n có hỗ trợ debug)
- **Test từng node** một để đảm bảo dữ liệu truyền đúng

#### **🔹 6. Schedule Trigger**
- **Node:** `Schedule Trigger` (scheduleTrigger)
  - **Cấu hình:**
    - **Timezone:** Chọn timezone phù hợp (VD: `Asia/Ho_Chi_Minh`)
    - **Cron:** `0 0 * * 1` (chạy vào **thứ Hai hàng tuần**, lúc 00:00)

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **manual** từng node quan trọng (VD: `Get Impression data`, `Get Many Reviews`)
   - Kiểm tra **Slack & Email** có nhận được không
2. **Bật Active workflow**:
   - Nhấp **Active** trên tab workflow
   - Kiểm tra **log** trong n8n để đảm bảo không lỗi

---
## **✍️ Mẹo & gợi ý nâng cao**
:::tip[**CÁCH NÂNG CAO HỆ THỐNG**]
1. **Thêm Logs & Monitoring**
   - Sử dụng **node `stickyNote`** để ghi lại lỗi hoặc thành công
   - **Kết hợp với Datadog/Google Sheets Logs** để theo dõi workflow

2. **Tự động Cập Nhật Google Business ID**
   - Nếu doanh nghiệp thay đổi, **cập nhật Google Sheet** và workflow sẽ tự động lấy dữ liệu mới

3. **Gửi Báo cáo Định Kỳ cho Khách Hàng**
   - **Tạo một workflow riêng** để gửi báo cáo cho khách hàng (không chỉ nội bộ)

4. **Kết hợp với Google Analytics**
   - **Thêm node `googleAnalytics`** để so sánh traffic website vs impressions Google Business

5. **Tự động Cập Nhật Tóm Tắt AI**
   - **Sử dụng `agent` node** để tự động cập nhật tóm tắt khi có review mới

6. **Báo Lỗi qua Slack/Email**
   - **Thêm node `if`** để gửi thông báo lỗi nếu workflow bị ngắt
   - **VD:** Nếu `Get Impression data` thất bại, gửi tin nhắn Slack cảnh báo

7. **Tạo Dashboard Báo cáo**
   - **Kết hợp với Google Data Studio** hoặc **Power BI** để tạo dashboard trực quan
   - **Lấy dữ liệu từ Google Sheets** được cập nhật tự động

---
## **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thu thập, so sánh và gửi báo cáo Google Business **bằng tay**. Với **AI tóm tắt tự động**, **so sánh tuần này vs tuần trước**, và **gửi báo cáo sang Slack/email**, các sếp có thể:
✔ **Quản lý hiệu quả** hơn doanh nghiệp
✔ **Ra quyết định** dựa trên dữ liệu chính xác
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược

**🚀 Hành động ngay!**
1. **Chuẩn bị Google Sheet** và các credential
2. **Import workflow** và **cấu hình**
3. **Test và bật Active**
4. **Theo dõi kết quả** trong Slack & Email

**🎁 Mã giảm giá VPS cho n8n (Self-hosted):**
:::info[**Hạ tầng ổn định 24/7**]
Để workflow chạy **không gián đoạn**, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💬 Cần hỗ trợ?**
- **Trên n8n Community**: [https://community.n8n.io/](https://community.n8n.io/)
- **Trên Discord n8n**: [https://n8n.io/discord](https://n8n.io/discord)
- **Gửi feedback**: [https://github.com/n8n-io/n8n/issues](https://github.com/n8n-io/n8n/issues)