---
title: "🚀 Tự Động Lấy & Xác Minh Email Của Người Quyết Định (Decision-Maker) Từ Google - AI + Apify"
description: "Workflow tự động hóa 100% không code giúp các sếp tìm kiếm, trích xuất và xác minh email chính xác của các nhà quản lý cấp cao từ kết quả tìm kiếm Google, sau đó lưu vào Google Sheets. Giúp tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-lay-xac-minh-email-decision-maker"
tags: [n8n, automation, lead-generation, ai-summarization, apify, openai, google-sheets]
keywords: [tự động hóa n8n, lấy email decision maker, apify google scraper, gpt-4.1 trích xuất email, xác minh email validkit, google sheets tự động]
---

# 🚀 **Tự Động Lấy & Xác Minh Email Của Người Quyết Định (Decision-Maker) Từ Google - AI + Apify**

### **Nỗi Đau Của Các Sếp Trong Lead Generation**
Bạn có bao giờ phải mất **từ 2-5 tiếng** để tìm kiếm và xác minh email của các nhà quản lý cấp cao (CEO, CTO, Director, VP...) từ Google? Hay phải **lặp đi lặp lại** các công cụ như Hunter.io, Apollo.io mà vẫn không đảm bảo độ chính xác cao? Với workflow này, các sếp sẽ **tự động hóa toàn bộ quy trình** chỉ trong vài phút, với kết quả **email xác minh 100% chính xác** và **lưu trữ sẵn trên Google Sheets** để sử dụng ngay.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 5 tiếng tìm kiếm thủ công, chỉ cần **1 lần setup** và workflow chạy tự động 24/7.
- **Độ chính xác cao**: Sử dụng **GPT-4.1** để trích xuất email từ kết quả Google và **ValidKit API** để xác minh, giảm thiểu sai sót lên đến **95%**.
- **Lưu trữ tự động**: Tất cả email xác minh được **ghi vào Google Sheets** với định dạng sẵn sàng export.
- **Cá nhân hóa**: Dễ dàng **cập nhật từ khóa tìm kiếm** để phù hợp với ngành nghề hoặc đối tượng mục tiêu.
- **Hoạt động liên tục**: Chạy trên **n8n self-hosted** để không phụ thuộc vào internet hoặc thời gian làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key Apify** (để lấy kết quả tìm kiếm Google):
   - Đăng ký tại [Apify](https://apify.com/) và lấy API key từ **Personal Access Token**.
2. **API Key OpenAI** (để sử dụng GPT-4.1):
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy API key từ **Settings > API Keys**.
3. **API Key ValidKit** (để xác minh email):
   - Đăng ký tại [ValidKit](https://validkit.com/) và lấy API key từ **Dashboard**.
4. **Google Sheets OAuth2**:
   - Tạo một **Google Sheet mới** và cấp quyền cho n8n qua **Google Cloud Console**.
5. **Từ khóa tìm kiếm** (ví dụ: `"CEO Vietnam" site:linkedin.com`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/12877](https://n8n.io/workflows/12877) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (tab **Import/Export**).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **10 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Credentials (Bắt Buộc)**
| Node | Tham Số Cần Điền | Ghi Chú |
|------|------------------|---------|
| **Apify Scraper** | `apifyApiKey` | Điền API Key từ Apify vào **Credentials > Apify API**. |
| **OpenAI Chat Model** | `openAiApi` | Điền API Key OpenAI vào **Credentials > OpenAI API**. |
| **Verify Email** | `validKitApiKey` | Điền API Key ValidKit vào **HTTP Request > Headers > Authorization**. |
| **Google Sheets** | `googleSheetsOAuth2Api` | Chọn **Google Sheets OAuth2** đã setup trước. |

##### **B. Cấu Hình Cụ Thể Mỗi Node**
1. **HTTP Request (Apify Scraper)**
   - **URL**: `https://api.apify.com/v2/act/...` (sẽ tự động lấy từ node **Manual Trigger**).
   - **Headers**:
     - `Authorization`: `Bearer {apifyApiKey}`.
     - `Content-Type`: `application/json`.
   - **Body**:
     ```json
     {
       "input": {
         "searchQuery": "CEO Vietnam site:linkedin.com",
         "maxResults": 50
       }
     }
     ```

2. **Split Out Organic Results**
   - **Expression**: `$json["body"]["results"]` (lấy danh sách kết quả từ Apify).

3. **AI Extract Owner Emails (Agent)**
   - **Prompt**: Workflow đã cấu hình sẵn, chỉ cần đảm bảo **OpenAI API Key** đúng.
   - **Output Parser**: Chọn **Structured Output Parser** để trích xuất email theo định dạng:
     ```json
     {
       "email": "string",
       "domain": "string",
       "name": "string"
     }
     ```

4. **Code (JavaScript) - Lọc Email Trùng Lặp**
   - **Code**:
     ```javascript
     // Loại bỏ email trùng lặp
     const uniqueEmails = [...new Map($input.map(item => [item.json.email, item])).values()];
     return uniqueEmails;
     ```

5. **Verify Email (ValidKit API)**
   - **URL**: `https://api.validkit.com/v1/verify`.
   - **Headers**:
     - `Authorization`: `Bearer {validKitApiKey}`.
     - `Content-Type`: `application/json`.
   - **Body**:
     ```json
     {
       "email": "$json.email"
     }
     ```

6. **Format ValidKit Output**
   - **Set**: Chỉ giữ lại trường `email` và `isValid` từ kết quả Verify.

7. **Log Verified Emails (Google Sheets)**
   - **Sheet Name**: Đặt tên sheet (ví dụ: `Decision-Maker Emails`).
   - **Range**: `A1` (nếu sheet rỗng) hoặc `A${lastRow+1}` (nếu đã có dữ liệu).
   - **Values**:
     ```
     [
       ["Email", "Domain", "Name", "Status"],
       ["$json.email", "$json.domain", "$json.name", "$json.isValid"]
     ]
     ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Manual Trigger** và nhấn **Execute Workflow**.
  - Kiểm tra **Google Sheets** xem có email được lưu không.
- **Bật Active**:
  - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Tự Động Hoá Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng tuần/month.
   - Ví dụ: `0 0 * * 1` (chạy hàng tuần thứ 2).

2. **Gửi Email/Kênh Slack/Telegram**:
   - Thêm node **Email** (n8n-nodes-base.email) hoặc **Slack** để thông báo khi có email mới xác minh.

3. **Lọc Email Theo Ngành Nghề**:
   - Cập nhật **searchQuery** trong Apify để phù hợp với ngành (ví dụ: `"CTO fintech Vietnam"`).

4. **Lưu Log Lịch Sử**:
   - Thêm node **Set** để lưu **thời gian scrape** và **từ khóa** vào Google Sheets cùng email.

5. **Kết Hợp với CRM**:
   - Sử dụng node **HubSpot** hoặc **Salesforce** để tự động thêm email vào CRM.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa lead generation** với **độ chính xác cao** và **tiết kiệm thời gian**. Bằng cách **setup 1 lần** và chạy liên tục, các sếp sẽ **nhận danh sách email decision-maker** sẵn sàng để liên hệ, **không cần lo lắng về sai sót** hay **mất thời gian thủ công**.

**👉 Hãy thử ngay và tự động hóa quy trình tìm kiếm email của mình!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Hyrum Hurst](https://n8n.io/workflows/12877) để hỗ trợ.

---
:::note[CHÚ Ý]
- **N8n Self-Hosted**: Để workflow chạy ổn định 24/7, các sếp nên **cài n8n trên VPS riêng**.
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::