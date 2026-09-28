---
title: "🚀 Tự Động Hóa Sinh Lập & Lọc Lead Tiềm Năng với Google Maps, GPT-4 & HubSpot (N8N)"
description: "Workflow tự động hóa 100% không code để quét địa chỉ từ Google Maps & Yellow Pages, xác thực email, enrich dữ liệu lead, lọc chất lượng và đồng bộ vào HubSpot - tiết kiệm 10+ giờ/tháng cho bộ phận Sales."
slug: "tu-dong-hoa-lead-generation-google-maps-gpt4-hubspot"
tags: [n8n, automation, sales, ai, hubspot, google-maps, gpt-4, no-code]
keywords: [tự động hóa lead generation, n8n workflow, enrich lead với GPT-4, đồng bộ HubSpot, quét địa chỉ Google Maps, lọc lead chất lượng]
---

# 🚀 **Tự Động Hóa Sinh Lập & Lọc Lead Tiềm Năng với Google Maps, GPT-4 & HubSpot**

### **🔍 Nỗi Đau Của Các Sếp Sales**
Bộ phận Sales của các sếp đang phải mất **giờ đồng hồ** để:
- **Quét thủ công** địa chỉ từ Google Maps và Yellow Pages.
- **Xác thực email** của lead (rất nhiều lead giả).
- **Enrich dữ liệu** (thêm thông tin như ngành nghề, quy mô doanh nghiệp, nhu cầu).
- **Lọc lead chất lượng** giữa hàng trăm lead không phù hợp.
- **Đồng bộ vào HubSpot** để theo dõi và tự động hóa pipeline.

**Kết quả?** Thời gian làm việc tăng gấp 2-3 lần, chất lượng lead thấp, và bộ phận Sales mệt mỏi.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tháng** cho bộ phận Sales (không cần quét, enrich, lọc lead thủ công).
✅ **Lead chất lượng cao** (được lọc bởi AI + quy tắc business logic).
✅ **Dữ liệu đồng bộ tự động** vào HubSpot (không cần copy-paste).
✅ **Báo cáo analytics** tự động export vào Google Sheets (theo dõi hiệu suất lead).
✅ **Cảnh báo Slack** khi có lead mới chất lượng (không bỏ lỡ cơ hội).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tài khoản Google Maps API** (để quét địa chỉ).
- **Tài khoản Yellow Pages API** (hoặc sử dụng API khác như Yelp).
- **API Key OpenAI** (để sử dụng GPT-4 trong quá trình enrich & lọc lead).
- **Tài khoản HubSpot** (để đồng bộ contact).
- **Slack Workspace** (để nhận cảnh báo lead mới).
- **Google Sheets** (để lưu lead và analytics).
- **VPS n8n** (để chạy workflow 24/7).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/4824).
2. Mở **n8n Editor** (trên VPS hoặc n8n.cloud).
3. Nhấn **"Import"** và chọn file JSON.
4. Hoặc copy toàn bộ JSON và paste vào **"Import"** trong n8n.

:::note[LƯU Ý]
- **Không chạy workflow ngay lập tức** sau khi import. Các sếp cần **cấu hình chi tiết** các node trước.
- **Không sử dụng n8n.cloud miễn phí** (do giới hạn API call của OpenAI và HubSpot).
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Dưới đây là **các node quan trọng** cần cấu hình kỹ lưỡng:

##### **🔧 Configuration Hub (Set Node)**
- **Cấu hình biến môi trường** (environment variables) cho toàn bộ workflow:
  - `GOOGLE_MAPS_API_KEY` (API Key từ Google Cloud).
  - `YELLOW_PAGES_API_KEY` (nếu sử dụng API này).
  - `OPENAI_API_KEY` (API Key từ OpenAI).
  - `HUBSPOT_API_KEY` (API Key từ HubSpot).
  - `SLACK_WEBHOOK_URL` (Webhook từ Slack).
  - `GOOGLE_SHEETS_SPREADSHEET_ID` (ID của Google Sheet lưu lead).

##### **🗺️ Google Maps Scraper (HTTP Request Node)**
- **Cấu hình URL API**:
  ```plaintext
  https://maps.googleapis.com/maps/api/place/textsearch/json?query={keyword}&key={GOOGLE_MAPS_API_KEY}
  ```
  - Thay `{keyword}` bằng từ khóa tìm kiếm (ví dụ: "công ty marketing TP.HCM").
- **Lọc kết quả** (sử dụng **Code Node** sau này) để lấy chỉ địa chỉ hợp lệ.

##### **📞 Yellow Pages Scraper (HTTP Request Node)**
- **Cấu hình URL API** (nếu sử dụng API này):
  ```plaintext
  https://api.yellowpages.com/v5/search?location={city}&category={category}&api_key={YELLOW_PAGES_API_KEY}
  ```
  - Thay `{city}` và `{category}` bằng vùng và ngành nghề mong muốn.

##### **🧹 Advanced Data Cleaner (Code Node)**
- **Mã JavaScript** sẽ:
  - Loại bỏ lead trùng lặp.
  - Lọc địa chỉ không hợp lệ.
  - Chuyển đổi dữ liệu thành định dạng chuẩn.
- **Lưu ý**: Các sếp có thể **tùy chỉnh mã** để phù hợp với ngành nghề.

##### **✉️ Email Verification (HTTP Request Node)**
- **Sử dụng API xác thực email** như:
  - [Hunter.io](https://hunter.io/) (API Key).
  - [ZeroBounce](https://www.zerobounce.net/) (API Key).
- **Cấu hình URL**:
  ```plaintext
  https://api.hunter.io/v2/email-verifier?email={email}&api_key={HUNTER_API_KEY}
  ```

##### **💎 Lead Enrichment Engine (Code Node)**
- **Sử dụng GPT-4 (OpenAI)** để enrich lead:
  ```javascript
  const response = await n8n.plugins.request({
    url: "https://api.openai.com/v1/chat/completions",
    method: "POST",
    headers: {
      "Authorization": `Bearer ${$input.all().OPENAI_API_KEY}`,
      "Content-Type": "application/json"
    },
    body: {
      model: "gpt-4",
      messages: [
        {
          role: "user",
          content: `Enrich this lead data: ${JSON.stringify($input.all().leadData)}. Provide industry, company size, and potential needs.`
        }
      ]
    }
  });
  ```
- **Lưu ý**:
  - **Giám sát chi phí OpenAI** (GPT-4 rất tốn token).
  - **Tùy chỉnh prompt** để phù hợp với ngành nghề.

##### **🎯 Quality Filter (If Node)**
- **Điều kiện lọc lead chất lượng**:
  - Email đã xác thực (`emailVerified: true`).
  - Địa chỉ hợp lệ (`addressValid: true`).
  - Score enrich từ GPT-4 cao (`enrichScore > 70`).
  - Ngành nghề phù hợp (`industry: ["marketing", "tech", "finance"]`).

##### **📊 Export Qualified Leads (Google Sheets Node)**
- **Cấu hình**:
  - **Spreadsheet ID**: ID của Google Sheet đã tạo.
  - **Sheet Name**: "Qualified_Leads".
  - **Dữ liệu export**: Lead đã lọc chất lượng.

##### **🏢 Create HubSpot Contact (HubSpot Node)**
- **Cấu hình**:
  - **API Key**: `$input.all().HUBSPOT_API_KEY`.
  - **Properties**:
    - `email` (trực tiếp từ lead).
    - `firstName`, `lastName` (nếu có).
    - `company` (từ enrich).
    - **Custom properties** (như `lead_score`, `industry`).

##### **🔔 Slack Alert (Slack Node)**
- **Cấu hình**:
  - **Webhook URL**: `$input.all().SLACK_WEBHOOK_URL`.
  - **Message template**:
    ```json
    {
      "text": "🚀 New Qualified Lead Alert!",
      "attachments": [
        {
          "title": "Lead Details",
          "text": `Name: ${$input.all().firstName} ${$input.all().lastName}\nEmail: ${$input.all().email}\nCompany: ${$input.all().company}\nIndustry: ${$input.all().industry}`,
          "color": "#36a64f"
        }
      ]
    }
    ```

##### **📈 Analytics Engine (Code Node)**
- **Tính toán metrics**:
  - Tỷ lệ lead chuyển đổi thành contact HubSpot.
  - Thời gian trung bình từ lead đến contact.
  - Ngành nghề có lead chất lượng nhất.
- **Export vào Google Sheets** (Sheet "Analytics").

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Run Workflow"** và kiểm tra từng node.
   - **Sửa lỗi** nếu có (ví dụ: API key sai, Google Sheets không kết nối).
2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động khi có trigger.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với CRM khác**: Thay HubSpot bằng Salesforce, Pipedrive.
- **Lưu log hoạt động**: Sử dụng **Sticky Note Node** để ghi lại lỗi và debug.
- **Gửi báo cáo định kỳ**: Sử dụng **Google Apps Script** để tự động gửi báo cáo qua email.
- **Tích hợp với Zoom/Calendly**: Khi lead chất lượng, tự động tạo cuộc gọi.
- **Sử dụng Webhook từ website**: Khi có lead từ landing page, tự động enrich và đồng bộ.
:::

---

### **📌 Kết Luận**
Workflow này **giải phóng bộ phận Sales** khỏi công việc thủ công, **tăng chất lượng lead** nhờ AI, và **tự động hóa pipeline** từ đầu đến cuối.

**Hành động ngay**:
1. **Đăng ký VPS n8n** để chạy 24/7 (giảm chi phí với mã **VPSN8N**).
2. **Import workflow** và cấu hình API keys.
3. **Test và bật hoạt động** để bắt đầu tự động hóa!

---
**🔗 Tài nguyên tham khảo**:
- [Tutorial Google Maps API](https://developers.google.com/maps/documentation/places/web-service/overview)
- [OpenAI API Docs](https://platform.openai.com/docs/api-reference)
- [HubSpot API Guide](https://developers.hubspot.com/docs/api/overview)

**📩 Liên hệ tác giả**:
David Olusola - [david@daexai.com](mailto:david@daexai.com) (dành cho các dự án tự động hóa phức tạp).